# Guard Sight CIRT Playbook Battle Card Reference Documentation

## Overview

Guard Sight provides a comprehensive library of CIRT (Cyber Incident Response Team) Playbook Battle Cards that deliver structured, actionable incident response guidance aligned with the MITRE ATT&CK framework. Each playbook follows the PICERL methodology for consistent security operations.

## PICERL Methodology

### (P) Preparation
Proactive security measures to prevent and prepare for incidents:
- Vulnerability patching and security control inspections
- Antivirus/EDR deployment and signature maintenance
- Network segmentation and centralized logging
- Backup validation and off-site storage
- User awareness training and phishing simulations
- Threat intelligence integration
- Response training and tabletop exercises

### (I) Identification
Detection and investigation of security incidents:
- Network traffic analysis (DNS, C2 connections, TOR/I2P)
- Endpoint monitoring (file changes, process activity, EDR alerts)
- Authentication monitoring (failed logins, privilege escalation)
- Email security (phishing, SPF/DKIM failures)
- Log correlation across IDS/IPS, SIEM, and threat intelligence

### (C) Containment
Tactical threat neutralization using the 6 D's:
- **Detect**: Identify scope and affected assets
- **Deny**: Block threat actor access
- **Disrupt**: Interrupt attack chains
- **Degrade**: Reduce adversary capabilities
- **Deceive**: Deploy deception technology
- **Destroy**: Terminate malicious processes

OODA Loop execution: Observe -> Orient -> Decide -> Act

### (E) Eradication
Complete threat removal:
- Close attack vectors
- Re-image compromised systems
- Remove persistence mechanisms
- Reset compromised credentials
- Implement new threat signatures

### (R) Recovery
Business restoration:
- Restore to RPO within RTO
- Verify backup integrity before restoration
- Address collateral damage
- Resolve related incidents
- Coordinate with legal and external parties

### (L) Lessons Learned
Continuous improvement:
- After-action reports
- Policy updates
- Detection rule enhancements
- User education updates
- Intelligence sharing

---

## Playbook Categories

### Initial Access Playbooks

#### GSPBC-1001: Mobile Device SIM Attacks
**MITRE ATT&CK**: T1451 - Exploit via Mobile Device

**Key Preparation**:
- Favor authenticator apps over SMS for 2FA
- Create strong account PIN/passphrase
- Use dedicated numbers for high-value accounts
- Use password managers
- Prepare backup communication methods (Hangouts, GVoice, Skype)

**Detection Indicators**:
- Unexplained, prolonged loss of cell service
- Unexpected customer service calls
- Password/authentication change alerts
- Suspicious login location alerts

**Containment Actions**:
- Notify mobile carrier immediately
- Request number disabled on compromised SIM
- Request number ported back to your SIM
- Document employee names, case numbers, dates
- Request IMEI logs preserved
- Change all passwords from trusted device (email first)

---

#### GSPBC-1053: Exploit Public-Facing Application
**MITRE ATT&CK**: T1190 - Exploit Public-Facing Application

**Key Preparation**:
- Deploy Web Application Firewalls (WAFs)
- Segment externally-facing servers with DMZ
- Review firewall/IDS/IPS rules regularly
- Apply least privilege principles

**Detection Indicators**:
- Deep packet inspection for SQL injection, known payloads
- Unusual firewall/IDS/IPS/SIEM log activity

**Containment Actions**:
- Perimeter enforcement for threat actor IPs
- Archive attack artifacts (IPs, user agents, requests)
- Determine attack source and pathway

---

#### GSPBC-1011: Drive-by Compromise
**MITRE ATT&CK**: T1189 - Drive-by Compromise

**Key Preparation**:
- Restrict web-based content (JavaScript, untrusted downloads)
- Use browser isolation technology
- Maintain browser and plugin updates

---

#### GSPBC-1012: Unauthorized VPN/VDI Access
**MITRE ATT&CK**: T1133 - External Remote Services

**Key Preparation**:
- Implement MFA for all remote access
- Monitor for anomalous login locations/times
- Restrict VPN access to authorized devices only

---

### Credential Access Playbooks

#### GSPBC-1002: Spearphishing/Phishing
**MITRE ATT&CK**: T1566 - Phishing

