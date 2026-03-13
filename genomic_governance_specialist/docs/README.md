# Genomic Governance Specialist Documentation

This directory contains reference materials and operational guidance for the Genomic Governance Specialist agent.

## Domain Overview

The Genomic Governance Specialist operates within the European Genomic Data Infrastructure (GDI) framework, supporting the 1+ Million Genomes (1+MG) initiative. This domain encompasses genomic data governance, data access committee operations, and SOP lifecycle management across European nodes.

## Core Knowledge Areas

### 1. GDI Framework and Structure

The European GDI project enables access to genomic, phenotypic, and clinical data across Europe. The infrastructure supports:

- **European-level operations**: Standardized procedures applied uniformly across all nodes
- **Node-specific implementations**: Templates adapted by individual GDI nodes
- **Repository structure**: SOPs organized in `sops/european-level/` and `sops/node-specific/` directories

### 2. Organizational Roles

| Role | Level | Primary Function |
|------|-------|------------------|
| Author | European/Node | Write SOP content, ensure compliance |
| Reviewer | European/Node | Review accuracy and consistency |
| Approver | European/Node | Confirm readiness, manage lifecycle |
| Authoriser | European | Grant official permission for releases |
| Main Repository Maintainer | European | Oversee creation, version control |
| Trainer | European/Node | Conduct SOP training |
| Node SOP Maintainer | Node | Monitor updates, ensure alignment |

### 3. SOP Lifecycle

#### Creation Workflow

1. OC/SDPC evaluates SOP request
2. Template shared with authors
3. Draft reviewed internally
4. OC/SDPC approval
5. Management Board authorization
6. SOP accessioning
7. Periodic review cycle initiated

#### Naming Conventions

- **European-level**: `GDI-SOPXXXX.vY` (e.g., `GDI-SOP0003.v1`)
- **Node templates**: `GDI-SOPXXXX.vY`
- **Node instances**: `GDI-SOPXXXX.vY_<NodeID>.vZ` (e.g., `GDI-SOP0001.v1_SWE.v1`)

### 4. Data Access Committee Operations

#### 1+MG DAC Recommendation Process

1. Application received and checked within 5 working days
2. Application marked as 'Recommended for Approval'
3. NCPs notified with 10 working day response window
4. Approval confirmed or NCP review process initiated
5. Data requestor informed of decision

#### Application Check Criteria

- Institutional sign-off (if applicable)
- Data analysis plan present and suitable
- Data minimisation principle met
- Algorithms suitable and transparent
- Ethical approval obtained
- Funding mechanisms in place
- Project description corresponds with data analysis plan

### 5. NCP Veto Process

When National Coordination Points (NCPs) identify concerns:

1. NCP distributes application recommendation to Data Holders and Permit Authorities
2. Veto justification communicated within 1 working day
3. 1+MG DAC reviews justification
4. Decision communicated to all parties
5. Consensus building process initiated if needed

### 6. Key Committees and Communication

#### Committees

- **Operations Committee (OC)**: `gdi-oc [at] elixir-europe.org`
- **Security and Data Protection Committee (SDPC)**: `gdi-sdpc [at] elixir-europe.org`
- **Management Board (MB)**: `gdi-mb [at] elixir-europe.org`

#### Communication Channels

- Slack: wp4-sop-discussions, wp4-european_level_operations
- GitHub Issues: Change requests
- GitHub Discussions: RFCs and community feedback

## SOP Template Structure

Every SOP must include:

1. **Metadata Table** (required)
2. **Index** (required)
3. **Document History** (required)
4. **Glossary** (required)
5. **Roles and Responsibilities** (required)
6. **Purpose** (required)
7. **Scope** (required)
8. Introduction and Background Information
9. Summary or Context Diagram
10. **Procedure** (required)
11. **References** (required)

## Review Checklist Categories

1. **Document Structure & Formatting**: Template compliance, consistency, metadata accuracy
2. **Content Completeness**: Purpose, scope, roles, procedures, references
3. **Clarity & Usability**: Language, terminology, glossary, examples
4. **Operational Feasibility**: Applicability, scalability, role feasibility
5. **Cross-Referencing**: No overlap, related SOP references, compliance

## Key Abbreviations

| Abbreviation | Description |
|--------------|-------------|
| 1+MG | 1+ Million Genomes |
| DAC | Data Access Committee |
| DPIA | Data Protection Impact Assessment |
| EDIC | European Digital Infrastructure Consortium |
| ELSI | Ethical, Legal, and Social Implications |
| FAIR | Findable, Accessible, Interoperable, Reusable |
| GDI | European Genomic Data Infrastructure |
| NCP | National Coordination Point |
| OC | Operations Committee |
| QMS | Quality Management System |
| RFC | Request For Comments |
| SDPC | Security and Data Protection Committee |
| SOP | Standard Operating Procedure |

## References

- [GDI SOP Repository](https://github.com/GenomicDataInfrastructure/standard-operating-procedures)
- [1+MG Framework](https://framework.onemilliongenomes.eu/)
- [GDI Zenodo Community](https://zenodo.org/communities/gdi/records)
- [FitSM Standards](https://www.fitsm.eu/)
