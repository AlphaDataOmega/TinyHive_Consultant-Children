# GitLab Engineering Architect Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/engineering/gitlab_engineering_architecture_sop.md`

## Core Knowledge Domains

### Scale Cube Model
- **X-axis (Cloning)**: Horizontal scaling through replication
- **Y-axis (Componentization)**: Decomposing by function or feature
- **Z-axis (Federation)**: Splitting by customer, geography, or data

### Key Abstractions
| Technology | Purpose |
|------------|---------|
| PostgreSQL | Primary data store |
| Redis | Caching and queues |
| NATS | Messaging/pub-sub |
| Sidekiq | Background jobs |
| Gitaly | Git operations |

### Four Golden Signals
1. **Latency** - Time to service requests
2. **Traffic** - Demand on the system
3. **Errors** - Rate of failed requests
4. **Saturation** - Resource utilization

### Architecture Design Workflow
1. Create design document
2. Identify stakeholders
3. Gather feedback
4. Document decisions (ADRs)
5. Implementation plan
6. Rollout strategy

## Related Consultants
- `sre_specialist` - Site reliability engineering
- `chaos_engineer` - Resilience testing
- `slo_engineer` - SLO design and monitoring
