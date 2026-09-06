# Vegeta — VulnHub

## Overview

Vegeta is a VulnHub training machine that combines web enumeration, source-code analysis, layered decoding, audio forensics, SSH access, and Linux privilege escalation.

> **Lab-only write-up:** The workflow is intended for the authorized VulnHub machine.

## Environment Setup

The source walkthrough describes importing the Vegeta `.ova` into VMware Workstation or VirtualBox and using a compatible isolated network such as Host-only or Bridged networking.

The attacker environment was Kali Linux.

## Methodology

1. Discover the target IP.
2. Enumerate TCP ports and services.
3. Inspect the web application.
4. Enumerate hidden web content.
5. Follow clues from `robots.txt`.
6. Inspect page source and decode Base64 content.
7. Extract and inspect the resulting QR code.
8. Continue directory enumeration when the QR information does not provide SSH access.
9. Locate an audio file and decode its Morse content.
10. Validate the recovered credentials through SSH.
11. Inspect shell history for privilege-escalation clues.
12. Demonstrate the resulting root access in the lab.

## 1. Target Discovery

The target IP was discovered with:

```bash
arp-scan --localnet
```

## 2. Port and Service Enumeration

The source walkthrough used:

```bash
nmap -p- -sSCV -T4 <target_ip>
```

Reported services:

- TCP/22 — OpenSSH 7.9p1 on Debian 10
- TCP/80 — Apache HTTP Server 2.4.38

## 3. Initial Web Enumeration

Browsing to the HTTP service initially revealed an image rather than a conventional application page.

Directory enumeration was performed with Dirsearch:

```bash
dirsearch -u http://<target_ip>
```

The source identified `robots.txt`, which contained a clue pointing toward the `/find_me` endpoint.

## 4. Source-Code Analysis and Base64

The `/find_me` endpoint contained concealed information in the page source.

The source walkthrough identified a Base64-encoded string near the end of the HTML. The data required **two decoding stages**, after which a QR code was obtained.

The QR code was inspected using `zbarimg`:

```bash
zbarimg <image-file>
```

The recovered information appeared useful but did not provide the SSH access required for the next stage. This was an important lesson in following evidence without assuming every clue is the final answer.

## 5. Deeper Directory Enumeration

The assessment continued with a larger SecLists content-discovery wordlist:

```bash
gobuster dir -u http://<target_ip> -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt
```

This revealed a `/bulma` directory.

## 6. Audio Forensics

An audio file was found within the discovered content. The source identified Morse code embedded in the recording.

The Morse signal was decoded with `multimon-ng`:

```bash
multimon-ng -a MORSE_CW -t wav bulma.wav
```

The decoded message revealed a username and password for the next stage.

**The recovered credentials are intentionally omitted from this public portfolio.**

## 7. SSH Access

The recovered lab credentials were used to authenticate over SSH:

```bash
ssh <username>@<target_ip>
```

Access was successful.

## 8. Privilege Escalation Investigation

After obtaining a shell, the walkthrough inspected shell history:

```bash
cat .bash_history
```

The history contained a clue involving modification of `/etc/passwd` and the creation of a root-like account.

The original walkthrough contains the exact credential material and account entry used by the challenge. Those values are intentionally **not reproduced in this public portfolio**.

## 9. Root Access

Following the challenge's local privilege-escalation path allowed the lab user to switch into the privileged account and obtain root-level access.

The final challenge flag was located under `/root`; its value is intentionally omitted.

## Attack Path

```text
HTTP
 ↓
robots.txt
 ↓
/find_me
 ↓
HTML source
 ↓
Base64 decoding
 ↓
QR code
 ↓
Further enumeration
 ↓
/bulma
 ↓
Audio file
 ↓
Morse decoding
 ↓
SSH credentials
 ↓
SSH access
 ↓
.bash_history clue
 ↓
Privilege escalation
 ↓
Root
```

## Skills Demonstrated

- ARP-based discovery
- Nmap
- Dirsearch
- Gobuster
- Web content enumeration
- HTML/source inspection
- Base64 decoding
- QR-code analysis
- Audio forensics
- Morse-code decoding
- SSH
- Linux privilege-escalation analysis
- Evidence-driven investigation

## Key Takeaways

Vegeta is valuable because the attack path is not a single obvious exploit. Progress depends on correlating clues across several layers: web content, source code, encoded data, QR information, directory enumeration, audio analysis, and finally host-level artifacts.

## Disclaimer

This write-up is based on an authorized VulnHub training machine. Credentials, flags, and target-specific secrets are intentionally excluded.