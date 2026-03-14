# ThreatConnect Playbook Specialist Documentation

## Overview

This documentation supports the ThreatConnect Playbook Specialist consultant in designing and implementing threat intelligence automation workflows using the ThreatConnect platform. The playbooks cover threat intelligence feed ingestion, indicator enrichment, malware analysis integration, phishing response, and security operations automation.

## Platform Architecture

### ThreatConnect Components

| Component | Purpose |
|-----------|---------|
| Threat Intelligence Platform (TIP) | Centralized IOC storage, tagging, lifecycle management |
| Playbook Engine | Visual workflow automation with triggers, apps, operators |
| Indicators | IOC objects (IP, Domain, URL, File Hash, Email, CIDR) |
| Groups | Contextual objects (Incidents, Campaigns, Threats, Events) |
| Tags | Classification labels for filtering and automation |
| Attributes | Custom metadata fields for enrichment data |
| DataStore | Key-value storage for playbook state and data |

### Playbook Building Blocks

| Element | Description |
|---------|-------------|
| Triggers | Events initiating playbook execution |
| Apps | Functional units performing specific operations |
| Operators | Logic components for data manipulation and flow |
| Variables | Data storage between playbook steps |
| Components | Reusable sub-playbooks for modular design |

## TCPB Naming Convention

### Category Prefixes

| Prefix | Full Name | Use Case |
|--------|-----------|----------|
| `TCPB-DC-` | Detection & Classification | Malware analysis, threat classification |
| `TCPB-HT-` | Helper/Tooling | Utility playbooks, parsers, transformations |
| `TCPB-MB-` | Mailbox | Email processing and extraction |
| `TCPB-MI-` | Indicator Management | IOC validation, deduplication, lifecycle |
| `TCPB-MT-` | Maintenance/Triggers | Scheduled tasks, datastore cleanup |
| `TCPB-TT-` | Threat Intelligence Triggers | Feed ingestion, rule imports, monitoring |
| `TCPB-UA-` | User Action | Interactive analyst-triggered playbooks |
| `TCPB-UT-` | Utility | URL manipulation, encoding/decoding |
| `TCPB-WF-` | Workflow | Process automation, escalation workflows |

### Naming Examples

```
TCPB-TT-CrowdStrike Snort Rules Ingest   (Threat Intelligence - vendor integration)
TCPB-UA-Have-I-Been-Pwned                 (User Action - enrichment service)
TCPB-MI-Indicator Uniqueness Validator    (Indicator Management - deduplication)
TCPB-HT-Array Serializer                  (Helper - utility function)
TCPB-DC-Analyze Malware With McAfee ATD   (Detection - sandbox integration)
```

## Core Playbook Categories

### 1. Threat Intelligence Feed Ingestion

#### CrowdStrike Intelligence Integration
```yaml
Playbook: TCPB-TT-CrowdStrike Snort Rules Ingest
Trigger: Timer (daily)
Dependencies: CrowdStrike Falcon Intelligence subscription
Parameters:
  - CrowdStrike Falcon Intelligence API ID
  - CrowdStrike Falcon Intelligence API Secret Key
Process:
  1. Authenticate with CrowdStrike API
  2. Download latest Snort rules
  3. Create signatures in ThreatConnect
  4. Tag with associated report numbers
  5. Add version as attribute
```

#### Recorded Future Alerts
```yaml
Playbook: TCPB-MT-Recorded Future Alerts API
Trigger: Timer (configurable)
Process:
  1. Query RF API for alerts in time window
  2. Parse alert data
  3. Create incidents from alerts
  4. Associate indicators with incidents
```

#### RSS Feed Processing
```yaml
Playbook: TCPB-TT-Google Alerts RSS Reader
Trigger: Timer
Process:
  1. Read Google Alerts RSS feed
  2. Extract URLs from entries
  3. Create URL indicators
  4. Apply classification tags
Use Case: Monitor for domains matching malicious patterns
```

