# SOAR Automation Engineer Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/soar_automation_playbooks_sop.md`

## Platform Support

### Catalyst (YAML)
```yaml
name: Phishing Response
description: Automated phishing workflow
steps:
  - name: Extract IOCs
    action: extract_indicators
  - name: Check Reputation
    action: virustotal_lookup
  - name: Block Sender
    action: block_email_sender
```

### Resolve (XML)
- ServiceNow integration
- Active Directory automation
- Event log monitoring
- Incident management procedures

### OASIS Open (JSON)
- Standard playbook format
- Parallel processing support
- APT response workflows

## Common Automation Patterns

### Phishing Response
1. Receive phishing alert
2. Extract URLs, domains, hashes
3. Check reputation (VT, URLScan)
4. Block malicious indicators
5. Search for other recipients
6. Create incident ticket

### Malware Analysis
1. Receive malware alert
2. Extract file hash
3. Submit to sandbox
4. Analyze results
5. Block if malicious
6. Update threat intel

### ServiceNow Integration
| Action | Use Case |
|--------|----------|
| Create Incident | Security alert |
| Update Ticket | Status changes |
| Close Ticket | Resolution |
| Bulk Create | Mass alerts |

### Loop Patterns
```
FOR EACH indicator IN indicators:
    check_reputation(indicator)
    IF malicious:
        block(indicator)
        notify(soc_team)
```

## Related Consultants
- `splunk_soar_specialist` - Splunk SOAR
- `xsoar_automation_specialist` - Cortex XSOAR
- `sentinel_soar_specialist` - Microsoft Sentinel
