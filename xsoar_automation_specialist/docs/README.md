# XSOAR Automation Specialist - Documentation

## Overview

This directory contains reference documentation and operational guides for Cortex XSOAR playbook development, security automation, and incident response orchestration.

## Core Competencies

### Phishing Incident Response

#### Email Processing
- Parse and process email headers (From, To, Subject, X-Headers)
- Extract email body content (HTML and plaintext)
- Handle multiple email formats: EML, MSG, SMTP, S/MIME
- Render HTML emails to images using Rasterize integration
- Process nested/attached emails (original forwarded messages)

#### Indicator Extraction
- Extract URLs from email body and attachments
- Extract email addresses from headers and content
- Extract file hashes (MD5, SHA1, SHA256) from attachments
- Extract IP addresses from email headers
- Supported file types: PDF, TXT, HTML, DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF, XML

#### Response Workflow
1. Acknowledge receipt to reporter
2. Process email and extract indicators
3. Enrich all extracted indicators
4. Calculate severity based on DBotScore
5. Render screenshots of suspicious URLs
6. Manual investigation decision point
7. Notify reporter of determination
8. Execute remediation (if malicious)
9. Close investigation

### Indicator Enrichment

#### IP Address Enrichment
- Resolve IP to hostname (DNS reverse lookup)
- Determine internal vs external classification
- CIDR range checking with IsIPInRanges
- Threat intelligence reputation lookup
- Geolocation and ASN information
- Endpoint correlation (if internal)

#### Domain Enrichment
- WHOIS registration data
- DNS record enumeration
- Threat intelligence reputation
- Category classification

#### URL Enrichment
- Screenshot capture with Rasterize
- Redirect chain analysis
- Threat intelligence reputation
- Domain extraction and enrichment

#### File Hash Enrichment
- Multi-vendor reputation checks
- Sandbox detonation submission
- Known malware database lookup
- File type and metadata analysis

#### Account Enrichment
- Active Directory user lookup
- Manager hierarchy retrieval
- Group membership enumeration
- Last login and status information

#### Endpoint Enrichment
- Hostname to IP resolution
- Operating system information
- Installed software inventory
- User session information

### Endpoint Containment

#### Supported EDR Platforms

| Platform | Capabilities |
|----------|--------------|
| Cortex XDR | Isolate, unisolate, file quarantine, block list |
| CrowdStrike Falcon | Device isolation, RTR commands |
| Microsoft Defender ATP | Machine isolation (full/selective), hunting |
| Carbon Black Response | Sensor isolation, ban hash |
| Cybereason | Machine isolation, malop remediation |
| FireEye HX | Host containment, file acquisition |

#### Isolation Workflow
1. Receive isolation request with endpoint identifiers
2. Determine available EDR integration
3. Execute platform-specific isolation command
4. Poll for isolation completion
5. Verify isolation status
6. Update incident with results

### File Detonation (Sandbox Analysis)

#### Supported Sandboxes

| Sandbox | Key Features |
|---------|--------------|
| Palo Alto WildFire | APK, JAR, DOC, PDF, PE, PKG, RAR |
| CrowdStrike Falcon X | PE, Office, PDF, APK, scripts |
| Joe Security | All file types, internet access option |
| VMRay | Comprehensive IOC extraction |
| FireEye AX | PE, Office, PDF, archive, image |
| Cuckoo | Open source, customizable |
| ANY.RUN | Interactive analysis, behavioral |
| Hybrid Analysis | Community threat intel |
| Lastline | Advanced evasion detection |
| ThreatGrid | Detailed behavioral analysis |
| Group-IB TDS Polygon | Email and document focus |
| SNDBOX | Microsoft Office specialization |

#### Detonation Workflow
1. Receive file for analysis
2. Submit to all available sandboxes in parallel
3. Poll for analysis completion (GenericPolling)
4. Retrieve analysis reports
5. Extract IOCs and verdicts
6. Populate DBotScore and file context

### Incident Response Plans

