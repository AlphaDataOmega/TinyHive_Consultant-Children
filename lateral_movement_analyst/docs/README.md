# Lateral Movement Analyst Documentation

## Overview

This documentation supports the Lateral Movement Analyst consultant child, which specializes in detecting and responding to MITRE ATT&CK Tactic TA0008 (Lateral Movement) attacks.

## Core Competencies

### MITRE ATT&CK Lateral Movement Techniques

| ID | Technique | Description |
|----|-----------|-------------|
| T1021 | Remote Services | Using RDP, SSH, SMB, VNC, WinRM |
| T1072 | Software Deployment Tools | Abusing enterprise deployment tools |
| T1080 | Taint Shared Content | Modifying shared network resources |
| T1091 | Replication Through Removable Media | USB-based propagation |
| T1210 | Exploitation of Remote Services | Exploiting vulnerabilities in remote services |
| T1534 | Internal Spearphishing | Phishing internal users from compromised accounts |
| T1550 | Use Alternate Authentication | Pass-the-Hash, Pass-the-Ticket, Web Session Cookie |
| T1563 | Remote Service Session Hijacking | Hijacking existing sessions |
| T1570 | Lateral Tool Transfer | Moving tools between systems |

### Pass-the-Hash (T1550.002) Focus

Pass-the-Hash is a primary technique where adversaries capture password hashes and use them to authenticate without knowing the plaintext password.

**Common Tools Used by Adversaries**:
- Mimikatz
- Impacket
- Metasploit
- CrackMapExec

**Prevention Controls**:
1. Enable Credential Guard on Windows 10/Server 2016+
2. Disable LM and NTLMv1 authentication
3. Use Protected Users Security Group for privileged accounts
4. Implement Local Administrator Password Solution (LAPS)
5. Restrict privileged accounts from network logons

## Detection Capabilities

### Key Detection Events

| Log Source | Event ID | Purpose |
|------------|----------|---------|
| Windows Security | 4624 | Successful logon (check LogonType=3, AuthPackage=NTLM) |
| Windows Security | 4625 | Failed logon attempts |
| Windows Security | 4648 | Explicit credential logon |
| Windows Security | 4768 | Kerberos TGT request |
| Windows Security | 4769 | Kerberos service ticket request |
| Windows Security | 5140 | Network share access (ADMIN$, C$) |
| Windows System | 7045 | Service installation |
| Sysmon | 1, 3, 7, 8, 10, 11 | Process, network, image load events |

### SIEM Detection Rules

#### Admin Share Access Detection
```
Event Source: Windows Security
Event ID: 5140
Share Name: ADMIN$ OR C$
User: NOT in approved_admin_list
Alert: Potential lateral movement via admin share
```

#### Pass-the-Hash Indicator
```
Event Source: Windows Security
Event ID: 4624
Logon Type: 3 (Network)
Authentication Package: NTLM
Source IP: Internal workstation
Destination: Server or different workstation
Alert: Possible Pass-the-Hash activity
```

#### Remote Service Installation
```
Event Source: Windows System
Event ID: 7045
Service Name: Contains random characters OR known malicious patterns
Alert: Potential lateral movement via service creation
```

## Incident Response Workflow

### Detection Workflow

1. Alert Triggered
2. Verify Alert Authenticity (false positive check, baseline review)
3. Investigate Associated Activity (review alerts for impacted assets)
4. Determine Scope (systems affected, accounts involved)
5. Escalate if Confirmed (notify Incident Commander)

### Containment Strategies by Technique

| Technique | Containment Approach |
|-----------|---------------------|
| Pass-the-Hash | Reset compromised account passwords; disable NTLM |
| RDP Abuse | Restrict RDP access; implement jump servers |
| SMB Lateral | Block unnecessary SMB traffic between segments |
| WMI/WinRM | Disable remote WMI where not required |
| PsExec | Block ADMIN$ share access; monitor service installations |

### OODA Loop Application

- **OBSERVE**: Gather all relevant data
- **ORIENT**: Analyze the threat context
- **DECIDE**: Choose containment strategy
- **ACT**: Execute containment measures
- **REPEAT**: As situation evolves

## Credential Remediation Procedures

### Standard Credential Reset
- Force password resets for affected accounts
- Revoke and reissue certificates for compromised accounts/devices

### Domain Controller Compromise
If DC compromise is suspected:
1. Reset all local account passwords (Guest, HelpAssistant, DefaultAccount, System, Administrator)
2. Reset krbtgt account password TWICE (wait for replication between resets)

### Full Domain Compromise
If ntds.dit file is exfiltrated: Reset ALL domain user passwords

## Recovery Requirements

### Post-Recovery Monitoring
- **Duration**: 72 hours minimum
- **Focus Areas**:
  - Authentication patterns for recovered accounts
  - Network traffic from recovered systems
  - Process execution on recovered endpoints
  - Signs of persistence mechanisms

### Recovery Verification Checklist
- [ ] All affected systems patched and updated
- [ ] Compromised credentials rotated
- [ ] Network segmentation verified
- [ ] Detection signatures updated
- [ ] EDR/AV fully operational
- [ ] Logging restored and verified
- [ ] Related security incidents resolved

## References

### MITRE ATT&CK
- [TA0008 - Lateral Movement](https://attack.mitre.org/tactics/TA0008/)
- [T1550.002 - Pass the Hash](https://attack.mitre.org/techniques/T1550/002/)
- [T1021 - Remote Services](https://attack.mitre.org/techniques/T1021/)

### Standards and Frameworks
- NIST SP 800-61r2 - Computer Security Incident Handling Guide
- Microsoft Security Documentation - Credential Guard
- CISA Lateral Movement Detection Best Practices

### Related SOPs
- Initial Access Detection and Response
- Credential Access Incident Response
- Persistence Detection and Remediation
- Privilege Escalation Response
