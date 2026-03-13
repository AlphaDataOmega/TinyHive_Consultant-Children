# Operations Runbook Engineer Documentation

## Overview

This documentation supports the operations_runbook_engineer consultant in creating and maintaining IT operations runbooks, procedures, and system documentation.

## Core Knowledge Areas

### Runbook Categories

| Category | Description | Examples |
|----------|-------------|----------|
| Incident Response | Guidelines for system failures | Service outage procedures, escalation paths |
| Troubleshooting | Diagnostic procedures | Log analysis, connectivity testing |
| Routine Maintenance | Regular operational tasks | Backups, updates, health checks |
| Disaster Recovery | Business continuity plans | Failover procedures, data recovery |
| Compliance | Regulatory procedures | Audit trails, security checks |

### Runbook Template Structure

Every runbook should include:

1. **Service Overview**
   - Service name and business purpose
   - Technical architecture overview
   - Service Level Agreements (SLAs)
   - Service owner and contact information
   - Dependencies and contributing applications

2. **System Documentation**
   - Hours of operation
   - Data and processing flows
   - Infrastructure and network design
   - Resilience and high availability configuration
   - Expected traffic and load patterns
   - Required resources (compute, storage, database)

3. **Security and Access Control**
   - Password and PII security measures
   - Ongoing security checks and CVE monitoring
   - Secrets management approach

4. **Operational Procedures**
   - Deployment processes
   - Batch processing schedules
   - Routine and sanity checks
   - Maintenance tasks (patching, log rotation, data cleardown)

5. **Monitoring and Alerting**
   - Log aggregation solution
   - Log message format
   - Metrics and health checks
   - Alerting thresholds

6. **Failover and Recovery**
   - Failover triggers and procedures
   - Recovery sequences
   - Verification steps

## Technology-Specific Runbooks

### Kubernetes Operations

#### Decoding Secrets
```sh
# List secrets
kubectl get secrets

# Extract secret value
kubectl get secret {{SECRET_NAME}} -o jsonpath='{.data.{{KEY}}}'

# Decode
echo '{{ENCODED_SECRET}}' | base64 --decode
```

**Security Note**: Clear terminal history after handling secrets.

### PostgreSQL Operations

#### Check Query History
```sql
-- Enable pg_stat_statements
CREATE EXTENSION pg_stat_statements;

-- Query history
SELECT * FROM pg_stat_statements;
```

#### Terminate Long-Running Queries
```sql
-- Find long-running queries
SELECT pid, now() - pg_stat_activity.query_start AS duration, query
FROM pg_stat_activity
WHERE state = 'active'
AND now() - pg_stat_activity.query_start > interval '5 minutes';

-- Cancel query (graceful)
SELECT pg_cancel_backend({{PID}});

-- Terminate query (forceful)
SELECT pg_terminate_backend({{PID}});
```

## Runbook Tools

| Tool | Description |
|------|-------------|
| Azure Automation | Process automation for Azure environments |
| Rundeck | Runbook automation with PagerDuty integration |
| Octopus Deploy | Runbook automation with CI/CD integration |
| Datadog Workflow | Automated remediation processes |

## Best Practices

1. **Use Standard Templates** - Maintain consistent format across all runbooks
2. **Encourage Discussion** - Have development teams own runbook activities
3. **Automate Checks** - Automate procedures where possible
4. **Keep Current** - Regular review and update cycles
5. **Mark Unknown Areas** - Clearly indicate missing information with WARNING
6. **Test Thoroughly** - Validate through tabletop exercises

## Maintenance Schedule

| Activity | Frequency | Owner |
|----------|-----------|-------|
| Review and update | Quarterly | Operations Team |
| Incident-based updates | After each incident | Incident Responder |
| Compliance review | Annually | Security/Compliance |
| Template updates | As needed | Documentation Team |

## References

- [SkeltonThatcher Run Book Template](https://github.com/SkeltonThatcher/run-book-template/)
- [Container Solutions Runbooks](https://containersolutions.github.io/runbooks/)
- [Prometheus Operator Runbooks](https://github.com/prometheus-operator/runbooks)
- [GitLab On-call Run Books](https://gitlab.com/gitlab-com/runbooks/)
