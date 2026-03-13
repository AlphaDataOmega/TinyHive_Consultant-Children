# SLO Engineer Documentation

## Overview

This consultant specializes in Service Level Objectives (SLOs) and Error Budget management, forming the foundation of Site Reliability Engineering practices. The SLO Engineer enables organizations to make data-driven decisions about system reliability and balance feature development with reliability investments.

## Core Concepts

### Service Level Indicators (SLIs)

Quantitative measures of service behavior that answer: "How is our service performing right now?"

| SLI Type | Use Case | Example Metric |
|----------|----------|----------------|
| **Availability** | Service uptime | Percentage of successful requests |
| **Latency** | Response time | 95th percentile response time |
| **Throughput** | Capacity | Requests per second |
| **Error Rate** | Quality | Percentage of failed requests |
| **Durability** | Data integrity | Data loss rate over time |

### Service Level Objectives (SLOs)

Target values for SLIs that define acceptable service behavior. They answer: "What level of performance is acceptable?"

| Availability Target | Monthly Error Budget | Suitable For |
|---------------------|---------------------|--------------|
| 99.0% | 7.2 hours | Internal tools, dev environments |
| 99.5% | 3.6 hours | Non-critical business services |
| 99.9% | 43.8 minutes | Customer-facing applications |
| 99.95% | 21.9 minutes | E-commerce, financial services |
| 99.99% | 4.38 minutes | Critical infrastructure |

### Service Level Agreements (SLAs)

Contractual obligations between service providers and customers, typically with financial or business consequences for violations.

### Error Budgets

The acceptable amount of unreliability, derived from SLOs:

```
Error Budget = (1 - SLO Target) x Time Window
```

Example for 99.9% SLO over 30 days:
```
Error Budget = (1 - 0.999) x 30 days = 0.03 days = 43.2 minutes
```

## Key Terminology

| Term | Definition |
|------|------------|
| **SLI** | A quantitative measure of service performance (e.g., latency, availability) |
| **SLO** | The target value or range for an SLI that defines acceptable behavior |
| **SLA** | A contractual commitment to customers with consequences for violations |
| **Error Budget** | The allowed amount of unreliability (100% minus SLO target) |
| **Budget Burn Rate** | How quickly the error budget is being consumed |
| **Toil** | Manual, repetitive operational work that should be automated |

## Implementation Guidance

### Defining SLIs

1. **Identify Critical User Journeys** — Document primary user actions (login, search, checkout)
2. **Map Backend Services** — Link user actions to services and dependencies
3. **Select SLI Types** — Choose metrics that reflect user experience

Example Prometheus recording rule:
```yaml
groups:
  - name: sli_recording_rules
    rules:
      - record: sli:availability:ratio
        expr: |
          sum(rate(http_requests_total{status=~"2.."}[5m]))
          /
          sum(rate(http_requests_total[5m]))
```

### Establishing SLOs

1. **Analyze Historical Data** — Review past performance for realistic targets
2. **Set Initial Targets** — Start conservative, adjust based on evidence
3. **Document Specifications** — Create SLO documents for each service

Example SLO specification:
```yaml
service: payment-api
slos:
  - name: availability
    description: "Payment API responds successfully to requests"
    sli: sli:availability:ratio
    target: 0.999
    window: 30d

  - name: latency
    description: "95th percentile response time"
    sli: histogram_quantile(0.95, http_request_duration_seconds_bucket)
    target: 200ms
    window: 30d
```

### Error Budget Policies

| Budget Remaining | Status | Actions |
|-----------------|--------|---------|
| > 50% | Green | Normal development velocity |
| 25-50% | Yellow | Review recent changes, increase monitoring |
| 10-25% | Orange | Freeze non-critical deployments |
| < 10% | Red | All hands on reliability, no new features |

### Risk Assessment

Before any change, evaluate its impact:

```
Risk Score = (Probability of Failure) x (Impact Duration) x (Affected Users %)
```

| Risk Score | Approval Required | Testing Requirements |
|------------|-------------------|---------------------|
| Low (< 0.1%) | Team lead | Unit tests |
| Medium (0.1-1%) | SRE review | Integration + load tests |
| High (1-5%) | Engineering director | Full regression + canary |
| Critical (> 5%) | VP approval | Staged rollout with rollback |

## Common Mistakes

| Mistake | Symptom | Fix |
|---------|---------|-----|
| Setting unrealistic SLOs | Constant alerts, ignored budgets | Use historical data to set achievable targets |
| Too many SLIs | Alert fatigue, unclear priorities | Focus on 3-5 critical user journey metrics |
| Not including dependencies | SLO violations from external causes | Track dependency SLIs separately |
| Ignoring error budget | Feature velocity disconnected from reliability | Enforce budget policies in deployment pipeline |

## References

- [Google SRE Book - Service Level Objectives](https://sre.google/sre-book/service-level-objectives/)
- [SLO Generator](https://github.com/google/slo-generator)
- [Prometheus SLO Recording Rules](https://prometheus.io/docs/practices/rules/)

## Source SOP

This consultant is based on: `SOP-SRE-Service-Level-Objectives-Error-Budgets.md`
