# MCP Server Configurations

This folder contains Model Context Protocol (MCP) server configurations for your organization.

---

## What is MCP?

MCP (Model Context Protocol) allows AI agents to interact with external tools and services. Each MCP server provides specific capabilities that agents can use.

---

## Configuring MCP Servers

### 1. Document Available MCPs

Create a folder for each MCP server your organization uses:

```
mcp/
├── README.md                    # This file
├── sonatype-mcp/               # Sonatype tools
│   ├── USAGE.md                # How agents use it
│   └── tools.md                # Available tools
├── jira-mcp/                   # Jira integration
│   └── USAGE.md
└── github-mcp/                 # GitHub integration
    └── USAGE.md
```

### 2. Document Tool Usage

For each MCP, document:
- What tools are available
- When agents should use them
- How to interpret results
- Common patterns

---

## Example: Sonatype MCP

### Available Tools

| Tool | Purpose | Used By |
|------|---------|---------|
| `getComponentVersion` | Check component vulnerabilities | AgentSecurity |
| `getRecommendedComponentVersions` | Find safe upgrade paths | AgentSecurity, AgentDev |
| `evaluateApplication` | Full app security scan | AgentSecurity |

### Usage Pattern

```
AgentSecurity: Check if dependency is safe

1. Call: mcp_sonatype-mcp_getComponentVersion
   - coordinates: "pkg:maven/org.example/library@1.0.0"

2. Check response:
   - If policy threat level >= 7: Create P0/P1 Beads task
   - If policy threat level 4-6: Create P2 Beads task
   - If policy threat level < 4: Document and monitor

3. For vulnerabilities found:
   - Call: mcp_sonatype-mcp_getRecommendedComponentVersions
   - Propose upgrade path to Agent0
```

---

## Agent Permissions

| Agent | MCP Access |
|-------|------------|
| Agent0 | All MCPs (for coordination) |
| AgentDev | GitHub, limited Sonatype |
| AgentSET | Testing tools, coverage tools |
| AgentSecurity | Sonatype, SAST tools |
| AgentUX | Design tools (if available) |

---

## Adding a New MCP

1. Create folder: `mcp/<mcp-name>/`
2. Create `USAGE.md` documenting:
   - Available tools
   - When to use each tool
   - Example commands
   - Result interpretation
3. Update this README
4. Notify agents in bootstrap prompts