**Key Preparation**:
- Routine phishing education and simulations
- Log incoming/outgoing emails
- Establish user reporting method for suspicious emails
- SPF/DKIM/DMARC implementation

**Detection Indicators**:
- Unusual DNS activity
- Emails with suspicious attachments
- Multiple identical emails from unknown sources
- Emails from typo domains
- SPF/DKIM failures

**Containment Actions**:
- Lock/reset passwords for affected users
- Perimeter enforcement for threat actor locations

**Recovery Actions**:
- Verify compromised credentials changed
- Restore/re-image systems with malware
- Blacklist phishing sources (addresses and domains)

---

#### GSPBC-1017: Password Spraying
**MITRE ATT&CK**: T1110.003 - Password Spraying

**Key Preparation**:
- Multi-factor authentication deployment
- Secure password policy enforcement
- Network segmentation to limit access
- Authentication logging to central location

**Detection Indicators**:
- Failed login attempts for default/common account names
- Same account failures across multiple systems
- Multiple system failures from single source

**Containment Actions**:
- Review logs for successful attacker logins
- Lock compromised accounts
- Perimeter enforcement

**References**:
- NIST Digital Identity Guidelines: https://pages.nist.gov/800-63-3/sp800-63-3.html
- Microsoft Password Guidance

---

#### GSPBC-1024: OS Credential Dumping
**MITRE ATT&CK**: T1003 - OS Credential Dumping

**Key Preparation**:
- Limit credential overlap across accounts/systems
- Secure Domain Controller backups
- Avoid domain accounts in local admin groups
- Add users to "Protected Users" AD security group
- Consider disabling WDigest and restricting NTLM

**Detection Indicators**:
- Processes/command-line arguments indicating credential dumping
- Unexpected processes interacting with lsass.exe
- Security Accounts Manager (SAM) access on local filesystem
- Domain controller replication requests and unscheduled activity
- Verify lsass.exe runs as protected process (Win 8.1+, Server 2012 R2+)

**Containment Actions**:
- Deploy EDR hunter/killer agents
- Remove affected system from network
- Determine attack source and pathway

**Recovery Actions**:
- Reset compromised passwords
- If Domain Admin compromised: reset krbtgt password
- Restore affected systems from clean backup

---

#### GSPBC-1048: Brute Force
**MITRE ATT&CK**: T1110 - Brute Force (all sub-techniques)

**Key Preparation**:
- Account lockout policies after failed attempts
- Multi-factor authentication
- Strong password policies
- Least privilege access

**Detection Indicators**:
- High volumes of authentication failures via:
  - Password guessing (T1110.001)
  - Password cracking (T1110.002)
  - Password spraying (T1110.003)
  - Credential stuffing (T1110.004)

**Lessons Learned**:
- View events as part of behavior chain, not in isolation

---

#### GSPBC-1035: Credentials from Password Stores
**MITRE ATT&CK**: T1555 - Credentials from Password Stores

**Key Preparation**:
- Limit password store access
- Monitor for credential store access attempts
- Use enterprise password management solutions

---

### Persistence Playbooks

#### GSPBC-1005: Backdoor User Accounts
**MITRE ATT&CK**: T1136 - Create Account

**Key Preparation**:
- Security alerts for privileged account creation
- Remove inactive/unused accounts
- Regular account auditing

**Detection Indicators**:
- Unusual DNS activity
- Privileged account creation
- Unexpected permission changes
- Review log activity of new accounts AND creating accounts
- Contact users out-of-band about new accounts

**Containment Actions**:
- Lock suspicious accounts
- Lock compromised accounts
- Review activity of new and compromised accounts
- Remove systems with malware from network

**Recovery Actions**:
- If Domain Admin access gained: reset krbtgt password

---

#### GSPBC-1009: Web Shells
**MITRE ATT&CK**: T1505.003 - Web Shell

**Key Preparation**:
- Disable script execution in non-required directories
- Web applications should not run with excessive privileges
- Use AppArmor, SELinux, or similar mitigations

**Detection Indicators**:
- Unusual error messages in web logs
- Unusual web traffic patterns
- Unexpected changes in document roots
- IPS/IDS and antivirus alerts

**Containment Actions**:
- Review web logs for web shell access instances

**Eradication Actions**:
- Scan web servers for other web shell instances
- Determine web shell placement method
- Reset potentially compromised passwords

