# TheHive Specialist Documentation

## Overview

This directory contains reference documentation for TheHive SIRP operations, SOAR integration, and incident response automation.

## Core Competencies

### TheHive Platform
- Security Incident Response Platform (SIRP) deployment and configuration
- Alert and case lifecycle management
- Observable/IOC tracking and correlation
- RESTful API integration and webhook processing

### SOAR Integration
- Shuffle orchestration and automation playbooks
- Cortex analyzer configuration for enrichment
- Bidirectional API communication patterns
- Webhook handler design and implementation

### Threat Intelligence
- MISP integration for threat intelligence sharing
- OpenCTI connectivity for IOC correlation
- Automated enrichment from community/commercial feeds
- Observable analysis workflows

### Incident Response
- NIST SP800-61 lifecycle implementation
- Alert triage and case promotion workflows
- Automated containment and eradication actions
- Evidence preservation and documentation

## Reference Architecture

```
                +------------------+
                |      SIEM        |
                | (Elastic/Splunk) |
                +--------+---------+
                         |
                         v
+------------------+   +-----------+   +------------------+
|       TIP        |<->|  TheHive  |<->|       SOA        |
| (MISP/OpenCTI)   |   |   (SIRP)  |   | (Shuffle/Cortex) |
+------------------+   +-----------+   +------------------+
                         |
                         v
                +------------------+
                |      ITSM        |
                |  (ConnectWise)   |
                +------------------+
```

## Key Workflows

### Alert Pipeline
1. SIEM/Wazuh generates security event
2. Webhook triggers alert creation in TheHive
3. Automated enrichment via Cortex/TIP
4. Analyst triage and severity assignment
5. Promote to case or close as false positive

### Case Management
1. Case created from promoted alert
2. Tasks assigned to analysts
3. Observables extracted and analyzed
4. Containment actions executed
5. Eradication and recovery performed
6. Case closed with documentation

### Automated Response
1. Alert triggers Shuffle playbook
2. IOCs extracted and enriched
3. Containment actions (firewall blocks, isolation)
4. TheHive updated with action results
5. Team notified via email/Slack

## Related SOPs

- TheHive SIRP Operations and Integration SOP
- Shuffle SOAR Playbook Development
- Cortex Analyzer Configuration
- MISP Threat Intelligence Integration
- Incident Response Workflow Automation

## External Resources

- [TheHive Project](https://thehive-project.org/)
- [Shuffle SOAR](https://shuffler.io/)
- [MISP Project](https://www.misp-project.org/)
- [OpenCTI](https://www.filigran.io/en/products/opencti/)
- [Cortex Analyzers](https://github.com/TheHive-Project/Cortex-Analyzers)
