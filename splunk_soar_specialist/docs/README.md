# Splunk SOAR Specialist Documentation

## Overview

This consultant specializes in Splunk SOAR (Security Orchestration, Automation, and Response) playbook development, security automation, and incident response orchestration. The specialist draws from comprehensive knowledge of 150+ vendor-provided playbooks covering incident response, threat hunting, and automated remediation.

## Core Competencies

### Incident Response Playbooks
- **Phishing Investigation and Response** — Extract artifacts, analyze attachments/URLs, verify sender domains, identify affected users, and execute approved containment
- **Ransomware Investigation and Containment** — Parallel execution of containment, investigation, and communication tracks
- **C2 Investigation** — Extract file/connection information, calculate threat scores, implement severity-based escalation
- **Malware Hunt and Containment** — EDR integration, scope assessment, patient zero identification, eradication workflows
- **Log4j (CVE-2021-44228) Response** — Host enumeration, exploitation detection, outbound connection analysis, mitigation options

### Threat Intelligence Operations
- Multi-source indicator enrichment (VirusTotal, PassiveTotal, GreyNoise, AbuseIPDB, Recorded Future)
- Internal sighting hunts across EDR, firewall, DNS, and proxy logs
- WannaCry-specific detection, investigation, prevention, and remediation playbooks

### Indicator Management
- Automated indicator collection and type separation (IP, domain, URL, hash, email, user, host)
- Multi-service blocking (Palo Alto Firewall, OpenDNS Umbrella, Carbon Black, Zscaler)
- Custom blocklist management and indicator tagging workflows

### Cloud Security Operations
- **AWS:** EC2 instance investigation and isolation, IAM user activity monitoring, inactive user detection
- **Azure:** Azure AD user census, group membership enumeration, MFA status monitoring
- **GCP:** Service account monitoring, unusual API call detection, cross-project access analysis

### Endpoint Response
- Host quarantine via CrowdStrike Falcon and Carbon Black
- Rootkit investigation with hidden process/file detection
- Malicious process termination and file deletion with safety checks

### Email Security
- Compromised email containment with LDAP integration
- Multi-sandbox attachment analysis (McAfee ATD, Carbon Black Cloud, Any.Run, Joe Sandbox)
- Suspicious sender domain enrichment

### Network Security
- DNS hijack investigation with historical record analysis
- Zscaler URL hunt and block workflows
- Rogue wireless access point detection and remediation

### Risk-Based Alerting
- Splunk Enterprise Security risk notable processing
- Automated alert classification and severity assignment
- Executive escalation and test machine de-escalation logic

## Integration Reference

### Supported Platforms

| Category | Integrations |
|----------|-------------|
| Endpoint Security | CrowdStrike Falcon, Carbon Black, Microsoft Defender, Symantec |
| Network Security | Palo Alto, Cisco ASA/Firepower, Zscaler, OpenDNS Umbrella, Fortinet |
| SIEM/Analytics | Splunk ES, Microsoft Sentinel, Chronicle, IBM QRadar |
| Threat Intelligence | VirusTotal, Recorded Future, ThreatConnect, ThreatQuotient, GreyNoise |
| Cloud Platforms | AWS (EC2, IAM, S3, CloudTrail), Azure (Azure AD, Sentinel), GCP |
| Identity & Access | Active Directory, Azure AD, LDAP, Okta |
| Email Security | Microsoft Exchange, Office 365, Proofpoint, Mimecast |
| Ticketing/ITSM | ServiceNow, Jira, BMC Remedy |
| Communication | Slack, Microsoft Teams, Email (SMTP) |

## Severity Levels

| Level | Description | Response Time |
|-------|-------------|---------------|
| Critical | Active breach, data exfiltration | Immediate |
| High | Confirmed malware, C2 activity | < 1 hour |
| Medium | Suspicious activity, policy violation | < 4 hours |
| Low | Informational, minor issues | < 24 hours |

## Escalation Matrix

| Condition | Escalate To | Communication |
|-----------|-------------|---------------|
| Executive targeted | Executive Protection | Immediate call |
| >10 users affected | Incident Commander | Slack + Email |
| Data exfiltration suspected | CISO | Phone + Email |
| Regulatory data involved | Legal/Compliance | Secure channel |
| Third-party involved | Vendor Management | Documented communication |

## Key Principles

1. **Automation First** — Leverage playbooks to reduce mean time to respond (MTTR)
2. **Human-in-the-Loop** — Critical containment actions require analyst approval
3. **Evidence Preservation** — Document all actions and maintain audit trails
4. **Escalation Paths** — Define clear severity-based escalation procedures
5. **Integration** — Utilize multiple security tools in coordinated response

## Related Resources

- Splunk SOAR Documentation: https://docs.splunk.com/Documentation/SOAR
- MITRE ATT&CK Framework: https://attack.mitre.org/
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