---

#### GSPBC-1007: Malicious Browser Extensions
**MITRE ATT&CK**: T1176 - Browser Extensions

**Key Preparation**:
- Whitelist approved browser extensions
- Monitor for unauthorized extension installations
- User education on extension risks

---

#### GSPBC-1019: BITS Jobs
**MITRE ATT&CK**: T1197 - BITS Jobs

**Key Preparation**:
- Monitor BITS job creation
- Limit BITS usage to authorized applications

---

#### GSPBC-1020: Pre-OS Boot
**MITRE ATT&CK**: T1542 - Pre-OS Boot

**Key Preparation**:
- Enable Secure Boot
- Monitor firmware integrity
- Use TPM-based boot verification

---

#### GSPBC-1041: Boot/Logon Autostart Execution
**MITRE ATT&CK**: T1547 - Boot or Logon Autostart Execution

**Key Preparation**:
- Monitor registry run keys
- Monitor startup folders
- Application whitelisting

---

### Lateral Movement Playbooks

#### GSPBC-1004: Pass the Hash
**MITRE ATT&CK**: T1550.002 - Pass the Hash

**Key Preparation**:
- Network segmentation and firewalls
- Disable NTLM authentication where possible (SMB, HTTP, SMTP)
- Centralized logging

**Detection Indicators**:
- Unusual user activity
- Unexpected logins using NTLM

**Containment Actions**:
- Lock accounts with suspected compromised hash
- Remove systems with malware from network

**Recovery Actions**:
- Change passwords of potentially compromised accounts
- Determine chain of events leading to incident
- Resolve related security incidents

---

#### GSPBC-1039: Alternate Authentication Material
**MITRE ATT&CK**: T1550 - Use Alternate Authentication Material

**Key Preparation**:
- Monitor for authentication token misuse
- Implement token expiration policies
- Detect pass-the-ticket attacks

---

#### GSPBC-1042: Replication Through Removable Media
**MITRE ATT&CK**: T1091 - Replication Through Removable Media

**Key Preparation**:
- Disable autorun for removable media
- USB device control policies
- Monitor removable media usage

---

#### GSPBC-1044: Taint Shared Content
**MITRE ATT&CK**: T1080 - Taint Shared Content

**Key Preparation**:
- Monitor file share modifications
- Implement file integrity monitoring
- Restrict write access to shared content

---

### Execution Playbooks

#### GSPBC-1029: User Execution
**MITRE ATT&CK**: T1204 - User Execution

**Key Preparation**:
- Employee security awareness training
- Restrict web-based content (JavaScript, untrusted downloads, browser extensions)
- Application whitelisting
- Reference GSPBC-1002 for phishing prevention

**Detection Indicators**:
- Abnormal network activity
- Unauthorized downloads
- Suspicious email attachments
- Unusual executables (.exe, .doc, .pdf, .xls, .rtf, .scr, .lnk, .pif, .cpl)

**Containment Actions**:
- Deploy EDR hunter/killer agents
- Remove affected system from network
- Determine attack source and pathway

---

#### GSPBC-1034: Native API
**MITRE ATT&CK**: T1106 - Native API

**Key Preparation**:
- Monitor for suspicious API calls
- Behavioral analysis for API abuse

---

#### GSPBC-1037: Deploy Container
**MITRE ATT&CK**: T1610 - Deploy Container

**Key Preparation**:
- Container image scanning
- Runtime security monitoring
- Restrict container privileges

---

#### GSPBC-1043: Exploitation for Client Execution
**MITRE ATT&CK**: T1203 - Exploitation for Client Execution

**Key Preparation**:
- Application sandboxing
- Exploit mitigation tools
- Regular patching

---

### Privilege Escalation Playbooks

#### GSPBC-1023: Exploitation for Privilege Escalation
**MITRE ATT&CK**: T1068 - Exploitation for Privilege Escalation

**Key Preparation**:
- Application sandboxing
- Windows Defender Exploit Guard or similar
- Good patch management practices

**Detection Indicators**:
- Unusual DNS activity
- Antivirus/EDR alerts
- IDS/IPS alerts
- Activity before/after escalation attempts may produce IOC

**Containment Actions**:
- Remove affected system from network
- Determine attack source and pathway

---

