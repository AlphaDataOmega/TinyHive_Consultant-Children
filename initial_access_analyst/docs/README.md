# Initial Access Analyst Documentation

## Overview

This directory contains reference materials for the Initial Access Analyst consultant specializing in detecting and responding to adversary initial foothold techniques per MITRE ATT&CK framework.

## MITRE ATT&CK Coverage

### T1133 - External Remote Services

Adversaries leverage external-facing remote services to initially access and/or persist within a network. Remote services such as VPNs, Citrix, and other access mechanisms allow users to connect to internal enterprise network resources from external locations.

| Attribute | Details |
|-----------|---------|
| Tactic | Initial Access |
| Technique ID | T1133 |
| Platforms | Containers, Linux, Windows |
| Permissions Required | User |
| Data Sources | Application Log, Logon Session, Network Traffic |

### T1189 - Drive-By Compromise

Adversaries gain access to a system through a user visiting a website over the normal course of browsing. The user's web browser is typically the target of exploitation.

| Attribute | Details |
|-----------|---------|
| Tactic | Initial Access |
| Technique ID | T1189 |
| Platforms | Linux, SaaS, Windows, macOS |
| Permissions Required | User |
| Data Sources | Application Log, File, Network Traffic, Process |

## Detection Indicators

### External Remote Services (T1133)

| Indicator | Detection Method | Priority |
|-----------|------------------|----------|
| Multiple failed authentication attempts | SIEM correlation | High |
| Authentication from unusual geographic locations | GeoIP analysis | High |
| Authentication outside normal business hours | Time-based rules | Medium |
| Concurrent sessions from different locations | Session analysis | Critical |
| Authentication immediately after account creation | New account monitoring | High |

### Drive-By Compromise (T1189)

| Indicator | Detection Method | Priority |
|-----------|------------------|----------|
| Browser spawning suspicious processes | EDR process monitoring | Critical |
| Connection to known exploit kit domains | Threat intelligence | Critical |
| Unexpected DLL loading | EDR/Sysmon | High |
| PowerShell execution from browser | Process tree analysis | Critical |
| C2 beacon patterns | Network traffic analysis | Critical |

## Investigation Procedures

### T1133 Investigation Steps

1. **Alert Triage (15 minutes)**
   - Review source IP address and geolocation
   - Identify target system and service
   - Check user account involved
   - Classify: True Positive, Suspicious, or False Positive

2. **User Verification (30 minutes)**
   - Contact user through out-of-band communication
   - Verify recent activity and location
   - Document user response

3. **Technical Analysis (1-2 hours)**
   - Gather VPN, RADIUS, AD, and MFA logs
   - Analyze network traffic and source IP reputation
   - Review endpoint EDR telemetry

### T1189 Investigation Steps

1. **Initial Triage (15 minutes)**
   - Identify affected endpoint
   - Review triggering alert and malicious URL
   - Determine criticality based on user access

2. **Evidence Collection (30 minutes)**
   - Collect proxy/web logs with full URLs
   - Gather DNS query logs
   - Export endpoint telemetry

3. **Malware Analysis (1-2 hours)**
   - Identify payload delivery method and exploit kit
   - Submit suspicious files to sandbox
   - Extract IOCs (IPs, domains, hashes)

## Containment Strategies

### Network Containment

| Action | Authority |
|--------|-----------|
| Block IP at perimeter | SOC Analyst |
| DNS sinkhole domain | Network Security |
| Isolate subnet | Network Ops + IR Lead |
| Block user access | IR Lead approval |

### Endpoint Containment

1. Enable network isolation via EDR console
2. Disable compromised user account
3. Force password reset and revoke active sessions
4. Capture memory before any destructive actions

## Eradication Procedures

### T1133 Eradication

- Patch exploited vulnerability
- Reset all affected account passwords
- Regenerate MFA tokens
- Rotate service account credentials
- Audit and remove unauthorized access grants

### T1189 Eradication

- Terminate malicious processes
- Remove malicious files and registry entries
- Clean startup locations and scheduled tasks
- Block identified malicious URLs
- Consider reimaging for confirmed compromise

## Key Metrics

| Metric | Target |
|--------|--------|
| Mean Time to Detect (MTTD) | < 1 hour |
| Mean Time to Respond (MTTR) | < 4 hours |
| Mean Time to Recover | < 24 hours |
| False Positive Rate | < 10% |
| Recurrence Rate | 0% |

## Detection Rules Reference

### VPN Geographic Anomaly

```
RULE: VPN_Geographic_Anomaly
TRIGGER: VPN_Authentication_Success
CONDITION:
  - User authenticated from Country_A
  - AND User authenticated from Country_B within 2 hours
  - AND Distance between locations > 500 miles
  - AND Travel time impossible (< 4 hours flight)
ACTION: Create HIGH severity alert
```

### Browser Exploit Execution

```
RULE: Browser_Exploit_Execution
TRIGGER: Process_Creation
CONDITION:
  - Parent process = (chrome.exe OR firefox.exe OR msedge.exe OR iexplore.exe)
  - AND Child process = (cmd.exe OR powershell.exe OR wscript.exe OR mshta.exe)
ACTION: Create CRITICAL severity alert, isolate endpoint
```

## Known Exploit Kits

| Exploit Kit | Characteristics |
|-------------|-----------------|
| RIG | Obfuscated JavaScript, multiple redirects |
| Magnitude | Malvertising delivery, geo-targeting |
| Fallout | CVE-2018-8174, CVE-2018-15982 |
| Purple Fox | Drive-by + worm capabilities |

## Related SOPs

- SOP-SEC-INITACCESS-001: Initial Access Incident Response
- SOP-SEC-PHISH-001: Phishing Response
- SOP-SEC-MALWARE-001: Malware Response

## Evidence Collection Commands

### Windows

```powershell
# Memory capture
winpmem_mini_x64.exe memory.raw

# Process listing
Get-Process | Export-Csv processes.csv

# Network connections
Get-NetTCPConnection | Export-Csv connections.csv
```

### Linux

```bash
# Memory capture
sudo dd if=/dev/mem of=memory.raw

# Process listing
ps auxww > processes.txt

# Network connections
netstat -tulpn > connections.txt
```
