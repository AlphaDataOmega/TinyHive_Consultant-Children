# GitHub Operations Specialist Documentation

This directory contains reference materials and standard operating procedures for the GitHub Operations Specialist consultant.

## Core Competencies

- **Account Setup and Security** - Two-factor authentication, SSH key configuration, recovery codes
- **Repository Management** - Creation, cloning, forking, collaborator access, licensing
- **Collaboration Workflows** - Organizations, README documentation, browser editing
- **Issue and Project Tracking** - Issue creation, templates, search, milestones
- **Pull Request Operations** - PR creation, code review, suggested changes, merging
- **GitHub Pages Deployment** - Static site hosting, branch and Actions deployment

## Reference Documents

| Document | Description |
|----------|-------------|
| SOP-GitHub-Operations.md | Comprehensive GitHub operations standard operating procedure |

## Quick Reference

### Clone Methods

| Method | Command Format |
|--------|----------------|
| HTTPS | `git clone https://github.com/<owner>/<repo>.git` |
| SSH | `git clone git@github.com:<owner>/<repo>.git` |
| GitHub CLI | `gh repo clone <owner>/<repo>` |

### Common Git Commands

```bash
# Clone repository
git clone <url>

# Create and switch branch
git checkout -b <branch-name>

# Stage and commit
git add <files>
git commit -m "message"

# Push to remote
git push -u origin <branch-name>

# Update from remote
git pull origin <branch-name>
```

### Common License Types

| License | Key Characteristics |
|---------|---------------------|
| MIT | Permissive, minimal restrictions |
| Apache 2.0 | Permissive with patent protection |
| GPL v3.0 | Copyleft, derivatives must be open source |
| BSD 2-Clause | Permissive, simplified BSD |
| BSD 3-Clause | Permissive with non-endorsement clause |

### Security Checklist

- [ ] Enable two-factor authentication
- [ ] Configure SSH key authentication
- [ ] Review repository visibility settings
- [ ] Verify collaborator access levels
- [ ] Store recovery codes securely
- [ ] Regular security audit of organization members

### GitHub Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `>` | Open VS Code in browser |
| `t` | Activate file finder |
| `w` | Switch branch/tag |
| `l` | Jump to line |
| `/` | Focus search bar |

## GitHub Pages URL Format

Sites are available at: `https://<username>.github.io/<repository-name>`

## Related Specialists

- **Software Engineering Lead** - Development workflows and practices
- **Operations Runbook Engineer** - CI/CD and automation
- **Security Partner Manager** - Access control and security policies
