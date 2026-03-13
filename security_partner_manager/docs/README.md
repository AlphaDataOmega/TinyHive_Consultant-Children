# Security Partner Manager - Documentation

## Overview

This directory contains reference documentation for the Security Partner Manager consultant, specializing in security partner program management, PRD/TDD security reviews, and vulnerability scanning coordination.

## Core Domain Knowledge

### Security Partner Program

A security partner program provides white-glove security services through dedicated security engineers embedded with specific engineering teams. Unlike traditional security consulting that supports everyone generally, security partners serve as long-term advisors to specific products or organizations.

### Key Program Benefits

| Benefit | Description |
|---------|-------------|
| **Context** | Partners understand past risks, codebases, core functionality, current issues, and anticipated future risks |
| **Execution Speed** | Historical context and product familiarity enable more efficient security reviews |
| **Advocacy** | Partners understand engineering challenges including weak controls, constraints, and architectural limitations |
| **Trade-off Identification** | Context-specific guidance enables quicker risk mitigation decisions |

### Security Partner vs Security Champion

| Role | Description |
|------|-------------|
| **Security Partner** | Security engineer from the security team providing dedicated services to specific engineering teams |
| **Security Champion** | Engineering/ops/IT team member with security interest or delegated security duties |

## Program Implementation Phases

### Phase 1: Initial Setup
- Determine program owner (TPM responsible for operations, metrics, escalations)
- Identify initial high-risk applications
- Meet with engineering/operations/product leaders to identify pain points
- Select pilot team based on risk and remediation challenges

### Phase 2: Partner Selection and Bootstrap
- Allocate senior AppSec engineer (L5+) with strong collaboration skills
- Join team meetings, Slack channels, gain Jira/repository access
- Conduct kickoff meeting with engineering leadership

### Phase 3: Execution and Expansion
- Execute pilot partnership
- Define success metrics
- Determine coverage methodology for expansion
- Perform retrospective after 1-3 months
- Expand to additional products/teams

## Security Review Procedures

### PRD Review Process
1. Review document line-by-line, add comments, flag missing data flows
2. Schedule design review meeting with PM and engineering
3. Send action items with clear expectations
4. Create prioritized tickets (P1/P2/P3)

### TDD Review Process
1. Verify data flow diagrams, PII handling, third-party integrations
2. Conduct engineering-focused security design review
3. Identify security requirements and missing controls
4. Create prioritized tickets with remediation guidance

## Security Scanning Operations

### Scanner Types
- **SAST**: Static Application Security Testing
- **SCA**: Software Composition Analysis
- **Cloud**: Cloud security configuration scanning
- **DAST**: Dynamic Application Security Testing

### Health Monitoring Steps
1. Verify scanner configuration and enablement
2. Establish baseline of findings
3. Ensure correct prioritization reaching engineering
4. Raise open vulnerabilities with engineering managers
5. Regularly review unremediated findings

## Program Metrics

### Coverage Metrics
- Total coverage across products/features
- Coverage across teams
- Coverage across product types (frontend, backend, mobile)
- Coverage across high/critical risk products

### Engagement Metrics
- Pull requests supported
- Mitigation guidance provided
- Design reviews/threat models conducted
- General support activities

### Support Allocation Metrics
- Time distribution across support types
- Volume trends over time
- PRD vs TDD review rates

### Experimental Metrics
- Partner average remediation time (cost comparison)
- Partner incident time reduction

## Related Resources

| Document | Purpose |
|----------|---------|
| Security Partner Program SOP | Complete operational procedures |
| Vulnerability Management SLA | Remediation timeline requirements |
| Security Exception Process | Risk acceptance workflows |
| Vendor Security Process | Third-party software review |

## Routing Guidelines

| Concern | Action |
|---------|--------|
| **Privacy** | Data collection/sharing changes - route to privacy team |
| **Vendor Usage** | Third-party software/integrations - route to vendor security |
| **Compliance** | Data storage regulations/policies - route to compliance team |