### 2. Indicator Enrichment Workflows

#### Multi-Source Enrichment

| Playbook | Source | Indicator Types | Authentication |
|----------|--------|-----------------|----------------|
| TCPB-IPQualityScore | IPQualityScore | IP, Email, URL | API Key |
| TCPB-Symantec Threat Intelligence | Symantec | Multiple | API credentials |
| TCPB-UA-Robtex Query | Robtex | IP, ASN | None (free) |
| TCPB-UA-Have-I-Been-Pwned | HIBP | Email | API Key |
| TCPB-UA-Cymon Query IP and Host | Cymon | IP, Host | Free/deprecated |

#### Have I Been Pwned Integration
```yaml
Playbook: TCPB-UA-Have-I-Been-Pwned
Trigger: User Action on EmailAddress indicator
Process:
  1. Query HIBP API for breach data
  2. Create incident for breach findings
  3. Add breach source tags to indicator
  4. Associate incident with indicator
Outputs:
  - Breach tags on indicator
  - Associated incident with breach details
  - PDF report generation
```

#### Dark Web Intelligence
```yaml
Playbook: TCPB-HT-Sixgill-DarkWeb-Domain-Investigation
Trigger: External webhook (SIEM)
Purpose: Threat hunting using dark web intelligence
Input: Domain from SIEM alert
Output: Dark web context for domain
```

### 3. Malware Analysis Integration

#### VMRay Workflow (Two-Phase)
```yaml
Phase 1 - Submission:
  Playbook: VMRay Submission
  Trigger: Malware document creation
  Actions:
    - Submit to VMRay sandbox
    - Add VMRay Sample ID attribute
    - Add VMRay Submission ID attribute
    - Tag as "vmray-processing"

Phase 2 - Results:
  Playbook: VMRay Get Results
  Trigger: Processing completion
  Actions:
    - Retrieve VMRay results
    - Parse indicators from analysis
    - Associate IOCs with malware
    - Change tag to "VMRay Processed"

Required Attributes:
  - VMRay Sample ID (custom)
  - VMRay Submission ID (custom)
```

#### McAfee ATD Integration
```yaml
Playbook: TCPB-DC-Analyze Malware With McAfee ATD
Trigger: Malware tagged with "atd_submit"
Dependencies: Active McAfee ATD instance
Process:
  1. Submit malware to ATD
  2. Poll for detonation completion
  3. Ingest severity-based results
  4. Create MD5/SHA1/SHA256 indicators
  5. Associate hashes with original sample
```

#### Multi-Engine Analysis
```yaml
Playbook: TCPB-UA-PolySwarm Marketplace
Trigger: User Action
Purpose: Submit files to PolySwarm multi-engine analysis
Benefit: Multiple AV verdicts from single submission
```

### 4. Phishing Response Automation

#### Abuse Inbox Processing
```yaml
Playbook: TCPB-UA-SlashNext Abuse Inbox
Trigger: Email forwarded to abuse mailbox
Requirements: SlashNext Phishing Incident Response App
Process:
  1. Extract URLs from email
  2. Deduplicate URL list
  3. Scan each URL with SlashNext
  4. Create malicious URL indicators
  5. Generate report with findings
  6. Store original email as document
  7. Associate indicators with report
  8. Send notification to platform
  9. Email scan status to sender
```

#### Email Indicator Extraction
```yaml
Playbook: TCPB-MB-Email and Indicator Extract
Trigger: Email receipt
Outputs:
  - URLs from email body
  - IP addresses
  - Domain names
  - File hashes (attachments)
  - Email addresses
```

### 5. Indicator Lifecycle Management

#### Deduplication
```yaml
Playbook: TCPB-MI-Indicator Uniqueness Validator
Trigger: New IOC creation
Types: Address, URL, Host, File, EmailAddress
Process:
  1. Check if indicator exists in other owners
  2. Tag duplicates with "multiple_owners"
  3. Display on dashboard for review

Dashboard TQL:
  typeName in ("Address", "EmailAddress", "File", "Host", "URL")
  and tag in ("multiple_owners")

Chart Type: Advanced Pie Chart grouped by Owner Name
Note: High-volume - runs on every IOC creation
```

