# Enterprise Data Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/data/enterprise_data_program_sop.md`

## Data Team Structure

### Hub & Spoke Model
| Component | Role |
|-----------|------|
| Hub (Data Team) | Platform, governance, enterprise models |
| Spokes (Functions) | Domain expertise, ad-hoc analysis |

### Data Team Pillars
| Team | Focus |
|------|-------|
| Analytics Engineering | Data models, transformations |
| Data Platform | Infrastructure, pipelines |
| Data Science | Advanced analytics, ML |
| Data Governance | Quality, catalog, policies |

## Data Platform Stack

| Layer | Technology |
|-------|------------|
| Warehouse | Snowflake |
| Transformations | dbt |
| Orchestration | Airflow |
| BI | Tableau |
| Catalog | Atlan |

### Data Layers
| Layer | Purpose |
|-------|---------|
| RAW | Source system extracts |
| PREP | Cleaned, standardized |
| PROD | Trusted, curated models |

## Data Governance

### Quality Dimensions
| Dimension | Description |
|-----------|-------------|
| Completeness | Required fields populated |
| Accuracy | Values are correct |
| Consistency | Matches across sources |
| Timeliness | Data is fresh |
| Uniqueness | No duplicates |

### Data Classification
| Level | Access |
|-------|--------|
| Public | Anyone |
| Internal | Employees |
| Confidential | Need to know |
| Restricted | Named individuals |

## Analytics Engineering

### Trusted Data Process
| Phase | Activities |
|-------|------------|
| Requirements | Define metrics, dimensions |
| Design | Model structure, relationships |
| Build | dbt models, tests |
| Review | Code review, validation |
| Deploy | Production release |

### Model Tiers
| Tier | SLA | Support |
|------|-----|---------|
| Tier 1 | 4 hours | Critical |
| Tier 2 | 8 hours | High |
| Tier 3 | 24 hours | Standard |

## Self-Service Analytics

### Access Tiers
| Tier | Capability |
|------|------------|
| Viewer | View dashboards |
| Explorer | Explore data |
| Creator | Build visualizations |
| Developer | Write SQL, models |

## Related Consultants
- `bioinformatics_analyst` - Scientific data
- `slo_engineer` - Metrics and SLOs
- `monitoring_engineer` - Observability data
