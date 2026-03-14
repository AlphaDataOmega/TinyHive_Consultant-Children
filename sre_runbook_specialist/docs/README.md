# SRE Runbook Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/it_operations/sre_runbooks_sop.md`

## Core Knowledge Domains

### SLI/SLO/SLA Framework
| Term | Definition |
|------|------------|
| SLI | Service Level Indicator (metric) |
| SLO | Service Level Objective (target) |
| SLA | Service Level Agreement (contract) |
| Error Budget | Allowed unreliability |

### Common SLIs
| Type | Metric |
|------|--------|
| Availability | % uptime |
| Latency | p50, p95, p99 |
| Throughput | Requests/sec |
| Error Rate | % failed requests |

### Error Budget Calculation
```
Error Budget = 1 - SLO
Example: 99.9% SLO = 0.1% error budget
= 43.8 minutes/month downtime allowed
```

### Runbook Structure
1. **Overview** - Service description
2. **Prerequisites** - Access, tools needed
3. **Symptoms** - How to identify the issue
4. **Diagnosis** - Investigation steps
5. **Resolution** - Fix procedures
6. **Escalation** - When to escalate
7. **Post-resolution** - Cleanup steps

### Incident Severity
| Level | Description | Response |
|-------|-------------|----------|
| P1 | Critical outage | All hands |
| P2 | Major degradation | On-call + backup |
| P3 | Minor impact | On-call |
| P4 | Low priority | Next business day |

### Deployment Strategies
| Strategy | Risk | Rollback |
|----------|------|----------|
| Blue-Green | Low | Instant |
| Canary | Low | Quick |
| Rolling | Medium | Gradual |
| Big Bang | High | Complex |

## Related Consultants
- `slo_engineer` - SLO design
- `monitoring_engineer` - Observability
- `chaos_engineer` - Resilience testing