#### GSPBC-1021: Group Policy Modification
**MITRE ATT&CK**: T1484 - Group Policy Modification

**Key Preparation**:
- Monitor GPO changes
- Implement GPO change approval process
- Audit GPO modifications

---

#### GSPBC-1045: Create/Modify System Process
**MITRE ATT&CK**: T1543 - Create or Modify System Process

**Key Preparation**:
- Monitor service creation/modification
- Restrict service installation privileges
- Application whitelisting

---

### Impact Playbooks

#### GSPBC-1000: Ransomware (Data Encrypted for Impact)
**MITRE ATT&CK**: T1486 - Data Encrypted for Impact

**Key Preparation**:
- Confirm backups are malware-free
- Establish cryptocurrency payment capability (contingency)
- Obtain decryption keys for known variants
- Confirm cybersecurity insurance coverage
- Conduct ransomware simulations
- Examine file shares for loose/open privileges
- Network segmentation with inter-segment logging
- Incorporate deception technology

**Detection Indicators**:
- Ransomware notes/messages
- Unusual/malicious file extensions
- User reports of corrupt/unreadable files
- High velocity file renaming
- CPU spikes on file sharing systems
- Unusual userland executables
- Network connections to C2/exploit kits
- Use of TOR or I2P

**Containment Actions**:
- Locate and isolate assets encrypting files
- Isolate impacted file sharing systems
- Close attack vector
- Fortify non-impacted systems
- Deploy EDR hunter/killer agents

**Eradication Actions**:
- Re-image impacted assets
- Inspect backups for IOC PRIOR to recovery
- Implement newly obtained threat signatures

**Recovery Actions**:
- Restore to RPO within RTO
- Restore from known clean backups

**References**:
- Paying ransoms is discouraged but should be executive contingency

---

#### GSPBC-1027: Disk Wipe
**MITRE ATT&CK**: T1561 - Disk Wipe

**Key Preparation**:
- Regular backups with hardened off-site/offline storage
- IT disaster recovery plan
- Threat intelligence utilization
- Know data loss notification laws/obligations

**Detection Indicators**:
- Attempts to write to MBR or partition table
- Unusual kernel driver activity
- Direct drive access using "\\.\" notation
- IDS/IPS and antivirus alerts

**Containment Actions**:
- Deploy EDR hunter/killer agents
- Determine what data was stored on device

---

#### GSPBC-1013: Defacement
**MITRE ATT&CK**: T1491 - Defacement

**Key Preparation**:
- File integrity monitoring for web content
- Backup web assets
- Monitor for unauthorized changes

---

#### GSPBC-1014: Inhibit System Recovery
**MITRE ATT&CK**: T1490 - Inhibit System Recovery (Disabling Volume Shadow Service)

**Key Preparation**:
- Monitor for VSS deletion attempts
- Protect backup services
- Off-site backup storage

---

#### GSPBC-1049: Resource Hijacking
**MITRE ATT&CK**: T1496 - Resource Hijacking

**Key Preparation**:
- Monitor for cryptomining activity
- Resource utilization monitoring
- Network traffic analysis for mining pools

---

### Exfiltration Playbooks

#### GSPBC-1003: Automated Exfiltration (Data Theft)
**MITRE ATT&CK**: T1020 - Automated Exfiltration

**Key Preparation**:
- Antivirus/Endpoint Protection on workstations
- Security awareness training

**Detection Indicators**:
- Unusual DNS activity
- Unusual file system activity
- Unusual network activity
- Antivirus/endpoint alerts

**Containment Actions**:
- Temporarily remove affected systems from network

**Recovery Actions**:
- Identify malware strain
- Determine what data may have been uploaded
- Block associated IP addresses on perimeter firewalls

---

#### GSPBC-1051: Exfiltration Over Physical Medium
**MITRE ATT&CK**: T1052 - Exfiltration Over Physical Medium

**Key Preparation**:
- USB device control
- DLP solutions
- Monitor removable media usage

---

### Reconnaissance Playbooks

#### GSPBC-1030: Active Scanning
**MITRE ATT&CK**: T1595 - Active Scanning

**Key Preparation**:
- Update firewall/IDS/IPS rules regularly
- Restrict access to RDP, SSH, and similar protocols
- Remove default banners from remote protocols
- Remove default headers from web applications

