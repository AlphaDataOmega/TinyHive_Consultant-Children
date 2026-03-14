# Threat Hunting Specialist Documentation

## Overview

This directory contains reference documentation for the Threat Hunting Specialist consultant, specializing in proactive threat hunting operations, hypothesis development, MITRE ATT&CK alignment, TTP-based detection, intelligence integration, and hunt-to-detection operationalization.

## Core Competencies

### Hunt Maturity Model (HMM)

| Level | Name | Characteristics | Target Capability |
|-------|------|----------------|-------------------|
| **HMM0** | Initial | No structured hunting, reactive only | Establish baseline |
| **HMM1** | Minimal | IOC-based hunting, ad-hoc searches | Basic threat detection |
| **HMM2** | Procedural | Structured hunts, regular cadence, TTP awareness | Operational hunting |
| **HMM3** | Innovative | Hypothesis-driven, TTP-focused, custom analytics | Advanced hunting |
| **HMM4** | Leading | Automated hunting, ML/AI integration, continuous | Industry leadership |

**Recommended Maturity Target**: HMM2-HMM3 for most organizations

### Hunt Lifecycle Phases

```
1. PLAN → 2. PREPARE → 3. EXECUTE → 4. ANALYZE → 5. VALIDATE → 6. DOCUMENT
                                                                      ↓
                                                            ← ← IMPROVE ← ←
```

| Phase | Key Activities | Outputs |
|-------|---------------|---------|
| **PLAN** | Define scope, develop hypothesis, identify data sources | Hunt plan document |
| **PREPARE** | Validate data availability, configure tools, review intel | Ready environment |
| **EXECUTE** | Run queries, collect artifacts, document observations | Hunt log, raw data |
| **ANALYZE** | Correlate findings, identify patterns, apply ATT&CK | Analysis notes |
| **VALIDATE** | Confirm TPs vs FPs, multi-source corroboration | Validated findings |
| **DOCUMENT** | Create hunt report, detection artifacts, lessons learned | Hunt report, detections |

## Hunt Types and Techniques

### Hunt Type Matrix

| Hunt Type | Maturity Level | Data Sources | Use Case |
|-----------|---------------|--------------|----------|
| **Intelligence-Driven** | HMM1-HMM3 | TI feeds, reports, IOCs | APT campaigns, malware families |
| **IOC-Based** | HMM1 | SIEM, EDR, network logs | Known indicator sweeps |
| **TTP-Based** | HMM2-HMM3 | EDR, Sysmon, process logs | Behavioral threat detection |
| **Anomaly-Based** | HMM3 | All sources, baselines | Statistical deviations, outliers |
| **Crown Jewel** | HMM2-HMM3 | Critical asset logs | Protect high-value systems |
| **Campaign-Based** | HMM3 | Multi-source correlation | Multi-stage adversary operations |

### Hypothesis Development Framework

**WHY-WHAT-WHERE-WHEN-HOW Structure:**

| Component | Description | Example |
|-----------|-------------|---------|
| **WHY** | Threat motivation | APT targeting intellectual property |
| **WHAT** | Expected evidence | Credential dumping via LSASS access |
| **WHERE** | Target systems | Domain controllers, critical servers |
| **WHEN** | Temporal factors | After-hours activity, weekends |
| **HOW** | Detection method | Process access analysis, memory inspection |

**Hypothesis Sources:**
- Threat intelligence (APT reports, malware analysis, campaigns)
- Incident history (previous attacks, common patterns)
- Security gaps (unmonitored surfaces, detection blind spots)
- Emerging threats (new CVEs, zero-days, novel TTPs)

## MITRE ATT&CK Hunting Priorities

### Tier 1: Critical Techniques (Hunt Monthly)

| Technique ID | Technique Name | Hunt Priority Rationale |
|--------------|----------------|------------------------|
| T1003.001 | LSASS Memory Dumping | High prevalence, enables lateral movement |
| T1059.001 | PowerShell Execution | Common in ransomware and APT campaigns |
| T1021.001 | Remote Desktop Protocol | Lateral movement, often abused |
| T1053.005 | Scheduled Task/Job | Persistence, common across all threat actors |
| T1078 | Valid Accounts | Difficult to detect, high impact |
| T1027 | Obfuscated Files/Info | Defense evasion, malware delivery |
| T1071.001 | Web Protocols (C2) | Command and control, data exfiltration |
| T1486 | Data Encrypted for Impact | Ransomware, business disruption |

