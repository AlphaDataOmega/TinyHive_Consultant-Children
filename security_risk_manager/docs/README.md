# Security Risk Manager Documentation

## Overview

This directory contains reference documentation for the Security Risk Manager consultant agent. The agent specializes in security exceptions program management and risk assessment operations.

## Source Material

The agent's capabilities are derived from the **Security Exceptions and Risk Management Program SOP**, which provides comprehensive guidance for:

- Establishing and operating a security exceptions program
- Managing situations where security requirements cannot be immediately met
- Conducting risk assessment interviews
- Tracking and reporting on security exceptions

## Key Concepts

### Exception Types

| Type | Description |
|------|-------------|
| Risk Extension | Temporary delay in remediation beyond standard SLA |
| Risk Acceptance | Formal acceptance of risk without remediation |
| Compensating Control | Alternative control in lieu of standard requirement |
| Policy Exception | Deviation from established security policy |

### Severity Levels and Approval Matrix

| Severity | Default Remediation | Product/Eng Approver | Security Approver | Extension Without Escalation |
|----------|---------------------|----------------------|-------------------|------------------------------|
| Critical | 0-7 days | VP/C-suite | VP/CISO | ~2 hours |
| High | ~30 days | Director | Director | 1-2 days |
| Medium | ~60 days | Manager | Manager | ~10 days |
| Low | ~90 days | None required | Sr/Staff Engineer | ~20 days |

### Program Roles

- **Security Exception Program Owner**: Oversees the program, handles escalations, manages metrics
- **Risk Owner**: Accountable for risks in their products/services/processes
- **Risk Approver**: Senior leaders who approve risk decisions
- **Subject Matter Expert (SME)**: Technical advisors for risk classification and remediation

## Core Workflows

### Exception Support (SME Role)
1. Receive stakeholder support request
2. Evaluate technical solutions
3. Propose preferred solution
4. Determine if exception required
5. Route to exceptions process
6. Assist with exception details

### Exception Approval (Risk Owner Role)
1. Review exception request
2. Determine exception type (delay vs. accept)
3. Decide on acceptance or rejection
4. Obtain required approvals

### Exception Intake (Program Owner Role)
1. Receive exception request
2. Evaluate request completeness
3. Determine risk approvers
4. Monitor exception progress
5. Add items to discussion meetings

## Program Metrics

- **Open Security Exceptions**: Total number of active exceptions
- **Expiring Security Exceptions**: Exceptions approaching deadline
- **Expired Exceptions Without Treatment**: Risks past resolution date
- **Exceptions by Status**: Breakdown by workflow state
- **Average Time to Initial Review**: Processing efficiency
- **Exceptions by Severity Level**: Risk distribution
- **Risk Extension vs Risk Acceptance**: Exception type trends

## Exception Request Requirements

Each exception must include:
- Title (precise description)
- Priority/Severity (aligned with vulnerability ranking)
- Assignee (responsible individual)
- Description (vulnerability and impact explanation)
- Pros and Cons (benefits and risks of accepting)
- Technical Uplift Path (remediation steps and effort)
- Fix By Date (aligned with SLAs)

## Risk Assessment Interview Categories

When conducting risk assessments, use these question categories:
- **Impact Questions**: Value and consequences of compromise
- **Threat Questions**: Forces that could cause impact
- **Vulnerability Questions**: Circumstances attracting threats
- **Fear Questions**: Underlying security concerns
- **Conditional Scenarios**: "What if" situations
- **VIP Employee Questions**: High-risk personnel identification
- **Best Practices Questions**: Assumption validation
- **Incident History Questions**: Past security events

## Related Documentation

- Vulnerability Management SOP
- Incident Response Procedures
- Security Policy Framework
- Compliance Requirements Matrix
