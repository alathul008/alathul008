# SOC Home Lab — SIEM & Incident Detection

A practical Security Operations Center (SOC) home lab focused on log analysis, alert triage, incident investigation, IOC identification, and security documentation.

> **Status:** In progress

## Objective

Build a small defensive security environment that demonstrates how a junior SOC analyst investigates suspicious activity from endpoint and authentication logs.

## Planned Lab Architecture

```text
Windows Endpoint ──┐
                   ├──> Log Collection ──> SIEM ──> Alerts ──> Investigation
Linux Endpoint ────┘                                  │
                                                       └──> Incident Report
```

## Detection Scenarios

The lab will cover realistic beginner-to-intermediate SOC scenarios:

- Repeated failed authentication attempts / brute-force activity
- Successful login following multiple failures
- Suspicious PowerShell execution
- Suspicious process activity
- Unusual network connections
- IOC extraction and enrichment
- Alert triage and severity assessment
- MITRE ATT&CK technique mapping

## Investigation Workflow

1. Collect and normalize logs
2. Identify suspicious events
3. Review surrounding activity and timeline
4. Extract relevant IOCs
5. Determine likely attack technique
6. Assess impact and severity
7. Document findings
8. Recommend containment and remediation

## Project Structure

```text
soc-home-lab/
├── README.md
├── detections/
├── investigations/
├── incident-reports/
├── screenshots/
└── sample-logs/
```

## Skills Demonstrated

- SIEM fundamentals
- Log analysis
- Alert triage
- Incident investigation
- IOC identification
- Timeline analysis
- MITRE ATT&CK mapping
- Security documentation

## Safety & Scope

This is a controlled home lab using systems and data owned or authorized by the lab operator. No unauthorized systems or real credentials should be used.

## Roadmap

- [ ] Deploy SIEM
- [ ] Connect Windows logs
- [ ] Connect Linux logs
- [ ] Create first detection rule
- [ ] Investigate authentication attacks
- [ ] Investigate suspicious PowerShell activity
- [ ] Map detections to MITRE ATT&CK
- [ ] Write incident reports
- [ ] Add sanitized screenshots and evidence
