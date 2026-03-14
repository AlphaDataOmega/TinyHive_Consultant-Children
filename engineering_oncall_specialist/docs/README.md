# Engineering On-Call Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/engineering/engineering_oncall_sop.md`

## On-Call Rotation Structure

### Rotation Types
| Type | Coverage | Best For |
|------|----------|----------|
| Follow-the-sun | 24/7, regional | Global teams |
| Primary/Secondary | 24/7, backup | Small teams |
| Weekly rotation | 7 days | Most teams |
| Daily rotation | 24 hours | High load |

### Rotation Tiers
| Tier | Role | Escalation |
|------|------|------------|
| Tier 1 | Primary on-call | First responder |
| Tier 2 | Secondary/backup | If T1 unavailable |
| Tier 3 | Manager | 15 min no response |
| Tier 4 | Executive | S1 incidents |

## Incident Severity

| Severity | Impact | Response | Resolution |
|----------|--------|----------|------------|
| S1 | Complete outage | Immediate | 4 hours |
| S2 | Major degradation | 15 min | 8 hours |
| S3 | Minor impact | 30 min | 24 hours |
| S4 | Low priority | 4 hours | 72 hours |

### Classification Criteria
| Factor | Questions |
|--------|-----------|
| Users affected | How many? All, subset, few? |
| Revenue impact | Is billing affected? |
| Data loss | Is data at risk? |
| Security | Is there a breach? |

## Incident Response Phases

| Phase | Activities |
|-------|------------|
| Detect | Alert triggers, validation |
| Respond | Acknowledge, assess severity |
| Mitigate | Stop bleeding, reduce impact |
| Resolve | Root cause fix |
| Review | Post-incident analysis |

## Communication

### During Incident
| Channel | Audience | Frequency |
|---------|----------|-----------|
| War room | Responders | Continuous |
| Status page | Customers | Every 30 min |
| Slack | Internal | As needed |
| Executives | Leadership | S1/S2 hourly |

## Post-Incident Review

### Blameless Culture
| Do | Don't |
|----|-------|
| Focus on systems | Blame individuals |
| Ask "what" and "how" | Ask "who" |
| Find improvements | Find fault |
| Share learnings | Hide mistakes |

### 5 Whys Template
1. Why did the incident occur?
2. Why did that happen?
3. Why did that happen?
4. Why did that happen?
5. Why did that happen? (Root cause)

## On-Call Compensation

| Component | Rate |
|-----------|------|
| Weekly stipend | $500-750 |
| Incident response | 1.5-2.5x hourly |
| TOIL | Hour for hour |

## Related Consultants
- `sre_runbook_specialist` - SRE runbooks
- `monitoring_engineer` - Observability
- `incident_response_lead` - Security incidents
