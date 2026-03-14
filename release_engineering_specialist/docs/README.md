# Release Engineering Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/engineering/deployment_releases_sop.md`

## Release Cadence

### Versioning (SemVer)
| Component | When to Increment |
|-----------|-------------------|
| Major (X.0.0) | Breaking changes |
| Minor (0.X.0) | New features |
| Patch (0.0.X) | Bug fixes |

### Release Schedule
| Type | Frequency | Example |
|------|-----------|---------|
| Monthly | 22nd each month | 16.0, 16.1 |
| Patch | As needed | 16.0.1 |
| Security | As needed | 16.0.2 |
| Continuous | Multiple/day | GitLab.com |

## Deployment Strategies

| Strategy | Risk | Rollback | Use Case |
|----------|------|----------|----------|
| Canary | Low | Fast | Production testing |
| Blue-Green | Low | Instant | Zero-downtime |
| Rolling | Medium | Gradual | Large clusters |
| Big Bang | High | Complex | Simple apps |

### Canary Stages
| Stage | Traffic | Duration |
|-------|---------|----------|
| 1 | 1% | 30 min |
| 2 | 5% | 1 hour |
| 3 | 25% | 2 hours |
| 4 | 50% | 4 hours |
| 5 | 100% | Complete |

## Feature Flags

### Flag Lifecycle
| Phase | Actions |
|-------|---------|
| Development | Create flag, default off |
| Testing | Enable in staging |
| Rollout | Gradual % increase |
| GA | Enable 100% |
| Cleanup | Remove flag code |

### Flag Types
| Type | Lifespan | Purpose |
|------|----------|---------|
| Release | Weeks | New features |
| Ops | Permanent | Kill switches |
| Experiment | Days | A/B tests |

## Rollback Procedures

### Decision Criteria
| Metric | Threshold | Action |
|--------|-----------|--------|
| Error rate | > 2x baseline | Investigate |
| Error rate | > 5x baseline | Rollback |
| Latency p99 | > 3x baseline | Investigate |
| SLO breach | Any | Rollback |

### Rollback Steps
1. Decide (Incident Commander)
2. Communicate (Status page)
3. Execute (Deploy previous)
4. Verify (Monitor metrics)
5. Document (PIR)

## Production Readiness

### Pre-Deployment Checklist
- [ ] Code reviewed and merged
- [ ] Tests passing (unit, integration, e2e)
- [ ] Database migrations tested
- [ ] Feature flags configured
- [ ] Monitoring/alerts ready
- [ ] Runbook updated
- [ ] Rollback plan documented

### Post-Deployment Verification
| Time | Check |
|------|-------|
| 0-5 min | Basic health, no errors |
| 5-30 min | Error rates, latency |
| 30-60 min | Business metrics |
| 1-24 hours | Long-term stability |

## Related Consultants
- `engineering_oncall_specialist` - On-call management
- `chaos_engineer` - Resilience testing
- `sre_runbook_specialist` - Runbooks
