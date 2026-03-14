# Security Program Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/security_program_templates_sop.md`

## Severity Level Definitions

| Level | Description | Response Time | Examples |
|-------|-------------|---------------|----------|
| SEV1 | Critical | Immediate | Data breach, ransomware, active intrusion |
| SEV2 | High | < 4 hours | Malware outbreak, credential compromise |
| SEV3 | Medium | < 24 hours | Phishing success, policy violation |
| SEV4 | Low | < 72 hours | Minor alerts, false positives |

## Incident Document Structure

### Working Document Sections
1. **Header** - Commander, version, severity, tickets
2. **Executive Summary** - One paragraph overview
3. **Detailed Description** - Full technical analysis
4. **Action Items** - Priority, status, owner, ETA
5. **Timeline** - Chronological event log
6. **Open Questions** - Unresolved items

### Postmortem Sections
1. **Summary** - What happened and impact
2. **Detection** - How was it found
3. **Response** - What was done
4. **Root Cause** - Why it happened
5. **Action Items** - What to improve
6. **Lessons Learned** - Key takeaways

## Security Metrics

| Category | Metric | Target |
|----------|--------|--------|
| Detection | MTTD (Mean Time to Detect) | < 24 hours |
| Response | MTTR (Mean Time to Respond) | < 4 hours |
| Recovery | MTTR (Mean Time to Recover) | < 8 hours |
| Volume | Incidents per month | Track trend |
| Effectiveness | False positive rate | < 10% |

## Vulnerability Management

| Priority | CVSS Score | Remediation SLA |
|----------|------------|-----------------|
| Critical | 9.0-10.0 | 24 hours |
| High | 7.0-8.9 | 7 days |
| Medium | 4.0-6.9 | 30 days |
| Low | 0.1-3.9 | 90 days |

## Program Roles

| Role | Responsibility |
|------|---------------|
| Incident Commander | Overall incident leadership |
| Communications Lead | Stakeholder updates |
| Technical Lead | Investigation and remediation |
| Scribe | Documentation and timeline |

## Related Consultants
- `incident_playbook_specialist` - Playbook development
- `incident_response_lead` - IR coordination
- `soc_operations_manager` - SOC management
