# Rapid7 InsightConnect Specialist Documentation

## Overview

This specialist provides expertise in Rapid7 InsightConnect (formerly Komand) security orchestration, automation, and response (SOAR) platform. The knowledge base is derived from 214 production-ready InsightConnect playbooks covering phishing response, endpoint containment, network blocking, threat enrichment, vulnerability management, and ChatOps automation.

## Core Competencies

### ChatOps Security Automation
- Microsoft Teams and Slack command-driven workflows
- Real-time security response from chat platforms
- Standardized command patterns for cross-team consistency

### Endpoint Containment
- Multi-EDR platform quarantine (CrowdStrike, Defender ATP, Carbon Black, SentinelOne, CylanceOPTICS, Trend Micro, Symantec, Cybereason, Insight Agent)
- InsightIDR alert-triggered containment
- Mimecast/Netskope correlation-based containment

### Firewall and Network Blocking
- Multi-vendor firewall automation (Palo Alto, Cisco ASA, Fortinet, Check Point, SonicWall, Cisco Meraki)
- Hash blacklisting across EDR platforms
- Microsoft Defender ATP indicator blocking
- Zscaler URL blacklisting
- Cross-platform synchronization

### Phishing Response
- Email search and deletion (Office 365, Gmail)
- Sender blocking via transport rules
- Spearphishing remediation with Mimecast/Office 365
- Phishing database management via Global Artifacts

### Threat Intelligence Enrichment
- OSINT enrichment (DNS, WHOIS, Team Cymru, GeoIP, URLScan)
- VirusTotal hash and URL analysis
- Recorded Future domain/IP/hash/URL intelligence
- CVE and vulnerability lookup (Rapid7 VDB, AttackerKB)

### User Account Management
- Active Directory operations (disable, enable, password reset, unlock)
- Azure AD operations (disable, password reset, session revocation)
- InsightIDR UBA alert-triggered user containment
- Multi-country authentication alerting

### Vulnerability Management
- InsightVM asset scanning via ChatOps
- Vulnerability exception automation
- Remediation ticket creation (ServiceNow, Jira, Zendesk)
- High-risk vulnerability alerting
- Asset lifecycle management

## ChatOps Command Reference

### Endpoint Commands
| Command | Description |
|---------|-------------|
| `!quarantine-endpoint <host>` | Isolate endpoint (multi-platform) |
| `!unquarantine-endpoint <host>` | Release endpoint from isolation |
| `!isolate-machine <host>` | Isolate endpoint (Cybereason) |

### Network Commands
| Command | Description |
|---------|-------------|
| `!block-host <IP>` | Block IP at firewall |
| `!unblock-host <IP>` | Remove IP block |
| `!blacklist-hash <hash>` | Block file hash |
| `!blacklist-indicators <IOC>` | Block indicators (Defender/CrowdStrike) |
| `!blacklist-url <URL>` | Block URL (Zscaler) |

### User Commands
| Command | Description |
|---------|-------------|
| `!disable-user-ad <user>` | Disable AD account |
| `!enable-user-ad <user>` | Enable AD account |
| `!reset-password-ad <user>` | Force password reset |
| `!unlock-user-ad <user>` | Unlock AD account |
| `!disable-user-azure <user>` | Disable Azure AD account |
| `!reset-password-azure <user>` | Reset Azure AD password |
| `!revoke-session-azure <user>` | Revoke Azure AD sessions |

### Email Commands
| Command | Description |
|---------|-------------|
| `!find-email <user> subject="..."` | Search emails |
| `!find-email <user> ... delete="True"` | Search and delete |
| `!block-sender <sender>` | Block email sender |

### Enrichment Commands
| Command | Description |
|---------|-------------|
| `!enrich-indicator <IOC>` | OSINT enrichment |
| `!enrich-hash <hash>` | VirusTotal hash analysis |
| `!lookup-vuln <CVE>` | Vulnerability lookup |
| `!lookup-domain <domain>` | Recorded Future domain intel |
| `!lookup-ip <IP>` | Recorded Future IP intel |
| `!geoip <IP>` | GeoIP lookup |

### Vulnerability Commands
| Command | Description |
|---------|-------------|
| `!scan-asset <host>` | Scan single asset |
| `!lookup-host <host>` | Get asset details |
| `!lookup-remediations` | Get top remediations |
| `!lookup-vulnerable-hosts <CVE>` | Find vulnerable hosts |

## Platform Architecture

### InsightConnect Components
- **Insight Orchestrator**: On-premises agent for internal network access
- **InsightConnect Cloud**: SaaS platform for workflow orchestration
- **Plugin Connections**: API credentials for integrated tools

### Workflow Export Format
Workflows are exported as `.icon` files (JSON format) containing:
- Workflow metadata and versioning
- Graph nodes defining workflow steps
- Plugin references and configurations
- Trigger definitions (API, ChatOps, scheduled)

## Integration Requirements

### Common Plugin Requirements
| Plugin | Purpose | Typical Version |
|--------|---------|-----------------|
| Microsoft Teams | ChatOps interface | 3.1.x |
| Active Directory LDAP | User management | 5.2.x |
| CrowdStrike Falcon | EDR integration | 2.2.x |
| Palo Alto Firewall | Network blocking | 6.1.x |
| ServiceNow | Ticketing | 4.0.x |
| Rapid7 InsightVM | Vulnerability scanning | 4.0.x |
| VirusTotal | Hash analysis | 2.x |

### Network Requirements
| Component | Port | Protocol | Purpose |
|-----------|------|----------|---------|
| Insight Orchestrator | 443 | HTTPS | Cloud communication |
| Active Directory | 389/636 | LDAP/LDAPS | User management |
| InsightVM Console | 3780 | HTTPS | API access |
| Firewall APIs | 443 | HTTPS | Rule management |

## Playbook Categories

| Category | Count | Description |
|----------|-------|-------------|
| Firewall/Blocking | 45 | Network blocking and hash blacklisting |
| Threat Enrichment | 41 | IOC enrichment and threat intelligence |
| Vulnerability Management | 40 | Asset scanning and remediation tracking |
| Endpoint Containment | 25 | Endpoint isolation and quarantine |
| Phishing Response | 19 | Email analysis and remediation |
| User Management | 14 | Account enable/disable/reset |
| Alerting | 5 | Alert routing and notification |
| Ticketing | 3 | Ticket creation and management |
| Other/Utility | 21 | Supporting workflows |

## Related Documentation

- Rapid7 InsightConnect Security Automation SOP (RAPID7-SOAR-SOP-001)
- InsightVM Integration Guide
- ChatOps Setup and Configuration
- Plugin Connection Reference
