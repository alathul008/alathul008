
<div align="center">

# 👋 ATHUL A L

### 🛡️ Cybersecurity | SOC | Detection Engineering | VAPT | Security Research

**B.Sc. Computer Science · CEH Certified · Hands-on Security Practitioner**

<p>
  <a href="https://github.com/alathul008?tab=repositories"><img src="https://img.shields.io/badge/GitHub-Portfolio-181717?style=for-the-badge&logo=github" alt="GitHub"></a>
  <a href="https://www.linkedin.com/in/athul-al-6a0a59285/"><img src="https://img.shields.io/badge/LinkedIn-Profile-0A66C2?style=for-the-badge&logo=linkedin" alt="LinkedIn"></a>
  <a href="mailto:alathul15@gmail.com"><img src="https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail" alt="Email"></a>
</p>

</div>

---

## 🧭 About Me

I'm a **Computer Science graduate and CEH-certified cybersecurity practitioner** building practical experience across both **offensive and defensive security**.

My work is centered around:

- 🔵 **SOC operations & security monitoring**
- 🧠 **Detection engineering & event correlation**
- 🪟 **Windows / Active Directory security**
- 🌐 **Network security & traffic analysis**
- 🔴 **Vulnerability assessment & web application security**
- 🔎 **OSINT / security research**
- ⚙️ **Security automation & Python**
- 🧪 **Hands-on labs, reproducible testing & technical documentation**

I prefer an evidence-driven workflow:

**Activity → Telemetry → Detection → Triage → Investigation → Evidence → ATT&CK → Response → Documentation**

---

# 🏆 Security Portfolio

## 🟦 Enterprise Cyber Range

### Detection Engineering · Active Directory · Purple Team · DFIR

My main security engineering project is an **isolated enterprise-style cyber range** built with VMware Workstation Pro.

**Core architecture:**

**pfSense → Segmented VMware Networks → Active Directory → Windows Endpoints → Wazuh/OpenSearch → Detection Engineering**

### Environment

| Component | Role |
|---|---|
| **FW-01 / pfSense** | Firewall & routing boundary |
| **DC-01** | Windows Server 2025 · AD / DNS / GC |
| **WIN-01** | Domain-joined Windows endpoint |
| **WAZUH-01** | Wazuh security monitoring |
| **ARCH-01** | Linux attack/operator workstation |
| **corp.home.arpa** | Active Directory domain |

### Detection Engineering

**DET-001 → DET-021 documented/completed**

The detection work covers areas including:

- PowerShell encoded-command activity
- CMD → PowerShell parent/child execution
- Account creation
- Scheduled task creation
- Windows service creation
- Failed logons
- Successful logon investigation
- Privileged logon telemetry
- Special privilege assignment
- Domain Admins / privileged-group changes
- Account lockout
- Process creation
- PowerShell process telemetry
- Multi-event account/privilege correlation
- PowerShell → network correlation
- PowerShell download telemetry boundaries

### Telemetry & Investigation

- Windows Security Event Logs
- Sysmon
- Wazuh agents
- Wazuh Manager
- Wazuh Indexer / OpenSearch
- Event correlation
- IOC / IOA / TTP analysis
- MITRE ATT&CK mapping
- Detection validation and replay
- Evidence-driven documentation