### Tier 2: Important Techniques (Hunt Quarterly)

| Technique ID | Technique Name | Hunt Priority Rationale |
|--------------|----------------|------------------------|
| T1547.001 | Registry Run Keys | Common persistence mechanism |
| T1055 | Process Injection | Defense evasion, stealth operations |
| T1070.004 | File Deletion | Anti-forensics, evidence destruction |
| T1218.011 | Rundll32 | Defense evasion, proxy execution |
| T1087 | Account Discovery | Reconnaissance, pre-attack phase |
| T1560 | Archive Collected Data | Pre-exfiltration staging |

### ATT&CK Coverage Tracking

**Coverage Metrics:**
- Techniques with detections: Track existing coverage
- Techniques hunted: Track hunt execution history
- Detection gaps: Identify uncovered high-risk techniques
- Hunt frequency: Monthly, quarterly, annual by tier

**Navigator Layer Usage:**
- Baseline assessment: Mark techniques with existing detections
- Hunt planning: Annotate by hunt priority (Tier 1/2/3)
- Progress tracking: Update after each hunt completion
- Reporting: Export coverage matrices for leadership

## Essential Data Sources

### Endpoint Telemetry

| Data Type | Source | Key Events | Retention |
|-----------|--------|------------|-----------|
| **Process Execution** | EDR, Sysmon Event ID 1 | Process creation, command lines, parent-child | 90 days |
| **Network Connections** | EDR, Sysmon Event ID 3 | Destination IPs, ports, processes | 90 days |
| **File Operations** | EDR, Sysmon Event ID 11 | File writes, executables, documents | 90 days |
| **Registry Modifications** | EDR, Sysmon Event ID 12-14 | Persistence keys, configuration changes | 90 days |
| **Authentication** | Windows Event 4624/4625 | Logon/logoff, logon types, source IPs | 1 year |
| **PowerShell Activity** | Event ID 4103/4104 | Script block logging, module logging | 90 days |
| **WMI Activity** | Sysmon Event ID 19-21 | WMI consumers, filters, bindings | 90 days |
| **DNS Queries** | EDR, Sysmon Event ID 22 | Domain lookups, query types | 30 days |

### Network Data

| Data Type | Source | Key Fields | Use Case |
|-----------|--------|------------|----------|
| **Netflow/IPFIX** | Network devices | Source/dest IP, ports, protocols, bytes | Traffic analysis, beaconing |
| **IDS/IPS Alerts** | Snort, Suricata | Alert signatures, payloads, metadata | Known threat detection |
| **Proxy Logs** | Web proxy, CASB | URLs, user agents, HTTP methods | Web-based threats, C2 |
| **Firewall Logs** | Next-gen firewalls | Allow/deny, applications, users | Perimeter analysis |
| **DNS Logs** | DNS servers, resolvers | Queries, responses, query types | C2, tunneling, DGA detection |

### Cloud and Identity

| Data Type | Source | Key Events | Use Case |
|-----------|--------|------------|----------|
| **Cloud API Calls** | AWS CloudTrail, Azure Activity | API calls, authentication, changes | Cloud infrastructure attacks |
| **Identity Events** | Azure AD, Active Directory | Authentication, MFA, password changes | Account compromise |
| **SaaS Activity** | CASB, SaaS audit logs | File access, sharing, downloads | Cloud data exfiltration |

## Hunt Techniques and Query Examples

### IOC-Based Hunt: File Hash Search

```sql
-- Search for malicious file hashes across endpoints (Splunk)
index=edr sourcetype=process_execution
| search hash IN ("a1b2c3d4e5f6...", "f6e5d4c3b2a1...", "...")
| stats count by host, hash, process_name, process_path, user
| lookup asset_inventory host OUTPUT criticality
| where count > 0
```

### TTP-Based Hunt: T1003.001 LSASS Credential Dumping

