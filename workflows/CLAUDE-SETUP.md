# Claude Code CLI Setup for Agent0 PDLC

This guide explains how to set up and use Agent0 PDLC with Claude Code (the `claude` CLI).

Reference: [Claude Code Agent Teams](https://code.claude.com/docs/en/agent-teams) | [Claude Code Sub-Agents](https://code.claude.com/docs/en/sub-agents)

---

## Prerequisites

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed
- Anthropic API key or Claude Pro/Max subscription
- Your three-tier framework in place:
  - `agent0-pdlc/` (generic framework)
  - `agent0-pdlc-<org>/` (organization level)
  - `agent0-pdlc-<app>/` (application level)

## Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

---

## Project Configuration

### 1. CLAUDE.md (Project Instructions)

Claude Code reads `CLAUDE.md` at the project root automatically. This is how you wire the framework in.

Create or update `CLAUDE.md` in your application repository:

```markdown
# Project Instructions

## Agent0 PDLC Framework

Read these in order of precedence (app > org > generic):

### Application Level
- agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md

### Organization Level
- agent0-pdlc-<org>/ORGANIZATION-RULES.md
- agent0-pdlc-<org>/shared/policies/SECURITY-POLICY.md
- agent0-pdlc-<org>/shared/mcp/GUIDE-MCP.md

### Generic Framework
- agent0-pdlc/GLOBAL-RULES.md
- agent0-pdlc/agents/orchestration/AGENT0.md
- agent0-pdlc/workflows/BEADS-PROTOCOL.md

## Skills (Load by Role)

Security: agent0-pdlc-<org>/shared/skills/security/
UX: agent0-pdlc-<org>/shared/skills/ux/
SET: agent0-pdlc-<org>/shared/skills/set/
Engineering: agent0-pdlc-<org>/shared/skills/engineering/
Product: agent0-pdlc-<org>/shared/skills/product/
```

### 2. MCP Configuration

Configure MCP servers in `.claude/settings.local.json` (project-level) or `~/.claude/settings.json` (global):

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/mcp-atlassian"],
      "env": {
        "ATLASSIAN_SITE": "sonatype.atlassian.net",
        "ATLASSIAN_EMAIL": "your-email@sonatype.com",
        "ATLASSIAN_API_TOKEN": "your-token"
      }
    },
    "guide-mcp": {
      "command": "npx",
      "args": ["-y", "@sonatype/guide-mcp"],
      "env": {}
    }
  }
}
```

Adjust the `guide-mcp` entry to match your actual Guide MCP package/configuration.

### 3. Permissions

Configure allowed tools in `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Write",
      "Shell",
      "mcp__atlassian__*",
      "mcp__guide-mcp__*"
    ]
  }
}
```

---

## Ensure Framework Access

Claude Code needs file access to all three tiers. Options:

**Option A: Symlinks in project root (Recommended)**
```bash
cd /path/to/your/app
ln -s /path/to/agent0-pdlc agent0-pdlc
ln -s /path/to/agent0-pdlc-<org> agent0-pdlc-<org>
```

**Option B: Sibling directories**

If all repos are siblings (e.g., `~/apps/agent0-pdlc`, `~/apps/agent0-pdlc-sonatype`, `~/apps/my-app`), reference them with relative paths (`../agent0-pdlc/`) in `CLAUDE.md`.

**Option C: Git submodules**
```bash
git submodule add https://github.com/mitchellsjohnson/agent0-pdlc.git agent0-pdlc
git submodule add <org-repo-url> agent0-pdlc-<org>
```

---

## Bootstrapping Agent0

### Start a Session

```bash
cd /path/to/your/app
claude
```

Claude Code automatically reads `CLAUDE.md`. Then paste:

```
You are Agent0, the Product Owner and Technical Lead for this project.

Read the framework documents referenced in CLAUDE.md (app > org > generic).

Apply the CRIT Framework:

CONTEXT: Orient yourself to this codebase.
ROLE: Determine which agents are needed.
INTERVIEW: Ask me about sprint goals, tickets, and constraints.
TASK: Create the sprint plan after I answer.

