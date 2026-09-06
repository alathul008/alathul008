# Ice — TryHackMe

## Overview

Ice is a vulnerable Windows training environment used to practice service enumeration, vulnerability research, exploitation, privilege escalation, and post-exploitation.

> **Lab-only write-up:** The techniques below are documented for the authorized TryHackMe training environment. Do not apply them to systems without permission.

## Methodology

1. Connect to the authorized lab network.
2. Enumerate TCP ports and services.
3. Identify the Icecast service and version.
4. Research the relevant vulnerability.
5. Obtain an initial Meterpreter session using the lab's intended exploit path.
6. Enumerate local privilege-escalation opportunities.
7. Elevate privileges and verify the resulting context.
8. Perform the room's post-exploitation exercises.

## 1. Reconnaissance

The source walkthrough used an aggressive Nmap scan to enumerate all TCP ports and services:

```bash
nmap -sS -p- -A <target_ip> -T5 | tee nmap-recon
```

Important discoveries included:

- TCP/3389 — Microsoft Remote Desktop Protocol (RDP)
- TCP/8000 — Icecast service
- The target hostname was also revealed during enumeration.

## 2. Vulnerability Research

The Icecast service running on port 8000 was researched for known vulnerabilities. The source walkthrough identifies **CVE-2004-1561** and an associated Metasploit module:

```text
exploit/windows/http/icecast_header
```

In Metasploit, the workflow documented in the source was:

```text
search icecast
use exploit/windows/http/icecast_header
```

The required target setting was `RHOST`; the callback address was configured to the lab VPN interface (`tun0`).

## 3. Initial Access

Running the selected module against the authorized lab target produced a Meterpreter session.

The important security concept is the complete chain:

```text
Exposed service
    ↓
Version identification
    ↓
Vulnerability research
    ↓
Known exploit
    ↓
Meterpreter session
```

## 4. Privilege Escalation

After obtaining the session, the walkthrough used Meterpreter's Local Exploit Suggester to identify possible local privilege-escalation paths:

```text
run post/multi/recon/local_exploit_suggester
```

The source identifies `exploit/windows/local/ms16_032_secondary_logon_handle_privesc` as an example of a suggested exploit. The required session and callback settings were then configured for the lab.

## 5. Verify the Elevated Context

After successful escalation, the walkthrough checked available privileges:

```text
getprivs
```

It specifically notes privileges such as `SeTakeOwnershipPrivilege` as useful indicators during Windows post-exploitation analysis.

The process list was then examined:

```text
ps
```

The source walkthrough migrated the session to `spoolsv.exe` and verified the resulting security context:

```text
migrate -N spoolsv.exe
getuid
```

The expected lab result was `NT AUTHORITY\\SYSTEM`.

## 6. Credential and Post-Exploitation Exercises

The source walkthrough then used Meterpreter's Kiwi extension for the room's credential-related exercises:

```text
load kiwi
help
creds_all
hashdump
```

The original room contains specific credentials and challenge answers. **Those values are intentionally omitted from this public portfolio.**

The source also records the following post-exploitation exercises from the lab:

- Desktop observation with `screenshare`
- Microphone capture with `record_mic`
- Timestamp manipulation with `timestomp`
- Kerberos Golden Ticket exercise with `golden_ticket_create`

These are documented here as lab concepts rather than operational instructions for real systems.

## 7. Remote Access Exercise

The walkthrough also records enabling RDP through Meterpreter's Windows management module and then connecting with the credentials obtained during the authorized lab:

```text
run post/windows/manage/enable_rdp
```

The original credentials are deliberately excluded from this repository.

## 8. Manual Exploitation Exercise

The source additionally mentions attempting manual exploitation using an Exploit-DB proof of concept. The exact external exploit content is not reproduced here; the purpose of the exercise was to compare automated Metasploit exploitation with manual vulnerability exploitation.

## Security Lessons

### Service exposure

Running an outdated network service can expose an organization to known vulnerabilities. Service enumeration and accurate version identification are therefore important first steps in an authorized assessment.

### Patch management

Known vulnerabilities can provide a direct path from an exposed service to code execution. Maintaining current software versions reduces this risk.

### Privilege separation

Initial code execution does not necessarily mean full compromise. Windows privilege boundaries and service-account permissions determine how far an attacker can progress.

### Post-exploitation controls

Credential dumping, process migration, remote access, and persistence mechanisms demonstrate why endpoint monitoring and least privilege are important defensive controls.

## Skills Demonstrated

- Nmap reconnaissance
- Windows service enumeration
- Vulnerability research
- Metasploit
- Meterpreter
- Local privilege-escalation analysis
- Windows privilege verification
- Post-exploitation analysis
- Security methodology and documentation

## Disclaimer

This write-up is based on work performed in an authorized TryHackMe training environment. No real-world systems are targeted or implied.