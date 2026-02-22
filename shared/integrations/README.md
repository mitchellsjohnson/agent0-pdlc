# Integrations (Template)

This directory contains documentation for external tool integrations used across your organization.

## Recommended Integrations

Create a markdown file for each tool your organization uses:

| File | Purpose |
|------|---------|
| `JIRA.md` | Project tracking (Jira, Linear, GitHub Issues) |
| `CONFLUENCE.md` | Documentation platform |
| `GITHUB.md` | Source control and code review |
| `CI-CD.md` | CI/CD pipeline (Jenkins, GitHub Actions, etc.) |
| `SCA.md` | Software Composition Analysis tool |

## File Template

```markdown
# [Tool Name] Integration

## Overview
What this tool does and why we use it.

## Access
How to authenticate and connect.

## Agent Usage
How agents interact with this tool (commands, MCP tools, URLs).

## Workflows
Common workflows agents should follow.
```

## How Agents Use Integrations

1. **Agent0** reads integration docs during bootstrap
2. **All agents** follow source control standards
3. **SecurityEngineer** uses SCA integrations for scanning
4. **SoftwareEngineerInTest** uses CI/CD for verification
