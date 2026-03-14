# AI/ML Engineering Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/engineering/ai_ml_engineering_sop.md`

## AI Development Principles

| Principle | Description |
|-----------|-------------|
| Customer-first | Focus on user value |
| Responsible | Ethical AI use |
| Iterative | Small, measured releases |
| Monitored | Observable and measurable |
| Documented | Clear decision records |

## Model Development Lifecycle

| Phase | Activities |
|-------|------------|
| Discovery | Problem definition, data assessment |
| Development | Model training, validation |
| Deployment | Infrastructure, rollout |
| Monitoring | Performance tracking |
| Iteration | Improvements, retraining |

## Data Requirements

### Data Categories
| Category | Handling |
|----------|----------|
| Public data | Standard use |
| Internal data | Access controls |
| Customer data | Privacy requirements |
| PII | Anonymization required |

## LLM Integration Patterns

### Architecture
| Component | Role |
|-----------|------|
| AI Gateway | Provider abstraction |
| Prompt Templates | Standardized prompts |
| Response Handler | Output processing |
| Context Manager | Input management |

### Provider Management
| Provider | Use Case |
|----------|----------|
| Primary | Production traffic |
| Fallback | Reliability backup |
| Specialized | Specific tasks |

## AI Feature Rollout

### Phases
| Phase | Audience | Duration |
|-------|----------|----------|
| 1 | AI Team | 1-2 weeks |
| 2 | Employees | 2-4 weeks |
| 3 | Opt-out beta | 2-4 weeks |
| 4 | GA | Ongoing |

## Performance Metrics

### Latency SLOs
| Feature | Target (p95) |
|---------|--------------|
| Code Suggestions | < 1 second |
| Chat Response | < 3 seconds |
| Code Review | < 5 seconds |

### Quality Metrics
| Metric | Description |
|--------|-------------|
| Acceptance rate | % suggestions accepted |
| User satisfaction | CSAT/NPS scores |
| Error rate | % failed requests |
| Hallucination rate | % incorrect outputs |

## Responsible AI

### Ethical Principles
| Principle | Implementation |
|-----------|---------------|
| Fairness | Bias testing |
| Transparency | Explainability |
| Privacy | Data protection |
| Safety | Human oversight |
| Accountability | Decision audit |

## AI Infrastructure

| Component | Purpose |
|-----------|---------|
| AI Gateway | Request routing |
| Model Registry | Version control |
| Feature Store | Feature management |
| Monitoring | Observability |

## Related Consultants
- `enterprise_data_specialist` - Data engineering
- `software_development_specialist` - Development practices
- `monitoring_engineer` - Observability
