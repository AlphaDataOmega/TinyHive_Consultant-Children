# SOC Operations Manager Documentation

## Overview

This documentation supports the SOC Operations Manager consultant agent, providing comprehensive guidance for Security Operations Center management, detection engineering, SOAR implementation, threat intelligence, metrics, and team development.

## Core Knowledge Domains

### 1. SOC Fundamentals

**SOC Definition:** A centralized unit combining people, processes, and technology to continuously monitor and improve an organization's security posture while preventing, detecting, analyzing, and responding to cybersecurity incidents.

**SOC vs CSIRT Activities:**

| SOC Core Services | CSIRT Core Services |
|-------------------|---------------------|
| Security monitoring and alerting | Incident coordination and management |
| Log management and analysis | Forensic analysis |
| Threat detection and triage | Malware analysis |
| Initial incident response | Threat hunting |
| Security tool management | Post-incident review |
| Compliance monitoring | Stakeholder communication |

**Technology Stack Components:**
- **SIEM:** Security Information and Event Management
- **SIRP:** Security Incident Response Platform
- **TIP:** Threat Intelligence Platform
- **SOA:** Security Orchestration and Automation
- **EDR/XDR:** Endpoint/Extended Detection and Response
- **NDR:** Network Detection and Response

### 2. SOC Organization and Structure

**Recommended Function-Based Team Structure:**

1. **Security Monitoring Team** — Primary detection and triage, initial incident response, fully autonomous operations
2. **Security Monitoring Engineering Team** — SIEM rule development, SOA playbook creation, reporting and metrics, uncommon use case handling
3. **Build/Project Management Team** — Tool integration, SIEM data ingestion, DevSecOps tasks, project management

**Key Roles:**
- SOC Analyst / SOC Analyst Lead
- Detection Engineer
- Threat Intel Analyst
- SIEM Expert / Data Scientist
- Incident Handler / Incident Manager
- SOC/CSIRT Manager

**24x7 Operations Models:**
- **On-call:** Pre-validated alert types with maximum severity only
- **True 24x7:** Consistent quality of service regardless of time
- Geographic distribution for follow-the-sun model

### 3. Detection Engineering

**PDCA Methodology:**

| Phase | Activities |
|-------|------------|
| **Plan** | Identify detection gaps, plan sensor deployment, schedule rule development |
| **Do** | Ingest logs, create detection rules, implement playbooks, document SOPs |
| **Check** | Validate data compliance, test automations, purple team assessments |
| **Act** | Fix issues, implement improvements |

**Top TTPs for Ransomware (MITRE ATT&CK):**
1. T1486: Data Encrypted for Impact
2. T1490: Inhibit System Recovery
3. T1027: Obfuscated Files or Information
4. T1047: Windows Management Instrumentation
5. T1036: Masquerading
6. T1059: Command and Scripting Interpreter
7. T1562: Impair Defenses
8. T1112: Modify Registry
9. T1204: User Execution
10. T1055: Process Injection

**Detection Use Case Categories:**
- XDR-like correlation (EDR + CASB/NDR/identity)
- Threat intel-based detections (IOC matching)
- Unblocked infection vector detection
- Persistence/bypass detection
- Impossible travel detection
- Successful bruteforce (T1110)
- Lateral movement (T1021.001)
- C2 activity (T1071.004)

**Detection-as-Code (DevSecOps):**
- SIEM rules in Git with YAML declarations
- SIEM apps/objects version controlled
- Audit policies (Sysmon XML, AuditD) in Git
- SOA playbooks version controlled
- SOPs/Wiki with Git integration

### 4. SOAR Implementation

**SOAR Components:**
1. **SIRP** — Security Incident Response Platform
2. **TIP** — Threat Intelligence Platform
3. **SOA** — Security Orchestration and Automation

**Detection Automation Use Cases:**
- Context enrichment (transfer alert context to SIRP)
- History retrieval (antimalware/SIEM/SIRP history)
- Asset enrichment (AD/asset management queries)

**Response Automation Use Cases:**
- Blocking actions (IP, URL, email sender, hash)
- Account actions (password reset, account disable)
- Reporting (vendor notifications, takedown requests)

**Recommended Tools:**
- Hash Checking: Munin, Posh-VT
- URL Analysis: CyberGordon, URLScan.io
- Sample Analysis: Malwoverview, Hybrid-Analysis, Joe's Sandbox
- Free SOA: Shuffle

### 5. Threat Intelligence Operations

