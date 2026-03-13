# Penetration Testing Manager - Documentation

This directory contains reference documentation for the Penetration Testing Manager consultant agent.

## Overview

The Penetration Testing Manager specializes in coordinating external penetration testing engagements from initial scoping through remediation tracking. This agent ensures security assessments are properly planned, executed, and followed up with actionable remediation.

## Core Knowledge Areas

### Engagement Lifecycle

1. **Pre-Engagement Planning**
   - Purpose identification (compliance, proactive security, post-incident, customer request)
   - Scoping document creation
   - Budget identification and approval
   - Vendor selection and onboarding

2. **Statement of Work (SOW)**
   - Scope definition
   - Methodology specification
   - Duration and pricing
   - Reporting requirements
   - Retesting provisions

3. **Pre-Engagement Preparation**
   - Access provisioning (credentials, VPN, network access)
   - Materials provision (source code, documentation, architecture diagrams)
   - Communication channel setup
   - Meeting schedule coordination

4. **During Engagement**
   - Active monitoring of communication channels
   - Issue handling and escalation
   - Environment availability management
   - Early remediation coordination for critical findings

5. **Post-Engagement**
   - Finding distribution and ticket creation
   - Stakeholder review and final readout
   - Root cause analysis
   - Retesting coordination
   - Report distribution

### Key Stakeholder Roles

| Role | Primary Responsibility |
|------|----------------------|
| Pentest Project Manager | End-to-end engagement coordination |
| Engineering Manager | Technical ownership and remediation |
| Software Engineer | Technical support and fix implementation |
| Operations/SRE | Infrastructure access and monitoring |
| Product Manager | Scope confirmation and risk ownership |
| Compliance Representative | Regulatory requirements |

### Remediation SLAs

| Severity | Target | Maximum |
|----------|--------|---------|
| Critical | 24-48 hours | 7 days |
| High | 7 days | 30 days |
| Medium | 30 days | 90 days |
| Low | 90 days | Next release cycle |
| Informational | Best effort | As appropriate |

### Report Requirements

**Minimum Contents:**
- Contact information (pentesters and client)
- Scope documentation (domains, IPs, methodology)
- Executive summary (suitable for auditors/customers)
- Technical findings with reproduction steps and evidence
- Severity ratings with CVSS methodology
- Remediation recommendations
- Retest status tracking

### Testing Methodologies

- OWASP Testing Guide
- OWASP Top Ten
- PTES (Penetration Testing Execution Standard)
- NIST SP 800-115
- SANS 25 Most Dangerous Software Errors
- PCI DSS Penetration Testing Requirements

## Reference Documents

- External Penetration Testing SOP
- Scoping Document Template
- Vendor Evaluation Scorecard
- Finding Ticket Template

## Program Metrics

| Metric | Purpose |
|--------|---------|
| Findings per engagement | Security posture trending |
| Time to remediation | Process efficiency |
| Retest pass rate | Fix quality measurement |
| Recurring finding types | Training/control needs identification |
| Cost per finding | ROI assessment |

