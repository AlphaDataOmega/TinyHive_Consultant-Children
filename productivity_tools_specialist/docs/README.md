# Productivity Tools Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/it_operations/productivity_tools_sop.md`

## Tool Selection Criteria

### Security Requirements
| Requirement | Priority |
|-------------|----------|
| SSO integration | Required |
| 2FA support | Required |
| Data encryption | Required |
| SOC 2 compliance | Preferred |
| GDPR compliance | Required (EU data) |

### Evaluation Factors
| Factor | Weight |
|--------|--------|
| Security | High |
| Integration | High |
| Usability | Medium |
| Cost | Medium |
| Support | Medium |

## Core Tool Stack

### Communication
| Tool | Purpose |
|------|---------|
| Slack | Real-time messaging |
| Gmail | Email |
| Zoom | Video conferencing |
| Loom | Async video |

### Productivity
| Tool | Purpose |
|------|---------|
| Google Calendar | Scheduling |
| Google Docs | Documentation |
| Google Sheets | Spreadsheets |
| Google Slides | Presentations |

### Security
| Tool | Purpose |
|------|---------|
| 1Password | Password management |
| YubiKey | Hardware 2FA |
| VPN | Network security |

## 2FA Methods (Priority Order)

| Method | Security Level |
|--------|----------------|
| FIDO2/YubiKey | Highest |
| Push notification | High |
| TOTP authenticator | Medium |
| SMS | Low (avoid) |

## Browser Extensions (Approved)

| Extension | Purpose |
|-----------|---------|
| uBlock Origin | Ad blocking |
| 1Password | Password fill |
| OneTab | Tab management |

## Platform Tools

### macOS
| Tool | Purpose |
|------|---------|
| Alfred/Raycast | Launcher |
| Rectangle | Window management |
| Paste | Clipboard history |
| Stream Deck | Automation |

### Linux
| Tool | Purpose |
|------|---------|
| Docker | Containers |
| VS Code | Editor |
| Terminal | CLI |

## Calendar Best Practices

| Practice | Benefit |
|----------|---------|
| Set working hours | Protect boundaries |
| Use Speedy Meetings | 5-10 min buffer |
| Block focus time | Deep work |
| Share calendar | Transparency |

## Onboarding Checklist

### Day 1
- [ ] Google Workspace access
- [ ] Slack configured
- [ ] 1Password setup
- [ ] 2FA enabled
- [ ] Calendar configured

### Week 1
- [ ] All tools provisioned
- [ ] Training completed
- [ ] Shortcuts learned
- [ ] Workflow established

## Related Consultants
- `corporate_it_operations_specialist` - IT operations
- `remote_communication_specialist` - Communication
- `documentation_standards_specialist` - Documentation
