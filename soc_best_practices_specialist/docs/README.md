# SOC Best Practices Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/soc_best_practices_sop.md`

## Core Knowledge Domains

### SOC Metrics & KPIs
| Metric | Description | Target |
|--------|-------------|--------|
| MTTD | Mean Time to Detect | <1 hour |
| MTTT | Mean Time to Triage | <15 min |
| MTTC | Mean Time to Contain | <4 hours |
| MTTR | Mean Time to Resolve | <24 hours |

### Compliance Frameworks
| Framework | Focus |
|-----------|-------|
| NIST CSF | Risk management |
| CIS Controls v8 | Security controls |
| MITRE ATT&CK | Threat detection |
| NIS2 | EU directive |

### Mission-Critical Tools
| Category | Tools |
|----------|-------|
| SIEM | Splunk, Elastic, Sentinel |
| SOAR | Splunk SOAR, Cortex XSOAR |
| TIP | MISP, ThreatConnect |
| EDR | CrowdStrike, Defender |

### Detection Engineering Maturity
1. **Ad-hoc** - Reactive, vendor rules only
2. **Managed** - Documented use cases
3. **Defined** - Detection-as-code
4. **Measured** - Coverage metrics
5. **Optimizing** - Continuous improvement

### Threat Intelligence Lifecycle
1. Direction - Requirements gathering
2. Collection - Source data gathering
3. Processing - Data normalization
4. Analysis - Intelligence production
5. Dissemination - Sharing findings
6. Feedback - Continuous improvement

## Related Consultants
- `soc_analyst` - Day-to-day operations
- `soc_product_playbook_specialist` - Product playbooks
- `threat_intel_manager` - TI program
