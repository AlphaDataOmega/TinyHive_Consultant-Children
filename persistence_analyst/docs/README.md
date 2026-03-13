# Persistence Analyst Documentation

## Overview

The Persistence Analyst specializes in detecting and responding to adversary persistence mechanisms as defined by MITRE ATT&CK Tactic TA0003. This role focuses on identifying how attackers maintain access to compromised systems across restarts, credential changes, and other interruptions.

## Core Competencies

### MITRE ATT&CK Persistence Techniques

| Technique ID | Technique Name | Key Detection Points |
|-------------|----------------|---------------------|
| T1053 | Scheduled Task/Job | Event ID 4698-4702, cron directories, systemd timers |
| T1505.003 | Web Shell | WAF alerts, FIM, web server logs, file analysis |
| T1547 | Boot or Logon Autostart Execution | Registry Run keys, startup folders, login scripts |
| T1098 | Account Manipulation | Privilege changes, group modifications, SSH keys |
| T1136 | Create Account | Event ID 4720, useradd logs, AD account creation |
| T1543 | Create or Modify System Process | Service installations, systemd unit changes |
| T1546 | Event Triggered Execution | WMI subscriptions, trap commands, accessibility features |

## Detection Methods

### Scheduled Tasks Detection

**Windows Systems:**
- Event ID 4698: A scheduled task was created
- Event ID 4699: A scheduled task was deleted
- Event ID 4700: A scheduled task was enabled
- Event ID 4701: A scheduled task was disabled
- Event ID 4702: A scheduled task was updated

**Linux Systems:**
- Monitor `/var/spool/cron/` directory changes
- Monitor `/etc/cron.d/` and `/etc/crontab` modifications
- systemd timer units in `/etc/systemd/system/`
- at job queue monitoring

### Web Shell Detection

**Indicators to Monitor:**
- Unusual POST requests to static pages
- Unexpected file changes in web directories
- IPS/IDS alerts for web shell signatures
- Anomalous parent-child process relationships (web server spawning cmd/PowerShell)
- Files with encoded/obfuscated content (eval(), base64_decode, shell_exec)

### Registry and Service Monitoring

**Key Registry Locations:**
```
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\System\CurrentControlSet\Services
```

## Incident Response Procedures

### Response Phases

1. **Investigation** — Scope assessment, IOC gathering, severity determination
2. **Containment** — Account lockdown, mechanism disablement, network isolation
3. **Eradication** — Remove artifacts, patch vulnerabilities, credential rotation
4. **Recovery** — System restoration, enhanced monitoring, lessons learned

### Containment Decision Matrix

| Persistence Type | Isolate System | Disable Mechanism | Block Network | Priority |
|-----------------|----------------|-------------------|---------------|----------|
| Scheduled Task (Admin) | Yes | Immediate | Yes | Critical |
| Scheduled Task (User) | Monitor | Immediate | Optional | High |
| Web Shell | Yes | Immediate | Yes | Critical |
| Registry Autorun | Monitor | Immediate | Optional | High |
| Service/Daemon | Yes | Immediate | Yes | Critical |
| Account-based | N/A | Lock Account | Yes | Critical |

### Severity Determination

| Factor | Low | Medium | High | Critical |
|--------|-----|--------|------|----------|
| Affected Assets | 1-2 systems | 3-10 systems | 11-50 systems | 50+ or critical |
| User Compromise | Standard user | Privileged user | Admin account | Domain admin |
| Data at Risk | Non-sensitive | Internal data | PII/Financial | IP/Critical |

## Tools and Resources

### Detection Tools

| Tool | Purpose | Platform |
|------|---------|----------|
| Sysmon | Advanced Windows logging | Windows |
| osquery | Endpoint visibility | Cross-platform |
| YARA | Pattern matching | Cross-platform |
| Autoruns | Autostart enumeration | Windows |
| chkrootkit | Rootkit detection | Linux |
| rkhunter | Rootkit detection | Linux |

### Response Tools

| Tool | Purpose |
|------|---------|
| Velociraptor | Endpoint investigation |
| GRR | Remote forensics |
| TheHive | Case management |
| MISP | Threat intelligence |

## Reference Links

- [MITRE ATT&CK Persistence Tactic](https://attack.mitre.org/tactics/TA0003/)
- [MITRE T1053 - Scheduled Task/Job](https://attack.mitre.org/techniques/T1053/)
- [MITRE T1505.003 - Web Shell](https://attack.mitre.org/techniques/T1505/003/)
- [CISA Web Shell Detection Advisory](https://www.cisa.gov/news-events/cybersecurity-advisories)

## Escalation Criteria

Escalate to management immediately if:
- Domain admin or equivalent access compromised
- Critical business systems affected
- Data exfiltration confirmed or suspected
- Attacker demonstrates ongoing access
- Persistence mechanism affects >10 systems
- Known APT indicators identified

## Evidence Collection Checklist

- [ ] Memory dump of affected systems
- [ ] Disk image or targeted collection
- [ ] Network traffic captures
- [ ] Log files (system, application, security)
- [ ] Malware samples (quarantined)
- [ ] Configuration files
- [ ] Timeline of events
