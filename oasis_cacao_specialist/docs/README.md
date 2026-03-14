# OASIS CACAO Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/oasis_cacao_playbooks_sop.md`

## CACAO Playbook Structure

### Required Fields
| Field | Type | Description |
|-------|------|-------------|
| type | string | Always "playbook" |
| spec_version | string | "1.0" |
| id | string | playbook--{uuid} |
| name | string | Playbook name |
| workflow_start | string | Start step ID |
| workflow | object | Step definitions |

### Step Types
| Type | Purpose | Next Step |
|------|---------|-----------|
| start | Entry point | on_completion |
| single | Single action | on_completion |
| parallel | Fork branches | next_steps[] |
| end | Terminal node | None |

## Command Types

| Type | Use Case |
|------|----------|
| manual | Human intervention |
| ssh | Remote shell commands |
| http-api | REST API calls |
| bash | Linux shell scripts |
| powershell | Windows automation |

## TLP Data Markings

| Level | Sharing |
|-------|---------|
| TLP-RED | Named recipients only |
| TLP-AMBER | Organization only |
| TLP-GREEN | Community sharing |
| TLP-WHITE | Public information |

## Workflow Pattern Examples

### Sequential Flow
```
start -> single -> single -> end
```

### Parallel Flow
```
start -> parallel -> [single, single] -> end
```

### Fork-Join
```json
{
  "type": "parallel",
  "next_steps": ["step-a", "step-b"],
  "on_completion": "join-step"
}
```

## Integration Patterns

| Platform | Integration Type |
|----------|-----------------|
| Splunk | REST API |
| QRadar | HTTPS API |
| CrowdStrike | OAuth2 API |
| Palo Alto | XML API |
| Cisco | REST/CLI |

## Playbook Types

| Type | Description |
|------|-------------|
| prevention | Block threats proactively |
| detection | Identify active threats |
| investigation | Analyze incidents |
| remediation | Remove threats |
| notification | Alert stakeholders |

## Related Consultants
- `soar_automation_engineer` - SOAR platforms
- `threat_intel_manager` - Threat intelligence
- `incident_response_lead` - IR coordination
