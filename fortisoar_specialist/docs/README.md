# FortiSOAR Specialist Documentation

## Overview

This documentation provides comprehensive procedures for security operations using the FortiSOAR (Fortinet Security Orchestration, Automation, and Response) platform, covering alert management, indicator handling, incident response, and integration with Fortinet security infrastructure.

## Core Competencies

### Alert Management
- Alert triage and escalation to incidents
- SLA management (acknowledgment and response tracking)
- SLA pause/resume functionality
- Violation notifications and stakeholder alerts

### Indicator Management
- Automated extraction from emails, alerts, and mapped fields
- Supported types: IP, Domain, URL, Email, File Hash (MD5/SHA1/SHA256), Host, Process
- Multi-source reputation enrichment
- Lifecycle management with TTL and expiry tracking

### Indicator Blocking
- Unified blocking workflow for all indicator types
- FortiGate quarantine-based IP blocking
- FortiEDR host isolation
- Domain and URL web filter blocking
- File hash blocking via CarbonBlack watchlists

### Threat Hunting
- Indicator hunting across EDR and SIEM
- CarbonBlack file hunting with host identification
- Elasticsearch IP queries
- Phishme Intelligence domain hunting

### Incident Response (NIST 800-61)
- Detection and analysis phase tasks
- Containment strategies
- Eradication procedures
- Recovery and validation
- Post-incident lessons learned

## Fortinet Integration Matrix

| Product | Operations |
|---------|------------|
| FortiGate Firewall | IP blocking, quarantine, unblock |
| FortiEDR | Host isolation, collector management |
| FortiSandbox | File/URL submission and analysis |
| Fortinet Web Filter | Domain/URL reputation lookup |
| FortiDeceptor | Attacker tag management |

## Third-Party Integrations

| Platform | Use Case |
|----------|----------|
| CarbonBlack Response | File hunting, host isolation |
| CarbonBlack Protect | File reputation, binary analysis |
| Elasticsearch | Log queries, IP hunting |
| VirusTotal | Multi-type indicator reputation |
| AlienVault OTX | Threat intelligence enrichment |
| Anomali ThreatStream | IP, domain, email, URL, file reputation |
| Exchange/IMAP | Email processing and phishing analysis |

## Key Playbooks Reference

| Category | Playbook |
|----------|----------|
| Alert Management | Alert - Escalate To Incident |
| Alert Management | Alert - Update SLA Details |
| Indicator | Extract Indicators |
| Indicator | Indicator (Type All) - Get Latest Reputation |
| Blocking | Action (Type All) - Block Indicators |
| Blocking | Action - IP Address - Block (Fortigate,FortiEDR) |
| Hunting | Hunt Indicators |
| Incident Response | Incident Response Plan (Type - Malware) |
| NIST Framework | NIST 800-61 - Upfront Tasks |

## SLA Configuration

### Acknowledgment SLA
- Tracked upon alert creation
- Due dates calculated by severity
- Violation monitoring and notification

### Response SLA
- Tracked upon status update
- Severity-based due date calculation
- Escalation procedures for violations

## Best Practices

1. **Alert Handling**
   - Process alerts within SLA timeframes
   - Extract indicators before investigation
   - Enrich indicators with reputation data
   - Document all actions taken

2. **Incident Response**
   - Follow NIST 800-61 framework phases
   - Document each phase transition
   - Assign clear ownership
   - Maintain chain of custody

3. **Indicator Management**
   - Use excludelists to reduce extraction noise
   - Set appropriate TTLs for indicators
   - Review expired indicators periodically
   - Maintain current reputation data

4. **Blocking Actions**
   - Document blocking reasons
   - Configure appropriate TTLs for blocks
   - Review blocks periodically
   - Maintain unblock procedures

## Escalation Path

| Level | Role |
|-------|------|
| Level 1 | SOC Analyst |
| Level 2 | Senior Analyst |
| Level 3 | Security Engineer |
| Level 4 | Security Manager |

## Global Variables

| Variable | Purpose |
|----------|---------|
| Excludelist_IPs | IPs to exclude from extraction |
| Excludelist_Domains | Domains to exclude from extraction |
| Excludelist_URLs | URLs to exclude from extraction |
| Default_Indicator_TTL_Days | Default indicator expiry period |
| Indicator_Type_Map | Field to indicator type mapping |

## Source Documentation

- [SOP-FortiSOAR-Security-Operations.md](/home/ubuntu/TinyHive-sops/SOP-FortiSOAR-Security-Operations.md)
