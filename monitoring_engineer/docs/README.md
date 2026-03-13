# Monitoring Engineer Documentation

This directory contains reference materials and procedures for the monitoring_engineer consultant.

## Core Documents

| Document | Description |
|----------|-------------|
| SOP-IT-MonitoringAndAlerting | Standard Operating Procedure for monitoring and alerting design |

## Quick Reference

### Four Golden Signals

| Signal | Definition | Example Metrics |
|--------|------------|-----------------|
| **Latency** | Time to service a request | Response time, p50/p95/p99 |
| **Traffic** | Demand on the system | Requests per second, active connections |
| **Errors** | Rate of failed requests | HTTP 5xx rate, exception count |
| **Saturation** | System capacity utilization | CPU usage, memory pressure, queue depth |

### Alert Severity Levels

| Severity | Definition | Response Time | Notification Method |
|----------|------------|---------------|---------------------|
| **P1 - Critical** | Service down, data loss risk | Immediate (< 5 min) | Phone call, SMS |
| **P2 - High** | Significant degradation | < 30 minutes | Push notification |
| **P3 - Medium** | Minor degradation | < 4 hours | Email, Slack |
| **P4 - Low** | No immediate impact | Next business day | Ticket creation |

### Standard Monitoring Stack

| Component | Tool Options | Purpose |
|-----------|--------------|---------|
| Metrics Collection | Prometheus, CloudWatch, Datadog | Time-series data storage |
| Log Aggregation | ELK Stack, CloudWatch Logs, Splunk | Centralized logging |
| Distributed Tracing | Jaeger, X-Ray, Zipkin | Request flow tracking |
| Dashboards | Grafana, CloudWatch Dashboards | Visualization |
| Alerting | PagerDuty, Opsgenie, AlertManager | Notification routing |

### Metric Types

1. **Counters** - Monotonically increasing values (requests, errors)
2. **Gauges** - Point-in-time values (temperature, queue size)
3. **Histograms** - Distribution of values (response time buckets)
4. **Summaries** - Pre-calculated quantiles (p50, p95, p99)

### Dashboard Design Layers

```
Layer 1: Executive Overview
  - SLO compliance status
  - System health summary
  - Active incidents

Layer 2: Service Health
  - Per-service latency, error rate, throughput
  - Dependency health
  - Resource utilization

Layer 3: Deep Dive
  - Detailed metrics for debugging
  - Log integration
  - Trace exploration
```

### Alert Configuration Required Fields

- Alert name (clear, descriptive)
- Severity level
- Condition/threshold
- Duration (avoid flapping)
- Runbook link
- Impact description
- Escalation path

### Alert Anti-Patterns to Avoid

| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| Alerting on causes | Miss user impact | Alert on symptoms/SLIs |
| No thresholds | Alert fatigue | Set meaningful thresholds |
| Missing runbooks | Slow response | Every alert needs a runbook |
| Too many alerts | Responder burnout | Consolidate and prioritize |
| Alerting on normal | Noise | Adjust thresholds to actual issues |

## Procedures

### Setting Up Monitoring

1. **Define Requirements** - Identify critical services, define SLIs, set SLO targets
2. **Deploy Infrastructure** - Set up Prometheus, Grafana, AlertManager stack
3. **Configure Metrics Collection** - Deploy exporters, configure scrape intervals
4. **Create Dashboards** - Build executive, service, and troubleshooting views
5. **Configure Alerts** - Define rules, set up notifications, create runbooks

### Validation Checklist

Before considering monitoring implementation complete:

- [ ] All critical services have metrics exported
- [ ] Four golden signals are captured for each service
- [ ] SLI dashboards are created and accessible
- [ ] Alert rules are defined with appropriate thresholds
- [ ] Every alert has an associated runbook
- [ ] Notification channels are configured and tested
- [ ] Log aggregation is operational
- [ ] Distributed tracing is implemented for key flows
- [ ] Validation scripts pass all checks
- [ ] Team is trained on dashboard and alert usage

## Resources

### Industry Standards
- Google SRE Book (free online)
- The Art of Monitoring by James Turnbull
- Prometheus: Up & Running by Brian Brazil

### Tool Documentation
- Prometheus: https://prometheus.io/docs/
- Grafana: https://grafana.com/docs/
- AlertManager: https://prometheus.io/docs/alerting/latest/alertmanager/
- PagerDuty: https://support.pagerduty.com/