📂 **[Explore the Cyber Range →](https://github.com/alathul008/cyber-range)**

---

# 🔵 SOC HomeLab

### SIEM · HIDS · FIM · Detection · Incident Response

A defensive-security home-lab project documenting SOC workflows using:

**Wazuh · Splunk · Suricata · AdGuard Home · Docker · WSL · Tailscale**

### What I worked with

- Centralized Windows/Linux logging
- SIEM investigation
- SPL searches
- Wazuh HIDS
- File Integrity Monitoring
- Rootkit detection
- Authentication-event analysis
- Alert triage
- Suspicious PowerShell investigation
- SSH brute-force scenarios
- Privilege-escalation investigation
- DNS visibility
- Suspicious-domain / beaconing analysis
- Network security telemetry
- MITRE ATT&CK mapping
- Incident-response documentation

> The repository contains sanitized portfolio material. Real credentials, tokens, private infrastructure details and sensitive data are excluded.

📂 **[Explore SOC HomeLab →](https://github.com/alathul008/SOC-HomeLab)**

---

# 🔴 Vulnerability Assessment & Web Security

## Authorized Web Application Assessment

Performed hands-on web security testing against authorized applications using:

**Burp Suite · SQLMap · Nmap · OWASP methodology · CVSS**

Documented findings included:

- SQL Injection
- Missing Rate Limiting
- Improper Access Control
- Exposed Git Repository

The assessment work included:

**Reconnaissance → Enumeration → Manual Testing → Validation → Impact Analysis → CVSS → Reporting → Remediation**

### Reporting

Produced formal vulnerability documentation with:

- Finding description
- Technical evidence
- Business/security impact
- Severity
- CVSS assessment
- Reproduction methodology
- Remediation guidance

> Public portfolio material is sanitized. Real client/production targets, credentials and sensitive evidence are intentionally excluded.

📂 **[Explore Vulnerability Assessment Portfolio →](https://github.com/alathul008/alathul008/tree/main/vulnerability-assessment)**

---

# 🧪 Penetration Testing & Boot-to-Root

## 11 Machines Completed

Hands-on boot-to-root practice across **TryHackMe and VulnHub**, documenting enumeration, exploitation, privilege escalation and post-exploitation methodology.

### Machines / Labs

| Platform | Machines |
|---|---|
| **VulnHub** | DC-1 · DC-2 · DC-3 · Raven · Cybersploit 2 · Vegeta |
| **TryHackMe** | Blue · Ignite · Ice · Basic Pentesting |
| **Additional Practice** | Penetration-testing and privilege-escalation scenarios |

### Skills demonstrated

- Network reconnaissance
- Port/service enumeration
- Web enumeration
- SMB enumeration
- WordPress/Joomla/Drupal assessment
- Vulnerability identification
- Exploit validation
- SQL injection
- Credential discovery
- Password/hash cracking
- Reverse shells
- SSH access
- Restricted-shell escape
- Linux privilege escalation
- Windows exploitation
- Docker privilege escalation
- SUID/SGID abuse
- Sudo misconfiguration abuse
- Sensitive Git exposure
- Steganography analysis

📂 **[Read the penetration-testing documentation →](https://github.com/alathul008/alathul008/tree/main/penetration-testing-labs)**

---

# 📚 Technical Security Documentation

My security portfolio is not only a list of tools — I document **how the investigation was performed and what evidence supported the conclusion**.

Documented lab topics include:

- 🔐 Password-protected ZIP cracking with John
- 🔑 SSH private-key passphrase recovery
- 🐧 SGID **sed** privilege escalation
- 🛠️ **sudo / Git** privilege escalation
- 🖼️ Steganography investigation
- 💉 Blind SQL Injection / SQLMap database enumeration
- 📦 Sensitive Git repository exposure
- 🐳 Docker group privilege escalation
- 🌐 SMB / EternalBlue exploitation
- 📝 WordPress / Joomla / Drupal assessments
- 🧩 Restricted-shell escape
- 🔍 Credential and hash analysis
- 🖥️ Linux and Windows privilege escalation

Each write-up is structured around **reconnaissance → exploitation → evidence → privilege escalation → lessons learned**.

---

# 🔎 MailRecon — Email OSINT Platform

### Privacy-first OSINT · Evidence Provenance · Explainable Risk

MailRecon is a local-first defensive investigation platform designed around a critical security principle:

> **An observation is evidence — not identity proof.**

### Capabilities

- Email normalization and classification
- Username candidate generation
- DNS / SPF / DMARC / DNSSEC analysis
- RDAP intelligence
- Gravatar correlation
- GitHub public-profile correlation
- Optional HIBP breach metadata
- Evidence provenance
- Explainable risk scoring
- Relationship graph
- Investigation timeline
- JSON / CSV / HTML / PDF reports
- SQLite persistence
- Privacy mode
- SSRF-conscious outbound validation
- API authentication
- Docker workflow
- CI, dependency auditing, secret scanning and SAST

📂 **[Explore MailRecon →](https://github.com/alathul008/mailrecon)**

---

# ⚙️ Security + Software Engineering

Cybersecurity is my primary focus, but I also build software to strengthen my engineering skills.

## 🟣 Opal

A full-stack application built with:

**Next.js · React · TypeScript · Prisma · Tailwind · Clerk · Stripe · React Query · Redux Toolkit · Zod**

Demonstrates:

- Modern App Router architecture
- Authentication
- Protected application flows
- API/server-side logic
- Database integration
- Payment-related functionality
- State management
- Form validation
- Component architecture

📂 **[Opal →](https://github.com/alathul008/Opal)**

## 🖥️ Opal Electron App

Desktop application work using:

**Electron · React · TypeScript · Vite · React Query · Socket.IO**

Includes Electron window management, IPC communication, preload isolation and desktop media/screen-source handling.

📂 **[Opal Electron App →](https://github.com/alathul008/opal-electron-app)**

---

# 🤖 Pascoe-Lite

### AI Payment Recovery · Gemini · Deterministic Safety Guardrails

Built for the **Razorpay AI Buildathon — AI Revenue Recovery track**.

Pascoe-Lite analyzes simulated failed-payment webhook telemetry and generates a tailored recovery strategy.

### Architecture

**Failed Webhook → Failure Analysis → Gemini → Structured Recovery → Deterministic Guardrails → Safe / Hold**

### Demonstrates

- Simulated payment-failure telemetry
- Gemini 2.5 Flash
- Structured JSON generation
- Failure-specific recovery strategies
- Customer messaging
- Sensitive-data detection
- False-urgency detection
- Guarantee detection
- Risk/fraud error handling
- Defense-in-depth AI safety

The important design principle is:

> **The LLM does not get the final safety decision.**

The deterministic guardrail layer can downgrade:

**Safe to deploy → Hold**

but never:

**Hold → Safe**

📂 **[Pascoe-Lite →](https://github.com/alathul008/pascoe-lite)**

---

# 🧭 Security Research & Responsible Disclosure

### YesWeHack

Reported a **CSRF (CWE-352)** security issue through responsible disclosure.

This experience reinforced:

- Vulnerability validation
- Security impact assessment
- Responsible disclosure
- Clear technical communication
- Coordinated remediation

---

# 🔐 IAM / Identity Security

Completed an **IAM Readiness Assessment** focused on:

- Role-Based Access Control
- Least Privilege
- Joiner / Mover / Leaver workflows
- Identity Governance
- Access lifecycle management
- Privileged-access considerations

---

# 🧰 Security Toolkit

### 🔵 SOC / Detection

**Wazuh · OpenSearch · Splunk · Sysmon · MITRE ATT&CK · Suricata**

### 🪟 Windows / Identity

**Windows Server · Active Directory · Windows Event Logs · PowerShell · Authentication · Authorization**

### 🌐 Network Security

**pfSense · Wireshark · Nmap · TCP/IP · DNS · Suricata · Network Traffic Analysis**

### 🔴 Offensive Security

**Burp Suite · OWASP Top 10 · SQLMap · Nmap · WPScan · Gobuster · Dirsearch · Metasploit · Hydra · John the Ripper**

### 🐧 Systems / Automation

**Linux · Arch Linux · Ubuntu · Docker · VMware · Bash · Python**

---

# 🎓 Education & Certifications

### 🎓 B.Sc. Computer Science

**University of Kerala**

**CGPA: 7.43 / 10**

### 📜 Certifications & Training

- **Certified Ethical Hacker (CEH)** — EC-Council
- **Advanced Diploma in Cyber Defence** — RedTeam Hacker Academy
- **Cybersecurity Analyst Job Simulation** — Tata / Forage
- **Advent of Cyber 2024** — TryHackMe

### 🏅 Achievement

**Rajyapuraskar — Scout & Guide**

---

# 📊 Portfolio at a Glance

| Area | Hands-on Evidence |
|---|---|
| 🛡️ Detection Engineering | **DET-001 → DET-021** |
| 🧪 Boot-to-Root | **11 machines** |
| 🔵 SOC / SIEM | **Wazuh · Splunk · OpenSearch** |
| 🪟 Windows Security | **AD · Sysmon · Event Logs** |
| 🌐 Network Security | **pfSense · Wireshark · Suricata · DNS** |
| 🔴 Web Security | **Burp · OWASP · SQLMap · CVSS** |
| 🔎 OSINT | **MailRecon** |
| 🤖 AI Security Engineering | **Pascoe-Lite** |
| 💻 Software Engineering | **Opal · Electron** |
| 🔐 IAM | **RBAC · Least Privilege · JML** |
| 📢 Responsible Disclosure | **CSRF / CWE-352** |
| 📚 Technical Documentation | **Architecture · Detection · VAPT · Lab Write-ups** |

---

# 🧠 How I Approach Security

~~~
        ┌─────────────────────┐
        │   Understand System │
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │   Generate / Gather │
        │      Telemetry      │
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │ Detect & Correlate  │
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │ Investigate Evidence│
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │ Map ATT&CK / Risk   │
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │ Respond / Remediate │
        └──────────┬──────────┘
                   ↓
        ┌─────────────────────┐
        │ Document & Improve  │
        └─────────────────────┘
~~~

---

# 🚀 Current Focus

**SOC Operations · Detection Engineering · Windows / Active Directory Security · Threat Hunting · Incident Investigation · Network Security · VAPT / Web Application Security · OSINT & Security Research · Security Automation · AI-Assisted Security Workflows**

---

# 📫 Connect

- 💼 **LinkedIn:** [linkedin.com/in/athul-al](https://www.linkedin.com/in/athul-al-6a0a59285/)
- 📧 **Email:** [athul15@gmail.com](mailto:alathul15@gmail.com)
- 🐙 **GitHub:** [github.com/alathul008](https://github.com/alathul008)

---

<div align="center">

### ⚡ Learn by doing. Validate with evidence. Document the investigation. Improve the defense.

**Security research published here is intended for authorized labs, educational environments, responsible disclosure, or appropriately scoped testing.**

</div>
