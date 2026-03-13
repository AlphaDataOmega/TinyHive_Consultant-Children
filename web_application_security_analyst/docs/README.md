# Web Application Security Analyst Documentation

## Overview

This directory contains documentation and reference materials for the web_application_security_analyst consultant agent, specializing in web application attack response and OWASP Top 10 security.

## Core Competencies

### Attack Detection and Response

| Attack Type | Key Indicators | Response Priority |
|-------------|----------------|-------------------|
| SQL Injection | UNION, SELECT, --, 1=1 in parameters | Critical |
| Command Injection | whoami, uname, pipe/semicolon chaining | Critical |
| Cross-Site Scripting (XSS) | Script tags, event handlers in input | High |
| Remote File Inclusion (RFI) | External URLs in include parameters | Critical |
| Local File Inclusion (LFI) | ../../../etc/passwd patterns | High |
| Web Shell Upload | POST to .php files, cmd/exec parameters | Critical |

### OWASP Top 10 Coverage

1. **Injection** - SQL, NoSQL, OS, LDAP injection detection and remediation
2. **Broken Authentication** - Session management and account takeover response
3. **Sensitive Data Exposure** - Data breach assessment and notification
4. **XML External Entities (XXE)** - XML processor misconfiguration detection
5. **Broken Access Control** - Unauthorized access investigation
6. **Security Misconfiguration** - Web server hardening assessment
7. **Cross-Site Scripting (XSS)** - Reflected, Stored, DOM-based response
8. **Insecure Deserialization** - RCE via object injection analysis
9. **Using Components with Known Vulnerabilities** - Dependency scanning
10. **Insufficient Logging & Monitoring** - Detection capability assessment

## Reference SOPs

- SOP-Web-Application-Attack-Response.md - Primary response procedures

## Tools Reference

### Detection and Scanning

| Tool | Purpose |
|------|---------|
| THOR Lite | IOC scanner for web shells and exploits |
| ClamAV | Antivirus scanning for web server malware |
| WPScan | WordPress security vulnerability scanning |
| URLScan.io | URL and page analysis |
| Sucuri SiteCheck | Website malware detection |
| OWASP ZAP | Dynamic application security testing |

### Web Application Firewalls

| WAF Solution | Configuration |
|--------------|---------------|
| ModSecurity | OWASP Core Ruleset (CRS) |
| CloudFlare | OWASP + Managed Rulesets |
| CrowdSec | Community-driven threat blocking |

### Threat Intelligence

| Platform | Purpose |
|----------|---------|
| OpenCTI | Threat intelligence platform integration |
| MISP | Malware information sharing |
| CyberGordon | IP/domain reputation lookup |
| VirusTotal | File and URL analysis |

## Log Analysis Patterns

### SQL Injection Detection

```
HTTP 200 + GET + patterns containing:
- Single quote followed by "or"
- "UNION", "SELECT", "DROP", "INSERT"
- "--" (SQL comment syntax)
- "1=1" or "1'='1"
```

### Command Injection Detection

```
HTTP 200 + GET + patterns containing:
- "whoami", "uname", "ifconfig", "netstat"
- "etc/passwd"
- "|", ";", "&&" in parameters
```

### Web Shell Indicators

```
HTTP 200 + POST + patterns containing:
- ".php" at end of query
- "shell", "panel", "admin", "cmd", "exec"
```

## HTTP Response Code Analysis

| Code | Security Significance |
|------|----------------------|
| 200 on unfamiliar files | Potential web shell or unauthorized access |
| 401/403 bursts | Authentication brute force attempts |
| 400 patterns | Request fuzzing or parameter manipulation |
| 500 errors | Injection attempts causing application errors |
| Multiple 404s | Directory and file enumeration |

## MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1190 | Exploit Public-Facing Application |
| T1491 | Defacement |
| T1055 | Process Injection |
| T1059 | Command and Scripting Interpreter |
| T1505.003 | Web Shell |

## Incident Response Workflow

1. **Detection** - WAF alert, SIEM correlation, user report, or bug bounty
2. **Triage** - Assess severity based on data access and RCE capability
3. **Containment** - Block attacker IP, disable vulnerable functionality, isolate server
4. **Investigation** - Log analysis, forensic imaging, threat intel correlation
5. **Eradication** - Remove malware, patch vulnerability, harden configuration
6. **Recovery** - Restore from clean backup, deploy fixes, verify effectiveness
7. **Post-Incident** - Document findings, conduct postmortem, implement improvements

## Framework Alignment

- NIST SP800-61 Rev 3 (Incident Response)
- NIST Cybersecurity Framework
- OWASP Top 10
- MITRE ATT&CK Framework
- NSA/CISA Web Shell Detection Guidelines
- HITRUST Threat Catalogue