Begin with your Context assessment and Interview questions.
```

### Resume a Session

```bash
claude --resume
```

Or start fresh and say:

```
Continue from where we left off. Read HANDOFF.md and run bd list.
```

---

## Multi-Agent Orchestration

Claude Code supports two approaches for running Agent0 PDLC teams:

### Option 1: Agent Teams (Native Coordination)

Claude Code has built-in [agent teams](https://code.claude.com/docs/en/agent-teams) with shared task lists, inter-agent messaging, and team coordination. This maps directly to the Agent0 SQUAD/COE model.

**Enable agent teams** (experimental, disabled by default):

```json
// .claude/settings.local.json or ~/.claude/settings.json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

**Create a SQUAD + COE team:**

```
Create an agent team for this sprint. Spawn teammates:

SQUAD:
- "dev-backend" - SoftwareEngineerAgent for backend work.
  Read agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-AGENT.md
  Skills: shared/skills/engineering/guide-mcp-usage.md, secure-coding.md
  Tickets: NEXUS-12345

- "dev-frontend" - SoftwareEngineerAgent for frontend work.
  Read agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-AGENT.md
  Skills: shared/skills/engineering/guide-mcp-usage.md
  Tickets: NEXUS-12346

COE (require plan approval before changes):
- "security" - SecurityEngineerAgent.
  Read agent0-pdlc-<org>/agents/security/Security-Engineer.md
  Skills: shared/skills/security/lifecycle-scan.md, threat-modeling.md
  Pre-push dependency gate is MANDATORY.

- "tester" - SoftwareEngineerInTestAgent.
  Read agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-IN-TEST-AGENT.md
  Skills: shared/skills/set/test-strategy.md, coverage-analysis.md

- "ux" - UXAgent.
  Read agent0-pdlc/agents/ux/UX-AGENT.md
  Skills: shared/skills/ux/design-system.md, accessibility-audit.md
```

**Key agent teams concepts:**

| Concept | Agent0 PDLC Mapping |
|---------|---------------------|
| Team lead | Agent0 (orchestrator) |
| Teammates | SQUAD (SoftwareEngineer instances) + COE specialists |
| Shared task list | Maps to Beads tasks |
| Plan approval mode | Use for COE agents (review before they modify code) |
| Direct messaging | Agent0 coordinates, teammates message each other |

**Display modes:**

- **In-process** (default): All teammates in one terminal. `Shift+Down` to cycle.
- **Split panes** (tmux/iTerm2): Each teammate in its own pane. See all output at once.

```json
// Force split panes
{ "teammateMode": "tmux" }
```

### Option 2: Custom Agents (`.claude/agents/`)

Define reusable agent definitions as markdown files in `.claude/agents/` (project) or `~/.claude/agents/` (user). These are Claude Code's equivalent of agent templates.

```
.claude/agents/
├── agent0.md              # Agent0 orchestrator
├── dev.md                 # SoftwareEngineer
├── security-reviewer.md   # SecurityEngineer
├── tester.md              # SET
└── ux-reviewer.md         # UXAgent
```

**Example: `.claude/agents/security-reviewer.md`**

```markdown
---
name: security-reviewer
description: SecurityEngineerAgent. Use when implementing auth, payments, handling sensitive data, or adding dependencies. Pre-push Guide MCP dependency check is mandatory.
model: inherit
---

You are SecurityEngineerAgent on this project.

Read:
- agent0-pdlc-<org>/agents/security/Security-Engineer.md
- agent0-pdlc-<org>/shared/policies/SECURITY-POLICY.md

Skills:
- agent0-pdlc-<org>/shared/skills/security/lifecycle-scan.md
- agent0-pdlc-<org>/shared/skills/security/threat-modeling.md

MCP: Use Guide MCP for all dependency checks. Pre-push gate is MANDATORY.
You have release veto authority.

When invoked:
1. Scan all new/changed dependencies via Guide MCP
2. Review code for OWASP Top 10 vulnerabilities
3. Check for hardcoded secrets
4. Verify auth/authz on all endpoints
5. Report findings by severity (Critical/High/Medium/Low)
```

**Invoke custom agents:**

```
/security-reviewer review the authentication module
```

Or let Claude delegate automatically based on the description field.

### Option 3: iTerm2 Manual Panes

For maximum control, run separate `claude` sessions in iTerm2 panes manually:

