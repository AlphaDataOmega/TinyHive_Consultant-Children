# Demisto SOAR Specialist - Documentation

## Overview

This directory contains reference documentation and operational guides for Demisto/XSOAR playbook development, security automation, and integration management.

## Core Competencies

### Phishing Incident Response
- Automated phishing detection and triage workflows
- Email file processing (EML, MSG, SMTP, S/MIME)
- Header parsing and indicator extraction
- URL screenshot capture and attachment analysis
- MineMeld threat intelligence integration

### Indicator Enrichment
- IP address enrichment with DBotScore integration
- CVE enrichment with CVSS score validation
- File-based indicator extraction (PDF, DOC, HTML, XLSX)
- Multi-source reputation data aggregation

### Endpoint Detection and Response

#### Fidelis Endpoint
- Alert management and host information queries
- Script execution with GenericPolling patterns
- File search, metadata retrieval, and download
- Behavioral queries (file, process, DNS)

#### Malwarebytes
- Scan and remediate/report operations
- Endpoint isolation (full, process, desktop, network)
- Managed endpoint inventory and status

#### Windows Defender ATP
- Machine health status and operations
- Alert creation and management
- Machine isolation (full, selective)
- Advanced hunting with KQL queries

### Threat Intelligence Management

#### ThreatConnect Operations
- Group management (Events, Campaigns, Threats, Incidents)
- Indicator lifecycle management
- Tag and security label application
- Indicator-to-group associations

### Cloud Security Monitoring

#### AWS CloudTrail
- Trail creation and configuration
- Logging control (start/stop)
- Event lookup and analysis
- CloudWatch and KMS integration

### ServiceNow ITSM Integration
- Ticket creation (incident, problem, change, task)
- Query and update operations
- Comment and link management
- File attachment handling
- Group and table queries

## Playbook Development Best Practices

### Context Management
- Use DeleteContext at playbook start for clean execution
- Validate outputs with VerifyContext and VerifyContextFields
- Implement proper error handling with PrintErrorEntry

### Polling Patterns
- Use GenericPolling for asynchronous operations
- Configure appropriate intervals and timeouts
- Define completion conditions with dt filters

### Timing Controls
- Use Sleep for required operation delays
- Allow adequate time for async operations (30+ seconds for isolation)
- Implement ScheduleCommand for scheduled tasks

## Integration Verification

### Pre-Flight Checklist
- API credentials configured and valid
- Network connectivity verified
- Required permissions granted
- Rate limits understood

### Output Verification
- Context contains expected keys
- Values match expected format
- No sensitive data in plaintext logs

## Quick Reference Commands

### Endpoint Security
```
fidelis-endpoint-list-alerts
fidelis-endpoint-host-info
fidelis-endpoint-file-search
malwarebytes-scan-and-remediate
malwarebytes-isolate-endpoint
microsoft-atp-list-alerts
microsoft-atp-isolate-machine
microsoft-atp-advanced-hunting
```

### Threat Intelligence
```
tc-add-indicator
tc-create-incident
tc-incident-associate-indicator
tc-get-indicators-by-tag
```

### Cloud Security
```
aws-cloudtrail-create-trail
aws-cloudtrail-start-logging
aws-cloudtrail-lookup-events
```

### ServiceNow
```
servicenow-create-ticket
servicenow-update-ticket
servicenow-add-comment
servicenow-query-tickets
```

## Related Resources

- Demisto/XSOAR Playbook Collection
- MITRE ATT&CK Framework
- ThreatConnect Documentation
- ServiceNow API Reference
- AWS CloudTrail User Guide
