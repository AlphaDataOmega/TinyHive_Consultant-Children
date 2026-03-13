# Execution Analyst Documentation

## Overview

This directory contains reference documentation for the Execution Analyst role, specializing in MITRE ATT&CK Tactic TA0002 (Execution) detection and response.

## MITRE ATT&CK Coverage

### Primary Techniques

| Technique ID | Name | Description |
|--------------|------|-------------|
| T1059 | Command and Scripting Interpreter | Abuse of command/script interpreters |
| T1059.001 | PowerShell | PowerShell command execution |
| T1059.003 | Windows Command Shell | cmd.exe abuse |
| T1059.004 | Unix Shell | bash/sh/zsh abuse |
| T1059.005 | Visual Basic | VBScript/VBA execution |
| T1059.006 | Python | Python interpreter abuse |
| T1059.007 | JavaScript | JavaScript engine abuse |
| T1047 | Windows Management Instrumentation | WMI execution |
| T1053 | Scheduled Task/Job | Task-based execution |
| T1204 | User Execution | User-triggered execution |
| T1559 | Inter-Process Communication | IPC-based execution |
| T1106 | Native API | Direct API execution |
| T1569 | System Services | Service-based execution |
| T1203 | Exploitation for Client Execution | Client-side exploits |

## Detection Capabilities

### Log Sources

- Windows PowerShell Operational Log (Event ID 4103, 4104)
- Windows Security Log (Event ID 4688 - Process Creation)
- Sysmon Event ID 1 (Process Creation)
- Microsoft-Windows-PowerShell/Operational
- Linux syslog and auditd
- EDR telemetry

### Key Detection Patterns

#### PowerShell Red Flags
- `-enc` or `-EncodedCommand` parameters
- `IEX` or `Invoke-Expression` usage
- `DownloadString` or `DownloadFile` calls
- `-ExecutionPolicy Bypass` flags
- `-WindowStyle Hidden` execution
- `FromBase64String` decoding
- `New-Object Net.WebClient` instantiation

#### CMD.exe Red Flags
- Spawned by Office applications (WINWORD.EXE, EXCEL.EXE, outlook.exe)
- `certutil -urlcache` downloads
- `bitsadmin /transfer` operations
- `regsvr32 /s /n /u /i:URL` execution
- `mshta vbscript:` or `mshta javascript:` patterns

#### Unix Shell Red Flags
- Shells spawned by httpd, nginx, apache2, java
- `curl | bash` or `wget | sh` patterns
- Base64 decoded execution
- Reverse shell patterns
- Unauthorized cron modifications

## Investigation Procedures

### Initial Triage

1. **Alert Validation** - Review triggering indicators and affected hosts
2. **Context Gathering** - Collect hostname, username, timestamp, full command line, parent process
3. **Severity Assessment** - Evaluate based on command type, user context, network activity

### Severity Matrix

| Criteria | Low | Medium | High | Critical |
|----------|-----|--------|------|----------|
| Command Type | Known admin tool | Encoded command | Download cradle | Active C2 |
| User Context | Admin account | Standard user | Service account | SYSTEM |
| Network Activity | None | Internal only | External outbound | Active exfiltration |
| Persistence | None suspected | Possible | Confirmed | Multiple mechanisms |

### Evidence Collection Checklist

- [ ] Process creation logs (4688, Sysmon 1)
- [ ] PowerShell script block logs (4104)
- [ ] Network connection logs
- [ ] DNS query logs
- [ ] File system artifacts
- [ ] Memory dump (if active threat)
- [ ] Timeline of events

## Response Actions

### Containment by Severity

| Severity | Action |
|----------|--------|
| Low | Monitor, document, continue investigation |
| Medium | Isolate endpoint from network, preserve evidence |
| High | Network isolation, credential reset, block IOCs |
| Critical | Emergency containment, executive notification, IR team activation |

### Eradication Steps

1. Terminate identified malicious processes
2. Remove downloaded payloads and dropped scripts
3. Clean registry persistence (Run keys)
4. Remove malicious scheduled tasks
5. Clear staging directories (%TEMP%, %APPDATA%, /tmp)

## Prevention Controls

### PowerShell Hardening

| Control | Purpose |
|---------|---------|
| Script Block Logging | Full visibility into executed scripts |
| Constrained Language Mode | Restrict dangerous PowerShell features |
| AMSI | Real-time script content scanning |
| Execution Policy (AllSigned) | Require signed scripts |
| Remove PowerShell v2 | Eliminate downgrade attacks |
| Module Logging | Track module loading activity |

### Application Controls

- Implement AppLocker or WDAC
- Block execution from user-writable directories
- Restrict script interpreter execution paths

## Related Resources

- [MITRE ATT&CK Execution Tactic](https://attack.mitre.org/tactics/TA0002/)
- [PowerShell Security Best Practices](https://docs.microsoft.com/en-us/powershell/scripting/security/)
- NIST SP800-61 Incident Response Guide

## Metrics

| Metric | Target |
|--------|--------|
| Mean Time to Detect (MTTD) | < 15 minutes |
| Mean Time to Respond (MTTR) | < 1 hour |
| False Positive Rate | < 10% |
| Investigation Closure | < 24 hours |
