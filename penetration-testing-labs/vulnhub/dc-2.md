# VulnHub DC-2 — WordPress Enumeration to Root

> **Lab:** VulnHub DC-2  
> **Focus:** Network enumeration, virtual-host resolution, WordPress enumeration, credential testing, restricted-shell escape, and sudo privilege escalation  
> **Environment:** Kali Linux + vulnerable DC-2 VM  
> **Scope:** Intentionally vulnerable lab environment

## Overview

DC-2 followed a practical attack chain:

**Host Discovery → Port Scanning → Hostname Resolution → WordPress Enumeration → Credential Testing → SSH Access → Restricted Shell Analysis → User Switching → Sudo Enumeration → Privilege Escalation**

## 1. Host Discovery

The target was identified on the isolated lab network using:

```bash
sudo arp-scan -l
```

## 2. Port & Service Enumeration

A comprehensive Nmap scan was performed:

```bash
nmap -p- -sSCV --script vuln -vv -T4 <target_ip>
```

The scan identified HTTP and SSH, with SSH running on a non-standard port.

## 3. Hostname Resolution

The web application was not directly accessible using the target IP, so the lab hostname was mapped locally through `/etc/hosts`. This allowed the application to be accessed using its expected hostname.

## 4. WordPress Enumeration

Directory enumeration identified the WordPress application. The login endpoint did not enforce an effective rate limit in the lab, so credential testing was investigated.

Instead of immediately using a large generic password list, a context-specific wordlist was generated from the site's content with CeWL:

```bash
cewl http://<lab-host> -w cewl.txt
```

WPScan was then used to enumerate WordPress users and test the generated list in the authorized lab environment.

> Discovered usernames and passwords are intentionally omitted from this public write-up.

## 5. SSH Access

One of the discovered lab credentials provided SSH access through the non-standard SSH port.

## 6. Restricted Shell Analysis

The initial account was constrained by a restricted Bash environment. The restriction was analyzed and an editor-based shell escape was used to obtain a normal shell within the lab.

The `PATH` environment was then restored so standard system utilities could be used normally.

## 7. Privilege Escalation

After switching to the appropriate local user, sudo permissions were enumerated:

```bash
sudo -l
```

The account was permitted to execute Git with elevated privileges without a password. Git's shell escape behavior was then used to demonstrate the privilege boundary failure and obtain root access in the lab.

## 8. Key Takeaways

- Non-standard ports should not be overlooked during enumeration.
- Hostname resolution can be essential when web applications rely on a specific virtual host.
- Context-specific wordlists can reduce unnecessary password-testing volume.
- Restricted shells should be assessed for escape paths and environmental weaknesses.
- `sudo -l` is an important privilege-escalation enumeration step.
- Allowing powerful binaries such as Git to execute with unrestricted root privileges can create a direct privilege-escalation path.

## Skills Demonstrated

`Nmap` `ARP Scan` `Dirsearch` `CeWL` `WPScan` `WordPress` `SSH` `Restricted Shells` `sudo` `Git` `GTFOBins` `Linux Privilege Escalation`

## Ethics & Scope

This write-up documents work performed against an intentionally vulnerable training machine. The techniques should only be used on systems where testing is explicitly authorized.
