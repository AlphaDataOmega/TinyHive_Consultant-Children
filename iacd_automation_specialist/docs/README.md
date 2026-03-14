# IACD Automation Specialist Documentation

## Overview

This consultant specializes in IACD (Integrated Adaptive Cyber Defense) Automate workflow development, BPMN-based security automation, and standards-based security orchestration. The specialist draws from comprehensive knowledge of 9 IACD Automate playbooks covering malware response, email security, firewall processing, threat intelligence, and rogue device detection.

## Core Competencies

### Malware Detection and Response
- **Malware Detection Response** — Multi-path alert routing (MAS, Web MPS, Email MPS) with SIEM and directory enrichment
- **Virus Alert Processing** — Username correlation from alerts or SIEM with directory context enrichment
- **New Malicious File Detection** — Dynamic analysis with file detonation, indicator extraction, and reputation checks

### Email Security
- **Suspicious Email Analysis** — Parallel URL extraction and attachment hash analysis with detonation
- **URL/Hash Reputation** — Multi-source reputation checking with malicious marker evaluation
- **Recipient Notification** — Automated user communication for malicious/non-malicious verdicts

### Firewall Alert Processing
- **Generic Firewall Alerts** — Multi-path routing for text messages, correlation events, and threat/traffic events
- **Threat Traffic Alerts** — Specialized parsing for threat and traffic events with WHOIS enrichment
- **Unknown URL Analysis** — Deduplication, parallel reputation/detonation, domain/IP reputation checks

### Threat Intelligence
- **Threat Feed Integration** — Automated IOC ingestion with IP, URL, and domain blocklist updates
- **Reputation Enrichment** — IP, URL, domain, and hash reputation from threat intelligence services
- **WHOIS Lookup** — Domain registration context for indicator enrichment

### Network Security
- **Rogue Device Detection** — Port scanning, OS detection, SIEM correlation, blocklist management
- **Blocklist Management** — Automated addition, analyst review, false positive removal
- **Watch Floor Notification** — Formatted email reports for security operations

## Workflow Reference

### Malware Detection Response

| Alert Type | Processing Path |
|------------|-----------------|
| MAS (Malware Analysis System) | Direct end |
| Web MPS | Set addresses, parallel WHOIS + SIEM lookup, format and email |
| Email MPS | Inbox inspection, recipient lookup, domain analysis, callback IPs |

**Key Actions:**
- Update case management
- Query SIEM for username
- Query directory for user information
- Extract and lookup source domain
- WHOIS information for external addresses
- IP reputation submission
- Format callback IPs and malware information
- Email watch floor

### Suspicious Email Analysis

| Track | Parallel Actions |
|-------|------------------|
| URL Track | Extract URLs, remove whitelisted, submit reputation |
| Attachment Track | Generate hashes, submit hash reputation, submit detonation |
| Consolidation | Format results, evaluate malicious markers |

**Decision Logic:**
- Malicious markers present: Email recipient AND analyst
- No malicious markers: Email recipient only

### Firewall Alert Generic

| Event Type | Workflow |
|------------|----------|
| Text Message | Send text response |
| Correlation Event | Update case |
| Traffic/Threat | Full enrichment with DNS check, parallel lookups |

**Parallel Enrichment:**
1. Username lookup (SIEM + directory)
2. IP information + reputation
3. Domain information + reputation + WHOIS

**Signal Events:**
- Unknown URL threat alert: Signal to URL analysis playbook
- Threats and traffic: Signal to threat/traffic playbook

### Unknown URL Analysis

| Phase | Actions |
|-------|---------|
| Deduplication | Check if seen previously |
| Seen URL | Increment count, update timestamp |
| New URL | Parallel: add to seen list, URL analysis, domain/IP analysis |

**URL Analysis Track:**
- Convert to URL format
- Parallel: reputation check + detonation
- Format results