#### False Positive Triage
```yaml
Playbook: TCPB-UA-False Positive Triage
Versions:
  Pre-5.7:
    - Standalone playbook with user-action trigger
    - Single playbook deployment

  Post-5.7:
    - Interface-based architecture
    - HTTP Interface playbook
    - Trigger Interface playbook
    - Component-based triage logic

Benefits: Flexible, interface-agnostic design
```

### 6. EDR Integration

#### Carbon Black YARA Deployment
```yaml
Playbook: TCPB-UA-Deploy_Yara_Rule_To_Carbon_Black
Trigger: User Action on Signature Details page
Method: SSH/SCP (no API available)
Parameters:
  - SSH Hostname: Yara Manager host
  - SSH Username: SSH credentials
  - SSH Password: SSH credentials
  - SSH Port: 22 (default)
Storage: Org Variables for credentials
```

### 7. GRC & ITSM Integration

#### RSA Archer
```yaml
Import: TCPB-HT-RSA Archer - Import Record
Create: TCPB-UA-RSA Archer - Create Record
Purpose: Bidirectional GRC platform integration
```

#### Jira
```yaml
Playbook: TCPB-UA-Get_All_JIRA_information
Trigger: User Action
Purpose: Retrieve complete Jira issue data
Use Case: Link indicators to security tickets
```

#### Exabeam
```yaml
Playbook: TCPB-UA-Query_Exabeam_Data_Lake
Trigger: User Action
Purpose: Search Exabeam for indicator context
Use Case: Correlate TI with UEBA findings
```

## Integration Requirements

### API Authentication Matrix

| Integration | Auth Type | Header/Parameter |
|-------------|-----------|------------------|
| CrowdStrike | OAuth | Bearer token |
| VirusTotal | API Key | x-apikey header |
| HIBP | API Key | hibp-api-key header |
| Recorded Future | API Token | Authorization header |
| SlashNext | API Key | Credentials |
| VMRay | API Key | API credentials |
| McAfee ATD | Credentials | Basic auth |

### Rate Limits

| Service | Limit | Implementation |
|---------|-------|----------------|
| VirusTotal (Public) | 4 requests/minute | 15-second delays |
| VirusTotal (Premium) | Higher limits | Batch processing |
| HIBP | 1 request/1.5 seconds | Sleep between calls |
| Robtex | Rate limited | Implement backoff |

### Required Custom Attributes

| Attribute Name | Type | Used By |
|----------------|------|---------|
| VMRay Sample ID | Text | VMRay playbooks |
| VMRay Submission ID | Text | VMRay playbooks |

## Version Compatibility

| Feature | Minimum Version |
|---------|-----------------|
| Workflow Templates | ThreatConnect 6.0 |
| DataStore Operations | ThreatConnect 6.0 |
| Enhanced User Actions | ThreatConnect 5.7 |
| Interface-based Playbooks | ThreatConnect 5.7 |
| Basic Playbooks | ThreatConnect 5.0+ |

## Trigger Types

| Trigger | Use Case | Configuration |
|---------|----------|---------------|
| Timer | Feed ingestion, monitoring | Cron-style schedule |
| Webhook | SIEM integration, external events | HTTP endpoint |
| User Action | Manual enrichment | UI button on object |
| Indicator Created | Validation, deduplication | Indicator type filter |
| Document Created | File processing | Document type filter |
| Email | Phishing intake | Mailbox configuration |

## Utility Playbooks

### Data Transformation

| Playbook | Purpose | Status |
|----------|---------|--------|
| TCPB-HT-Array Serializer | Process arrays sequentially | DEPRECATED |
| TCPB-HT-PDF Reader | Extract text from PDFs | Active |
| TCPB-HT-URL Reader | Fetch web content | Active |
| TCPB-UA-Punycode DecoderEncoder | IDN encoding | Active |

