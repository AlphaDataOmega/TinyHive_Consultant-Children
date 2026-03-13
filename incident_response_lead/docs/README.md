# Incident Response Lead - Documentation

## Overview

This directory contains reference documentation and resources for the Incident Response Lead consultant agent specializing in incident response lifecycle management, PICERL framework execution, incident command, forensic investigation oversight, and post-incident review processes.

## Core Competencies

### Incident Command Structure

The Incident Response Lead operates as the Incident Commander (IC) during security incidents:

- **Incident Commander (IC)**: Single source of truth, coordinates all response activities
- **Deputy IC**: Supports IC, tracks parallel workstreams, assumes IC role if needed
- **Scribe**: Documents timeline, decisions, actions, and meeting notes
- **Subject Matter Experts (SMEs)**: Provide technical expertise and execute tasks
- **Liaison Team**: Manage internal and external communications

### PICERL Framework

The six-phase incident response lifecycle:

1. **Preparation**: User education, application allowlisting, account controls, backups, host/server/network hardening
2. **Identification**: Incident assessment, functional/information impact analysis, incident classification
3. **Containment**: ACLs, blocks, account disablement, system isolation, malicious process termination
4. **Eradication**: System rebuild, password resets, hostile account removal, malware deletion
5. **Recovery**: Business continuity activation, fail-over implementation, system restoration, integrity validation
6. **Lessons Learned**: After-action reviews, root cause analysis, improvement action items

### Investigation Phase Activities

- Create incident file with functional/information impact, attack vector, timeline, evidence
- Collect initial leads through interviews and supporting data
- Develop investigative plan using MITRE ATT&CK framework
- Create and deploy IOCs (network-based, host-based, behavioral)
- Collect evidence from host and network artifacts
- Analyze evidence and enrich with threat intelligence

### Evidence Categories

**Host-Based Artifacts:**
- Running processes and services
- Parent-child process trees
- Executable hashes
- Listening ports and connections
- Persistence mechanisms (Run keys, scheduled tasks, autoruns)
- Artifacts of execution (Prefetch, Shimcache)
- Event logs and anti-virus detections

**Network-Based Artifacts:**
- DNS traffic and anomalies
- RDP, VPN, SSH sessions
- URI and user agent strings
- Connections to threat indicators

### Remediation Categories

- **Protect**: Patch systems, update signatures, enable MFA, strengthen passwords
- **Detect**: Enhance logging, update IDS signatures with IOCs
- **Contain**: Implement ACLs/blocks, disable accounts, isolate systems
- **Eradicate**: Rebuild systems, reset credentials, remove malware

### Post-Incident Review

After-action review key questions:
1. What happened? (Timeline with data/artifacts)
2. What was supposed to happen? (Deviations from process)
3. What were the root causes?
4. How can we improve? (Stop/Start/Continue action items)

## Key Metrics

- Average Cost Per Incident
- Average Time to Detect (MTTD)
- Average Time to Contain (MTTC)
- Average Time to Expel (MTTE)
- Average Time to Notify
- Incidents per Severity
- False Positive Rate per Use Case
- Incidents per Attack Technique

## Reference Frameworks

- NIST SP800-61 (Incident Response Lifecycle)
- MITRE ATT&CK Framework
- SANS Incident Handling Guide
- NIST Cybersecurity Framework

## Common Mistakes to Avoid

1. **Premature Mitigation**: Modifying volatile data or tipping off attacker
2. **Touching Adversary Infrastructure**: Alerting adversary to detection
3. **Preemptive Blocking**: Blocking before investigation complete
4. **Preemptive Credential Resets**: Resetting credentials before understanding scope
5. **Failure to Preserve Logs**: Not collecting or retaining critical logs
6. **Using Compromised Communications**: Adversary observing response activities
7. **Fixing Symptoms Only**: Not investigating root cause

## Related Agents

- `soc_analyst`: SOC operations, detection engineering, threat intelligence
- `malware_response_analyst`: Malware analysis and remediation
- `vulnerability_analyst`: Vulnerability assessment and management
- `cloud_security_engineer`: Cloud security architecture and response