**Domain/IP Analysis Track:**
- Extract domain or IP
- Route: IP only, Domain only, or Both
- Submit reputation, format results, WHOIS lookup

### Threat Feed to Blocklist

| IOC Type | Processing |
|----------|------------|
| IP IOCs | Format IPs, append IP blocklist |
| URL IOCs | Format URLs, append URL blocklist |
| Domain IOCs | Format domains, append domain blocklist |
| Other IOCs | Update case only (no blocklist action) |

### Rogue Alert Response

| Step | Action |
|------|--------|
| 1 | Receive alert |
| 2 | Port scan and OS detection |
| 3 | SIEM username lookup |
| 4 | Directory lookup (if username found) |
| 5 | Blocklist check |
| 6 | Add to blocklist OR mark duplicate |
| 7 | Parallel: analyst input + write blocklist |
| 8 | Format report, email watch floor |

## BPMN Pattern Reference

### Gateway Types

| Gateway | Symbol | Usage |
|---------|--------|-------|
| Exclusive (XOR) | Diamond with X | Single path based on condition |
| Parallel (AND) | Diamond with + | All paths execute concurrently |
| Inclusive (OR) | Diamond with O | One or more paths based on conditions |

### Task Types

| Task | Usage |
|------|-------|
| Service Task | Automated API/integration calls |
| Send Task | Email/notification dispatch |
| User Task | Analyst approval/input required |
| Receive Task | Wait for external input/callback |

### Event Types

| Event | Usage |
|-------|-------|
| Start Event | Workflow trigger (alert reception) |
| End Event | Workflow completion |
| Signal Event | Inter-playbook communication |

## Integration Reference

### Security Information and Event Management (SIEM)

| Query Type | Purpose |
|------------|---------|
| Username lookup | Correlate IP/host to user identity |
| Recipient lookup | Find email recipients from mail logs |
| Source lookup | Determine internal source of DNS requests |

### Directory Services

| Attribute | Usage |
|-----------|-------|
| User information | Full context (name, department, manager) |
| Contact details | Enable notification workflows |
| Group membership | Determine user privileges |

### Threat Intelligence

| Service | IOC Types |
|---------|-----------|
| IP Reputation | IPv4/IPv6 addresses |
| URL Reputation | Full URLs with paths |
| Domain Reputation | Domain names |
| Hash Reputation | MD5, SHA1, SHA256 file hashes |
| WHOIS | Domain registration information |

### Dynamic Analysis

| Capability | Target |
|------------|--------|
| File Detonation | Executable files, documents, archives |
| URL Detonation | Suspicious URLs for phishing analysis |
| Indicator Extraction | IPs, URLs, dropped files from sandbox |

### Blocking Infrastructure

| Target System | Blocklist Type |
|---------------|----------------|
| Firewall | IP addresses |
| Web Proxy | URLs |
| DNS Resolver | Domains |

## Severity and Response

| Marker | Response |
|--------|----------|
| Suspicious markers absent | Update case, close ticket |
| Suspicious markers present | Notify analyst, select mitigations |
| Malicious confirmed | Block indicators, notify affected users |
| Duplicate detection | Update as duplicate, skip redundant processing |

## Key Principles

1. **Standards-Based** — Use BPMN 2.0 for portable, shareable playbooks
2. **Parallel Execution** — Concurrent enrichment reduces response time
3. **Graceful Degradation** — Continue with partial data when integrations fail
4. **Deduplication** — Prevent redundant analysis of known indicators
5. **Human-in-the-Loop** — Analyst approval for destructive actions
6. **Watch Floor Model** — Centralized notification for security operations
7. **Case Management** — Track all workflows through ticketing system

## Related Resources

- IACD Framework: https://www.iacdautomate.org/
- BPMN 2.0 Specification: https://www.omg.org/spec/BPMN/2.0/
- Camunda BPMN Engine: https://camunda.com/
- MITRE ATT&CK Framework: https://attack.mitre.org/
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
