# VulnHub DC-3 — Joomla SQL Injection to Root

> **Lab:** VulnHub DC-3  
> **Focus:** Web application enumeration, Joomla fingerprinting, SQL injection, credential exposure, reverse-shell access, and Linux privilege escalation  
> **Environment:** Kali Linux + vulnerable DC-3 VM  
> **Scope:** Intentionally vulnerable lab environment

## Overview

DC-3 was approached using a structured penetration-testing workflow:

**Reconnaissance → Scanning → Web Enumeration → Vulnerability Research → Exploitation → Initial Access → Privilege Escalation**

The lab exposed a Joomla 3.7.0 web application. Version identification led to research into CVE-2017-8917, an SQL injection vulnerability. Database enumeration exposed Joomla user data, and the recovered credentials were used to obtain administrative access. A template-editing feature then provided a path to a low-privileged shell, followed by kernel-level privilege escalation to root.

## 1. Reconnaissance

The target was identified within the isolated lab network using ARP-based host discovery.

```bash
sudo arp-scan -l
```

## 2. Service Enumeration

A full TCP scan with service/version detection was performed:

```bash
nmap -sC -sV -p- --script vuln <target_ip>
```

The assessment identified HTTP as the relevant exposed service.

## 3. Web Enumeration

The web application was fingerprinted as **Joomla 3.7.0**. JoomScan was used to validate the CMS information.

```bash
joomscan -u http://<target_ip>
```

## 4. Vulnerability Research

SearchSploit was used to research vulnerabilities associated with the identified Joomla version.

```bash
searchsploit joomla 3.7.0
```

The research identified **CVE-2017-8917**, an SQL injection vulnerability affecting the Joomla version used by the lab.

## 5. SQL Injection & Database Enumeration

SQLMap was used in the lab to validate the injection and enumerate the backend database. The Joomla database was identified, followed by enumeration of the users table and extraction of password hashes.

The recovered hash was identified as bcrypt and tested with John the Ripper. The recovered credential enabled access to the Joomla administrator interface.

> Credentials and target-specific values are intentionally omitted from this public portfolio write-up.

## 6. Initial Access

The Joomla Template Editor was identified as a route to server-side code execution in the lab. A PHP reverse-shell technique was used to obtain a low-privileged shell.

## 7. Privilege Escalation

System and kernel information was enumerated:

```bash
uname -a
lsb_release -a
```

The lab system was found to be affected by a known kernel local privilege-escalation condition. After validating the finding in the lab, the exploit was compiled and executed, resulting in root access.

## 8. Key Takeaways

- Full-port enumeration established the attack surface.
- CMS fingerprinting and version identification were critical to finding the Joomla vulnerability.
- SQL injection can expose application data and user credential material.
- Administrative functionality can become an execution vector when unsafe server-side editing is available.
- Privilege escalation requires separate host-level enumeration after obtaining initial access.

## Skills Demonstrated

`Nmap` `JoomScan` `SearchSploit` `SQLMap` `John the Ripper` `Joomla` `SQL Injection` `Web Enumeration` `Linux Privilege Escalation` `Post-Exploitation`

## Ethics & Scope

This write-up documents work performed against an intentionally vulnerable training machine. The techniques should only be used on systems where testing is explicitly authorized.