```sql
-- Detect processes accessing LSASS memory (Splunk/Sysmon)
index=sysmon EventCode=10
| where TargetImage="C:\\Windows\\System32\\lsass.exe"
| where GrantedAccess IN ("0x1010", "0x1410", "0x1438", "0x143a", "0x1fffff")
| lookup process_whitelist SourceImage OUTPUT is_whitelisted
| where is_whitelisted!=1
| stats count by ComputerName, SourceImage, SourceCommandLine, SourceUser

-- Detect MiniDump via comsvcs.dll (Splunk/Sysmon)
index=sysmon EventCode=1
| where Image="*\\rundll32.exe"
| where CommandLine="*comsvcs.dll*MiniDump*"
| table _time, ComputerName, User, CommandLine, ParentImage
```

### TTP-Based Hunt: T1059.001 PowerShell Abuse

```sql
-- Detect encoded PowerShell commands (KQL/Microsoft Defender)
DeviceProcessEvents
| where ProcessCommandLine has_any ("-enc", "-EncodedCommand", "FromBase64String")
| extend DecodedCommand = base64_decode_tostring(extract(@"-enc(?:odedCommand)?\s+(\S+)", 1, ProcessCommandLine))
| project Timestamp, DeviceName, AccountName, FileName, ProcessCommandLine, DecodedCommand

-- Detect PowerShell download cradles (Splunk/PowerShell logs)
index=powershell EventCode=4104
| where ScriptBlockText="*Net.WebClient*" OR ScriptBlockText="*DownloadString*"
  OR ScriptBlockText="*Invoke-WebRequest*" OR ScriptBlockText="*IEX*"
| table _time, ComputerName, User, ScriptBlockText
```

### Anomaly-Based Hunt: Rare Process Execution

```sql
-- Find processes executed <5 times in 90 days (Splunk)
index=edr sourcetype=process_execution earliest=-90d
| stats count dc(host) as unique_hosts by process_name, process_hash
| where count < 5
| lookup virustotal_api process_hash OUTPUT vt_detections
| where vt_detections > 0 OR isnull(vt_detections)
| join process_hash [search index=edr earliest=-7d]
| table _time, host, process_name, process_hash, count, vt_detections
```

### Stack Counting: Rare User-Agents

```sql
-- Identify uncommon user-agents (Splunk/Proxy logs)
index=proxy earliest=-30d
| stats count by user_agent
| sort count
| head 50
| join user_agent [search index=proxy earliest=-24h
  | stats values(src_ip) as source_ips, values(dest_domain) as domains by user_agent]
| table user_agent, count, source_ips, domains
```

## Hunting Tools and Platforms

### SIEM Platforms

| Platform | Query Language | Strengths | Use Case |
|----------|---------------|-----------|----------|
| **Splunk** | SPL | Powerful analytics, large-scale data | Historical analysis, correlation |
| **Microsoft Sentinel** | KQL | Azure integration, built-in hunts | Cloud-focused hunts, Azure AD |
| **Elastic Stack** | EQL, KQL | Open-source, scalable | Cost-effective hunting |
| **QRadar** | AQL | Strong correlation engine | Network-focused hunts |

### EDR Platforms

| Platform | Strengths | Hunt Capabilities |
|----------|-----------|-------------------|
| **CrowdStrike Falcon** | Behavioral IOAs, threat graph | Process analysis, fileless malware |
| **Microsoft Defender** | Windows integration, KQL | Windows hunts, threat analytics |
| **SentinelOne** | Autonomous response, deep visibility | Active hunting, automated remediation |
| **Carbon Black** | Deep endpoint data, live response | Forensic investigations, binary analysis |

### Open-Source Hunting Tools

| Tool | Purpose | Use Case |
|------|---------|----------|
| **Velociraptor** | Endpoint forensics, artifact collection | Live response, hunt deployments |
| **OSQuery** | SQL-based endpoint querying | Cross-platform endpoint state queries |
| **Sigma** | Generic signature format | Portable detection rules across SIEMs |
| **YARA** | Pattern matching for malware | File-based IOC hunting, memory scanning |
| **Zeek** | Network protocol analysis | C2 detection, protocol anomalies |
| **Chainsaw** | Windows event log analysis | Fast EVTX searching |
| **RITA** | Beacon detection | C2 beaconing analysis from Zeek logs |

## Finding Validation Process

### Validation Workflow

```
INITIAL FINDING → TRIAGE → ENRICHMENT → ANALYSIS → CLASSIFICATION → ESCALATION
```

### Classification Criteria

