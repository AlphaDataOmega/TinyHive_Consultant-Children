# Credential Security Specialist Documentation

## Overview

This directory contains reference documentation, procedures, and resources for credential compromise response, secrets management, and IAM security operations.

## Core Competencies

### Credential Compromise Response
- Detection from SIEM alerts, GuardDuty findings, external breach notifications
- Initial triage: credential type, access level, exposure scope, blast radius assessment
- Containment: disable credentials, revoke sessions, apply deny-all policies
- Eradication: API activity analysis, persistence mechanism removal, iterative investigation
- Recovery: credential rotation, application restoration, configuration validation

### Secrets Management
- Enterprise secrets platforms: HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, GCP Secret Manager
- Automated credential rotation and lifecycle management
- Secret scanning integration: TruffleHog, GitLeaks, detect-secrets, git-secrets
- Pre-commit hooks and CI/CD pipeline scanning

### IAM Security and Hygiene
- Regular access reviews: weekly, monthly, quarterly audit cycles
- Inactive user detection and automated cleanup workflows
- Service account management with documented ownership
- Least privilege enforcement and privilege escalation prevention

### Account Takeover Prevention
- MFA enforcement with hardware security key preference
- Adaptive authentication and risk-based access controls
- Behavioral analytics: impossible travel, anomalous location, off-hours access
- Device fingerprinting and session management
- Anti-phishing measures: SPF, DKIM, DMARC, brand monitoring

### Breach Monitoring
- Integration with HIBP, Recorded Future, SpyCloud, DeHashed
- Automated breach notification workflows
- Corporate credential exposure classification and response

## Cloud Platform Procedures

### AWS
- IAM user credential compromise: disable access keys, delete login profile, deactivate MFA
- IAM role compromise: session revocation via inline deny policy with TokenIssueTime condition
- CloudTrail analysis via Athena queries for compromised credential activity

### Azure AD
- User account compromise: block sign-in, revoke refresh tokens, reset password
- Service principal compromise: remove credentials, disable application
- Integration with Azure AD banned password list

### GCP
- Service account compromise: disable account, delete keys
- Audit log analysis for principal activity

## Key Metrics

| Metric | Target |
|--------|--------|
| Mean Time to Detect (MTTD) | < 24 hours |
| Mean Time to Contain (MTTC) | < 1 hour |
| Mean Time to Recover (MTTR) | < 24 hours |
| Credential Age | < 90 days |
| Unused Credentials (30+ days) | 0 |

## Credential Rotation Schedule

| Credential Type | Rotation Frequency |
|-----------------|-------------------|
| IAM user access keys | 90 days |
| Service accounts | 30-90 days |
| OAuth tokens | Per provider definition |
| SSH keys | 180 days |

## Quick Reference: First 15 Minutes

1. **IDENTIFY** - Credential type, access level, exposure duration
2. **CONTAIN** - Disable credential immediately, document before changes
3. **COMMUNICATE** - Open incident ticket, notify on-call, brief stakeholders
4. **INVESTIGATE** - Pull activity logs, check lateral movement, look for persistence

## Related Resources

- NIST SP 800-61r2: Computer Security Incident Handling Guide
- NIST SP 800-63B: Digital Identity Guidelines
- CIS Controls v8: Control 5 - Account Management
- AWS Security Incident Response Guide
- MITRE ATT&CK Credential Access Techniques

## Tools

### Secrets Management
- HashiCorp Vault
- AWS Secrets Manager
- Azure Key Vault
- GCP Secret Manager
- CyberArk

### Secret Scanning
- TruffleHog
- GitLeaks
- detect-secrets
- git-secrets
- SpectralOps

### Breach Monitoring
- Have I Been Pwned (HIBP)
- Recorded Future
- SpyCloud
- DeHashed

### SOAR Platforms
- Splunk SOAR (Phantom)
- Palo Alto XSOAR
- Microsoft Sentinel
- Tines
- TheHive
