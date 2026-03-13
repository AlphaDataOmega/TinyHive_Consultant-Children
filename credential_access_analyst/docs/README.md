# Credential Access Analyst Documentation

## Overview

This documentation supports the Credential Access Analyst role in detecting, investigating, and responding to credential-based attacks as defined by MITRE ATT&CK Tactic TA0006 (Credential Access).

## MITRE ATT&CK Coverage

### Primary Tactic

| Tactic | ID | Description |
|--------|-----|-------------|
| Credential Access | TA0006 | Techniques for stealing credentials like account names and passwords |

### Covered Techniques

| Technique ID | Technique Name | Sub-Techniques |
|-------------|----------------|----------------|
| T1110 | Brute Force | Password Spraying (T1110.003), Password Guessing, Credential Stuffing |
| T1003 | OS Credential Dumping | LSASS Memory, SAM, NTDS, DCSync, /etc/passwd and /etc/shadow |
| T1555 | Credentials from Password Stores | Browser credentials, Keychain, Password Managers |
| T1552 | Unsecured Credentials | Files, Registry, Cloud Instance Metadata, Private Keys |
| T1556 | Modify Authentication Process | Domain Controller, Pluggable Authentication Modules |
| T1558 | Steal or Forge Kerberos Tickets | Kerberoasting, Golden Ticket, Silver Ticket, AS-REP Roasting |
| T1539 | Steal Web Session Cookie | Session hijacking via cookie theft |
| T1606 | Forge Web Credentials | SAML Tokens, Web Cookies |

## Detection Capabilities

### Password Spraying Detection

| Indicator | Detection Logic | Threshold |
|-----------|-----------------|-----------|
| Failed logins for default accounts | Alert on failed auth to Administrator, admin, root, guest | Any occurrence |
| Same account across multiple systems | Single account fails on 5+ systems within 10 minutes | 5 systems/10 min |
| Multiple accounts from same source | Single IP fails on 10+ accounts within 30 minutes | 10 accounts/30 min |
| Low and slow attempts | Failed auth below lockout threshold but sustained over time | Pattern analysis |

### Credential Dumping Detection

| Indicator | Detection Logic | Severity |
|-----------|-----------------|----------|
| LSASS process access | Unusual process accessing lsass.exe | High |
| SAM database access | Access to SAM, SYSTEM, or SECURITY hives | High |
| DCSync activity | Replication requests from non-DC systems | Critical |
| Mimikatz signatures | Known tool signatures in memory | Critical |
| NTDS.dit access | Attempts to copy or access NTDS.dit | Critical |

### Kerberos Attack Detection

| Attack | Detection Indicators | Response Priority |
|--------|---------------------|-------------------|
| Kerberoasting | High volume of TGS requests for SPNs | High |
| AS-REP Roasting | Requests for accounts without pre-auth | Medium |
| Golden Ticket | TGT with unusual lifetime or encryption | Critical |
| Silver Ticket | Service ticket anomalies | High |
| Pass-the-Ticket | Ticket reuse from different IPs | High |

## Investigation Procedures

### Initial Triage

1. **Confirm the Alert**
   - Validate detection fidelity (true positive vs. false positive)
   - Identify affected accounts and systems
   - Determine attack timeline

2. **Scope Assessment**
   - Identify all systems accessed by compromised credentials
   - Map lateral movement paths
   - Assess data access and potential exfiltration

3. **Evidence Collection**
   - Preserve authentication logs
   - Capture memory from affected systems (if credential dumping suspected)
   - Document network connections and traffic patterns
   - Collect endpoint telemetry

### Key Investigation Questions

- What credentials were targeted or compromised?
- How long has the attack been ongoing?
- What systems did the attacker access?
- Were privileged credentials compromised?
- Is there evidence of persistence mechanisms?
- Was data accessed or exfiltrated?

## Containment Procedures

### Immediate Actions (First 30 Minutes)

1. **Account Lockdown**
   - Disable compromised accounts immediately
   - Reset passwords for affected accounts
   - Revoke active sessions and tokens
   - Force re-authentication for affected users

2. **Network Isolation**
   - Isolate compromised endpoints from the network
   - Block attacker source IPs at the firewall
   - Implement additional network ACLs as needed

3. **System Isolation**
   - Quarantine systems showing credential dumping activity
   - Disable remote access to affected systems
   - Preserve systems for forensic analysis

### Extended Containment

1. **Credential Reset Strategy**
   - Reset KRBTGT password (twice, 10+ hours apart)
   - Reset service account passwords
   - Rotate certificates and secrets
   - Reset machine account passwords if necessary

2. **Access Review**
   - Audit privileged group membership
   - Review recent permission changes
   - Check for unauthorized service principals

## Investigation Tools

| Tool Category | Examples | Use Case |
|--------------|----------|----------|
| SIEM | Splunk, Sentinel, Elastic | Log analysis and correlation |
| EDR | CrowdStrike, Defender, Carbon Black | Endpoint investigation |
| Network | Zeek, Wireshark, NetFlow | Traffic analysis |
| Memory | Volatility, Rekall | Credential artifact recovery |
| AD Tools | BloodHound, PingCastle | Attack path analysis |

## Preparation Requirements

### Technical Controls

1. **Logging and Monitoring**
   - Centralized SIEM collection from all authentication systems
   - Enhanced audit logging for Kerberos, NTLM, LDAP, and password events
   - Minimum 90-day log retention

2. **Multi-Factor Authentication**
   - MFA for all privileged accounts
   - MFA for remote access and VPN
   - Phishing-resistant MFA (FIDO2, hardware tokens) for high-value targets

3. **Password Policy**
   - Minimum 14 characters for standard users
   - Minimum 20 characters for privileged accounts
   - Password blocklists for common passwords

### Administrative Controls

1. **Account Hygiene**
   - Regular audit and disable unused accounts
   - Just-in-time privileged access
   - Separate privileged and non-privileged accounts
   - Quarterly service account reviews

## References

### MITRE ATT&CK

- [Credential Access Tactic (TA0006)](https://attack.mitre.org/tactics/TA0006/)
- [Password Spraying (T1110.003)](https://attack.mitre.org/techniques/T1110/003/)
- [OS Credential Dumping (T1003)](https://attack.mitre.org/techniques/T1003/)
- [Steal or Forge Kerberos Tickets (T1558)](https://attack.mitre.org/techniques/T1558/)

### Industry Standards

- NIST SP 800-63B: Digital Identity Guidelines
- NIST SP 800-61: Computer Security Incident Handling Guide
- CIS Controls: Identity Management and Access Control
- Microsoft Security Best Practices for Active Directory
