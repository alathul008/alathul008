# VulnHub DC-1 — Drupal Enumeration & Linux Privilege Escalation

> **Lab:** VulnHub DC-1  
> **Focus:** Host discovery, service enumeration, Drupal fingerprinting, exploit research, shell access, SUID enumeration, and Linux privilege escalation  
> **Environment:** Kali Linux + vulnerable DC-1 VM  
> **Scope:** Intentionally vulnerable lab environment

## Overview

DC-1 demonstrated an end-to-end Linux penetration-testing workflow:

**Host Discovery → Port Scanning → Web Enumeration → CMS Fingerprinting → Exploit Research → Initial Shell → SUID Enumeration → Root**

## 1. Host Discovery

The target VM was identified within the lab network using ARP discovery:

```bash
sudo arp-scan -l
```

## 2. Service Enumeration

A full TCP scan with service detection was performed:

```bash
nmap -p- -sSCV <target_ip>
```

HTTP and SSH were identified as exposed services, with the HTTP service hosting a Drupal application.

## 3. Web & CMS Enumeration

The Drupal site was inspected manually and with directory enumeration. Droopescan was then used to identify Drupal version and module information.

```bash
droopescan scan drupal -u http://<target_ip>
```

## 4. Vulnerability Research & Initial Access

SearchSploit was used to research Drupal 7 vulnerabilities. Metasploit was then used within the lab to validate an applicable exploit and obtain a Meterpreter session.

The shell was upgraded to a more stable interactive environment for subsequent host enumeration.

## 5. Privilege Escalation

System-level enumeration included checking for SUID binaries:

```bash
find / -perm -4000 2>/dev/null
```

A misconfigured SUID `find` binary was identified as a privilege-escalation vector. The finding was validated in the isolated lab, resulting in root access.

## 6. Key Takeaways

- Host discovery and complete port enumeration established the attack surface.
- CMS fingerprinting helped narrow vulnerability research.
- SearchSploit and Metasploit were used as complementary research and validation tools.
- Obtaining a shell is only the initial access phase; local enumeration is essential for privilege escalation.
- SUID binaries should be reviewed carefully because unsafe privilege assignments can cross security boundaries.

## Skills Demonstrated

`ARP Scan` `Nmap` `Dirsearch` `Droopescan` `SearchSploit` `Metasploit` `Meterpreter` `Drupal` `SUID` `GTFOBins` `Linux Privilege Escalation`

## Ethics & Scope

This case study documents work performed against an intentionally vulnerable training machine. The techniques should only be used against systems where testing is explicitly authorized.
