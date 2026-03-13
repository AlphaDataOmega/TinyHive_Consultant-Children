# TinyHive Consultant Children

Pre-built consultant agent scaffolds for TinyHive. Each consultant is a specialized child agent that can be spawned on-demand.

## Available Consultants

| Consultant | Purpose |
|------------|---------|
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
├── IDENTITY.md      # Agent identity and capabilities
├── crons/           # Scheduled tasks
├── docs/            # Reference documentation
├── memory/          # Persistent memory
├── projects/        # Active projects
├── scratch/         # Working area
└── subagents/       # Child agents
```

## Usage

Copy a consultant into your TinyHive `consultants/children/` directory:

```bash
cp -r incident_investigator /path/to/tinyhive/consultants/children/
```

Or clone and symlink:

```bash
git clone https://github.com/AlphaDataOmega/TinyHive_Consultant-Children.git
ln -s $(pwd)/TinyHive_Consultant-Children/incident_investigator /path/to/tinyhive/consultants/children/
```

## License

MIT
