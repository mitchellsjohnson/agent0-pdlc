# MCP Server Configurations (Template)

This directory contains Model Context Protocol (MCP) server documentation for your organization.

## What is MCP?

MCP allows AI agents to interact with external tools and services. Each MCP server provides specific capabilities.

## Recommended MCPs to Document

| MCP | Purpose |
|-----|---------|
| Project tracking MCP | Jira/Linear/GitHub Issues access |
| Security scanning MCP | Dependency intelligence, vulnerability data |
| Documentation MCP | Confluence/Notion access |

## File Template

For each MCP server, create a markdown file documenting:

```markdown
# [MCP Name]

## Overview
What tools this MCP provides.

## Available Tools
| Tool | Purpose |
|------|---------|
| tool-name | What it does |

## Usage Patterns
Step-by-step workflows for common agent tasks.

## Agent Permissions
Which agents should use which tools.
```

## Agent Access Matrix

| Agent | Recommended MCP Access |
|-------|----------------------|
| Agent0 | All MCPs (coordination) |
| SoftwareEngineer | Source control, dependency checking |
| SecurityEngineer | Security scanning, dependency checking |
| SoftwareEngineerInTest | CI/CD, test reporting |
| UXAgent | Design tools (if available) |
