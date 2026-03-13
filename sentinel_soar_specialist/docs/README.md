# Sentinel SOAR Specialist Documentation

## Overview

This directory contains reference documentation and standard operating procedures for Microsoft Sentinel SOAR playbook development and Azure Logic Apps automation.

## Core Competencies

### Microsoft Sentinel SOAR
- Incident and alert trigger automation
- Automation rule configuration and ordering
- Incident comment and entity management
- Watchlist integration for dynamic response

### Azure Logic Apps
- Managed identity authentication
- Nested playbook orchestration
- Parallel branch execution
- Error handling with scopes

### Playbook Categories

| Category | Description |
|----------|-------------|
| User Management | AAD user blocking, session revocation, admin approvals |
| Network Remediation | Multi-vendor IP/URL blocking across firewalls |
| Enrichment | Threat intelligence from Graph, GreyNoise, Recorded Future |
| Azure Resources | VM isolation, NSG management, snapshot creation |
| ITSM Integration | JIRA, ServiceNow bidirectional sync |
| IoT/OT Security | Maintenance windows, production line routing |

## Trigger Types

| Type | Use Case |
|------|----------|
| Incident Trigger | Production automation via automation rules |
| Alert Trigger | On-demand analysis, specific alert types |
| Scheduled Trigger | Health checks, reporting, compliance |
| HTTP Trigger | ITSM sync, webhook-based automation |

## Authentication Methods

| Method | Best For |
|--------|----------|
| Managed Identity | Azure resource access (recommended) |
| Service Principal | Cross-tenant, specific permissions |
| API Keys | Third-party integrations |
| OAuth 2.0 | User-context operations |

## Key Playbooks

### User Account Management
- **Block-AADUserOrAdmin** - Disable compromised users with admin approval workflow
- **Revoke-AADSignInSessions** - Revoke all active sessions for compromised users

### Network Remediation
- **Remediation-IP** - Master playbook for multi-vendor IP blocking
- **Remediation-URL** - Master playbook for URL blocking across security products

### Threat Intelligence
- **Get-AlertEntitiesEnrichment** - Multi-source Microsoft security enrichment
- **Enrich-SentinelIncident-GreyNoise-IP** - GreyNoise RIOT and Context API enrichment
- **RecordedFuture_IOC_Enrichment** - Recorded Future indicator enrichment
- **HaveIBeenPwned Integration** - Breach detection playbooks

### Azure Resource Protection
- **Isolate-AzureVMtoNSG** - Network isolate compromised VMs with approval
- **Notify-ASCAlertAzureResource** - Resource owner notification

## Required Permissions

### Microsoft Graph API
| Permission | Use Case |
|------------|----------|
| User.Read.All | Read user profiles |
| User.ReadWrite.All | Modify user accounts |
| Directory.Read.All | Read directory data |
| Directory.ReadWrite.All | Modify directory objects |
| IdentityRiskyUser.Read.All | Read risk assessments |
| MailboxSettings.Read | Read mailbox settings |

### Azure RBAC Roles
| Role | Capabilities |
|------|--------------|
| Microsoft Sentinel Reader | View incidents, workbooks |
| Microsoft Sentinel Responder | Update incidents, run playbooks |
| Microsoft Sentinel Contributor | Full incident management |
| Logic App Contributor | Manage Logic Apps |

## Third-Party Integrations

| Vendor | Integration Type |
|--------|------------------|
| CrowdStrike | Threat intelligence, device isolation |
| Palo Alto | Firewall rules, Wildfire analysis |
| Fortinet | FortiGate firewall management |
| Cisco Meraki | Network policy management |
| Zscaler | URL filtering, cloud security |
| ServiceNow | ITSM ticket management |
| JIRA | Service desk integration |
| GreyNoise | IP reputation |
| Recorded Future | Threat intelligence |
| HaveIBeenPwned | Breach detection |

## Deployment Checklist

### Pre-Deployment
- [ ] Verify Azure subscription permissions
- [ ] Identify required API permissions
- [ ] Prepare API keys for external services
- [ ] Create Key Vault for secrets
- [ ] Document existing automation rules

### Deployment
- [ ] Deploy Logic App from template
- [ ] Configure managed identity
- [ ] Authorize API connections
- [ ] Assign RBAC roles
- [ ] Configure automation rules

### Validation
- [ ] Test with sample incident
- [ ] Verify incident comments
- [ ] Check error handling
- [ ] Validate notifications
- [ ] Review run history

## Best Practices

### Design Principles
1. **Modularity** - Use nested playbooks for reusable components
2. **Error Handling** - Implement try-catch patterns with scopes
3. **Idempotency** - Design playbooks to be safely re-runnable
4. **Logging** - Add comments to incidents for audit trails
5. **Testing** - Test in non-production before deployment

### Naming Conventions
```
Format: {Action}-{Target}-{Trigger}
Examples:
- Block-AADUser-Incident
- Enrich-IP-GreyNoise
- Notify-Teams-Alert
- Sync-JIRA-Incident
```

### Security Considerations
- Store API keys in Azure Key Vault
- Use managed identities where possible
- Rotate credentials regularly
- Audit access logs
- Never hardcode credentials

## Diagnostic Queries

```kusto
// Find playbook execution failures
AzureDiagnostics
| where ResourceType == "WORKFLOWS"
| where status_s == "Failed"
| project TimeGenerated, resource_workflowName_s, error_message_s
| order by TimeGenerated desc

// Track incident processing
SecurityIncident
| where TimeGenerated > ago(24h)
| where Comments contains "playbook"
| project TimeGenerated, IncidentNumber, Title, Comments
```

## References

- [Microsoft Sentinel Automation](https://docs.microsoft.com/azure/sentinel/automate-incident-handling-with-automation-rules)
- [Logic Apps Connectors](https://docs.microsoft.com/connectors/)
- [Managed Identity](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/)
- [Microsoft Graph Permissions](https://docs.microsoft.com/graph/permissions-reference)
- [Azure Sentinel GitHub Playbooks](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks)

## Source SOP

This specialist is based on: `SOP-Microsoft-Sentinel-SOAR-Playbooks.md`