### Array Processing (Replacement)

```yaml
Deprecated: TCPB-HT-Array Serializer
Replacement Options:
  1. Array Iterator App (install required)
  2. Array Iterator Component (no install)

Location: github.com/ThreatConnect-Inc/threatconnect-playbooks
```

### Monitoring

| Playbook | Target | Alert Type |
|----------|--------|------------|
| TCPB-TT-Github Activity Monitor | Github users | Activity notifications |
| TCPB-TT-Page Monitor | Web pages | Change detection |
| TCPB-TT-Iris Investigate Monitor | DomainTools | Infrastructure changes |

## Error Handling Patterns

### Retry Logic
```yaml
Playbook: TCPB-HT-Repeat until Success
Pattern:
  1. Execute operation
  2. Check for success
  3. If failure, wait and retry
  4. Maximum retry count
  5. Final failure notification
```

### API Error Handling
```yaml
Rate Limit (429):
  - Implement exponential backoff
  - Log retry attempts
  - Continue after delay

Authentication Error (401/403):
  - Log credential failure
  - Notify administrator
  - Halt playbook

Timeout:
  - Extend timeout for slow APIs
  - Implement async polling pattern
```

## Dashboard Configuration

### Duplicate Indicator Dashboard

```sql
TQL Query:
typeName in ("Address", "EmailAddress", "File", "Host", "URL")
and tag in ("multiple_owners")

Display Options:
  - Number Card: Total duplicate count
  - Advanced Pie Chart: By owner distribution
  - Group By: Owner Name
```

## Deployment Checklist

### Pre-Deployment
- [ ] Verify ThreatConnect version compatibility
- [ ] Create required custom attributes
- [ ] Configure API credentials
- [ ] Test external API connectivity
- [ ] Review rate limits and configure delays
- [ ] Set up Org Variables for sensitive config

### Deployment
- [ ] Import playbook (.pbx or .pbxz)
- [ ] Configure trigger settings
- [ ] Set input parameters
- [ ] Enable playbook
- [ ] Test with sample data

### Post-Deployment
- [ ] Monitor execution logs
- [ ] Verify indicator creation
- [ ] Check tag application
- [ ] Validate enrichment data
- [ ] Review error rates

## Maintenance

### Daily
- Review playbook execution logs
- Check for API errors
- Verify feed ingestion completion

### Weekly
- Audit indicator quality
- Review false positive rates
- Check duplicate indicator counts
- Validate enrichment coverage

### Monthly
- Rotate API credentials
- Review and tune rate limits
- Update deprecated playbooks
- Assess new integration needs

## Reference Documentation

| Resource | URL |
|----------|-----|
| ThreatConnect Playbooks GitHub | github.com/ThreatConnect-Inc/threatconnect-playbooks |
| ThreatConnect KB | kb.threatconnect.com |
| CrowdStrike Falcon | falcon.crowdstrike.com/documentation |
| VirusTotal API | developers.virustotal.com |
| VMRay | docs.vmray.com |
| McAfee ATD | mcafee.com/enterprise/en-us/products/advanced-threat-defense.html |
| Carbon Black Yara Manager | developer.carbonblack.com/guide/enterprise-response/cb-yara-manager-guide |
| SlashNext | slashnext.com |
| HIBP API | haveibeenpwned.com/API |

## Glossary

| Term | Definition |
|------|------------|
| TIP | Threat Intelligence Platform |
| IOC | Indicator of Compromise |
| TCPB | ThreatConnect Playbook (naming prefix) |
| PBX | Playbook export format |
| PBXZ | Compressed playbook bundle |
| DataStore | Key-value storage for playbook state |
| Org Variables | Organization-wide configuration storage |
| User Action | Analyst-triggered playbook execution |
| Component | Reusable sub-playbook module |
| Interface | Abstract playbook entry point (post-5.7) |
