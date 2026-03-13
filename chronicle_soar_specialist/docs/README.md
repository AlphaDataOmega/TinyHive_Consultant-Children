# Chronicle SOAR Specialist Documentation

## Overview

This consultant specializes in Google Chronicle SOAR (formerly Siemplify) playbook development, providing expertise in automated security operations workflows for restricted hours detection, phishing triage, and certificate validation.

## Core Playbooks

### 1. Restricted Hours Logon Attempt Detection

**Trigger**: Alert Name matches "User Attempted Logon on Restricted Hours"

**Workflow Steps**:
1. Priority escalation to High
2. Logon type classification (RDP Type 10, Interactive Type 2, Service/Task)
3. Add logon type insight to case
4. Manager contact retrieval from Azure AD
5. Workstation connectivity check
6. External IP reputation check via APIVoid
7. User enrichment with manager details
8. Password reset (manual approval required)

**Key Integrations**: Azure Active Directory, APIVoid, Siemplify

### 2. Phishing Email Enrichment and Triage

**Trigger**: Alert contains "Phishing" tag

**Workflow Steps**:
1. Hash enrichment via ThreatFuse (Anomali ThreatStream)
2. MITRE ATT&CK technique lookup (T1566.002)
3. URL entity selection and grouping
4. User identity enrichment via Hibob
5. Source user threat intelligence check
6. Priority adjustment based on findings
7. Analyst decision point (escalate or close)
8. Case tagging based on determination

**Triage Decision Matrix**:
| Indicator Type | Threat Score | Confidence | Action |
|---------------|--------------|------------|--------|
| File Hash | >= 80 | >= 80 | Immediate escalation |
| Email Address | >= 80 | >= 80 | Block sender, escalate |
| URL | >= 80 | >= 80 | Block URL, notify users |
| Any | < 50 | < 50 | Auto-close as false positive |

### 3. Website Certificate Validation

**Trigger**: Alert Name = "Website Certificate Validation"

**Workflow Steps**:
1. Certificate details retrieval (issuer, dates, chain status)
2. Case name adjustment with website identifier
3. Expiration check conditional branch
4. Expired path: Tag, screenshot capture, escalation
5. Valid path: Auto-close case

**Certificate Monitoring Thresholds**:
| Days to Expiration | Status | Action |
|-------------------|--------|--------|
| > 30 days | Green | Auto-close |
| 15-30 days | Yellow | Create reminder |
| 7-14 days | Orange | Alert IT Operations |
| 1-7 days | Red | Critical alert |
| < 1 day | Critical | Emergency response |

## Integration Requirements

### Azure Active Directory
- **Permissions**: User.Read.All, User.ReadWrite.All, Directory.Read.All
- **Purpose**: User/manager lookups, password resets

### ThreatFuse (Anomali ThreatStream)
- **Purpose**: Threat intelligence enrichment
- **Default Parameters**: Severity threshold Low, Confidence threshold 0

### APIVoid
- **Purpose**: IP reputation checking
- **Threshold**: 1 (any blacklist hit triggers alert)

### Hibob
- **Purpose**: Employee HR data enrichment
- **Data Retrieved**: Name, email, department, manager, site, employment status

### ScreenshotMachine
- **Purpose**: Website visual capture for evidence
- **Parameters**: 2000ms delay, JPG format

### MITRE ATT&CK
- **Purpose**: Attack technique context and detection guidance
- **Key Techniques**: T1566 (Phishing), T1566.001 (Attachment), T1566.002 (Link)

## Priority Levels and Response Times

| Priority | Response Time | Escalation |
|----------|---------------|------------|
| Critical | < 15 minutes | Immediate CISO notification |
| High | < 1 hour | Security Manager notification |
| Medium | < 4 hours | SOC Lead review |
| Low | < 24 hours | Batch review acceptable |

## Case Closure Reasons

| Reason | Use Case |
|--------|----------|
| NotMalicious | Confirmed false positive, valid certificate |
| Maintenance | Authorized scheduled activity |
| Malicious | Confirmed threat, actual phishing |
| Inconclusive | Insufficient data for decision |

## Windows Logon Type Reference

| Type | Description | Security Implication |
|------|-------------|---------------------|
| 2 | Interactive (keyboard/screen) | Physical access |
| 3 | Network (file share) | Remote resource access |
| 10 | RemoteInteractive (RDP) | Remote Desktop session |
| 4/5 | Batch/Service | Automated processes |

## Source Reference

- SOP Document: SOP-CHRONICLE-SOAR-001
- Platform: Google Chronicle / Siemplify SOAR
- Source Playbook Files:
  - Attempt_To_Logon_on_Restricted Hours.json
  - Phishing-Enrichment_and_Triage.json
  - Website_Certificate_Validation.json
