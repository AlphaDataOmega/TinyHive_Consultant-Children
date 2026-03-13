# Impact Analyst Documentation

## Overview

This directory contains reference materials and standard operating procedures for the Impact Analyst consultant, specializing in MITRE ATT&CK Impact (TA0040) incident response.

## MITRE ATT&CK Impact Techniques Coverage

| Technique ID | Technique Name | Sub-Techniques |
|-------------|----------------|----------------|
| T1485 | Data Destruction | - |
| T1486 | Data Encrypted for Impact (Ransomware) | - |
| T1489 | Service Stop | - |
| T1490 | Inhibit System Recovery | - |
| T1491 | Defacement | T1491.001 (Internal), T1491.002 (External) |
| T1495 | Firmware Corruption | - |
| T1496 | Resource Hijacking | - |
| T1498 | Network Denial of Service | T1498.001 (Direct Network Flood), T1498.002 (Reflection Amplification) |
| T1499 | Endpoint Denial of Service | T1499.001 (OS Exhaustion), T1499.002 (Service Exhaustion), T1499.003 (Application Exhaustion), T1499.004 (Application Exploitation) |
| T1529 | System Shutdown/Reboot | - |
| T1531 | Account Access Removal | - |
| T1561 | Disk Wipe | T1561.001 (Content Wipe), T1561.002 (Structure Wipe) |
| T1565 | Data Manipulation | T1565.001 (Stored Data), T1565.002 (Transmitted Data), T1565.003 (Runtime Data) |

## Key Detection Indicators

### Ransomware (T1486)
- Files renamed with unusual extensions (.crypt, .locked, .encrypted)
- Ransom notes (text files, HTML, wallpaper changes)
- Mass file modification in short time periods
- Volume Shadow Copy deletion (vssadmin delete shadows)
- bcdedit commands to disable recovery

### Data Destruction (T1485)
- Mass file deletions in short time windows
- Use of secure deletion tools (sdelete, shred, wipe)
- Shadow copy deletion events
- Deletion of system files or critical business data

### Defacement (T1491)
- Unauthorized modifications to web page content
- New files appearing in web directories
- Web shell activity indicators
- SQL injection or RFI attempts in logs

### Resource Hijacking (T1496)
- Sustained high CPU/GPU usage without legitimate cause
- Connections to mining pools
- Stratum protocol traffic
- Unusual outbound traffic patterns

### Denial of Service (T1498/T1499)
- Sudden traffic volume increases
- Amplification attack patterns (DNS, NTP reflection)
- SYN/UDP flood patterns
- Application crash loops or resource exhaustion

## Response Workflow

### 1. Initial Triage
- Confirm incident type and Impact technique
- Document initial observations with timestamps
- Determine scope and affected systems
- Assess business impact (functional, information, financial, regulatory)

### 2. Containment
- Isolate affected systems from network
- Block C2 domains and IP addresses
- Quarantine file shares and databases
- Protect backup systems with highest priority

### 3. Eradication
- Remove malicious artifacts and persistence mechanisms
- Rebuild affected systems from known-good media
- Apply security patches
- Deploy custom detection signatures

### 4. Recovery
- Attempt decryption using No More Ransom tools
- Restore from verified clean backups
- Bring systems online incrementally
- Monitor closely for re-infection

### 5. Lessons Learned
- Conduct post-incident review
- Update documentation and detection rules
- Address identified security gaps
- Brief leadership on improvements

## Ransomware Identification Resources

- [ID Ransomware](https://id-ransomware.malwarehunterteam.com/)
- [No More Ransom Crypto Sheriff](https://www.nomoreransom.org/crypto-sheriff.php)
- [No More Ransom Decryption Tools](https://www.nomoreransom.org/en/decryption-tools.html)

## Critical Response Guidelines

### Ransomware Incidents
1. **DO NOT** power down encrypted systems (may not restart)
2. **DO** quarantine infected systems immediately
3. **DO** protect backup infrastructure
4. **DO** preserve volatile evidence before forensic actions
5. **DO** escalate ransom payment decisions to leadership

### Defacement Incidents
1. **PRIORITY**: Take down harmful content immediately
2. Capture evidence (screenshots, logs) before changes
3. Investigate attack vector (SQL injection, RFI, web shells)
4. Restore from verified clean backups

### Data Destruction/Disk Wipe
1. **DO NOT** shutdown systems (preserve volatile memory)
2. Immediately isolate affected systems
3. Prevent spread to other systems
4. Protect backup systems with highest priority

## Related SOPs

- MITRE-ATT&CK-Impact-SOP.md - Comprehensive Impact incident response procedures
- IRP-Ransom - Ransomware-specific incident response playbook
- IRP-Malware - Malware incident response playbook

## Contact and Escalation

- Security Operations Center: Immediate escalation for Impact incidents
- Legal Counsel: Required before external communications
- Board/Leadership: Required for ransom payment decisions
- Insurance Provider: Notify early for resource coordination