**True Positive (TP):**
- Activity confirmed malicious or unauthorized
- Clear policy violation or abnormal behavior
- Matches known threat patterns with high confidence
- Multiple corroborating indicators

**False Positive (FP):**
- Legitimate business activity
- Authorized change or maintenance
- Known system behavior
- Resolved through context

**Benign True Positive (BTP):**
- Detects actual behavior (not FP)
- Behavior is authorized/legitimate
- Example: Security testing, approved scanning

**Inconclusive:**
- Insufficient data for determination
- Requires additional investigation
- Subject matter expert consultation needed

### Validation Techniques

**Timeline Analysis:**
- Reconstruct event sequences
- Expand time windows (-6 hours before, +6 hours after)
- Identify cause-and-effect patterns
- Distinguish attack chains from isolated events

**Pivot Analysis:**
- IP Address → Other IPs, domains, infrastructure
- User Account → Systems accessed, files touched
- File Hash → Other hashes, malware family
- Process → Parent/child processes, network connections
- Domain → IP resolutions, certificates, WHOIS

**Multi-Source Corroboration:**
- Validate with independent data sources
- Cross-reference EDR, network, authentication logs
- Enrich with threat intelligence
- Consult subject matter experts

## Incident Handoff Requirements

### Handoff Package Elements

| Element | Description | Format |
|---------|-------------|--------|
| **Executive Summary** | High-level finding overview | 1-paragraph summary |
| **Technical Details** | IOCs, TTPs, affected systems | Structured tables |
| **Evidence Package** | Logs, screenshots, forensic artifacts | Organized files |
| **Timeline** | Chronological event sequence | Visual timeline |
| **Impact Assessment** | Scope, severity, business impact | Risk matrix |
| **Remediation Guidance** | Containment, eradication, recovery steps | Prioritized checklist |
| **Detection Artifacts** | IOCs, YARA rules, Sigma rules | Machine-readable |

### IOC Formats

**File-Based IOCs:**
- SHA256, SHA1, MD5 hashes
- File paths and names
- File sizes and timestamps

**Network-Based IOCs:**
- IP addresses and ports
- Domain names and URLs
- SSL/TLS certificate fingerprints
- User-agent strings

**Host-Based IOCs:**
- Registry keys and values
- Service names
- Scheduled task names
- User accounts (unauthorized)
- Process names and command lines

**Behavioral IOCs:**
- Process parent-child relationships
- Network connection patterns
- File operation sequences
- Authentication anomalies

### Remediation Prioritization

**Immediate Actions (0-4 hours):**
- Containment: Isolate compromised systems
- Credential protection: Disable compromised accounts
- Perimeter blocking: Block C2 infrastructure
- Evidence preservation: Capture memory, extend log retention

**Short-Term Actions (24-72 hours):**
- Eradication: Remove malware, eliminate persistence
- Validation: Confirm removal, verify no re-infection
- Credential reset: Reset compromised credentials

**Long-Term Actions (1-4 weeks):**
- Root cause remediation: Patch vulnerabilities, harden configs
- Detection deployment: Operationalize hunt findings
- After-action review: Document lessons learned

## Hunt Metrics and KPIs

### Activity Metrics

| Metric | Target | Purpose |
|--------|--------|---------|
| **Hunts Completed** | 12-24 per year | Measure program activity |
| **ATT&CK Techniques Hunted** | 30-50 annually | Ensure broad coverage |
| **Hunt Hours Invested** | 40-80 per hunt | Resource planning |

### Effectiveness Metrics

| Metric | Calculation | Target |
|--------|------------|--------|
| **True Positive Rate** | TPs / Total Findings | >30% |
| **False Positive Rate** | FPs / Total Findings | <60% |
| **Detections Created** | New rules per hunt | 2-5 per hunt |
| **Incidents Identified** | Hunts finding threats | 2-4 per year |

### Coverage Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **ATT&CK Coverage** | Techniques with detections | Progressive increase |
| **Asset Coverage** | Critical assets hunted | 100% |
| **Data Source Utilization** | Sources queried per hunt | All available |

## Hunt Documentation Templates

### Hunt Plan Structure

