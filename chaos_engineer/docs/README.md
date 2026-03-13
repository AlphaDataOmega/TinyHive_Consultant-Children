# Chaos Engineer Documentation

This directory contains reference materials and operational guides for chaos engineering and toil automation practices.

## Core Competencies

### Chaos Engineering

Chaos engineering is the discipline of experimenting on a system to build confidence in its capability to withstand turbulent conditions in production. Key concepts include:

- **Steady State Hypothesis** — Define normal operating behavior using measurable metrics
- **Blast Radius** — Control the scope of impact during experiments
- **Fault Injection** — Deliberate introduction of failures to test resilience
- **Game Days** — Scheduled events for practicing failure response

### Toil Automation

Toil is manual, repetitive, automatable work that scales linearly with service size and lacks enduring value. The goal is to maintain toil below 50% of team time.

## Experiment Categories

| Category | Examples |
|----------|----------|
| Infrastructure | Server shutdown, disk failure, memory exhaustion |
| Network | Latency injection, packet loss, DNS failures |
| Application | Service dependency failures, database unavailability |
| State | Corrupted data, clock skew, certificate expiration |
| Load | Traffic spikes, resource exhaustion |

## Automation Levels

1. **Script Automation** — Replace manual commands with version-controlled scripts
2. **Scheduled Automation** — Use cron, systemd timers, or job schedulers
3. **Event-Driven Automation** — Trigger on alerts, deployments, or requests
4. **Self-Healing Systems** — Automatic remediation without human intervention

## Tooling

### Chaos Engineering Tools
- Chaos Monkey (Netflix)
- Gremlin
- Litmus (Kubernetes-native)
- Chaos Toolkit (open-source)

### Automation Solutions
| Task Category | Solution |
|---------------|----------|
| Certificate management | Let's Encrypt + cert-manager |
| User provisioning | SCIM + Identity Provider |
| Backup management | Velero, AWS Backup |
| Log rotation | logrotate + monitoring |
| Capacity scaling | Horizontal Pod Autoscaler |
| Incident response | PagerDuty + Rundeck |

## Related SOPs

- SOP-Chaos-Engineering-and-Toil-Automation.md
- SRE-INC-001: Incident Management SOP
- SRE-SLO-001: SLI/SLO/SLA Definition SOP
- SRE-RUN-001: Runbook Writing SOP

## References

- [Principles of Chaos Engineering](https://principlesofchaos.org/)
- [Google SRE Book - Eliminating Toil](https://sre.google/sre-book/eliminating-toil/)
- [Chaos Toolkit Documentation](https://chaostoolkit.org/)
- [Netflix Chaos Engineering](https://netflixtechblog.com/tagged/chaos-engineering)