#### Containment Plan
- **Isolate Endpoint** - Network isolation to prevent lateral movement
- **Disable Account** - Block user access via Active Directory
- **Quarantine File** - Isolate malicious files on endpoint
- **Block Indicators** - Add to block lists (IP, domain, URL, file hash)
- **Clear User Session** - Force reauthentication (Okta)

#### Eradication Plan
- **Delete File** - Remove malicious files from endpoints
- **Kill Process** - Terminate malicious processes by name
- **Reset Password** - Expire user passwords in AD

#### Recovery Plan
- **Unisolate Endpoint** - Restore network connectivity
- **Restore File** - Recover quarantined files if needed

### Active Directory Investigation

#### Investigation Steps
1. Review AdminSDHolder permissions for unauthorized access
2. Run AD ACL Scanner for permission anomalies
3. Review compromised user list from ACL report
4. Set compromised usernames in incident context
5. Disable compromised accounts
6. Review AD event logs for suspicious activity
7. Remediate based on findings

#### Key Events to Monitor
- 4794: DSRM account password change attempt
- 4780: ACLs set on admin accounts
- 4739/643: Domain policy changes
- 4713/617: Kerberos policy changes
- 4724/628: Account password reset attempts
- 4735/639: Security-enabled local group changes
- 4737/641: Security-enabled global group changes
- 4755/659: Security-enabled universal group changes

## Playbook Development Patterns

### Task Configuration

#### Standard Task Properties
```yaml
id: "1"
taskid: uuid-value
type: regular|condition|playbook|title|collection|start
task:
  id: uuid-value
  name: Task Name
  description: Task description
  script: integration|||command
  type: regular
  iscommand: true
  brand: IntegrationBrand
nexttasks:
  '#none#':
    - "2"
scriptarguments:
  argname:
    simple: value
    complex:
      root: ContextPath
separatecontext: false
continueonerror: false
skipunavailable: true
quietmode: 0
```

#### Conditional Task
```yaml
type: condition
conditions:
  - label: "yes"
    condition:
      - - operator: isExists
          left:
            value:
              simple: ContextPath
            iscontext: true
nexttasks:
  '#default#':
    - "skip_task"
  "yes":
    - "execute_task"
```

### Context Management

#### Standard Context Paths
| Context | Fields |
|---------|--------|
| `IP` | Address, Geo.Country, ASN, Hostname |
| `Domain` | Name, DNS, WHOIS.Registrar |
| `URL` | Data, Category, Screenshot |
| `File` | Name, MD5, SHA1, SHA256, Size, Type |
| `Account` | Username, Email, DisplayName, Manager |
| `Endpoint` | Hostname, IP, OS, MAC |
| `DBotScore` | Indicator, Type, Score, Vendor, Reliability |

#### DBotScore Values
| Score | Meaning | Recommended Action |
|-------|---------|-------------------|
| 0 | Unknown | Investigate further |
| 1 | Good/Clean | No action needed |
| 2 | Suspicious | Review and monitor |
| 3 | Malicious | Block and remediate |

### Input Transformers

| Transformer | Purpose | Example |
|-------------|---------|---------|
| `uniq` | Deduplicate array | Remove duplicate IPs |
| `join` | Array to string | CSV list creation |
| `split` | String to array | Parse comma-separated input |
| `SetIfEmpty` | Default value | Provide fallback |
| `toLowerCase` | Case normalization | Hostname standardization |
| `toUpperCase` | Case normalization | Hash standardization |

### Polling Configuration

#### GenericPolling Inputs
| Input | Purpose | Default |
|-------|---------|---------|
| `Ids` | Items to poll | Required |
| `PollingCommandName` | Status check command | Required |
| `PollingCommandArgName` | Argument for IDs | `ids` |
| `Interval` | Minutes between polls | 1 |
| `Timeout` | Maximum minutes | 10 |
| `dt` | Completion filter | Required |

