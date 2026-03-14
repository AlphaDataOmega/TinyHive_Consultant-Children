# Software Development Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/engineering/software_development_practices_sop.md`

## Development Principles

| Principle | Description |
|-----------|-------------|
| Iteration | Small, frequent changes |
| Efficiency | Optimize for outcomes |
| Simplicity | KISS principle |
| Reliability | Build resilient systems |
| Velocity | Ship frequently |
| Quality | Right the first time |
| Predictability | Consistent delivery |

## Code Review Process

### Response SLOs
| Type | SLO |
|------|-----|
| Standard MR | 2 business days |
| Urgent MR | 4 hours |
| Security fix | Immediate |

### Review Roles
| Role | Authority |
|------|-----------|
| Reviewer | Approve code quality |
| Maintainer | Merge authority |
| CODEOWNER | Required approval |

## Merge Request Workflow

### MR Requirements
- [ ] Tests passing
- [ ] Code reviewed
- [ ] Documentation updated
- [ ] Security considered
- [ ] Performance verified

### Broken Master SLOs
| Phase | SLO |
|-------|-----|
| Triage | 4 hours |
| Resolution | 4 hours |
| Total | 8 hours max |

## Required Approvals

| Change Type | Approvers |
|-------------|-----------|
| Backend | Backend maintainer |
| Frontend | Frontend maintainer |
| Database | Database maintainer |
| API | API owner |
| Security | AppSec team |

## Testing Requirements

### Test Pyramid
| Layer | Quantity | Speed |
|-------|----------|-------|
| Unit | Many | Fast |
| Integration | Some | Medium |
| E2E | Few | Slow |

### Coverage Targets
| Type | Target |
|------|--------|
| Backend | 80-90% |
| Frontend | 70-80% |
| Critical paths | 100% |

## Security Practices

### Severity SLOs
| Severity | Resolution |
|----------|------------|
| Critical | Immediate |
| High | 30 days |
| Medium | 90 days |
| Low | 180 days |

### Required Scans
- SAST (Static analysis)
- Dependency scanning
- Secret detection
- DAST (Dynamic analysis)
- Container scanning

## Technical Debt

### Capacity Allocation
| Activity | % Time |
|----------|--------|
| Feature development | 70-80% |
| Tech debt | 20-30% |

### Prioritization
| Quadrant | Priority |
|----------|----------|
| High impact, low effort | Do first |
| High impact, high effort | Plan |
| Low impact, low effort | Quick wins |
| Low impact, high effort | Avoid |

## Related Consultants
- `release_engineering_specialist` - Deployments
- `engineering_oncall_specialist` - Operations
- `software_engineering_lead` - Team leadership
