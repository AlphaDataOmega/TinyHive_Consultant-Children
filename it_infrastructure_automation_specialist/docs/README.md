# IT Infrastructure Automation Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/it_operations/infrastructure_automation_sop.md`

## Automation Categories

### Active Directory
| Workflow | Description |
|----------|-------------|
| User Creation | Create accounts from Excel/CSV |
| Password Expiry | Notify users of expiring passwords |
| Account Disable | Disable inactive accounts |
| Group Sync | Synchronize group memberships |
| Termination | Full offboarding workflow |

### Network Devices (Cisco)
| Task | Purpose |
|------|---------|
| Config Backup | Daily configuration backup |
| Version Report | Inventory IOS versions |
| Interface Status | Monitor interface health |
| Routing Table | Display IP routing |
| Log Collection | Retrieve router logs |

### Application Monitoring
| Check | Action |
|-------|--------|
| Service Status | Monitor Windows services |
| Process Memory | Find top memory consumers |
| Software Inventory | Report installed software |
| Anti-virus Status | Verify AV running |
| Stuck Processes | Kill hung processes |

### Security Monitoring
| Event ID | Meaning |
|----------|---------|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4720 | Account created |
| 4732 | User added to group |
| 4740 | Account locked out |

## XML Workflow Structure

```xml
<Workflow name="TaskName">
  <Activity name="Step1" type="ExecuteCommand">
    <Parameters>
      <Host>{{hostname}}</Host>
      <Command>command here</Command>
    </Parameters>
  </Activity>
  <Activity name="Step2" depends="Step1">
    ...
  </Activity>
</Workflow>
```

## Variable Syntax

| Pattern | Usage |
|---------|-------|
| `{{variable}}` | Runtime substitution |
| `${env.VAR}` | Environment variable |
| `#result.field#` | Previous step output |

## User Lifecycle Phases

| Phase | Automated Tasks |
|-------|----------------|
| Onboarding | Create account, groups, mailbox, home folder |
| Maintenance | Password reset, group changes, access reviews |
| Offboarding | Disable, revoke access, archive data, notify |

## VMware Automation

| Task | Description |
|------|-------------|
| VM Provisioning | Create VMs from template |
| Snapshot Management | Create/delete snapshots |
| Power Operations | Start/stop/restart VMs |
| Resource Reports | CPU/memory utilization |

## Related Consultants
- `sre_runbook_specialist` - SRE runbooks
- `monitoring_engineer` - Observability
- `cloud_security_engineer` - Cloud automation
