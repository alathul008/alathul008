# TryHackMe Blue — Windows SMB Exploitation

> **Lab:** TryHackMe Blue  
> **Focus:** Windows reconnaissance, SMB vulnerability validation, exploitation, privilege escalation, and credential-hash analysis  
> **Environment:** Authorized TryHackMe training environment  
> **Scope:** Intentionally vulnerable lab machine

## Overview

This lab demonstrated a Windows exploitation workflow centered on the **EternalBlue / MS17-010** SMB vulnerability.

**Reconnaissance → Vulnerability Validation → Exploitation → Session Upgrade → SYSTEM Access → Hash Analysis**

## 1. Reconnaissance

A full-port Nmap scan was used to identify exposed services:

```bash
nmap -sS -Pn -A -p- -T5 <target_ip>
```

SMB was identified as an important attack surface.

## 2. Vulnerability Validation

The SMB service was tested specifically for MS17-010:

```bash
nmap -sS -Pn -p 445 <target_ip> --script smb-vuln-ms17-010.nse
```

The lab machine was confirmed vulnerable.

## 3. Exploitation

Metasploit was used in the authorized training environment to select the MS17-010 EternalBlue module and establish an initial shell.

## 4. Privilege Escalation & Session Upgrade

The initial shell was converted to a Meterpreter session using the appropriate Metasploit post module. Privilege level was then verified, and the lab machine was brought to `NT AUTHORITY\SYSTEM`.

Process enumeration and migration were also practiced to understand Windows session context.

## 5. Credential Hash Analysis

With elevated access in the lab, Windows password hashes were collected and the relevant user hash was analyzed with John the Ripper.

> Passwords, hashes, and flags are intentionally excluded from this public portfolio.

## 6. Key Takeaways

- Full-port enumeration is important even when common services are expected.
- Vulnerability-specific Nmap scripts can help validate suspected weaknesses.
- SMB vulnerabilities can have severe consequences on unpatched Windows systems.
- Post-exploitation requires careful session and privilege verification.
- Credential material obtained during authorized testing should be handled securely and never published unnecessarily.

## Skills Demonstrated

`Nmap` `SMB` `MS17-010` `EternalBlue` `Metasploit` `Meterpreter` `Windows Privilege Escalation` `John the Ripper` `Hash Analysis`

## Ethics & Scope

This case study is based on an intentionally vulnerable TryHackMe training environment. Exploitation techniques must only be performed against systems where explicit authorization exists.
