# Cybersploit 2 — VulnHub

## Overview

Cybersploit 2 is a vulnerable Linux training machine demonstrating network discovery, service enumeration, web-based credential disclosure, SSH access, and Docker-based privilege escalation.

> **Lab-only write-up:** This workflow is documented for the authorized VulnHub challenge environment.

## Methodology

1. Discover the target host.
2. Enumerate exposed services.
3. Inspect the web application for information disclosure.
4. Decode the disclosed data.
5. Validate the credentials through SSH.
6. Enumerate local privileges and group membership.
7. Identify Docker as the privilege-escalation vector.
8. Demonstrate the impact of excessive Docker privileges.

## 1. Network Discovery

The source walkthrough identified the target with:

```bash
sudo arp-scan -l
```

## 2. Service Enumeration

All TCP ports and service versions were enumerated using:

```bash
nmap -p- -sSCV <target_ip>
```

The source identified:

- TCP/22 — SSH
- TCP/80 — HTTP

## 3. Web Application Analysis

The HTTP service presented credential information that was obfuscated using the **ROT47** cipher.

The important lesson here was that encoding is not encryption. An exposed credential that is merely transformed with a reversible encoding/cipher can still result in account compromise.

The source walkthrough decoded the value and recovered valid lab credentials. The actual credential values are **not included** in this public write-up.

## 4. SSH Initial Access

The recovered lab credentials were validated through SSH:

```bash
ssh <username>@<target_ip>
```

After authentication, the walkthrough located `hint.txt`, which pointed toward Docker as the next stage of the challenge.

## 5. Privilege Enumeration

Local group membership was checked with:

```bash
id
```

The important finding was membership in the Docker group.

Membership in a privileged Docker group can have security consequences because Docker may be capable of interacting with the host filesystem with high privileges.

## 6. Docker Privilege Escalation

The source walkthrough demonstrated the impact by starting an Alpine container while mounting the host filesystem:

```bash
docker run -v /:/mnt -it alpine chroot /mnt
```

In the isolated training VM, this resulted in a root context over the host filesystem.

The source also documented an alternative lab demonstration that mounted `/etc` and modified the host's passwd database. That technique is **not reproduced here as an operational persistence recipe**; the important portfolio takeaway is the security impact of unrestricted Docker privileges.

## 7. Impact

The attack path was:

```text
HTTP
 ↓
Obfuscated credential disclosure
 ↓
Credential decoding
 ↓
SSH user access
 ↓
Docker group membership
 ↓
Host filesystem access
 ↓
Root-level compromise
```

The source assessment rates the Docker group misconfiguration as **Critical** because it can lead to full host compromise.

## Security Recommendations

- Do not expose credentials through web pages, even in obfuscated form.
- Store credentials securely and use appropriate password hashing.
- Restrict Docker group membership to trusted administrators.
- Treat access to the Docker daemon as highly privileged.
- Monitor changes to Docker configuration and daemon access.
- Apply container isolation and least-privilege principles.
- Avoid mounting sensitive host directories into containers unless required.

## Skills Demonstrated

- ARP-based network discovery
- Nmap
- Web application analysis
- ROT47 decoding
- SSH
- Linux privilege enumeration
- Docker security assessment
- Container-based privilege escalation analysis
- Risk assessment and remediation

## Key Takeaway

The most important lesson from this machine is that container tooling can become a privilege boundary failure when administrative access to the Docker daemon is granted too broadly.

## Disclaimer

This write-up is based on an authorized VulnHub training environment. Credentials, flags, and unnecessary secrets are intentionally omitted.