# LetsDefend IR Specialist Documentation

## Overview

This directory contains reference materials and procedures for the LetsDefend IR Specialist agent, which responds to malware, phishing, and ransomware incidents using the LetsDefend methodology.

## Core Playbooks

### Malware Incident Response

The malware playbook follows this workflow:

1. **Verify Alert** — Confirm alert is true positive from Tier-1 escalation
2. **Connect to Machine** — Access affected device via Endpoint Security console
3. **Analyze Malware** — Use VirusTotal, AnyRun, Hybrid Analysis to identify threat
4. **Determine Malware Type** — Categorize as spyware, adware, ransomware, worm, or rootkit
5. **Identify Initial Access** — Determine root cause (phishing, exploit, valid accounts, supply chain)
6. **Define Scope** — Check if IOCs appear on multiple machines
7. **Analyze Spread** — Identify propagation method
8. **Check Quarantine Status** — Verify endpoint security action
9. **Verify Execution** — Determine if malware executed successfully
10. **Check C2 Communication** — Search logs for C2 address access
11. **Contain Systems** — Isolate affected devices
12. **Backup Evidence** — Preserve memory, disk, logs before eradication
13. **Eradicate Malware** — Remove files, registry entries, persistence mechanisms
14. **Recover Systems** — Restore from backup, apply patches, reset credentials
15. **Document Lessons Learned** — Record artifacts and recommendations

### Phishing Incident Response

The phishing playbook follows this workflow:

1. **Parse Email** — Extract sender, recipient, timestamp, SMTP address, subject, attachments
2. **Check for Attachments/URLs** — Identify malicious content
3. **Analyze URL/Attachment** — Use sandbox analysis services
4. **Determine if Malicious** — Classify threat type and extract IOCs
5. **Check Email Delivery** — Verify if email reached user inbox
6. **Contact User** — Delete email and interview user about interactions
7. **Assess User Interaction** — Determine if link clicked or attachment opened
8. **Perform Header Analysis** — Check SPF, DKIM, DMARC, analyze received headers
9. **Contain Threat** — Isolate endpoints, reset credentials, block IOCs
10. **Document Lessons Learned** — Record artifacts and recommendations

### Ransomware Incident Response

The ransomware playbook follows this workflow:

1. **Verify Alert** — Confirm ransomware activity from Tier-1 escalation
2. **Connect to Machine** — Access affected device
3. **Identify via Ransom Notes** — Check desktop/drives for ransom messages
4. **Identify via Characteristics** — Analyze payment method, language, support features
5. **Identify via File Analysis** — Check encrypted file extensions and icons
6. **Use Automated Services** — Upload samples to ID Ransomware, No More Ransom
7. **Identify Root Cause** — Determine initial access vector
8. **Analyze Initial Access** — Map to MITRE ATT&CK technique
9. **Determine Scope** — Search for IOCs across environment
10. **Contain Ransomware** — Immediately isolate from network, stop backup processes
11. **Backup Evidence** — Capture memory (may contain encryption keys)
12. **Eradicate Ransomware** — Remove executable and persistence mechanisms
13. **Recover Systems** — Restore from backup, use decryption tools, or rebuild
14. **Document Lessons Learned** — Record artifacts and recommendations

## Severity Classification

| Severity | Response Time | Examples |
|----------|---------------|----------|
| Critical | < 15 minutes | Active ransomware, confirmed data exfiltration |
| High | < 1 hour | Confirmed malware infection, successful credential theft |
| Medium | < 4 hours | Suspicious activity, blocked phishing attempt |
| Low | < 24 hours | False positive, informational alert |

## Analysis Tools

| Tool | Purpose | URL |
|------|---------|-----|
| VirusTotal | Multi-engine malware scanning | https://www.virustotal.com |
| AnyRun | Interactive malware sandbox | https://any.run |
| Hybrid Analysis | Automated malware analysis | https://www.hybrid-analysis.com |
| ID Ransomware | Ransomware identification | https://id-ransomware.malwarehunterteam.com |
| No More Ransom | Decryption tools | https://www.nomoreransom.org |
| MXToolbox | Email header analysis | https://mxtoolbox.com/EmailHeaders.aspx |

## Evidence Collection Checklist

- [ ] Memory dump (capture before shutdown)
- [ ] Disk image (full or targeted)
- [ ] Malware samples (password-protected archive)
- [ ] System logs (system, security, application)
- [ ] Network captures (if available)
- [ ] Ransom notes (for ransomware)
- [ ] Email headers (for phishing)
- [ ] Timeline of events
- [ ] Screenshots of findings

## MITRE ATT&CK Initial Access Techniques

| Technique | MITRE ID | Investigation Focus |
|-----------|----------|---------------------|
| Drive-by Compromise | T1189 | Browser history, web proxy logs |
| Exploit Public-Facing Application | T1190 | Web server logs, vulnerability assessment |
| External Remote Services | T1133 | VPN/RDP logs, access times |
| Phishing | T1566 | Email logs, user interviews |
| Replication Through Removable Media | T1091 | USB device logs |
| Supply Chain Compromise | T1195 | Software inventory, update history |
| Trusted Relationship | T1199 | Third-party access logs |
| Valid Accounts | T1078 | Authentication logs, credential sources |

## Documentation Templates

### Incident Ticket Template

```
Ticket ID: [AUTO-GENERATED]
Date/Time: [TIMESTAMP]
Analyst: [NAME]

INITIAL ALERT
- Alert Source:
- Alert Type:
- Severity:
- Affected System(s):

VERIFICATION
- True Positive: [YES/NO]
- Verification Method:

ANALYSIS
- Threat Type:
- IOCs Identified:
- Scope:

CONTAINMENT
- Actions Taken:
- Timestamp:

ERADICATION
- Actions Taken:
- Timestamp:

RECOVERY
- Actions Taken:
- Timestamp:

CLOSURE
- Root Cause:
- Recommendations:
- Lessons Learned:
```

### Artifact Documentation Template

```
ARTIFACT RECORD

File/Object Name:
Hash (MD5):
Hash (SHA1):
Hash (SHA256):
File Size:
First Seen:
Location Found:
Analysis Results:
Associated IOCs:
```

## Escalation Criteria

**Escalate to IR Lead when:**
- Multiple systems affected
- Confirmed data exfiltration
- Ransomware encryption active
- Executive/VIP systems involved
- Regulatory notification may be required

**Escalate to Management when:**
- Critical business systems affected
- Customer data potentially compromised
- Ransom demand received
- Law enforcement involvement needed
- Public disclosure required

## Related SOPs

- SOP-LetsDefend-Incident-Response-Playbooks.md
- IRP-Malware incident response procedures
- IRP-Ransom ransomware response procedures
