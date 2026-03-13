# Collection Analyst Documentation

## Overview

This directory contains reference materials for the Collection Analyst consultant, specializing in MITRE ATT&CK Collection tactic (TA0009) detection and response.

## MITRE ATT&CK Coverage

### Primary Tactic
| Tactic | Tactic ID | Description |
|--------|-----------|-------------|
| Collection | TA0009 | The adversary is trying to gather data of interest to their goal |

### Key Techniques
| Technique ID | Name | Description |
|--------------|------|-------------|
| T1560 | Archive Collected Data | Data compressed/encrypted before exfiltration |
| T1123 | Audio Capture | Recording audio via microphone |
| T1119 | Automated Collection | Scripts/tools for mass data gathering |
| T1115 | Clipboard Data | Data copied from clipboard |
| T1530 | Data from Cloud Storage | Accessing cloud storage objects |
| T1602 | Data from Configuration Repository | SNMP/network configs |
| T1213 | Data from Information Repositories | SharePoint, Confluence, etc. |
| T1005 | Data from Local System | Sensitive local files |
| T1039 | Data from Network Shared Drive | Mapped drives, file shares |
| T1025 | Data from Removable Media | USB, external drives |
| T1114 | Email Collection | Email box access/forwarding |
| T1056 | Input Capture | Keylogging, credential capture |
| T1185 | Browser Session Hijacking | Man-in-the-browser attacks |
| T1113 | Screen Capture | Screenshots of victim screens |
| T1125 | Video Capture | Recording via camera |

## Detection Quick Reference

### Email Collection Indicators (T1114)
- Unusual login activity from new locations or devices
- Changes to email forwarding rules
- Delegation settings modifications
- Security features being disabled
- OAuth application consent grants
- Mailbox export activities

### Local Data Collection Indicators (T1005)
- Mass file reads from sensitive directories
- Access to credential stores (SAM, NTDS.dit, /etc/shadow)
- Database file access (*.mdf, *.sqlite, *.db)
- Archive creation activities

### Archive Collection Indicators (T1560)
- Execution of compression utilities (7zip, WinRAR, tar, gzip)
- PowerShell Compress-Archive usage
- Large archive file creation
- Encryption of archive files

### Input/Screen Capture Indicators (T1056, T1113)
- Processes hooking keyboard APIs
- Suspicious DLL injection
- SetWindowsHookEx API calls
- BitBlt/PrintWindow API calls
- Screenshot file creation

## Investigation Tools

| Tool | Purpose |
|------|---------|
| 365Inspect | Microsoft 365 security assessment |
| Sparrow (CISA) | M365 compromise detection |
| Semperis Purple Knight | AD security assessment |
| Prowler | AWS security assessment |
| Amazon Macie | S3 data discovery and protection |

## Response Timeline

### First 15 Minutes
1. Confirm incident
2. Identify scope
3. Begin containment
4. Notify SOC Manager

### First Hour
1. Complete containment
2. Begin evidence collection
3. Escalate appropriately
4. Start detailed investigation

### First 4 Hours
1. Complete investigation
2. Begin eradication
3. Prepare communications
4. Document findings

## Related SOPs

- MITRE ATT&CK Collection Tactic SOP (MITRE-TA0009-COLLECTION)

## References

- [MITRE ATT&CK Collection Tactic](https://attack.mitre.org/tactics/TA0009/)
- [Email Collection Technique](https://attack.mitre.org/techniques/T1114/)
- NIST SP800-61 Incident Response Lifecycle
