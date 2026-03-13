# Tines Automation Specialist Documentation

## Overview

This documentation supports the Tines Automation Specialist consultant in designing and implementing security automation workflows using the Tines SOAR platform. The workflows cover detection and response, threat intelligence operations, identity management, data loss prevention, and deception technology integration.

## Core Workflow Categories

### 1. Detection and Response Automation

#### CrowdStrike Detection Analysis
- **Trigger**: Scheduled (every 5 minutes)
- **Process**: Query new detections, extract behaviors and hashes, enrich with VirusTotal, create Jira cases
- **Integrations**: CrowdStrike Falcon, VirusTotal, Jira, Slack

#### SentinelOne Threat Remediation
- **Trigger**: Daily at 9:00 AM
- **Process**: Query unresolved threats, validate with VirusTotal, execute automated remediation
- **Actions**: Mark as threat, kill process, quarantine file, initiate scan, ban hash
- **Integrations**: SentinelOne, VirusTotal, Jira

### 2. Threat Intelligence Operations

#### US-CERT IOC Monitoring
- **Trigger**: Scheduled RSS feed check
- **Process**: Parse advisories, extract IOCs from PDFs, enrich with threat intelligence, notify analysts
- **IOC Types**: IPv4, domains, hashes, URLs
- **Integrations**: US-CERT RSS, IOC Parser, VirusTotal

#### Elastic Security Alert Triage with IP Blocking
- **Trigger**: Webhook from Elastic Security
- **Process**: Create case, check IP reputation with GreyNoise, block malicious IPs on GCP firewall
- **Integrations**: Elastic Security, GreyNoise, GCP Compute, Elasticsearch, OSQuery

### 3. Identity and Access Management

#### AWS IAM Inactive User Cleanup
- **Trigger**: Scheduled
- **Process**: Enumerate users, analyze service access, classify inactivity, create cases, enable deactivation
- **Classification**: Never used (created >30 days, no access) or Inactive (last access >30 days)
- **Actions**: Attach/detach AWSDenyAll policy
- **Integrations**: AWS IAM, Jira

### 4. Data Loss Prevention

#### Google Drive Public File Enforcement
- **Trigger**: Webhook from Panther SIEM
- **Process**: Authenticate via domain-wide delegation, retrieve file metadata, notify user via Slack, handle response
- **User Options**: Remove permissions, confirm intentional, request SIRT review
- **Timeout**: 10 hours auto-remediation
- **Integrations**: Google Drive API, Slack, Panther

### 5. Deception Technology Integration

#### Thinkst Canary Alert Processing
- **Trigger**: Canary Tools webhook
- **Alert Types**: CanaryBird (honeypot devices), CanaryToken (DNS/PDF/AWS tokens)
- **Process**: Fetch incident details, enrich source IP, classify priority, create case, escalate
- **Priority Levels**: Highest (restricted zone), Medium (trusted zone), Low (default)
- **Integrations**: Thinkst Canary, Auth0 Signals, GreyNoise, Jira, PagerDuty, Slack

## Platform Requirements

### Required Integrations

| Integration | Purpose | Required Scopes |
|-------------|---------|-----------------|
| CrowdStrike | EDR Detections | Detection: Read/Write, Hosts: Read/Write |
| SentinelOne | Threat Management | API Token with Full Access |
| VirusTotal | Hash/IOC Analysis | API Key (Premium recommended) |
| Jira | Case Management | Create/Update Issues |
| Slack | Notifications | Bot Token with Chat Permissions |
| AWS IAM | Identity Management | IAM Admin Access |
| Google Workspace | DLP Enforcement | Domain-Wide Delegation |
| Elastic Security | SIEM Operations | API Access |
| Thinkst Canary | Deception Alerts | API Token |
| GreyNoise | IP Reputation | Community or Enterprise API |
| PagerDuty | Escalation | Events API v2 |

### Tines Resources Configuration

```yaml
Resources:
  - crowdstrike_domain: "falcon.us-2.crowdstrike.com"
  - jira_domain: "company.atlassian.net"
  - jira_username: "service-account@company.com"
  - slack_url: "https://hooks.slack.com/services/XXX"
  - sentinelone_server: "usea1.sentinelone.net"
  - elasticsearch_url: "https://elastic.company.com:9200"
  - kibana_url: "https://kibana.company.com"
  - canary_domain: "tenant.canary.tools"

Credentials:
  - crowdstrike: OAuth Token
  - virustotal: API Key
  - jira: API Token
  - slack: Bot Token
  - sentinelone: API Token
  - aws: AWS4-HMAC-SHA256 Signature
  - gcp_svc_acct_jwt_sign: Service Account Private Key
  - canary: API Token
  - greynoise: API Key
  - pagerduty: Events API Key
```

