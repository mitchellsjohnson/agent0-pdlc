# Integrations

This folder contains configuration for external tool integrations used by your organization.

---

## Available Integrations

| File | Purpose | Required |
|------|---------|----------|
| `JIRA-INTEGRATION.md` | Jira project setup, ticket workflows | If using Jira |
| `LIFECYCLE-INTEGRATION.md` | SCA scanning (Sonatype Lifecycle, Snyk, etc.) | If using SCA |
| `SAST-INTEGRATION.md` | SAST tool configuration | If using SAST |
| `SOURCE-CONTROL.md` | Git standards, branch policies | Recommended |

---

## How Agents Use Integrations

1. **Agent0** reads integration docs during bootstrap
2. **AgentSecurity** uses scan integrations for security reviews
3. **AgentSET** uses testing integrations for coverage reports
4. **All agents** follow source control standards

---

## Adding an Integration

Create a new markdown file with:

```markdown
# [Tool Name] Integration

## Overview
What this tool does and why we use it.

## Configuration
How to configure the tool for this organization.

## Agent Usage
How agents should interact with this tool.

## Commands
Specific commands agents can run.

## Interpreting Results
How to read and act on tool output.
```

---

## Example: JIRA-INTEGRATION.md

```markdown
# Jira Integration

## Projects
- NEXUS - Nexus Repository
- IQSERVER - Lifecycle Server

## Workflows
1. Agent0 creates Jira tickets for sprint items
2. Link Beads tasks to Jira tickets
3. Update Jira status when Beads status changes

## Agent Commands
- Create ticket: `jira create --project NEXUS --type Task --summary "..."`
- Link to Beads: Include Jira ticket ID in Beads task description
```
