# Incident Playbook Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/incident_response_playbooks_sop.md`

## Incident Type Coverage

### Critical Incidents
| Type | Key Actions |
|------|-------------|
| Zero-Day | Isolate, patch assessment, compensating controls |
| Ransomware | Isolate, backup verification, negotiation decision |
| Active Intrusion | Contain, preserve evidence, threat hunt |

### Standard Incidents
| Type | Key Actions |
|------|-------------|
| Malware | Isolate, analyze, remediate, sweep |
| Phishing | Block sender, scan recipients, awareness |
| Insider Threat | Access review, HR coordination, evidence |
| IAM Incident | Password reset, session kill, access audit |

### Playbook Structure
1. **Preparation** - Tools, access, contacts ready
2. **Identification** - Detection and triage
3. **Containment** - Stop the spread
4. **Eradication** - Remove the threat
5. **Recovery** - Restore operations
6. **Lessons Learned** - Improve for next time

### Evidence Priority
| Priority | Evidence Type |
|----------|---------------|
| 1 | Memory dumps |
| 2 | Running processes |
| 3 | Network connections |
| 4 | Disk images |
| 5 | Logs |

### Windows Event IDs to Monitor
| Event ID | Meaning |
|----------|---------|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4720 | Account created |
| 4732 | User added to group |
| 7045 | Service installed |

## Related Consultants
- `incident_response_lead` - IR coordination
- `malware_response_analyst` - Malware analysis
- `soc_analyst` - SOC operations