```markdown
# Threat Hunt Plan: [Name]

## Hunt Metadata
- Hunt ID: TH-2026-XXX
- Hunter: [Name]
- Date Planned: YYYY-MM-DD
- Hunt Type: [IOC/TTP/Anomaly/Campaign]

## Hypothesis
[Clear, testable hypothesis statement]

## MITRE ATT&CK Mapping
- Tactics: [List]
- Techniques: [T####.### - Name]

## Data Sources
- Primary: [Main sources]
- Secondary: [Supporting sources]

## Hunt Queries
[Platform-specific queries]

## Success Criteria
- True Positive: [What confirms threat]
- False Positive: [What disproves threat]
```

### Hunt Report Structure

```markdown
# Threat Hunt Report: [Name]

## Executive Summary
[2-3 paragraph summary]

## Hypothesis Result
[Confirmed / Refuted / Partially Confirmed / Inconclusive]

## Findings
### Finding 1: [Title]
- Severity: [Critical/High/Medium/Low]
- Confidence: [High/Medium/Low]
- Evidence: [Description]
- Recommendations: [Actions]

## Detections Created
[New SIEM rules, EDR policies, Sigma rules]

## Lessons Learned
- What worked well
- What could improve
- Process improvements
```

## Continuous Improvement Process

### Monthly Hunt Retrospective

**Agenda:**
1. Review completed hunts (findings, outcomes, challenges)
2. Metrics review (TP rate, detections created, coverage)
3. Process improvements (tools, techniques, documentation)
4. Next month planning (hunt priorities, resource allocation)

### Quarterly Program Review

**Stakeholders:**
- CISO / Security Director
- SOC Manager
- Hunt Team Lead
- Detection Engineering Lead

**Topics:**
- Program metrics and effectiveness
- Key findings and impact
- Maturity progression
- Strategic direction and priorities

### Annual Strategic Planning

**Objectives:**
- Maturity advancement (HMM level progression)
- ATT&CK coverage expansion
- Hunt efficiency improvements
- Tool and platform enhancements
- Team training and development

## Hunt Playbook Development

Develop reusable playbooks for common TTPs:

**Playbook Elements:**
- MITRE ATT&CK mapping
- Data sources required
- Hunt queries (SIEM, EDR, network)
- Expected indicators and false positives
- Validation checklist
- Escalation criteria
- Historical results tracking

**Playbook Examples:**
- HP-001: LSASS Credential Dumping (T1003.001)
- HP-002: PowerShell Abuse (T1059.001)
- HP-003: Lateral Movement via RDP (T1021.001)
- HP-004: Scheduled Task Persistence (T1053.005)
- HP-005: DNS Tunneling C2 (T1071.004)

## Related Resources

- **Source SOP**: `/home/ubuntu/TinyHive-sops/cybersecurity/threat_hunting_sop.md`
- **MITRE ATT&CK**: https://attack.mitre.org/
- **Hunting Maturity Model**: David Bianco's HMM framework
- **SANS FOR508**: Advanced Incident Response, Threat Hunting, and Digital Forensics
- **ThreatHunting.net**: Free threat hunting resources
- **Sigma HQ**: https://github.com/SigmaHQ/sigma
- **Velociraptor**: https://docs.velociraptor.app/

## Integration with Other Consultants

### Collaborative Workflows

**Threat Intel Manager** (`consultants/threat_intel_manager`):
- Receives IOCs and threat intelligence for hunt hypothesis development
- Validates hunt findings against TI feeds
- Shares hunt-discovered IOCs for TIP ingestion

**SOC Analyst** (`consultants/soc_analyst`):
- Receives hunt-based detection rules for SIEM deployment
- Escalates suspicious alerts for hunt investigation
- Validates hunt findings during triage

**Incident Response Lead** (`consultants/incident_response_lead`):
- Receives validated hunt findings requiring incident response
- Provides post-incident IOCs/TTPs for future hunts
- Collaborates on after-action reviews

**Detection Engineer** (if available):
- Receives hunt findings for detection rule development
- Optimizes hunt queries for production alerting
- Tracks ATT&CK coverage jointly

**SOC Operations Manager** (`consultants/soc_operations_manager`):
- Prioritizes hunt targets based on strategic direction
- Reviews hunt program metrics and maturity
- Allocates resources for hunt operations

---

**Document Version**: 1.0
**Last Updated**: 2026-03-14
**Maintained By**: Threat Hunting Team