**Intelligence Lifecycle:**
1. Planning & Direction
2. Collection
3. Processing & Exploitation
4. Analysis & Production
5. Dissemination & Integration

**Intelligence Types:**
- **Tactical:** IOCs, detection signatures
- **Operational:** TTPs, attack methods
- **Strategic:** Threat landscape, actor profiles

**TIP Recommendations:**
- Community/Open Source: MISP, OpenCTI
- Commercial: Sekoia.io, ThreatQuotient, Recorded Future

**Intelligence Sources:**
- Commercial feeds: ESET, Sekoia.io, Mandiant, Recorded Future
- Community feeds: URLHaus, Feodo Tracker, Malware Bazaar, ThreatFox
- Query portals: VirusTotal, AbuseIPDB, OTX AlienVault

### 6. Metrics and KPIs

**SOC/CSIRT KPIs:**

| Category | Metrics |
|----------|---------|
| Volume | SIEM alerts, verified alerts, top incident types |
| Quality | False positive rules, longest handling time rules, TTP coverage |
| Response Time | MTTH, MTTT, MTTC, MTTR |
| Operational | New rules deployed, playbooks deployed, purple team validations |

**Response Time Definitions:**
- **MTTH:** Mean Time to Handle (alert assignment)
- **MTTT:** Mean Time to Triage (alert verification)
- **MTTC:** Mean Time to Contain (initial response)
- **MTTR:** Mean Time to Remediate (full remediation)

**Compliance KPIs:**
- Endpoint security coverage percentage
- MFA coverage for critical applications
- Security training completion rate
- Phishing campaign metrics (report rate, click-through rate)

### 7. HR and Training Program

**Training Progression:**

**SOC Analyst Training:**
- Free: PaloAlto Fundamentals, LetsDefend, Cybrary MITRE ATT&CK
- Practice: BlueTeamLabs, CyberDefenders, SOC Vel
- SIEM-specific: Splunk certifications, Microsoft Sentinel Ninja

**CSIRT/Incident Response Training:**
- Free: FIRST Training, Malware Traffic Analysis, Hack The Box
- Paid: GIAC GCIH, SANS FOR508/FOR572/FOR578/FOR610

**Certification Roadmap:**

| Level | Certifications |
|-------|---------------|
| Entry | BTL1, CEH, vendor fundamentals |
| Intermediate | Splunk Power User, SC-200, OSDA |
| Advanced | SANS SEC555/SEC450/SEC541, CISSP |

**NICE Framework Alignment:**
- Cyber Defense Analyst = SOC Analyst
- Cyber Defense Infrastructure Support = Detection Engineer
- Incident Response Analyst = Incident Handler

### 8. AI and Machine Learning Integration

**ML Use Cases:**
- Network traffic anomaly detection
- Binary execution anomaly detection

**GenAI/LLM Use Cases:**
- Command line analysis (obfuscated commands)
- Registry key analysis
- CTI report summarization
- Attack understanding and response suggestions

**AI Security Considerations:**
- ENISA Multilayer Framework for AI Cybersecurity
- OWASP LLM and GenAI Security Best Practices
- NIST AI 600 guidelines

### 9. Maturity Assessment

**Assessment Tools:**
- Basic: Google SecOps Assessment
- Thorough: SOC-CMM Self-Assessment Tool
- CSIRT: OpenCSIRT SIM3 Self-Assessment

**Purple Team Frameworks:**
- RedCanary Atomic Red Team
- CTID Adversary Emulation Library

**Assessment Documentation:**
- Vectr for detection capability results
- ATT&CK Navigator for coverage visualization

## Reference Standards and Frameworks

- MITRE ATT&CK Enterprise Matrix
- MITRE D3FEND
- NIST SP800-61 (Incident Handling)
- NIST Cybersecurity Framework
- NIST 800-181 NICE Framework
- CIS 18 Critical Security Controls
- ISO 27035 (Incident Management)
- FIRST CSIRT Services Framework

## Essential Reading

- MITRE: 11 Strategies of a World-Class Cybersecurity Operations Center
- ENISA: Good Practice Guide for Incident Management
- FIRST: Building a SOC (Start Small)
- NCSC: Building a Security Operations Centre
- David Bianco: Pyramid of Pain

## Detection Engineering Resources

- Sigma HQ: https://github.com/SigmaHQ/sigma
- Splunk Security Content: https://research.splunk.com/
- Elastic Detection Rules: https://github.com/elastic/detection-rules
- SOC Prime: https://socprime.com/
- MITRE CAR: https://car.mitre.org/analytics/
