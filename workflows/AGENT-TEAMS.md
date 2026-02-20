# Agent Teams Orchestration

Agent0 PDLC uses the **Gastown Pattern** for multi-agent orchestration. Agent0 acts as the "Mayor" - spawning, coordinating, and managing a team of specialized agent "City Workers."

---

## Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         GASTOWN PATTERN                                      │
│                                                                             │
│                           ┌─────────────┐                                   │
│                           │   Agent0    │                                   │
│                           │   (Mayor)   │                                   │
│                           └──────┬──────┘                                   │
│                                  │                                           │
│              ┌───────────────────┼───────────────────┐                      │
│              │                   │                   │                      │
│              ▼                   ▼                   ▼                      │
│    ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐             │
│    │      SQUAD      │ │       COE       │ │     BEADS       │             │
│    │  (City Workers) │ │  (Specialists)  │ │ (Written Record)│             │
│    │                 │ │                 │ │                 │             │
│    │ SoftwareEng 1-4 │ │ SET, Security   │ │ Persistent task │             │
│    │ DevOps          │ │ UX              │ │ tracking        │             │
│    └─────────────────┘ └─────────────────┘ └─────────────────┘             │
│                                                                             │
│    Agent Teams: Real-time coordination (SendMessage)                        │
│    Beads: Durable task record (bd create, bd update, bd sync)               │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Prerequisites

### Enable Agent Teams (Claude Code)

Agent teams are experimental. Enable them in your settings:

```json
// ~/.config/claude/settings.json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

### Install Beads

```bash
npm install -g @beads/bd
cd your-project
bd init
```

---

## How Agent0 Orchestrates

Agent0 uses two complementary systems:

| System | Purpose | Persistence |
|--------|---------|-------------|
| **Agent Teams** | Real-time spawning and messaging | Session-scoped |
| **Beads** | Task tracking and audit trail | Git-backed, permanent |

### Agent Teams Tools

- `TeamCreate` - Create a team with shared task list
- `Task` with `team_name` - Spawn teammates
- `SendMessage` - Direct communication
- `TaskCreate/TaskUpdate/TaskList` - Team task coordination

### Beads Commands

```bash
bd create "Task title" -p 1      # Create task (P1 priority)
bd update <id> --status in_progress
bd close <id> --reason "Done"
bd sync                          # Sync before git operations
```

---

## Sprint Workflow

### 1. Bootstrap Agent0

```
You are Agent0, the Product Owner and Technical Lead.

Read: agent0-pdlc/agents/orchestration/AGENT0.md

You orchestrate using agent teams (TeamCreate, Task, SendMessage) and
track work in Beads (bd create, bd update, bd sync).

Apply the CRIT Framework, then spawn your team.
```

### 2. Agent0 Creates Team

```
TeamCreate:
  team_name: "sprint-auth"
  description: "Authentication feature sprint"
```

### 3. Agent0 Creates Tasks in Beads

```bash
bd create "Implement JWT service" -p 0 -d "TICKET-123"
bd create "Add RBAC middleware" -p 1 -d "TICKET-124"
bd create "Security review" -p 1 -d "TICKET-125"
```

### 4. Agent0 Spawns SQUAD

```
Task:
  description: "Backend authentication"
  subagent_type: "general-purpose"
  name: "dev-backend"
  team_name: "sprint-auth"
  prompt: |
    You are SoftwareEngineerAgent on sprint-auth.
    Read: agent0-pdlc/agents/engineering/SOFTWARE-ENGINEER-AGENT.md

    Your scope: JWT service and RBAC (TICKET-123, TICKET-124)

    Use Beads to track your work:
    - bd update <id> --status in_progress (when starting)
    - bd close <id> --reason "Done" (when complete)

    Message Agent0 when blocked or finished.
```

### 5. Agent0 Spawns COE

```
Task:
  description: "Security review"
  subagent_type: "general-purpose"
  name: "security"
  team_name: "sprint-auth"
  mode: "plan"
  prompt: |
    You are SecurityEngineerAgent on sprint-auth.
    Read: agent0-pdlc/agents/security/SECURITY-ENGINEER-AGENT.md

    Review SQUAD work for security issues.
    You have release veto authority.

    First: Establish security baseline.
    Then: Review as features complete.
```

### 6. Coordination Loop

Agent0 monitors progress and coordinates:

```
# Check team task status
TaskList

# Message specific teammate
SendMessage:
  type: "message"
  recipient: "dev-backend"
  content: "JWT service looks good. Please proceed with RBAC."
  summary: "Approve JWT, start RBAC"

# Update Beads when work completes
bd close jwt-task --reason "Implemented and reviewed"
```

### 7. Session End

```bash
# Sync Beads
bd sync

# Commit and push
git add -A
git commit -m "Sprint: auth feature complete"
git push

# Shutdown teammates
SendMessage:
  type: "shutdown_request"
  recipient: "dev-backend"
  content: "Sprint complete. Please shut down."

# Clean up team
TeamDelete
```

---

## Best Practices

### Task Sizing

- **Too small**: Coordination overhead exceeds benefit
- **Too large**: Teammates work too long without check-ins
- **Just right**: 1-4 hours of focused work per task

### Avoid File Conflicts

Assign non-overlapping file ownership:
- `dev-backend` owns `src/auth/`
- `dev-frontend` owns `src/components/`

### Use Beads as Ground Truth

- Agent Teams messages are ephemeral (session-scoped)
- Beads tasks persist across sessions
- Always `bd sync` before ending session

### COE Review Pattern

1. SQUAD completes feature
2. Agent0 notifies COE via SendMessage
3. COE reviews and reports findings
4. Agent0 approves or requests changes
5. Beads task closed when accepted

---

## Comparison: Agent Teams vs Manual Multi-Window

| Aspect | Agent Teams | Manual Multi-Window |
|--------|-------------|---------------------|
| Setup | Programmatic (Agent0 spawns) | Manual (human creates windows) |
| Coordination | SendMessage tool | Copy/paste between terminals |
| Task tracking | TaskList + Beads | Beads only |
| Scalability | Easy to add teammates | Manual pane management |
| Session resume | Limited (experimental) | N/A |

---

## Troubleshooting

### Teammates Not Responding

Check if teammate is idle:
```
TaskList  # Shows teammate status
```

Send a message to wake them:
```
SendMessage:
  type: "message"
  recipient: "dev-backend"
  content: "Are you blocked? Please report status."
```

### Lost Teammate Context

Teammates don't persist across sessions. If Agent0 session ends:
1. Start new Agent0 session
2. Read HANDOFF.md and Beads (`bd list`)
3. Create new team and spawn new teammates

### Beads Out of Sync

```bash
bd sync --force  # Force sync from remote
bd validate      # Check for issues
```

---

## Reference

- [Agent Teams Documentation](https://code.claude.com/docs/en/agent-teams)
- [Beads Protocol](BEADS-PROTOCOL.md)
- [Agent0 Operating Manual](../agents/orchestration/AGENT0.md)
