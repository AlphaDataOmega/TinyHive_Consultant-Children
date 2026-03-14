# Shuffle SOAR Specialist Documentation

## Overview

This consultant specializes in Shuffle SOAR (Security Orchestration, Automation, and Response) workflow development, security automation, and incident response orchestration using the open-source Shuffle platform. The specialist draws from comprehensive knowledge of 17+ workflow templates covering email security, threat intelligence, cloud security, and SIEM integration.

## Core Competencies

### Email Security Workflows
- **IMAP Email Processing** — Schedule-based email polling with IOC extraction and threat intelligence enrichment via VirusTotal and GreyNoise
- **Gmail Integration** — Gmail API workflow for message retrieval, processing, and automated read status management
- **Microsoft Outlook Graph** — Microsoft Graph API integration for enterprise email security automation
- **OWA Integration** — Exchange OWA email handling with GPG decryption support for encrypted messages
- **Single Email Analysis** — Comprehensive email threat analysis pipeline with multi-source enrichment

### Threat Intelligence Operations
- **IP Reputation Analysis** — GreyNoise integration with intelligent caching for IP threat scoring
- **Hash Analysis** — VirusTotal file hash reputation checking with local cache optimization
- **URL Analysis** — URL reputation scoring via VirusTotal with cache-first architecture
- **IOC Parsing** — Automated extraction of IPs, domains, URLs, and hashes from unstructured text
- **Multi-Source Enrichment** — PassiveTotal, URLScan.io, and Cortex analyzer integration

### Cloud Security Operations
- **AWS EC2 IP Blocking** — Security Group modification for SSH and FTP attack containment
- **AWS S3 Access Control** — Bucket policy updates to block malicious IP access
- **Automated Containment** — Real-time blocking triggered by security alerts

### SIEM/EDR Integration
- **Wazuh Webhook Handler** — Alert ingestion and processing with TheHive case creation
- **Wazuh Active Response** — Command execution on Wazuh agents for automated remediation
- **TheHive Integration** — Case management, alert creation, and artifact tracking

### Communication Automation
- **Slack Notifications** — Simple and block message formatting for SOC alerting
- **Webex Integration** — Team creation, room management, and incident communication

## Workflow Reference

### Email Security Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| Email reader IMAP | Schedule, Subflow | Polls IMAP mailbox, extracts IOCs, enriches with VirusTotal/GreyNoise |
| Gmail reader | Schedule | Gmail API polling with message labeling and phishing detection hooks |
| [EMAIL] Get Outlook graph mail | Subflow | Microsoft Graph API email retrieval for enterprise environments |
| [EMAIL] Get emails from mailbox | Schedule, Subflow | OWA integration with GPG decryption capability |
| [EMAIL] Single email handler | Manual | Complete email analysis with URLScan.io, PassiveTotal, and TheHive |
| Handle_Multiple_Emails | Schedule, Subflow | Batch email processing with encryption handling |

### Threat Intelligence Workflows

| Workflow | Trigger | Key Functions |
|----------|---------|---------------|
| IP Threatlist Shuffle | Webhook | parse_ioc, get_cache_value, set_cache_value, GreyNoise lookup |
| Hash Threatlist Shuffle | Manual | Hash extraction, VirusTotal enrichment, cache management |
| URL Threatlist Shuffle | Manual | URL parsing, VirusTotal analysis, score aggregation |
| [IOC] Basic analysis | Manual | Multi-type IOC parsing with VirusTotal enrichment |

### Cloud Security Workflows

| Workflow | Cloud Service | Action |
|----------|---------------|--------|
| AWS S3 block IP | AWS S3 | Update bucket policy to deny access from malicious IP |
| SSH_Block_IP_AWS_Firewall | AWS EC2 | Add deny rule to Security Group for SSH attackers |
| FTP_Block_IP_AWS_Firewall | AWS EC2 | Block FTP brute force with Cortex enrichment |

### SIEM Integration Workflows

| Workflow | Platform | Integration |
|----------|----------|-------------|
| [WAZUH] Webhook handler | Wazuh | Alert processing, TheHive case creation |
| Wazuh command execution | Wazuh | Active response command execution via Wazuh API |

### Communication Workflows

| Workflow | Platform | Features |
|----------|----------|----------|
| Send Message to Slack | Slack | Simple text and Block Kit message formatting |
| Webex examples | Webex | Team/room management, message posting |

## Shuffle Tools Functions Reference