#### Example dt Filters
```
# WildFire: poll until all reports have Success status
WildFire.Report(val.Status!=='Success').SHA256

# Sandbox: poll until analysis is complete
Joe.Analysis(val.Status!=='finished').WebID
```

## Quick Reference Commands

### Indicator Reputation
```
ip reputation=<ip>
domain reputation=<domain>
url reputation=<url>
file reputation=<hash>
```

### Endpoint Operations
```
# Cortex XDR/XSIAM
core-isolate-endpoint endpoint_id=<id>
core-unisolate-endpoint endpoint_id=<id>
core-quarantine-files endpoint_id=<id> file_hash=<hash>
core-blocklist-files hash_list=<hashes>
core-restore-file endpoint_id=<id> file_hash=<hash>

# CrowdStrike
cs-falcon-contain-host ids=<device_id>
cs-falcon-lift-containment ids=<device_id>

# Microsoft Defender
microsoft-atp-isolate-machine machine_id=<id>
microsoft-atp-unisolate-machine machine_id=<id>
```

### Active Directory
```
ad-get-user username=<user>
ad-disable-account username=<user>
ad-enable-account username=<user>
ad-expire-password username=<user>
ad-get-user-manager username=<user>
```

### Email Operations
```
send-mail to=<email> subject=<subject> body=<body>
rasterize url=<url>
rasterize-email htmlBody=<html>
```

### Blocking Operations
```
# Zscaler
zscaler-blacklist-ip ip=<ip>
zscaler-blacklist-url url=<url>

# PAN-OS (via sub-playbooks)
PAN-OS - Block IP - Custom Block Rule
PAN-OS - Block IP - Static Address Group
```

### Threat Intelligence
```
mitre-get-indicator-name attack_ids=<technique_id>
attack-pattern attack_pattern=<name>
```

### Utility Scripts
```
IsIntegrationAvailable brandname=<integration>
DeleteContext all=yes
SetAndHandleEmpty key=<key> value=<value>
PrintErrorEntry message=<error_message>
IsIPInRanges ip=<ip> range=<cidr_list>
```

## Integration Verification Checklist

### Pre-Deployment
- [ ] Integration instance configured
- [ ] API credentials validated
- [ ] Test connection successful
- [ ] Required permissions granted
- [ ] Rate limits documented

### Playbook Testing
- [ ] Test with sample incident
- [ ] Verify context output
- [ ] Check error handling paths
- [ ] Validate timeout behavior
- [ ] Review War Room entries

## Related Playbooks

### Phishing
- Phishing - Core v2
- Process Email - Core v2
- Extract Indicators From File - Generic v2
- Search And Delete Emails - Generic v2
- Get Original Email - Generic v2

### Enrichment
- Entity Enrichment - Generic v3
- IP Enrichment - Generic v2
- Domain Enrichment - Generic v2
- URL Enrichment - Generic v2
- File Enrichment - Generic v2
- Account Enrichment - Generic v2.1
- Endpoint Enrichment - Generic v2.1
- CVE Enrichment - Generic v2

### Containment
- Containment Plan
- Isolate Endpoint - Generic V2
- Block IP - Generic v3
- Block Domain - Generic
- Block URL - Generic
- Block Indicators - Generic v2
- Block Account - Generic

### Response Lifecycle
- Eradication Plan
- Recovery Plan
- Endpoint Investigation Plan
- Endpoint Malware Investigation - Generic V2

### Detonation
- Detonate File - Generic
- Detonate URL - Generic
- Detonate File - WildFire
- Detonate File - CrowdStrike Falcon X
- Detonate File - JoeSecurity

### Investigation
- Active Directory Investigation
- Active Directory - Get User Manager Details
- Command-Line Analysis

### Utility
- GenericPolling
- Context Polling - Generic
- Field Polling - Generic
- Calculate Severity - Generic v2
- Dedup - Generic v4

## Related Resources

- Cortex XSOAR Documentation
- Palo Alto Networks Content Hub
- MITRE ATT&CK Framework
- NIST Computer Security Incident Handling Guide (SP 800-61)
