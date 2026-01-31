# Beads Protocol

[Beads](https://github.com/steveyegge/beads) is a distributed, git-backed graph issue tracker designed for AI agents. It provides persistent, structured memory for coding agents, replacing messy markdown plans with a dependency-aware graph.

---

## The Golden Rule

> **Markdown (.md) is for humans** - explains what, why, decisions
> **Beads is for machines** - tracks tasks, status, ownership, dependencies

**NEVER mix them.**

---

## Overview

Beads provides:
- **Git as Database**: Issues stored as JSONL in `.beads/`. Versioned, branched, and merged like code.
- **Agent-Optimized**: JSON output, dependency tracking, and auto-ready task detection.
- **Zero Conflict**: Hash-based IDs (`bd-a1b2`) prevent merge collisions in multi-agent/multi-branch workflows.
- **Invisible Infrastructure**: SQLite local cache for speed; background daemon for auto-sync.
- **Compaction**: Semantic "memory decay" summarizes old closed tasks to save context window.

---

## Installation

Install Beads globally:

```bash
# Via npm
npm install -g @beads/bd

# Via Homebrew
brew install beads

# Via Go
go install github.com/steveyegge/beads/cmd/bd@latest

# Via curl
curl -fsSL https://raw.githubusercontent.com/steveyegge/beads/main/scripts/install.sh | bash
```

Initialize in your project:
```bash
cd your-project
bd init
```

This creates:
```
.beads/
├── config.yaml     # Beads configuration
├── issues.jsonl    # Issue storage (JSONL format)
├── metadata.json   # Project metadata
└── README.md       # Beads documentation
```

**Optional yarn scripts** for convenience:
```json
{
  "scripts": {
    "bd:list": "bd list",
    "bd:ready": "bd ready",
    "bd:sync": "bd sync"
  }
}
```

---

## Core Commands

### List Tasks

```bash
# All tasks
yarn bd:list

# Filter by status
yarn bd:list --status open
yarn bd:list --status in_progress
yarn bd:list --status done

# Filter by assignee
yarn bd:list --assignee AgentDev1

# Filter by priority
yarn bd:list --priority 0    # P0 (critical)
yarn bd:list --priority 1    # P1 (high)
```

### View Ready Work

```bash
# Tasks that are unblocked and can be started
yarn bd:ready

# Ready work for specific agent
yarn bd:ready --assignee AgentDev1
```

### Create Tasks

```bash
# Basic task
yarn bd create "Implement user authentication"

# With priority (0=critical, 1=high, 2=medium, 3=low)
yarn bd create "Fix login bug" -p 0

# With type (task, bug, epic, story)
yarn bd create "Add dark mode" -t task

# With description
yarn bd create "Refactor API" -d "Detailed description here"

# With assignee
yarn bd create "Write tests" --assign AgentSET

# Full example
yarn bd create "Add OAuth support" \
  -p 1 \
  -t task \
  -d "Implement OAuth 2.0 with Google and GitHub providers" \
  --assign AgentDev1 \
  --depends-on "auth-001"
```

### Update Tasks

```bash
# Update status
yarn bd update <id> --status in_progress
yarn bd update <id> --status blocked
yarn bd update <id> --status done

# Reassign
yarn bd update <id> --assignee AgentDev2

# Add comment
yarn bd update <id> --comment "Waiting on API spec"

# Update priority
yarn bd update <id> --priority 0
```

### Close Tasks

```bash
# Close with reason
yarn bd close <id> --reason "Completed and tested"

# Close as won't do
yarn bd close <id> --reason "Out of scope" --wontdo
```

### Sync

```bash
# Sync before git operations (REQUIRED before push)
yarn bd:sync
```

---

## Task Structure

Each task has:

```json
{
  "id": "task-001",
  "title": "Implement user authentication",
  "description": "Add JWT-based auth with refresh tokens",
  "type": "task",
  "priority": 1,
  "status": "open",
  "assignee": "AgentDev1",
  "dependencies": ["task-000"],
  "blockers": [],
  "created": "2026-01-30T10:00:00Z",
  "updated": "2026-01-30T14:30:00Z",
  "comments": [
    {
      "author": "Agent0",
      "text": "Assigned to AgentDev1",
      "timestamp": "2026-01-30T10:00:00Z"
    }
  ]
}
```

### Status Values

| Status | Meaning |
|--------|---------|
| `open` | Task created, not started |
| `in_progress` | Work has begun |
| `blocked` | Cannot proceed (see blockers) |
| `review` | Ready for review |
| `done` | Completed |
| `wontdo` | Closed without completion |

### Priority Values

| Priority | Level | Response Time |
|----------|-------|---------------|
| 0 | Critical | Immediate (drop everything) |
| 1 | High | This sprint |
| 2 | Medium | Next sprint |
| 3 | Low | Backlog |

### Task Types

| Type | Use For |
|------|---------|
| `epic` | Large features spanning multiple tasks |
| `story` | User-facing feature |
| `task` | Technical work item |
| `bug` | Defect fix |

---

## Workflow Patterns

### Agent0 Creates Sprint Plan

```bash
# Create epic
yarn bd create "User Authentication System" -t epic -p 1

# Create tasks under epic
yarn bd create "Design auth API" -t task --parent auth-epic --assign Agent0
yarn bd create "Implement JWT service" -t task --parent auth-epic --assign AgentDev1 --depends-on auth-api
yarn bd create "Add login UI" -t task --parent auth-epic --assign AgentDev2 --depends-on auth-api
yarn bd create "Write auth tests" -t task --parent auth-epic --assign AgentSET --depends-on auth-jwt,auth-ui
yarn bd create "Security review" -t task --parent auth-epic --assign AgentSecurity --depends-on auth-tests
```

### AgentDev Picks Up Work

```bash
# Check what's ready
yarn bd:ready --assignee AgentDev1

# Start work
yarn bd update auth-jwt --status in_progress

# Add progress comment
yarn bd update auth-jwt --comment "Started implementation, using jose library"

# Mark for review
yarn bd update auth-jwt --status review

# After approval, close
yarn bd close auth-jwt --reason "Implemented and approved by AgentSET"
```

### COE Reviews

```bash
# AgentSET marks tests complete
yarn bd update auth-tests --status done --comment "All tests passing, 87% coverage"

# AgentSecurity flags issue
yarn bd update auth-security --status blocked --comment "Found CVE in dependency, creating blocker"
yarn bd create "Fix jose CVE" -t bug -p 0 --blocks auth-security --assign AgentDev1
```

### Handling Blockers

```bash
# Mark task as blocked
yarn bd update task-123 --status blocked

# Create blocker task
yarn bd create "API spec needed" -t task -p 1 --blocks task-123

# When blocker resolved
yarn bd close blocker-task --reason "Spec delivered"
# Original task auto-unblocks
```

---

## Integration with Git

### Before Commit

```bash
# Update task status
yarn bd update task-123 --status done --comment "Implemented"

# Sync beads
yarn bd:sync

# Commit together
git add -A
git commit -m "feat: implement feature X (closes task-123)"
```

### Before Push

```bash
# ALWAYS sync before push
yarn bd:sync
git push
```

### Commit Message Convention

Reference Beads tasks in commits:

```
feat: add user authentication (task-001)

Implements JWT-based auth with refresh tokens.

Closes: task-001
Relates: epic-auth
```

---

## Querying and Filtering

### Advanced Queries

```bash
# All open tasks for sprint
yarn bd:list --status open,in_progress

# All blocked tasks
yarn bd:list --status blocked

# Tasks by multiple assignees
yarn bd:list --assignee AgentDev1,AgentDev2

# Tasks in epic
yarn bd:list --parent auth-epic

# Tasks with dependencies
yarn bd:list --has-dependencies

# Tasks blocking others
yarn bd:list --is-blocking
```

### Export and Reports

```bash
# Export to JSON
yarn bd:list --format json > sprint-status.json

# Summary report
yarn bd report

# Burndown data
yarn bd burndown
```

---

## Configuration

### .beads/config.yaml

```yaml
project:
  name: "your-project"
  version: "1.0.0"

defaults:
  priority: 2
  type: task
  
statuses:
  - open
  - in_progress
  - blocked
  - review
  - done
  - wontdo

priorities:
  0: critical
  1: high
  2: medium
  3: low

integrations:
  jira:
    enabled: false
    project: ""
    sync: manual
    
  github:
    enabled: true
    repo: "owner/repo"
    sync: auto
```

---

## Best Practices

### Task Granularity

- **Too big**: "Build the entire feature" ❌
- **Too small**: "Add semicolon" ❌
- **Just right**: "Implement login form with validation" ✅

Rule of thumb: 1-4 hours of work per task

### Dependencies

- Explicit is better than implicit
- Minimize dependency chains
- Avoid circular dependencies
- Use `--depends-on` not comments

### Comments

- Keep factual (not emotional)
- Note blockers and resolutions
- Reference files/commits when relevant
- Don't duplicate MD content

### Sync Discipline

- Sync before all git operations
- Sync at end of every session
- Sync before handoff

---

## Anti-Patterns

### Don't

- Track tasks in Markdown ❌
- Create tasks without context ❌
- Forget to update status ❌
- Skip sync before push ❌
- Use Beads for documentation ❌

### Do

- Keep tasks atomic ✅
- Update status as you work ✅
- Add meaningful comments ✅
- Sync religiously ✅
- Reference related tasks ✅

---

## Troubleshooting

### Tasks Out of Sync

```bash
# Force sync from remote
yarn bd:sync --force

# Rebuild index
yarn bd rebuild
```

### Corrupted State

```bash
# Validate tasks
yarn bd validate

# Fix issues
yarn bd repair
```

### Merge Conflicts in .beads/

```bash
# Beads handles JSONL merge automatically
# If manual intervention needed:
git checkout --theirs .beads/tasks.jsonl
yarn bd:sync --merge
```

---

## Summary

| Command | Purpose |
|---------|---------|
| `yarn bd:list` | View all tasks |
| `yarn bd:ready` | View unblocked tasks |
| `yarn bd create "..."` | Create new task |
| `yarn bd update <id>` | Update task |
| `yarn bd close <id>` | Close task |
| `yarn bd:sync` | Sync with remote |

**Remember**: Beads is for machines, Markdown is for humans.
