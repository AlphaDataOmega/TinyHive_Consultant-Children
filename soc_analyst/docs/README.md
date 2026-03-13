# SOC Analyst Documentation

This directory contains reference materials for SOC operations, detection engineering, and threat intelligence management.

## Core Competency Areas

### SOC Operations
- Security Operations Center fundamentals and mission
- SOC vs CSIRT activity delineation
- Team organization (functional teams vs L1/L2/L3 tiering)
- 24x7 operations and shift management
- RACI matrix development

### Detection Engineering
- PDCA approach to detection development
- TTP detection prioritization using MITRE ATT&CK
- Detection use case categories:
  - XDR-like correlation (EDR + CASB/NDR/proxy/identity)
  - Threat intel-based IOC matching
  - Unblocked infection vector detection
  - Persistence and bypass detection
  - Authentication attack detection (bruteforce, credential compromise, lateral movement)
  - C&C activity and DNS beaconing
  - Obfuscated script detection
- Detection-as-code with CI/CD pipelines

### Threat Intelligence
- Intelligence lifecycle (planning, collection, processing, analysis, dissemination)
- TIP platform selection (MISP, OpenCTI, commercial options)
- Intelligence source management (commercial feeds, community feeds, OSINT)
- Automation for collection, detection, and response

### SOAR Implementation
- SIRP, TIP, and SOA integration
- Detection automation use cases (enrichment, correlation, IOC lookup)
- Response automation use cases (blocking, containment, reporting)
- Automation tooling and platforms

### Metrics and KPIs
- SOC/CSIRT KPIs (alert volume, verification rates, handling times)
- Compliance KPIs (endpoint coverage, MFA coverage, training completion)
- SLAs (MTTH, MTTT, MTTC, MTTR)
- Detection quality assessment through purple teaming

## Key Frameworks and Standards

- **NIST SP800-61 rev2** — Incident response lifecycle
- **MITRE ATT&CK** — Adversary tactics, techniques, and procedures
- **MITRE D3FEND** — Defensive techniques
- **SOC-CMM** — SOC capability maturity model
- **SIM3** — Security incident management maturity model
- **SIGMA** — Generic signature format for SIEM systems
- **FIRST CSIRT Services Framework** — CSIRT capability categories

## Training Resources

### Free Training Paths
- PaloAlto Fundamentals of SOC
- LetsDefend SOC Fundamentals
- Microsoft Sentinel Ninja
- Splunk free training courses
- CrowdSec Cybersecurity Fundamentals

### Challenge Platforms
- BlueTeamLabs
- CyberDefenders
- SOC Vel
- Malware Traffic Analysis

### Certifications
- GIAC GCIH, GCIA
- SANS SEC450, SEC501, SEC555
- Splunk Certified Cyberdefense Analyst
- OffensiveSecurity OSDA

## Assessment Tools

- **SOC Assessment:** Google SecOps Assessment, SOC-CMM Self-Assessment
- **CSIRT Assessment:** OpenCSIRT SIM3, ENISA Cybersecurity Maturity Framework
- **Detection Assessment:** Atomic Red Team, CTID Adversary Emulation Library, Vectr

## Reference Documentation

This agent should maintain familiarity with:
- Detection strategy documents with ATT&CK mapping
- Detection matrices showing coverage by sensor
- Standard operating procedures for alert handling
- Audit policies defining logging requirements
- RACI matrices for SOC/CSIRT responsibilities
