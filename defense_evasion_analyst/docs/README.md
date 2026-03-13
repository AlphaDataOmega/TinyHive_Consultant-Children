# Defense Evasion Analyst Documentation

## Overview

This documentation provides comprehensive guidance for detecting, responding to, and recovering from Defense Evasion attacks as defined by MITRE ATT&CK Tactic TA0005.

## Covered Techniques

| Technique | MITRE ID | Description |
|-----------|----------|-------------|
| Disabling Security Software | T1562.001 | Tampering with AV/EDR to prevent detection |
| Install Root Certificate | T1553.004 | Installing malicious certificates for trust abuse |
| Process Injection | T1055 | Injecting code into legitimate processes |
| Obfuscated Files or Information | T1027 | Encoding/encrypting payloads to evade detection |
| Indirect Command Execution | T1202 | Using trusted binaries to execute commands |
| Subvert Trust Controls | T1553 | Bypassing code signing and trust mechanisms |
| Domain Policy Modification | T1484 | Modifying GPO for persistence/privilege |
| Impair Defenses | T1562 | Disabling security monitoring and controls |

## Detection Indicators

### Common Indicators
- Unusual DNS activity
- Antivirus/Endpoint alerts
- IDS/IPS alerts
- Unusual absence of logs from security software
- Firewall, IDS, IPS, and SIEM anomalies

### Process Injection Detection (T1055)
Monitor Windows API calls:
- CreateRemoteThread
- SuspendThread / SetThreadContext / ResumeThread
- QueueUserAPC / NtQueueApcThread
- VirtualAllocEx
- WriteProcessMemory

Linux-specific:
- Monitor ptrace system calls
- Utilize Yama security module for access control

### Obfuscation Detection (T1027)
- File-based detection (signatures, packers)
- Heuristic-based detection (suspicious patterns)
- Network-based detection (NIDS, email gateway)
- Behavior-based detection (runtime analysis)
- Reputation-based detection (threat intelligence)

### Certificate Abuse Detection (T1553.004)
- Enumerate root certificates periodically
- Compare against known-good baseline
- Monitor for unexpected certificate installations
- Check Autoruns with Microsoft/Windows entries visible

## Response Framework

### Containment Actions
1. Inventory all affected assets and technologies
2. Apply D6 Framework: Detect | Deny | Disrupt | Degrade | Deceive | Destroy
3. Apply OODA Loop: Observe -> Orient -> Decide -> Act
4. Issue perimeter enforcement for threat actor locations
5. Disconnect affected systems from network

### Evidence Preservation
- Archive IP addresses, user agents, and requests
- Determine attack source and pathway
- Create forensic backups before eradication

### Technique-Specific Response

| Technique | Primary Response |
|-----------|------------------|
| T1562.001 | Restore AV, scan all systems |
| T1553.004 | Remove cert, enumerate all systems |
| T1055 | EDR kill agent, forensic backup |
| T1027 | Multi-layer detection analysis |
| T1202 | Audit command execution capabilities |
| T1553 | Application control enforcement |
| T1484 | GPO permissions audit |
| T1562 | Permissions hardening |

## Eradication Steps

### Standard Eradication
1. Close attack vector via preparation steps
2. Patch asset vulnerabilities
3. Perform endpoint/AV scans
4. Reset compromised passwords
5. Review logs of impacted assets

### Extended Eradication (Advanced Techniques)
1. Create forensic backups
2. Inspect all assets for IOCs
3. Validate backups before recovery

## Recovery Objectives

1. Restore to RPO within RTO
2. Assess collateral damage
3. Determine root cause
4. Resolve related incidents
5. Restore from clean backup

## External Resources

- [MITRE ATT&CK - Defense Evasion](https://attack.mitre.org/tactics/TA0005/)
- [Process Injection Techniques](https://attack.mitre.org/techniques/T1055/)
- [Yama Security Module](https://www.kernel.org/doc/html/latest/adminguide/LSM/Yama.html)
- [Code Signing Certificate Attacks](https://posts.specterops.io/code-signing-certificate-cloning-attacks-and-defenses-6f98657fc6ec)
- [GuardSight GSVSOC IRP](https://github.com/guardsight/gsvsoc_cybersecurity-incident-response-plan)

## Quick Reference Matrix

| Technique | Key Detection | Primary Tool |
|-----------|---------------|--------------|
| Security Software Disable | Missing logs | SIEM correlation |
| Root Certificate Install | Cert enumeration | Group Policy |
| Process Injection | API monitoring | EDR/Sysmon |
| Obfuscation | Multi-layer scan | AV/Sandbox |
| Indirect Execution | Process creation | Sysmon |
| Trust Subversion | Autoruns | Application control |
| Domain Policy Mod | GPO monitoring | AD audit logs |
| Impair Defenses | Registry/FW changes | Host monitoring |