| Function | Input | Output | Use Case |
|----------|-------|--------|----------|
| `parse_ioc` | Text containing IOCs | Structured IOC list by type | Extract indicators from emails, logs |
| `filter_list` | Array + condition | Filtered array | Select specific IOC types or scores |
| `get_cache_value` | Cache key | Cached value or null | Retrieve previous analysis results |
| `set_cache_value` | Key + value + TTL | Confirmation | Store analysis for future lookups |
| `merge_lists` | Multiple arrays | Combined array | Aggregate results from multiple sources |
| `add_list_to_list` | Target list + items | Extended list | Append new IOCs to existing list |
| `run_math_operation` | Numbers + operation | Result | Calculate threat scores |
| `repeat_back_to_me` | Any input | Same input | Debug workflows, transform data |

## Integration Reference

### Supported Platforms

| Category | Integrations |
|----------|-------------|
| Email Systems | IMAP, Gmail API, Microsoft Graph API, OWA |
| Threat Intelligence | VirusTotal, GreyNoise, PassiveTotal, URLScan.io, Cortex |
| Case Management | TheHive |
| Cloud Platforms | AWS EC2, AWS S3 |
| SIEM/EDR | Wazuh |
| Communication | Slack, Webex |
| Utilities | HTTP, GPG Tools, Shuffle Tools |

### Trigger Types

| Type | Use Case | Configuration Example |
|------|----------|----------------------|
| WEBHOOK | Real-time alert processing | `POST /api/v1/hooks/{workflow_id}` |
| SCHEDULE | Periodic email polling | Every 5 minutes, hourly, daily |
| SUBFLOW | Modular workflow composition | Parent workflow invokes child |

## Workflow Design Patterns

### Pattern 1: Cache-First Enrichment

```
Input IOC
    |
    v
Check Cache --> [Hit] --> Return Cached Result
    |
    v [Miss]
Query External TI
    |
    v
Calculate Score
    |
    v
Store in Cache
    |
    v
Return Result
```

**Benefits**: Reduces API calls, improves response time, lowers costs

### Pattern 2: Multi-Stage Email Analysis

```
Email Received
    |
    v
Extract IOCs (parse_ioc)
    |
    +---> URLs --> VirusTotal/URLScan.io
    |
    +---> Domains --> PassiveTotal/VirusTotal
    |
    +---> IPs --> GreyNoise
    |
    +---> Hashes --> VirusTotal
    |
    v
Aggregate Results
    |
    v
Create TheHive Case (if malicious)
    |
    v
Send Notification
```

### Pattern 3: Automated Cloud Containment

```
Security Alert (Webhook)
    |
    v
Parse Attacker IP
    |
    v
Validate (not whitelisted)
    |
    v
Block in AWS Security Group
    |
    v
Create TheHive Alert
    |
    v
Send Notification
```

## Best Practices

### Workflow Development

1. **Use Descriptive Names** — Name actions clearly for audit trail readability
2. **Implement Error Branches** — Handle API failures gracefully
3. **Cache Aggressively** — Reduce external API dependencies
4. **Test with Sample Data** — Validate before production deployment
5. **Use Subflows** — Create reusable components for common patterns

### Security Considerations

1. **Credential Storage** — Use Shuffle's built-in credential management
2. **Input Validation** — Validate webhook inputs to prevent injection
3. **Rate Limiting** — Implement delays to respect API limits
4. **Least Privilege** — Use minimal permissions for integrations
5. **Audit Logging** — Enable comprehensive logging for compliance

### Performance Optimization

1. **Parallel Execution** — Run independent enrichments concurrently
2. **Conditional Branching** — Skip unnecessary steps based on context
3. **Cache TTL Management** — Balance freshness vs. API usage
4. **Batch Processing** — Group similar operations when possible

## Severity Classification

| Level | Description | Example Triggers |
|-------|-------------|------------------|
| Critical | Active attack, data exfiltration | Multiple failed logins + successful access |
| High | Confirmed malicious indicators | VirusTotal score > 10 detections |
| Medium | Suspicious activity | Unknown sender + external links |
| Low | Informational | Policy violation, minor anomaly |

## Related Resources

- Shuffle Documentation: https://shuffler.io/docs
- Shuffle GitHub: https://github.com/Shuffle/Shuffle
- Shuffle Apps Repository: https://github.com/Shuffle/python-apps
- TheHive Project: https://thehive-project.org/
- Wazuh Documentation: https://documentation.wazuh.com/
- VirusTotal API: https://developers.virustotal.com/
- GreyNoise API: https://docs.greynoise.io/
