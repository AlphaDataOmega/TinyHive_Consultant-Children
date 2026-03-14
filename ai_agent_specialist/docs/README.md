# AI Agent Specialist Documentation

## Overview

This consultant specializes in designing and architecting agents for the TinyHive agentic OS. The role encompasses creating agent definitions, planning hierarchies, and ensuring all agent behaviors comply with SPINE governance.

## TinyHive Agent Architecture

### Agent Types

| Type | Purpose | Examples |
|------|---------|----------|
| **MIND** | User interaction, task orchestration | ado_live_mind |
| **BODY** | Task execution via controllers | ado_live_body |
| **SPINE** | Governance, permissions, auditing | ado_live_spine |
| **Consultants** | Domain expertise, advisory | sre_specialist, testing_engineer |

### Agent Hierarchy

```
V (Human Owner)
└── SPINE (Governance)
    ├── Watchdog (monitoring)
    ├── Healer (recovery)
    ├── Auditor (compliance)
    ├── Archivist (documentation)
    ├── Guidance (advisory)
    └── Permissions (lease management)
└── MIND (Orchestration)
    └── Consultants (domain experts)
└── BODY (Execution)
    ├── controller_hub
    ├── controller_ssh
    └── controller_playwright
```

## IDENTITY.md Format

Every TinyHive agent requires an IDENTITY.md file with these sections:

### Required Sections

```markdown
# AGENT-NAME

Agent ID: `path/agent_name`
Parent: `parent_id` (PARENT_NAME)
Role: brief role description

## Purpose
What this agent does and why it exists.

## Responsibilities
1. **Area** — Description of responsibility

## Capabilities
- What the agent can do

## Constraints
- What the agent must not do
- Follow SPINE governance policies
```

### Optional Sections

```markdown
## Children
| Agent | Role | Purpose |
Table of child agents (for parent agents only)

## Message Routing
| Message Type | Route To |
Routing table (for parent agents only)

## Operating Pattern
How the agent wakes and operates (reactive, cron, etc.)

## Key Documents Managed
Files this agent is responsible for (for Archivist-like roles)
```

## Consultant Design Guidelines

Consultants are stateless domain experts that MIND can summon to assist V with specialized tasks.

### Consultant Characteristics

- **Advisory only** — Provide expertise and recommendations, no direct system access
- **Stateless** — No persistent memory between invocations
- **Domain-focused** — Deep expertise in a specific area
- **SPINE-compliant** — All recommendations respect governance policies

### Standard Consultant Structure

```
consultants/children/{consultant_name}/
├── IDENTITY.md          # Agent definition
└── docs/
    └── README.md        # Detailed documentation
```

### Responsibility Categories

1. **Analysis** — Examine situations, provide assessments
2. **Planning** — Create strategies, develop approaches
3. **Guidance** — Advise on best practices, recommend actions
4. **Documentation** — Help structure and write documents
5. **Review** — Evaluate work, identify issues

## Workflow Design Patterns

### Reactive Agents

Wake when messaged by parent or another agent:

```markdown
## Operating Pattern
- Primarily reactive — wakes when queried by other agents or parent
- Responds to specific message types routed by parent
```

### Cron-Based Agents

Wake on schedule for autonomous tasks:

```markdown
## Operating Pattern
- Wakes every {interval} via cron
- Performs {task}, reports findings to parent
- Escalates {conditions} to parent for V approval
```

### Event-Driven Agents

Wake in response to system events:

```markdown
## Operating Pattern
- Triggered by {event_type} events
- Processes event, takes action within lease permissions
- Logs all actions to lease chain
```

## Lease Integration

Agents requiring elevated permissions must request leases through the Permissions agent.

### Lease Request Pattern

1. Agent identifies need for elevated permission
2. Agent sends lease request to parent
3. Parent routes to SPINE → Permissions
4. Permissions evaluates against policy
5. If within threshold: auto-approve
6. If above threshold: escalate to V
7. Lease granted with expiration, logged to chain

### Constraint Examples

```markdown
## Constraints
- Cannot execute shell commands without active lease
- Must request lease for file modifications outside docs/
- Lease requests must include justification
- Follow SPINE governance policies
```

## Integration with TinyHive Core

### Controller Integration

Agents in BODY execute tasks via controllers:

| Controller | Purpose |
|------------|---------|
| controller_hub | Central task routing |
| controller_ssh | Remote shell execution |
| controller_playwright | Browser automation |
| controller_push | Notifications |
| controller_telegram | Telegram messaging |

### Message Flow

```
V → MIND → routes to appropriate agent/consultant
         → BODY for execution tasks
         → SPINE for governance questions

Agent → Parent → SPINE (for lease requests)
              → V (for escalations)
```

## Best Practices

1. **Clear boundaries** — Each agent has a focused purpose
2. **Explicit constraints** — State what agents cannot do
3. **Escalation paths** — Always define how to escalate to parent/V
4. **SPINE compliance** — All agents follow governance policies
5. **Minimal permissions** — Request only necessary lease scopes
6. **Documentation** — Maintain docs alongside IDENTITY.md