**Detection Indicators**:
- Excessive requests on public-facing assets from single source
- Abnormal requests for applications and protocols
- Suspicious user-agent strings and artifacts

**Containment Actions**:
- Archive scanning artifacts (IPs, user agents, requests)
- Perimeter enforcement for threat actor locations

**Recovery Actions**:
- Assess exposed technologies

---

### Discovery Playbooks

#### GSPBC-1040: Process Discovery
**MITRE ATT&CK**: T1057 - Process Discovery

**Key Preparation**:
- Monitor for process enumeration commands
- Behavioral analysis for discovery activity

---

#### GSPBC-1054: Password Policy Discovery
**MITRE ATT&CK**: T1201 - Password Policy Discovery

**Key Preparation**:
- Monitor for policy enumeration
- Limit policy information disclosure

---

### Collection Playbooks

#### GSPBC-1018: Cloud Email Compromise
**MITRE ATT&CK**: T1114 - Email Collection

**Key Preparation**:
- MFA for cloud email access
- Monitor for suspicious email forwarding rules
- Audit mailbox access

---

### Resource Development Playbooks

#### GSPBC-1032: Compromise Accounts
**MITRE ATT&CK**: T1586 - Compromise Accounts

**Key Preparation**:
- Monitor for compromised credential usage
- Dark web monitoring for organizational credentials
- Password breach monitoring

---

### Special Scenarios

#### GSPBC-1008: CEO Fraud / Money Mule Scams
**Key Preparation**:
- Wire transfer verification procedures
- Executive impersonation awareness
- Out-of-band verification for financial requests

---

#### GSPBC-1010: Device Theft / Device Loss
**Key Preparation**:
- Full disk encryption
- Remote wipe capability
- Asset tracking
- Quick response procedures for lost devices

---

## MITRE ATT&CK Quick Reference

| Playbook | Technique ID | Technique Name |
|----------|--------------|----------------|
| GSPBC-1000 | T1486 | Data Encrypted for Impact |
| GSPBC-1001 | T1451 | Exploit via Mobile Device |
| GSPBC-1002 | T1566 | Phishing |
| GSPBC-1003 | T1020 | Automated Exfiltration |
| GSPBC-1004 | T1550.002 | Pass the Hash |
| GSPBC-1005 | T1136 | Create Account |
| GSPBC-1009 | T1505.003 | Web Shell |
| GSPBC-1017 | T1110.003 | Password Spraying |
| GSPBC-1023 | T1068 | Exploitation for Privilege Escalation |
| GSPBC-1024 | T1003 | OS Credential Dumping |
| GSPBC-1027 | T1561 | Disk Wipe |
| GSPBC-1029 | T1204 | User Execution |
| GSPBC-1030 | T1595 | Active Scanning |
| GSPBC-1048 | T1110 | Brute Force |
| GSPBC-1053 | T1190 | Exploit Public-Facing Application |

## External Resources

### Guard Sight Resources
- **GSVSOC Incident Response Plan**: https://github.com/guardsight/gsvsoc_cybersecurity-incident-response-plan
- **GSVSOC CIRT Playbook Battle Cards**: https://github.com/guardsight/gsvsoc_cirt-playbook-battle-cards

### Government Resources
- **IT Disaster Recovery Planning**: https://www.ready.gov/it-disaster-recovery-plan
- **Report Cybercrime (IC3)**: https://www.ic3.gov/Home/FAQ
- **NIST Digital Identity Guidelines**: https://pages.nist.gov/800-63-3/sp800-63-3.html

### MITRE Resources
- **MITRE ATT&CK Framework**: https://attack.mitre.org
- **ATT&CK Mitigations**: https://attack.mitre.org/mitigations/
- **ATT&CK Data Sources**: https://attack.mitre.org/datasources/

## Integration with Other Consultants

The Guard Sight Specialist works with:
- **SOC Analyst**: Alert triage and initial identification
- **Incident Response Lead**: Major incident coordination
- **Malware Response Analyst**: Malware identification and analysis
- **Credential Access Analyst**: Credential theft investigation
- **Lateral Movement Analyst**: Movement detection and containment
- **Persistence Analyst**: Persistence mechanism eradication
- **NIST CSF Specialist**: Framework compliance alignment
- **Threat Intel Manager**: IOC enrichment and intelligence sharing