## Implementation Patterns

### Deduplication Strategies

```yaml
By Source Host (5 min):
  Path: src_host
  Period: 300 seconds
  Purpose: Prevent alert flooding

By Content Hash (24 hours):
  Path: fileContentHash + agent_id
  Period: 86400 seconds
  Purpose: Avoid duplicate threat processing

By Incident Key (variable):
  Path: dst_host + src_host + description
  Period: Configurable
  Purpose: Consolidate related incidents
```

### Rate Limiting

```yaml
VirusTotal:
  Public API: 4 requests/minute
  Implementation: 30-second delay between requests
  Error Handling: Retry on 429/204 status

CrowdStrike:
  Implementation: Batch requests where possible
  Pagination: Handle IsTruncated responses

SentinelOne:
  Pagination: 100 items per page
  Implementation: Process in batches with delays
```

### Error Handling

```yaml
HTTP Request Failures:
  - Log error status
  - Retry with exponential backoff
  - Alert on persistent failures

API Authentication:
  - Token refresh before expiry
  - Credential rotation procedures
  - Fallback notification on auth failure

Empty Results:
  - Graceful handling
  - Alternative enrichment sources
  - Document data unavailability
```

## MITRE ATT&CK Mapping

| Workflow | Tactics | Techniques |
|----------|---------|------------|
| CrowdStrike Detection | Multiple | Based on detection type |
| SentinelOne Remediation | Defense Evasion, Execution | T1059, T1027 |
| IP Blocking | Command & Control | T1071 |
| Canary Alerts | Lateral Movement, Discovery | T1046, T1018 |
| IAM Cleanup | Credential Access | T1078 |
| DLP Enforcement | Exfiltration | T1567 |

## Severity Classification Matrix

| Score | Level | Response Time | Escalation |
|-------|-------|---------------|------------|
| 90-100 | Critical | 15 minutes | Immediate PagerDuty |
| 70-89 | High | 1 hour | Slack + Jira |
| 40-69 | Medium | 4 hours | Jira only |
| 0-39 | Low | 24 hours | Batch review |

## Deployment Checklist

### Pre-Deployment
- [ ] Document all required API credentials
- [ ] Verify API rate limits and quotas
- [ ] Test integrations in sandbox environment
- [ ] Define escalation contacts
- [ ] Create Jira project and issue types
- [ ] Configure Slack channels and webhooks
- [ ] Set up email distribution lists

### Deployment
- [ ] Import Tines stories
- [ ] Configure resources and credentials
- [ ] Set scheduling for automated workflows
- [ ] Enable monitoring for all actions
- [ ] Test webhook endpoints

### Post-Deployment
- [ ] Monitor for errors in first 24 hours
- [ ] Validate case creation
- [ ] Verify notification delivery
- [ ] Document any customizations

## Maintenance Schedule

### Weekly
- Review failed action logs
- Check API quota usage
- Validate credential validity

### Monthly
- Review and tune deduplication settings
- Update threat intelligence sources
- Audit automated response actions
- Update documentation

### Quarterly
- Full workflow testing
- Credential rotation
- Integration health check
- Performance optimization review

## Reference Documentation

| Platform | Documentation URL |
|----------|-------------------|
| Tines | https://hub.tines.com/docs |
| CrowdStrike | https://falcon.crowdstrike.com/documentation |
| SentinelOne | https://usea1.sentinelone.net/docs |
| VirusTotal | https://developers.virustotal.com |
| AWS IAM | https://docs.aws.amazon.com/IAM/latest/APIReference |
| Google Drive | https://developers.google.com/drive/api |
| Elastic Security | https://www.elastic.co/guide/en/security |
| Thinkst Canary | https://docs.canary.tools |
| GreyNoise | https://docs.greynoise.io |
| PagerDuty | https://developer.pagerduty.com |

## Glossary

- **SOAR**: Security Orchestration, Automation, and Response
- **EDR**: Endpoint Detection and Response
- **IOC**: Indicator of Compromise
- **DLP**: Data Loss Prevention
- **IAM**: Identity and Access Management
- **SIEM**: Security Information and Event Management
- **Canary/Honeypot**: Deception technology to detect intrusions
- **MTTR**: Mean Time to Respond
- **Story**: Tines workflow automation unit
- **Action**: Individual step within a Tines story
