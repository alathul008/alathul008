# TryHackMe Ignite — Fuel CMS RCE to Root

> **Lab:** TryHackMe Ignite  
> **Focus:** Web enumeration, CMS identification, vulnerability research, authenticated RCE, shell stabilization, credential discovery, and privilege escalation  
> **Environment:** Authorized TryHackMe training environment  
> **Scope:** Intentionally vulnerable lab machine

## Overview

Ignite demonstrated a boot-to-root workflow against a vulnerable Fuel CMS installation.

**Reconnaissance → Service Enumeration → CMS Identification → Vulnerability Research → RCE → Shell Access → Credential Discovery → Root**

## 1. Reconnaissance

Target availability and exposed services were checked before application testing.

```bash
ping -c 4 <target_ip>
nmap -Pn -sS <target_ip> -T4 -n -v
```

The lab exposed an HTTP service hosting Fuel CMS.

## 2. Application Enumeration

The default Fuel CMS installation page was identified and the CMS backend login endpoint was located.

The application version was researched with SearchSploit:

```bash
searchsploit fuel cms 1.4
```

## 3. Vulnerability Research

The research identified an authenticated remote-code-execution condition in Fuel CMS. The vulnerable application functionality involved the page-selection parameter used by the CMS backend.

## 4. Initial Access

The relevant exploit was validated against the authorized lab target, resulting in a shell. A Netcat listener was used for the reverse-shell connection and the shell was stabilized for further enumeration.

> Target-specific credentials, IP addresses, flags, and payload details are intentionally omitted from this public portfolio.

## 5. Privilege Escalation

After initial access, application configuration directories were manually inspected for credential material:

```bash
cd /var/www/html/fuel/application/config/
grep -r -i "password\|user" .
```

Database configuration information provided the credential material needed to demonstrate root-level access in the lab.

## 6. Key Takeaways

- Service enumeration quickly identified the exposed web application.
- CMS version identification enabled focused vulnerability research.
- SearchSploit helped connect the identified software version with known vulnerabilities.
- Application configuration files can contain sensitive credentials and should never expose secrets unnecessarily.
- Post-exploitation enumeration is critical for identifying privilege-escalation paths.

## Skills Demonstrated

`Nmap` `SearchSploit` `Fuel CMS` `Web Enumeration` `RCE` `Reverse Shells` `Netcat` `Linux Enumeration` `Credential Discovery` `Privilege Escalation`

## Ethics & Scope

This case study is based on an intentionally vulnerable TryHackMe training environment. Exploitation techniques must only be performed against systems where explicit authorization exists.
