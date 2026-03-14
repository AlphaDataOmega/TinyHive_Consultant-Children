# Corporate IT Operations Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/it_operations/corporate_it_operations_sop.md`

## IT Service Management

### ITIL Processes
| Process | Purpose |
|---------|---------|
| Incident Management | Restore service quickly |
| Problem Management | Prevent recurring incidents |
| Change Management | Control infrastructure changes |
| Service Request | Handle standard requests |

### Support Tiers
| Tier | Scope | SLA Target |
|------|-------|------------|
| L1 | Basic issues, password resets | 4 hours |
| L2 | Complex issues, escalations | 8 hours |
| L3 | Engineering, root cause | 24 hours |

## Access Provisioning

### Provisioning Workflow
| Step | Action | Owner |
|------|--------|-------|
| 1 | Request submitted | Employee/Manager |
| 2 | Approval | Manager |
| 3 | Provisioning | IT Automation |
| 4 | Verification | IT Security |

### Deprovisioning Timeline
| Event | Action | Timeframe |
|-------|--------|-----------|
| Termination | Disable accounts | Immediate |
| Voluntary exit | Archive data | Same day |
| Account deletion | Remove all access | 30 days |

## Device Management

### Laptop Lifecycle
| Phase | Actions |
|-------|---------|
| Procurement | Standard specs, imaging |
| Deployment | MDM enrollment, user setup |
| Operations | Patch management, monitoring |
| Refresh | 3-4 year cycle |
| Decommission | Secure wipe, disposal |

### Endpoint Security
| Control | Tool |
|---------|------|
| MDM | JAMF (Mac), Intune (Windows) |
| EDR | CrowdStrike, Carbon Black |
| Encryption | FileVault, BitLocker |
| Antivirus | Integrated EDR |

## Identity and Access Management

### Okta Architecture
| Component | Function |
|-----------|----------|
| Universal Directory | Central identity store |
| SSO | Single sign-on |
| MFA | Multi-factor auth |
| Lifecycle Management | Automated provisioning |

### Authentication Standards
| Factor | Method |
|--------|--------|
| Primary | Password + SSO |
| Secondary | Authenticator app, hardware key |
| Recovery | Manager verification |

## Compliance Controls

### ITGC Framework
| Control Area | Examples |
|--------------|----------|
| Access Controls | Provisioning, reviews |
| Change Management | CAB, testing, rollback |
| Operations | Backup, monitoring |
| Security | Encryption, logging |

### User Access Reviews
| Frequency | Scope |
|-----------|-------|
| Quarterly | Critical systems |
| Semi-annual | Standard applications |
| Annual | All access |

## Cloud Services

### Multi-Cloud Strategy
| Provider | Primary Use |
|----------|-------------|
| GCP | Production infrastructure |
| AWS | Specific workloads |
| Azure | Microsoft integration |

## Related Consultants
- `cloud_security_engineer` - Cloud security
- `sre_runbook_specialist` - SRE operations
- `monitoring_engineer` - Observability
