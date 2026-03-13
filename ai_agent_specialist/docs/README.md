# AI Agent Specialist Documentation

## Overview

This consultant specializes in AI agent workflows, prompt engineering, and LLM-assisted development. The role encompasses designing structured procedures that enable AI agents to perform complex tasks reliably and reproducibly.

## Core Competencies

### Agent SOP Development

Agent SOPs (Standard Operating Procedures) are markdown-based instruction sets that guide AI agents through sophisticated workflows. Key features include:

- **Natural Language Workflows**: Plain English instructions requiring no prompt engineering expertise
- **Parameterized Inputs**: Flexible reuse across different contexts and projects
- **RFC 2119 Constraints**: MUST, SHOULD, MAY keywords for precise behavioral control
- **Progress Tracking**: Document progress for transparency and resumability

### Available SOP Types

| SOP | Purpose | Use Cases |
|-----|---------|-----------|
| **codebase-summary** | Comprehensive codebase analysis and documentation | Project onboarding, documentation creation, system understanding |
| **pdd** | Prompt-driven development methodology | Complex problem solving, architectural decisions, system design |
| **code-task-generator** | Intelligent task breakdown and planning | Project planning, sprint preparation, requirement analysis |
| **code-assist** | TDD-based code implementation | Feature development, bug fixes, refactoring |
| **eval** | Automated evaluation workflow for AI agents | Evaluation planning, test data generation, result analysis |

## Directory Structure Standards

```
.agents/
├── summary/               # codebase-summary output (always commit)
│   └── *.md
├── planning/              # pdd output (often worth committing)
│   └── {project_name}/
│       ├── rough-idea.md
│       ├── idea-honing.md
│       ├── research/
│       ├── design/
│       └── implementation/
├── tasks/                 # code-task-generator output (optionally commit)
│   └── {project_name}/
│       └── step01/
│           └── task-*.code-task.md
└── scratchpad/            # code-assist working files (add to .gitignore)
    └── {project_name}/
        └── {task_name}/
```

## SOP Format Specification

### Required Sections

1. **Title**: `# SOP Name`
2. **Overview**: Concise description of purpose and use cases
3. **Parameters**: Required and optional inputs with descriptions
4. **Steps**: Workflow steps with RFC 2119 constraints
5. **Examples**: Concrete usage scenarios (recommended)
6. **Troubleshooting**: Common issues and resolutions (recommended)

### RFC 2119 Keywords

| Keyword | Meaning |
|---------|---------|
| **MUST** / **REQUIRED** | Absolute requirement |
| **MUST NOT** / **SHALL NOT** | Absolute prohibition |
| **SHOULD** / **RECOMMENDED** | Strong recommendation (may have exceptions) |
| **SHOULD NOT** / **NOT RECOMMENDED** | Strong discouragement (may have exceptions) |
| **MAY** / **OPTIONAL** | Truly optional behavior |

### Constraint Best Practices

Always provide context for negative constraints:

**Good:**
```markdown
- You MUST NOT use ellipses (...) because your output will be read aloud by text-to-speech
- You MUST NOT run `git push` because this could publish unreviewed code
```

**Bad:**
```markdown
- You MUST NOT use ellipses
- You MUST NOT run git push
```

## Workflow Methodologies

### Code Assist Workflow (TDD-Based)

1. **Setup**: Initialize project environment and directory structures
2. **Explore Phase**: Analyze requirements, research patterns, create context document
3. **Plan Phase**: Design test strategy, create implementation plan
4. **Code Phase**: Implement tests first, then code following RED -> GREEN -> REFACTOR
5. **Commit Phase**: Follow Conventional Commits, document in progress.md

### Prompt-Driven Development (PDD)

1. **Create Project Structure**: Set up directories for research, design, implementation
2. **Initial Process Planning**: Clarify starting approach with user
3. **Requirements Clarification**: Ask ONE question at a time, document in idea-honing.md
4. **Research**: Document findings with mermaid diagrams and references
5. **Iteration Checkpoint**: Summarize and confirm readiness to proceed
6. **Detailed Design**: Create comprehensive design document
7. **Implementation Plan**: Develop checklist-based implementation steps
8. **Summary**: Present all artifacts and suggested next steps

### Evaluation Framework

1. **Planning**: Analyze agent, design evaluation strategy, define metrics
2. **Test Data Generation**: Generate test cases in JSONL format
3. **Evaluation Execution**: Implement and run evaluation pipeline
4. **Analysis and Reporting**: Generate comprehensive eval-report.md

## Integration Options

### MCP Server
```bash
strands-agents-sops mcp --sop-paths ~/custom-sops
```

### Anthropic Skills
```bash
strands-agents-sops skills --output-dir ./skills
```

### Cursor IDE
```bash
strands-agents-sops commands --type cursor --output-dir .cursor/commands
```

### Python SDK
```python
from strands import Agent
from strands_tools import editor, shell
from strands_agents_sops import code_assist

agent = Agent(
    system_prompt=code_assist,
    tools=[editor, shell]
)
```

## Best Practices

1. **Keep Steps Focused**: Each step accomplishes one clear objective
2. **Use Clear Constraints**: Be specific about requirements vs recommendations
3. **Provide Examples**: Show concrete usage for complex workflows
4. **Natural Language**: Write descriptions that are easy to understand
5. **Specify Artifacts**: Include file paths for all created artifacts
6. **Include Troubleshooting**: Anticipate common issues with resolution steps

## References

- [Strands Agents Documentation](https://strandsagents.com/)
- [RFC 2119 Keywords](https://datatracker.ietf.org/doc/html/rfc2119)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Anthropic Skills](https://support.claude.com/en/articles/12512176-what-are-skills)
