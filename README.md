<p align="center">
  <img src="https://alphadataomega.com/tinyhive-logo.png" alt="TinyHive" width="80" />
</p>

<h1 align="center">TinyHive Consultant Children</h1>

<p align="center">
  <strong>Specialized AI Consultant Agents for TinyHive</strong><br>
  Pre-built expert agents that can be spawned on-demand.
</p>

---

## What Are Consultants?

Consultants are **specialized child agents** that provide expert capabilities in specific domains. Unlike general-purpose agents, consultants have:

- **Deep domain expertise** defined in their IDENTITY.md
- **Focused capabilities** for specific tasks
- **Reusable scaffolds** that can be fetched from GitHub

## Available Consultants

| Consultant | Expertise |
|------------|-----------|
| `compliance_officer` | Regulatory compliance, policy adherence, audit preparation |
| `content_contributor` | Content creation, documentation, copywriting |
| `expense_manager` | Expense tracking, budget analysis, financial reporting |
| `incident_investigator` | Security incident response, root cause analysis |
| `onboarding_specialist` | Employee/user onboarding, training coordination |
| `one_on_one_facilitator` | Meeting facilitation, 1:1 coaching support |
| `sre_specialist` | Site reliability, infrastructure, incident response |
| `testing_engineer` | QA, test automation, quality assurance |
| `variant_calling_specialist` | Genomic variant analysis, bioinformatics |

## Structure

Each consultant follows the standard TinyHive agent scaffold:

```
consultant_name/
├── IDENTITY.md      # Agent identity, expertise, and constraints
├── docs/
│   └── README.md    # Additional documentation
├── crons/           # Scheduled tasks
├── memory/          # Persistent memory
├── projects/        # Active projects
├── scratch/         # Working area
└── subagents/       # Child agents (if any)
```

## Installation

### Via TinyHive CLI

```bash
# List available consultants
python3 -m setup.registry_sync list consultants

# Fetch a specific consultant
python3 -m setup.registry_sync fetch consultant incident_investigator

# Sync all consultants from your consultants.json config
python3 -m setup.registry_sync sync consultants
```

### Manual

```bash
# Clone the repo
git clone https://github.com/AlphaDataOmega/TinyHive_Consultant-Children.git

# Copy a consultant to your TinyHive
cp -r TinyHive_Consultant-Children/incident_investigator \
      ~/.tinyhive/consultants/children/
```

### During Onboarding

When setting up TinyHive, the onboarding wizard lets you select consultants. They're added to your `config/consultants.json`:

```json
{
  "consultants": [
    {
      "id": "incident_investigator",
      "enabled": true,
      "fetched": false
    }
  ]
}
```

Run `registry_sync sync consultants` to fetch them.

## Creating Custom Consultants

### 1. Create the scaffold

```bash
mkdir -p my_consultant/{crons,memory,projects,scratch,subagents,docs}
```

### 2. Write IDENTITY.md

```markdown
# MY-CONSULTANT

Agent ID: `consultants/my_consultant`

## Role
Brief description of what this consultant does.

## Expertise
- Specific skill 1
- Specific skill 2
- Domain knowledge

## Capabilities
- What actions this consultant can perform
- Tools and methods available

## Constraints
- Boundaries and limitations
- What requires approval
- What is forbidden

## Working Style
How this consultant approaches problems.
```

### 3. Add to this repo (optional)

Submit a PR to share your consultant with the community.

## Integration with TinyHive

Consultants are spawned under the `consultants` domain:

```
~/.tinyhive/
└── consultants/
    └── children/
        ├── incident_investigator/
        ├── sre_specialist/
        └── your_consultant/
```

They can be invoked by MIND or other agents when specialized expertise is needed.

## Related Repositories

| Repo | Description |
|------|-------------|
| [tinyhive_v0-EX](https://github.com/AlphaDataOmega/tinyhive_v0-EX) | Standalone Linux edition |
| [TinyHive-Controllers](https://github.com/AlphaDataOmega/TinyHive-Controllers) | Controller integrations |

## License

MIT

---

<p align="center">
  Part of the <a href="https://github.com/AlphaDataOmega">TinyHive</a> ecosystem
</p>
