# Cursor IDE Setup for Agent0 PDLC

This guide explains how to set up and use Agent0 PDLC with Cursor IDE.

Reference: [Cursor Subagents](https://cursor.com/docs/context/subagents) | [Cursor Skills](https://cursor.com/docs/context/skills)

---

## Prerequisites

- [Cursor IDE](https://cursor.sh/) installed
- Access to AI model (Claude Sonnet 4, Claude Opus 4, GPT-4, etc.)
- Your three-tier framework in place:
  - `agent0-pdlc/` (generic framework)
  - `agent0-pdlc-<org>/` (organization level)
  - `agent0-pdlc-<app>/` (application level)

---

## Initial Setup

### 1. Open Your Project in Cursor

```bash
cursor /path/to/your/app
```

### 2. Add All Framework Tiers to Workspace

Cursor needs access to all three tiers. Add them as workspace folders:

**Option A: Symlinks (Recommended)**
```bash
cd /path/to/your/app
ln -s /path/to/agent0-pdlc agent0-pdlc
ln -s /path/to/agent0-pdlc-<org> agent0-pdlc-org
```

**Option B: Multi-root Workspace**
1. File → Add Folder to Workspace
2. Add `agent0-pdlc/`
3. Add `agent0-pdlc-<org>/`
4. Save workspace

### 3. Configure Cursor Settings

Add to `.cursor/settings.json`:

```json
{
  "cursor.agent.defaultModel": "claude-sonnet-4",
  "cursor.agent.contextFiles": [
    "agent0-pdlc/agents/AGENT0.md",
    "agent0-pdlc/GLOBAL-RULES.md",
    "agent0-pdlc/workflows/BEADS-PROTOCOL.md"
  ]
}
```

---

## Bootstrapping Agent0

### Step 1: Open Agent Panel

- Press `Cmd+L` (Mac) or `Ctrl+L` (Windows/Linux)
- Or click the Agent icon in the sidebar

### Step 2: Select Your Model

Choose your preferred model:
- **Claude Sonnet 4** - Fast, good for most tasks
- **Claude Opus 4** - Most capable, complex tasks
- **GPT-4** - Alternative option

### Step 3: Paste Agent0 Bootstrap Prompt

```
You are Agent0, the Product Owner and Technical Lead for this project.

Read and internalize these documents in order:
1. agent0-pdlc/agents/AGENT0.md - Your operating manual
2. agent0-pdlc/GLOBAL-RULES.md - Non-negotiable rules
3. agent0-pdlc/workflows/BEADS-PROTOCOL.md - Communication protocol
4. agent0-pdlc-org/ORGANIZATION-RULES.md - Organization policies
5. agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md - How to build this app

Your first task: Orient yourself to this codebase and prepare to bootstrap your team.

After reading, report back with:
1. Project understanding (what is this codebase?)
2. Current state (any existing HANDOFF.md or Beads tasks?)
3. Recommended SQUAD size (how many AgentDev instances?)
4. COE requirements (which specialists needed?)
5. Proposed sprint scope (what should we tackle first?)
```

### Step 4: Agent0 Provides Team Structure

Agent0 will analyze your codebase and recommend:
- Number of AgentDev instances (typically 1-4)
- Which COE specialists are needed
- Initial sprint scope

---

## Multi-Agent Orchestration in Cursor

Cursor supports two approaches for running Agent0 PDLC teams:

### Option 1: Subagents (Native Delegation)

Cursor has built-in [subagents](https://cursor.com/docs/context/subagents) that Agent0 can delegate tasks to. Each subagent runs in its own context window and returns results to the parent. Subagents can run in parallel.

**Create custom subagents in `.cursor/agents/`:**

```
.cursor/agents/
├── security-reviewer.md    # SecurityEngineerAgent
├── tester.md               # SoftwareEngineerInTestAgent
├── ux-reviewer.md          # UXAgent
└── debugger.md             # Debugging specialist
```

**Example: `.cursor/agents/security-reviewer.md`**

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

When invoked:
1. Scan all new/changed dependencies via Guide MCP
2. Review code for OWASP Top 10 vulnerabilities
3. Check for hardcoded secrets
4. Report findings by severity (Critical/High/Medium/Low)
```

**Invoke subagents:**
```
/security-reviewer review the authentication module
/tester run tests and check coverage for the new API
```

Or let the agent delegate automatically based on descriptions.

**Subagents vs Agent0 PDLC mapping:**

| Cursor Concept | Agent0 PDLC Mapping |
|---------------|---------------------|
| Parent agent | Agent0 (orchestrator) |
| Custom subagents | COE specialists (Security, SET, UX) |
| Background subagents | Parallel SQUAD work |
| Built-in explore | Codebase research |
| Built-in bash | Build/test execution |

### Option 2: Multi-Tab Mode

Open multiple agent panels for parallel work:

1. **Tab 1: Agent0** - Orchestration
2. **Tab 2: AgentDev1** - Feature A
3. **Tab 3: AgentDev2** - Feature B
4. **Tab 4: AgentSET** - Testing

**How to create tabs:**
1. Click "+" next to agent panel
2. Paste the specific agent's bootstrap prompt
3. Each tab is an independent agent session

### Agent Bootstrap Prompts

**AgentDev Bootstrap:**
```
You are AgentDev1, a Software Engineer on this project.

Read and internalize:
1. agent0-pdlc/agents/AGENTDEV.md - Your operating manual
2. agent0-pdlc/GLOBAL-RULES.md - Non-negotiable rules
3. agent0-pdlc-org/ORGANIZATION-RULES.md - Org policies
4. agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md - How to build

You report to Agent0. Pull tasks from Beads.
Your scope: [Agent0 will define]

Acknowledge and await your first task from Agent0.
```

**AgentSET Bootstrap:**
```
You are AgentSET, the Software Engineer in Test for this project.

Read and internalize:
1. agent0-pdlc/agents/AGENTSET.md - Your operating manual
2. agent0-pdlc/GLOBAL-RULES.md - Non-negotiable rules
3. agent0-pdlc-org/policies/TESTING-POLICY.md - Org testing policy
4. agent0-pdlc-<app>/TESTING-STRATEGY.md - App testing strategy

You advise Agent0 and review SQUAD work.
You have authority to block releases on quality grounds.

Acknowledge and report your baseline assessment.
```

**AgentSecurity Bootstrap:**
```
You are AgentSecurity, the Security Architect for this project.

Read and internalize:
1. agent0-pdlc/agents/AGENTSECURITY.md - Your operating manual
2. agent0-pdlc/GLOBAL-RULES.md - Non-negotiable rules
3. agent0-pdlc-org/policies/SECURITY-POLICY.md - Org security policy
4. agent0-pdlc-<app>/SECURITY-STRATEGY.md - App security strategy

You advise Agent0 and review SQUAD work.
You have release veto authority for security issues.

Acknowledge and report your baseline security assessment.
```

**AgentUX Bootstrap:**
```
You are AgentUX, the UX Architect for this project.

Read and internalize:
1. agent0-pdlc/agents/AGENTUX.md - Your operating manual
2. agent0-pdlc/GLOBAL-RULES.md - Non-negotiable rules
3. agent0-pdlc-org/policies/UX-STANDARDS.md - Org UX standards
4. agent0-pdlc-<app>/UX-STRATEGY.md - App UX strategy

You advise Agent0 and review SQUAD work.
You have authority to block releases on UX grounds.

Acknowledge and report your baseline UX assessment.
```

---

## Workflow: Running a Sprint

### 1. Sprint Planning (Agent0)

```
Agent0, create a sprint plan for: [describe goals]

Use Beads to track tasks. Assign to appropriate agents.
```

### 2. Task Execution (SQUAD)

Agent0 assigns tasks via Beads:
```bash
yarn bd create "Implement feature X" -t task -d "Details..." --assign AgentDev1
```

AgentDev checks tasks:
```bash
yarn bd:ready
```

### 3. Quality Review (COE)

AgentSET reviews:
```
AgentSET, review the work completed by AgentDev1 for [feature].
Run tests, check coverage, report findings.
```

### 4. Accept and Close (Agent0)

```
Agent0, review and accept the completed work.
Update Beads, prepare for next iteration.
```

---

## Session Management

### Starting a Session

1. Open Cursor in your project
2. Bootstrap Agent0 (or say "continue" if HANDOFF.md exists)
3. Agent0 reads HANDOFF.md and resumes

### Ending a Session

Tell Agent0:
```
Agent0, we're ending this session. Please:
1. Sync Beads
2. Commit all changes
3. Create HANDOFF.md
4. Push to remote
```

### Resuming a Session

```
Agent0, continue from where we left off.
Read HANDOFF.md and Beads to understand current state.
```

---

## Tips and Best Practices

### Context Management

- Keep agent context focused (don't load entire codebase)
- Use `@file` references for specific files
- Clear context if agent gets confused

### Parallel Work

- Assign non-overlapping tasks to different agents
- Use Beads dependencies to coordinate
- Have Agent0 resolve conflicts

### Debugging Issues

- If agent is confused: restart the session
- If agent lost context: re-paste bootstrap prompt
- If agent is slow: reduce context, use faster model

### Performance

- Use Claude Sonnet for routine tasks
- Use Claude Opus for complex architecture
- Batch similar tasks together

---

## Troubleshooting

### Agent Not Reading Framework

Ensure all three tiers are accessible:
```bash
ls agent0-pdlc/agents/AGENT0.md
ls agent0-pdlc-org/ORGANIZATION-RULES.md
ls agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md
```

### Agent Ignoring Rules

Re-paste the bootstrap prompt with emphasis:
```
STOP. Re-read agent0-pdlc/GLOBAL-RULES.md carefully.
You MUST follow these rules. Acknowledge each rule.
```

### Agent Lost Context

```
Your context may have been lost. Please re-read:
1. agent0-pdlc/agents/AGENT0.md
2. HANDOFF.md
3. yarn bd:list

Then continue from the current state.
```

---

## Advanced: Cursor Rules

Create `.cursor/rules/agent0-pdlc.md` for persistent rules:

```markdown
# Agent0 PDLC Rules

Always follow:
1. Read agent0-pdlc/GLOBAL-RULES.md
2. Use Beads for task tracking
3. Keep MD and Beads separate
4. Sync and push before ending session
```

This ensures rules persist across sessions.
