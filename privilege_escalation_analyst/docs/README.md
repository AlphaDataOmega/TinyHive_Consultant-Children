# Privilege Escalation Analyst Documentation

## Overview

This directory contains reference materials and procedures for privilege escalation incident response.

## MITRE ATT&CK Coverage (TA0004 - Privilege Escalation)

| Technique ID | Technique Name | Platforms |
|-------------|----------------|-----------|
| T1134 | Access Token Manipulation | Windows |
| T1484.001 | Group Policy Modification | Windows |
| T1548 | Abuse Elevation Control Mechanism | Linux, Windows, macOS |
| T1548.001 | Setuid and Setgid | Linux, macOS |
| T1548.002 | Bypass User Account Control | Windows |
| T1548.003 | Sudo and Sudo Caching | Linux, macOS |
| T1548.004 | Elevated Execution with Prompt | macOS |
| T1055 | Process Injection | Linux, Windows, macOS |

## Required Tools

| Tool Category | Required Tools |
|---------------|----------------|
| SIEM/Log Analysis | Splunk, Elastic SIEM, Microsoft Sentinel |
| EDR Solutions | CrowdStrike, Microsoft Defender ATP, Carbon Black |
| Forensic Tools | Volatility, Velociraptor, KAPE, FTK |
| Network Analysis | Wireshark, Zeek, Network TAPs |
| Credential Analysis | Mimikatz detection tools, token analysis utilities |
| Policy Management | Group Policy Management Console (GPMC) |

## Detection Indicators

### Windows Event IDs to Monitor

| Event ID | Description |
|----------|-------------|
| 4672 | Special privileges assigned to new logon |
| 4673 | A privileged service was called |
| 4674 | An operation was attempted on a privileged object |
| 4688 | A new process has been created (with command line logging) |
| 5136 | Directory Service object modification (GPO changes) |
| 5137 | Directory Service object creation |

### Windows API Calls (Process Injection)

- CreateRemoteThread
- SuspendThread
- SetThreadContext
- ResumeThread
- QueueUserAPC
- NtQueueApcThread
- VirtualAllocEx
- WriteProcessMemory

### Linux/Unix Key Log Files

| Log File | Purpose |
|----------|---------|
| /var/log/auth.log | Authentication and sudo events |
| /var/log/secure | Security events (RHEL/CentOS) |
| /var/log/audit/audit.log | SELinux and auditd events |
| /var/log/syslog | General system events |

## Immediate Response Checklist

```
[ ] 1. Validate alert - confirm privilege escalation
[ ] 2. Identify technique (Token Manipulation/GPO/Elevation Bypass/etc.)
[ ] 3. Lock compromised accounts
[ ] 4. Isolate affected systems
[ ] 5. Preserve evidence (memory, logs, artifacts)
[ ] 6. Notify IR Lead
[ ] 7. Begin investigation
[ ] 8. Document all actions
```

## Escalation Criteria

| Severity | Criteria | Response Time |
|----------|----------|---------------|
| Critical | Admin/root compromise, Domain admin access | Immediate |
| High | Service account compromise, Multiple systems | 15 minutes |
| Medium | Single user privilege escalation, Limited scope | 1 hour |
| Low | Failed privilege escalation attempt | 4 hours |

## Containment Priority Actions

| Priority | Action | Timeframe |
|----------|--------|-----------|
| Critical | Lock compromised user accounts | Immediate |
| Critical | Remove affected systems from the network | Within 15 minutes |
| High | Disable compromised service accounts | Within 30 minutes |
| High | Revoke elevated access tokens | Within 30 minutes |
| Medium | Block known attacker IPs at perimeter | Within 1 hour |
| Medium | Disable suspicious scheduled tasks/services | Within 1 hour |

## Evidence Collection Commands

### Windows

```powershell
# Collect running processes with tokens
Get-Process | Select-Object Name, Id, @{n='Token';e={$_.Handle}}

# Review scheduled tasks
Get-ScheduledTask | Where-Object {$_.State -ne 'Disabled'}

# Check for UAC bypass indicators
reg query "HKEY_CURRENT_USER\Software\Classes\ms-settings\shell\open\command"

# Review GPO changes
Get-GPO -All | Where-Object {$_.ModificationTime -gt (Get-Date).AddDays(-7)}

# Check for token manipulation artifacts
Get-WinEvent -FilterHashtable @{LogName='Security';ID=4672,4673,4674} -MaxEvents 100
```

### Linux/Unix

```bash
# Find setuid/setgid binaries
find / -type f \( -perm -4000 -o -perm -2000 \) -ls 2>/dev/null

# Review sudo history
grep -i sudo /var/log/auth.log | tail -100

# Check for process injection (ptrace)
grep -i ptrace /var/log/audit/audit.log

# Review cron jobs for persistence
crontab -l && ls -la /etc/cron.*

# Check sudoers file modifications
ls -la /etc/sudoers /etc/sudoers.d/
```

## Related SOPs

- Privilege Escalation Incident Response SOP
- Credential Compromise Incident Response SOP
- Lateral Movement Incident Response SOP
- Malware Incident Response SOP

## External References

- [MITRE ATT&CK TA0004 - Privilege Escalation](https://attack.mitre.org/tactics/TA0004/)
- [Atomic Red Team Testing - T1548](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1548.001/T1548.001.md)
- NIST SP 800-61 Rev. 2 - Computer Security Incident Handling Guide
- SANS Incident Handler's Handbook
