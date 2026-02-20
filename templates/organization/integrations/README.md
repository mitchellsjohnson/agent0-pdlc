# Integrations

This folder contains configuration for external tool integrations used by your organization.

---

## Available Integrations

| File | Purpose | Required |
|------|---------|----------|
| `TICKETING-INTEGRATION.md` | Ticketing system setup, ticket workflows | If using ticketing |
| `LIFECYCLE-INTEGRATION.md` | SCA scanning (dependency scanner, Snyk, etc.) | If using SCA |
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

## Example: TICKETING-INTEGRATION.md

```markdown
# Ticketing Integration

## Projects
- PROJ - Main Project
- BACKEND - Backend Services

## Workflows
1. Agent0 creates tickets for sprint items
2. Link Beads tasks to tickets
3. Update ticket status when Beads status changes

## Agent Commands
- Create ticket: Use your ticketing system CLI or API
- Link to Beads: Include ticket ID in Beads task description
```
