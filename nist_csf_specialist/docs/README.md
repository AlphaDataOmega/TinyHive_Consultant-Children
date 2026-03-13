# NIST CSF Specialist Documentation

## Overview

The NIST CSF Specialist provides expertise in implementing the NIST Cybersecurity Framework through CISA-aligned playbooks. This specialist manages 51 interconnected workflows across the five CSF functions and coordinates threat intelligence, CVE handling, and incident response operations.

## Core Knowledge Domains

### NIST Cybersecurity Framework Functions

| Function | Workflow Count | Primary Focus |
|----------|----------------|---------------|
| **IDENTIFY (ID)** | 8 | Asset management, threat intelligence curation, CVE processing |
| **PROTECT (PR)** | 3 | Vulnerability management, patch testing and deployment |
| **DETECT (DE)** | 18 | Alert processing, IOC evaluation, system monitoring |
| **RESPOND (RS)** | 18 | COA execution, blocking actions, system remediation |
| **RECOVER (RC)** | 3 | List maintenance, feed monitoring, conflict resolution |

### Threat Intelligence Workflows

#### STIX Processing Pipeline
1. **Curate Incoming STIX Messages** - Validate against SOC-defined rules and submitter behavior
2. **Create Submitter Behavior Profile** - Maintain reputation scoring for intelligence sources
3. **Threat Intel Receipt** - Extract IOCs, IDS rules, and COAs from validated STIX objects
4. **Review Submitted IDS Rules** - SOC approval workflow for external IDS rules

#### Intelligence Sharing
- **Submit IOC Sighting** - Share sighting data when organizational thresholds met
- **Share Event Information** - Format and distribute approved intel via TAXII
- **Remove False Positive STIX Object** - Clean TIP and update submitter profiles

### CVE Handling Workflow

```
Process Incoming CVE
    |-> Duplicate Check
    |-> Network Presence Check
    |-> Risk/Severity Assessment
        |-> CVE Patch Testing (PROTECT)
            |-> Verify CVE Patch Testing
                |-> Patch Systems for CVE
```

**Key Decision Points:**
- CVE already addressed: Terminate
- No network presence: Update scanners, mark N/A
- Meets response threshold: Trigger patch testing
- All other CVEs: Generate NOC ticket per policy

### IOC Processing and Risk Scoring

#### Evaluation Flow
1. Check against block/allow lists
2. Determine local prevalence (IPs, domains, URLs, files, emails)
3. Calculate risk score based on:
   - Asset information (machine type, server vs workstation, network location)
   - Vulnerability risk (severity of potential compromise)
   - Mission risk (impact, asset criticality, quarantine impact)

#### Blocking Actions by IOC Type
| IOC Type | Actions |
|----------|---------|
| IP Address | Add to IDS + Block at Firewall |
| Domain/URL | Add to IDS + Block at Proxy + Block at Firewall |
| File | Block at Endpoint + Add Hash to IDS |
| Email | Block at Email Security + Add to Blocked Senders |

### Course of Action (COA) Execution

#### System COA Alert Review
- Present suggested COAs to SOC operator
- IOC blocking selection
- System remediation triggering
- Information sharing coordination

#### Account COA Alert Review
- Policy-based actions for user types (general, privileged, service accounts)
- Automatic password resets when policy allows
- Escalation for infrastructure breach indicators

#### Heartbeat Failure COAs
- Service restart approval
- Reinstall from configuration management
- Server rebuild from restoration image

### ICS-Specific Workflows

1. **ICS Asset Integrity Check** - Run organization-defined integrity checks
2. **ICS Asset Mitigation** - Quarantine, hot spare migration, restoration
3. **ICS Asset Recovery** - Functionality testing and verification

## Automation Levels

| Level | Description |
|-------|-------------|
| **Fully Automated** | No human intervention; executes on policy thresholds |
| **Semi-Automated** | Requires human approval at decision points |
| **Manual with Automation Support** | Human-driven with automated enrichment |

## Integration Requirements

| System | Purpose |
|--------|---------|
| SOAR Platform | Workflow orchestration, case management |
| SIEM | Alert ingestion, log correlation |
| TIP | STIX processing, threat intelligence management |
| TAXII Server | Intelligence sharing |
| IDS/IPS | Rule deployment, alert processing |
| EDR | Endpoint blocking, investigation data |
| Firewall | IP/domain blocking |
| Proxy/DNS Sinkhole | Domain/URL blocking |
| Email Security | Sender blocking, phishing analysis |
| CMDB | Asset information, hot spare identification |
| Configuration Management | System restoration, patch deployment |
| Ticketing System | SOC/NOC notifications, approvals |
| Vulnerability Scanner | CVE validation, patch verification |

## Critical Path Scenarios

| Scenario | Workflow Path |
|----------|---------------|
| **Phishing Email** | Suspicious Email Triage -> Identify Systems/IOCs -> Process IOCs -> Evaluate -> Risk Score -> COAs -> Blocking |
| **CVE Response** | Process CVE -> Patch Testing -> Verify -> Deploy Patches |
| **ICS Incident** | ICS Alert -> Identify Systems -> Response Review -> Integrity Check -> Mitigation -> Recovery |
| **Service Failure** | Heartbeat Failure -> Identify Systems -> Response Review -> COAs -> Reinstall -> Rebuild |
| **Account Compromise** | Account Alert -> Monitor Account -> Account COA Review |

## Roles and Responsibilities

### SOC
- Alert triage and analysis
- IOC evaluation and response decisions
- Account incident response
- False positive determination
- Information sharing approval

### NOC
- CVE remediation within policy
- Patch deployment
- Service restoration
- System rebuild coordination

### Threat Intelligence Team
- STIX curation and validation
- Submitter profile management
- False positive handling
- Information sharing execution
- IDS rule review
- Feed health monitoring

### ICS Operations
- ICS alert response
- Asset integrity verification
- Asset mitigation and recovery

### Service Owners
- Service restart approval
- Reinstall/rebuild approval

## Reference

This documentation is derived from the CISA Automated Indicator Sharing (AIS) playbook collection aligned to the NIST Cybersecurity Framework.