```
┌─────────────────────────────┬─────────────────────────────┐
│       SQUAD WINDOW          │         COE WINDOW          │
│  ┌───────────┬───────────┐  │  ┌───────────┬───────────┐ │
│  │  Agent0   │ AgentDev1 │  │  │ AgentSET  │ AgentSec  │ │
│  ├───────────┼───────────┤  │  ├───────────┼───────────┤ │
│  │ AgentDev2 │ AgentDev3 │  │  │ AgentUX   │  (Empty)  │ │
│  └───────────┴───────────┘  │  └───────────┴───────────┘ │
└─────────────────────────────┴─────────────────────────────┘
```

Each pane runs `claude` independently. Coordination happens through Beads, HANDOFF.md, and git -- not through built-in messaging. This approach works without the experimental agent teams feature.

---

## Agent Bootstrap Prompts (for Options 2 and 3)

**SoftwareEngineerAgent:**
```
You are SoftwareEngineerAgent (AgentDev1) on this project.

Read:
- agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-AGENT.md
- agent0-pdlc/GLOBAL-RULES.md
- agent0-pdlc-<org>/ORGANIZATION-RULES.md
- agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md

Skills:
- agent0-pdlc-<org>/shared/skills/engineering/guide-mcp-usage.md
- agent0-pdlc-<org>/shared/skills/engineering/secure-coding.md

Tickets in scope: [TICKET-123, TICKET-456]
Your scope: [Agent0 defines this]

Check Beads for your assigned tasks: bd ready
```

**SecurityEngineerAgent:**
```
You are SecurityEngineerAgent on this project.

Read:
- agent0-pdlc/agents/security/SECURITY-ENGINEER-AGENT.md
- agent0-pdlc-<org>/agents/security/Security-Engineer.md
- agent0-pdlc-<org>/shared/policies/SECURITY-POLICY.md

Skills:
- agent0-pdlc-<org>/shared/skills/security/lifecycle-scan.md
- agent0-pdlc-<org>/shared/skills/security/threat-modeling.md

MCP: Use Guide MCP for all dependency checks (see shared/mcp/GUIDE-MCP.md).
You have release veto authority. Pre-push dependency gate is MANDATORY.
First: establish security baseline. Scan dependencies, report findings.
```

**SoftwareEngineerInTestAgent:**
```
You are SoftwareEngineerInTestAgent on this project.

Read:
- agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-IN-TEST-AGENT.md
- agent0-pdlc/GLOBAL-RULES.md
- agent0-pdlc-<org>/shared/policies/TESTING-POLICY.md

Skills:
- agent0-pdlc-<org>/shared/skills/set/test-strategy.md
- agent0-pdlc-<org>/shared/skills/set/coverage-analysis.md

You have authority to block releases on quality grounds.
First: establish baseline. Run tests, report coverage, identify gaps.
```

**UXAgent:**
```
You are UXAgent on this project.

Read:
- agent0-pdlc/agents/ux/UX-AGENT.md
- agent0-pdlc-<org>/shared/policies/UX-STANDARDS.md

Skills:
- agent0-pdlc-<org>/shared/skills/ux/design-system.md
- agent0-pdlc-<org>/shared/skills/ux/accessibility-audit.md
- agent0-pdlc-<org>/shared/skills/ux/figma-review.md

You have authority to block releases on UX grounds.
First: review current UI state, report design system compliance.
```

---

## Session Management

### Ending a Session

```
Agent0, end this session:
1. bd sync
2. git add -A && git commit -m "Session: [description]"
3. git push
4. Create HANDOFF.md for next session
```

### Handoff Between Sessions

Claude Code sessions are ephemeral. Continuity comes from:

1. **HANDOFF.md** - What was done, what's next, decisions made
2. **Beads** - Task state (bd list, bd ready)
3. **Git history** - What changed
4. **CLAUDE.md** - Persistent project instructions (always loaded)

---

## Tips

### Context Window Management

- Claude Code has a large context window but it's still finite
- Reference files by path rather than pasting full contents
- Use `CLAUDE.md` for persistent instructions that survive session resets

### Beads Integration

```bash
npm install -g @beads/bd
bd init

bd ready            # What can I work on?
bd list             # All tasks
bd create "Title"   # New task
bd close <id>       # Complete task
bd sync             # Sync before push
```

### Claude Code Flags

```bash
claude                    # Interactive session
claude --resume           # Resume last session
claude -p "prompt"        # One-shot prompt
claude --model opus       # Use Claude Opus
claude --model sonnet     # Use Claude Sonnet (default)
```
