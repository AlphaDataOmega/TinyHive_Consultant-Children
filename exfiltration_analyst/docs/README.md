# Exfiltration Analyst Documentation

## Overview

This directory contains reference documentation and operational procedures for the Exfiltration Analyst consultant specializing in data exfiltration detection, investigation, and response aligned with MITRE ATT&CK Exfiltration tactic (TA0010).

## Core Competencies

### MITRE ATT&CK TA0010 Technique Coverage

| Technique ID | Technique Name | Description |
|--------------|----------------|-------------|
| T1020 | Automated Exfiltration | Automated data gathering and transfer after collection |
| T1020.001 | Traffic Duplication | Leveraging network mirroring for data capture |
| T1030 | Data Transfer Size Limits | Chunked transfers to avoid detection thresholds |
| T1048 | Exfiltration Over Alternative Protocol | Using non-C2 protocols for data transfer |
| T1048.001 | Symmetric Encrypted Non-C2 Protocol | Data transfer via symmetric encryption (SSH) |
| T1048.002 | Asymmetric Encrypted Non-C2 Protocol | Data transfer via asymmetric encryption (HTTPS) |
| T1048.003 | Unencrypted/Obfuscated Non-C2 Protocol | Transfer via DNS, ICMP, or obfuscated channels |
| T1041 | Exfiltration Over C2 Channel | Data encoded within command and control traffic |
| T1011 | Exfiltration Over Other Network Medium | WiFi, cellular, or alternative network paths |
| T1011.001 | Exfiltration Over Bluetooth | Data transfer via Bluetooth connections |
| T1052 | Exfiltration Over Physical Medium | Removable media and physical devices |
| T1052.001 | Exfiltration over USB | USB drives and external storage devices |
| T1567 | Exfiltration Over Web Service | Using legitimate web services as transfer mechanism |
| T1567.001 | Exfiltration to Code Repository | Transfer via GitHub, GitLab, Bitbucket APIs |
| T1567.002 | Exfiltration to Cloud Storage | Transfer via cloud storage providers |
| T1029 | Scheduled Transfer | Time-based exfiltration to blend with normal traffic |
| T1537 | Transfer Data to Cloud Account | Cross-account transfers within cloud environments |

## Detection Sources

### Network-Based Detection
- Data Loss Prevention (DLP) alerts for sensitive data patterns
- Network traffic analysis for volume and timing anomalies
- DNS analytics for tunneling detection
- Protocol anomaly detection for non-standard usage

### Endpoint Detection
- USB and removable media monitoring (Event ID 6416)
- Process and application monitoring (archive tools, cloud sync)
- File system monitoring for staging directories

### Cloud and Web Service Detection
- Cloud Access Security Broker (CASB) alerts
- Web proxy logs for upload tracking
- Cloud audit logs for API activity

## Indicator Categories

| Indicator Type | Examples |
|----------------|----------|
| Volume-based | Large outbound transfers, unusual upload sizes |
| Timing-based | Off-hours transfers, scheduled patterns |
| Destination-based | Unknown external IPs, suspicious domains, TOR exit nodes |
| Protocol-based | DNS tunneling, ICMP data, non-standard port usage |
| User-based | Privileged account anomalies, departing employee activity |
| Device-based | Unknown USB devices, unauthorized mobile connections |

## Investigation Procedures

### Initial Triage (First 30 Minutes)
1. Validate alert and rule out false positive
2. Identify affected systems and users
3. Determine data types potentially involved
4. Assess current status (ongoing vs. completed)
5. Begin evidence preservation

### Detailed Investigation Areas
- **Network Exfiltration**: Traffic analysis, C2 channel analysis, alternative protocol investigation
- **USB/Physical Media**: Device identification, data access analysis, scope determination
- **Cloud Exfiltration**: Account analysis, service enumeration, cross-account transfers

## Severity Assessment Matrix

| Criteria | Critical | High | Medium | Low |
|----------|----------|------|--------|-----|
| Data Type | PII, Trade Secrets, PHI | Confidential Business | Internal Only | Public |
| Volume | >1GB or bulk records | 100MB-1GB | 10-100MB | <10MB |
| User Type | Admin/Privileged | Standard Employee | Contractor | Guest |
| Duration | Ongoing | <24 hours | <7 days | >7 days (historical) |

## Containment Strategies

### Immediate Containment (First Hour)
- **Network**: Block destination IPs/domains, isolate endpoints, disrupt C2 channels
- **Account**: Disable compromised accounts, revoke sessions, reset credentials
- **Physical**: Enable USB blocking, secure workstations

### Extended Containment
- Network segmentation and microsegmentation
- Enhanced monitoring and logging
- Additional sensor deployment

## Regulatory Notification Requirements

| Regulation | Timeline |
|------------|----------|
| GDPR | 72 hours |
| HIPAA | 60 days |
| PCI-DSS | Immediately |
| State Breach Laws | 30-90 days typically |
| SEC | 4 business days |

## Related Documentation

- MITRE ATT&CK Framework - Exfiltration Tactic: https://attack.mitre.org/tactics/TA0010/
- NIST SP800-61 Computer Security Incident Handling Guide
- SANS Incident Handler's Handbook
- CIS Controls v8

## Tools Reference

| Category | Tools |
|----------|-------|
| Network Analysis | Wireshark, Zeek, NetworkMiner |
| Endpoint Forensics | Velociraptor, KAPE, FTK |
| Memory Analysis | Volatility, Rekall |
| Log Analysis | Splunk, Elastic, Graylog |
| DLP | Symantec DLP, Microsoft Purview, Netskope |
| CASB | Microsoft Defender for Cloud Apps, Netskope, Zscaler |
