# Data Exfiltration Analyst Documentation

## Overview

This directory contains reference documentation and standard operating procedures for the Data Exfiltration Analyst consultant role. The analyst specializes in detecting, investigating, and responding to unauthorized data transfers across all exfiltration vectors.

## Core Competencies

### MITRE ATT&CK Exfiltration Techniques (TA0010)

| MITRE ID | Technique | Description |
|----------|-----------|-------------|
| T1020 | Automated Exfiltration | Automated processing and exfiltration of collected data |
| T1020.001 | Traffic Duplication | Leveraging traffic mirroring for data exfiltration |
| T1030 | Data Transfer Size Limits | Exfiltration in fixed-size chunks to avoid detection |
| T1048 | Exfiltration Over Alternative Protocol | Using protocols different from C2 channel |
| T1048.001 | Symmetric Encrypted Non-C2 Protocol | Exfiltration over symmetrically encrypted protocols |
| T1048.002 | Asymmetric Encrypted Non-C2 Protocol | Exfiltration over asymmetrically encrypted protocols |
| T1048.003 | Unencrypted/Obfuscated Non-C2 Protocol | Exfiltration over unencrypted protocols |
| T1041 | Exfiltration Over C2 Channel | Data theft via existing command and control channel |
| T1011 | Exfiltration Over Other Network Medium | Alternative network mediums (WiFi, Bluetooth, RF) |
| T1011.001 | Exfiltration Over Bluetooth | Data exfiltration via Bluetooth |
| T1052 | Exfiltration Over Physical Medium | Physical devices (USB, external drives) |
| T1052.001 | Exfiltration over USB | USB-based data theft |
| T1567 | Exfiltration Over Web Service | Legitimate external web services |
| T1567.001 | Exfiltration to Code Repository | GitHub, GitLab, etc. |
| T1567.002 | Exfiltration to Cloud Storage | AWS S3, Google Drive, Dropbox, etc. |
| T1029 | Scheduled Transfer | Timed exfiltration to blend with normal activity |
| T1537 | Transfer Data to Cloud Account | Cloud-to-cloud data transfer |

## Detection Mechanisms

| Detection Type | Data Sources | Alert Triggers |
|---------------|--------------|----------------|
| Volume-based | NetFlow, Proxy logs | Unusual data transfer volumes |
| Protocol-based | Firewall, IDS/IPS | Non-standard protocols, DNS tunneling |
| Destination-based | Proxy, DNS | Connections to suspicious domains/IPs |
| Time-based | SIEM correlation | After-hours large data transfers |
| Behavioral | UEBA | Deviation from user baseline |
| Content-based | DLP | Sensitive data patterns detected |

## Exfiltration Classification

| Category | Indicators |
|----------|-----------|
| Cyber Threat (External) | C2 beaconing, malware presence, unauthorized access |
| Insider Threat | Employee-associated activity, legitimate credentials |
| Unintentional Exposure | Misconfiguration, email to wrong recipient |
| Physical Exfiltration | USB activity, device loss |
| Cloud-based | Unauthorized cloud service uploads |

## Incident Severity Matrix

| Severity | Criteria | Response Time |
|----------|----------|---------------|
| Critical | Mass PII exposure, active exfiltration, ransomware | Immediate |
| High | Significant IP theft, customer data, ongoing | 1 hour |
| Medium | Limited scope, contained, historical | 4 hours |
| Low | Minimal impact, false positive likely | 24 hours |

## Tool Integration

| Tool Type | Integration Purpose |
|-----------|-------------------|
| SIEM | Alert correlation, log aggregation |
| SOAR | Playbook automation, case management |
| EDR | Endpoint telemetry, response actions |
| DLP | Content inspection, policy enforcement |
| CASB | Cloud application visibility |
| NDR | Network traffic analysis |
| Threat Intel | IOC enrichment, context |

## Compliance Notification Requirements

| Regulation | Notification Requirement | Timeline |
|-----------|-------------------------|----------|
| GDPR | Supervisory authority and data subjects | 72 hours |
| HIPAA | HHS and affected individuals | 60 days |
| PCI-DSS | Card brands and acquiring bank | Immediate |
| State Laws | Varies by jurisdiction | Varies |
| SEC | Material cybersecurity incidents | 4 business days |

## Quick Reference: Immediate Actions

```
FIRST 30 MINUTES:
[ ] Validate alert/notification
[ ] Open incident ticket
[ ] Classify exfiltration type
[ ] Determine data sensitivity
[ ] Escalate to incident commander
[ ] Begin evidence preservation
[ ] Disable compromised credentials
[ ] Implement network blocks
```

## Related Documentation

- IRP-DataExfiltration-SOP.md - Full incident response procedures
- IRP-DataLoss - Data Loss/Data Breach playbook
- IRP-Malware - Malware Response playbook
- IRP-AccountCompromised - Account Compromise playbook
- IRP-Ransomware - Ransomware Response playbook

## References

- [MITRE ATT&CK TA0010: Exfiltration](https://attack.mitre.org/tactics/TA0010/)
- [NIST SP 800-61r2: Computer Security Incident Handling Guide](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)
- [AWS Security Incident Response Guide](https://docs.aws.amazon.com/whitepapers/latest/aws-security-incident-response-guide/welcome.html)
