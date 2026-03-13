# LogicHub Automation Specialist Documentation

## Overview

This documentation supports the LogicHub Automation Specialist consultant role, providing comprehensive guidance for LogicHub SOAR platform workflow development, security automation, and threat intelligence orchestration.

## Core Competencies

### LogicHub Platform Architecture

- **Flows:** Visual workflow definitions containing nodes and actions
- **Integrations:** Connections to external security tools and services
- **Custom Lists:** Managed datasets for lookups and baselines
- **Modules:** Reusable workflow components
- **Operators:** Data transformation and filtering functions

### Data Flow Pattern
```
Trigger -> Data Collection -> Enrichment -> Analysis -> Decision -> Action -> Notification
```

## Playbook Categories

### 1. Phishing and Email Analysis

#### Automated Email Attachment Analysis
- IMAP mailbox polling for unread emails
- Attachment extraction and VirusTotal submission
- Detection result parsing (vendor flags, positive counts, MD5 hashes)
- HTML report generation and SMTP distribution

#### Automated URL Analysis
- URL extraction from email body (JSON array format)
- Deduplication and batch processing
- VirusTotal URL reputation scanning
- Suspicious URL filtering and alerting

### 2. Threat Intelligence and IOC Management

#### CrowdStrike Hash Blocking
- SHA256 hash validation (64 character hexadecimal)
- Duplicate checking against existing blocklist
- CrowdStrike IOC API submission with platform targeting
- Error handling and verification workflows

#### Hash Lookup and Analysis
- Bulk hash processing from CSV or URL sources
- VirusTotal file hash analysis with rate limiting
- Vendor-specific detection extraction (McAfee, etc.)
- Malware family classification reporting

#### TOR Exit Node Monitoring
- Scheduled download from public TOR exit node lists
- File processing and distribution
- Firewall administrator notification
- Network security correlation support

### 3. Vulnerability Management

#### CVE Watchdog Monitoring
- CIRCL CVE API integration (last 200 CVEs)
- Field extraction: CVSS, attack vector, impact scores
- Pattern matching against organizational technology stack
- History-based deduplication
- CVSS threshold filtering (default >= 5)
- Email notification with CVE details

### 4. Data Leakage Prevention

#### GitHub Keyword Monitoring
- GitHub Code Search API integration
- Keyword-based repository scanning
- File path and SHA hash extraction
- Public/private repository flagging
- Priority-based alerting (CRITICAL/HIGH/MEDIUM)

### 5. Network Security

#### IP Blacklist Monitoring
- Authentication log correlation
- Custom list lookup for blacklisted IPs
- Real-time alerting for blacklisted IP logins
- Geolocation enrichment support

### 6. Detection and Alert Triage

#### SIEM Alert Triage Framework
- AlienVault SIEM integration
- Alert normalization and deduplication
- Threat intelligence enrichment
- LogicHub case creation
- Jira ticket generation with SLA

#### Windows Detection Rules
- **Credential Access:** LSASS dump, Kerberoasting
- **Persistence:** Scheduled tasks, GPO, systemd
- **Defense Evasion:** Event log disabling, SDelete, timestomping
- **Discovery:** Unix enumeration, log file access
- **Lateral Movement:** PSEXEC, ADMIN$ share, RDP
- **Command and Control:** NTP/DNS amplification, data tunneling

## Integration Reference

### Required Integrations by Use Case

| Use Case | Integrations |
|----------|--------------|
| Phishing Analysis | IMAP, SMTP, VirusTotal, File Tools |
| Threat Intelligence | VirusTotal, CrowdStrike, Web API |
| Vulnerability Management | Web API, SMTP, Custom Lists |
| Detection | SIEM (AlienVault), EDR (CrowdStrike), SMTP |

### API Rate Limiting

| Integration | Free Tier | Premium Tier |
|-------------|-----------|--------------|
| VirusTotal | 4 req/min | 1000+ req/min |
| GitHub API | 60 req/hr (unauth) | 5000 req/hr (auth) |
| CIRCL CVE | No limit | N/A |

## Custom List Schemas

### Blacklisted IP
```json
{
  "columns": [
    {"name": "IP", "dataType": "string"}
  ]
}
```

### CVE Watchdog History
```json
{
  "columns": [
    {"name": "CVE_Id", "dataType": "string"},
    {"name": "CVE_Published", "dataType": "string"},
    {"name": "CVE_Modified", "dataType": "string"}
  ]
}
```

### CVE Watchdog Patterns
```json
{
  "columns": [
    {"name": "cve_pattern", "dataType": "string"}
  ]
}
```

## LQL Query Reference

### Data Extraction
```sql
SELECT get_json_object(`result`, '$.field') AS field_name FROM table
```

### Filtering
```sql
SELECT * FROM table WHERE field > 'value' AND isnull(other_field) = 'true'
```

### Joining
```sql
joinTables([table1, table2], ["common_field"], "left")
```

### Pattern Matching
```sql
matchPattern(source_table, $.field_to_match, pattern_table, $.pattern_column)
```

## Notification Templates

### Alert Email Template
```
Subject: [SECURITY ALERT] {alert_type}

Alert Details:
- Time: {timestamp}
- Source: {source_system}
- Severity: {severity}

Description:
{alert_description}

Recommended Actions:
{remediation_steps}

Investigation Link: {case_url}
```

### Report Email Template
```
Subject: {report_name} - {date}

Summary:
{executive_summary}

Findings:
{html_table}

Generated by LogicHub Automation
```

## Troubleshooting

### Common Issues

#### IMAP Connection Failures
- Verify IMAP server and port (usually 993 for SSL)
- Check credentials and app-specific passwords
- Confirm SSL verification settings

#### VirusTotal API Errors
- Monitor API quota usage
- Implement rate limiting delays
- Check API key validity

#### Email Delivery Failures
- Verify SMTP authentication
- Check encryption settings (TLS required)
- Confirm recipient addresses

## Related Resources

- [LogicHub SOAR SOPs](/home/ubuntu/TinyHive-sops/cybersecurity/logichub_soar_sops.md)
- MITRE ATT&CK Framework mapping for detection rules
- SPINE governance policies
