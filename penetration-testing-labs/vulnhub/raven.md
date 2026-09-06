# Raven — VulnHub

## Overview

Raven is a vulnerable Linux training machine used to practice network discovery, web enumeration, WordPress assessment, credential testing, SSH access, and privilege escalation through sudo misconfiguration.

> **Lab-only write-up:** The techniques documented here are for the authorized VulnHub environment. Do not test systems without permission.

## Environment

The source walkthrough used Kali Linux on VMware as the attacker machine and Raven on VirtualBox as the target.

## Methodology

1. Discover the target on the local lab network.
2. Enumerate all exposed TCP services.
3. Identify the web application.
4. Enumerate WordPress users and authentication weaknesses.
5. Obtain authorized lab credentials.
6. Use SSH for initial shell access.
7. Enumerate local users and sudo permissions.
8. Abuse the permitted Python binary to obtain root in the lab.

## 1. Target Discovery

The target was discovered using ARP-based local network enumeration:

```bash
sudo arp-scan -l
```

This identifies hosts on the local network and their MAC addresses.

## 2. Port and Service Enumeration

A full TCP scan with service/version detection was performed:

```bash
nmap -p- -sSCV <target_ip>
```

The source walkthrough identified:

- TCP/22 — SSH
- TCP/80 — HTTP

The HTTP service hosted a WordPress installation.

## 3. Web Enumeration

Directory enumeration was performed with Dirsearch:

```bash
dirsearch -u http://<target_ip>
```

The significant discovery was the WordPress login/application path.

## 4. WordPress Enumeration

WPScan was used to enumerate WordPress users and test the supplied lab wordlist:

```bash
wpscan -u http://<target_ip>/wordpress --enumerate u --passwords <wordlist>
```

The source walkthrough reports discovery of two valid lab users, `micheal` and `steven`, with associated passwords.

**Credentials are intentionally omitted from this public portfolio.**

## 5. Initial Access

The discovered credentials were tested against SSH in the lab:

```bash
ssh micheal@<target_ip>
```

SSH access was successful. The walkthrough also records discovery of two challenge flags during exploration of the user's environment. The flag values are intentionally omitted.

The source notes that one flag was visible in the source code of `service.html`.

## 6. Local Privilege Enumeration

The initial user did not have useful sudo permissions. The walkthrough then switched to the second authorized lab user and checked sudo configuration:

```bash
sudo -l
```

The important finding was that `steven` could execute `/usr/bin/python` with sudo privileges without a password.

This is a classic **sudo misconfiguration**: a broadly capable interpreter should not normally be granted unrestricted root execution through sudo.

## 7. Privilege Escalation

The source walkthrough used the Python sudo permission with a GTFOBins-style shell escape to obtain a root context in the lab.

The key security chain was:

```text
WordPress enumeration
      ↓
Credential discovery
      ↓
SSH access
      ↓
User enumeration
      ↓
sudo -l
      ↓
Python allowed as root
      ↓
Root shell
```

Once root access was obtained, the final challenge flag was located under `/root`. The flag itself is intentionally excluded.

## Security Findings

### WordPress credential weakness

Credential testing exposed valid accounts in the training environment. In a real application, password spraying/brute-force resistance, strong passwords, MFA, and appropriate monitoring would reduce this risk.

### Excessive sudo privilege

Allowing a user to execute a general-purpose interpreter as root effectively grants that user a path to arbitrary root-level command execution.

**Recommended control:** grant only the minimum commands required and avoid unrestricted interpreter execution through sudo.

## Skills Demonstrated

- ARP-based host discovery
- Nmap
- HTTP enumeration
- Dirsearch
- WordPress enumeration
- WPScan
- Credential security assessment
- SSH
- Linux user enumeration
- sudo configuration analysis
- Privilege escalation
- Security documentation

## Lessons Learned

The machine demonstrates why penetration testing should not stop after finding an initial credential. A successful assessment follows the entire attack path and checks whether local privilege boundaries prevent further compromise.

## Disclaimer

This write-up is based on an authorized VulnHub training machine. Credentials, flags, and target-specific secrets are intentionally excluded.