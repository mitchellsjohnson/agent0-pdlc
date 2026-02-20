# Global Rules – All Agents

This document defines non-negotiable rules for all agents working with this framework.

---

## The Cardinal Rule

> **Read Markdown to understand the system.**
> **Read Beads to understand the work.**
> **Never rely on one to replace the other.**

---

## MD vs Beads (Non-Negotiable)

### Markdown (.md) – Human-readable

Markdown explains intent, requirements, decisions, and constraints.

**MD answers:**
- What are we building?
- Why does it exist?
- What decisions were made?
- What constraints apply?

**MD must NOT contain:**
- Task lists
- TODOs with checkboxes
- Sequencing of work
- Ownership assignments
- Status updates

### Beads – Machine-readable

[Beads](https://github.com/steveyegge/beads) tracks work state: tasks, subtasks, dependencies, status, ownership.

**Beads answers:**
- What work exists?
- What is done / not done?
- Who owns it?
- What depends on what?

**Beads commands:**
```bash
bd list                     # View all tasks
bd ready                    # View ready work (unblocked)
bd create "Title" -p 0      # Create a P0 task
bd update <id> --status in_progress  # Update status
bd close <id> --reason "Done"        # Close task
bd sync                     # Sync before push
```

### The Rule

**If a file mixes both intent (MD) and task tracking (Beads), it must be split.**

---

## Framework Hierarchy (Non-Negotiable)

All agents read configuration from three levels in this order of precedence:

1. **Application level** (`agent0-pdlc-<app>/`) - Highest priority, app-specific
2. **Organization level** (`agent0-pdlc-<org>/`) - Org policies
3. **Generic level** (`agent0-pdlc/`) - Framework defaults

When rules conflict, higher precedence wins:
- App overrides Org
- Org overrides Generic

**Agents must have access to all three levels to operate correctly.**

---

## Data Protection (Non-Negotiable)

### 🚫 ABSOLUTE PROHIBITION: Database Deletion

**THE FOLLOWING ARE FORBIDDEN unless the human explicitly says "delete the database":**

```bash
# FORBIDDEN commands (examples):
rm -rf target                    # May contain database
rm -rf */target                  # May contain database
mvn clean                        # Deletes target directories
./mvnw clean                     # Deletes target directories
```

**Database locations to NEVER delete:**
- `target/application-data/` - Contains database files
- `*/db/*.mv.db` - H2 database files
- Any path containing `application-data`, `db/`, or `.mv.db`

**WHY:** Deleting databases destroys ALL user data, repositories, configurations, and test state. This has caused repeated catastrophic data loss.

**SAFE alternatives:**
- Delete specific subdirectories (not the whole target)
- Use `mvn package` without `clean`
- Delete only build artifacts, preserve `application-data`

### General Data Protection

**NEVER delete data directories without explicit human confirmation:**
- Database files
- Blob storage
- User data directories
- Configuration state

**If an operation might delete data:**
1. Warn the human
2. Show what would be deleted
3. Ask for explicit confirmation
4. Ask again for destructive operations
5. Only proceed after double confirmation

---

## Session Completion (Non-Negotiable)

Work is NOT complete until pushed to remote.

**Mandatory end-of-session workflow:**
```bash
bd sync
git add -A
git commit -m "Session: [description]"
git pull --rebase
git push
git status  # MUST show "up to date with origin"
```

**Rules:**
- NEVER stop before pushing (if changes exist)
- If push fails, resolve and retry until it succeeds
- Always create HANDOFF.md if session is ending
- Provide context for next session

---

## Communication Protocol (Non-Negotiable)

### Agent-to-Agent Communication

All agent coordination happens through:
1. **Beads** - Task assignment and status
2. **Code** - Implementation
3. **MD files** - Context and decisions

Agents do NOT communicate through:
- Chat messages
- Verbal instructions
- Ephemeral notes

### Agent-to-Human Communication

- Report progress clearly
- Flag blockers immediately
- Propose solutions, not just problems
- Respect decisions after escalation

---

## Quality Gates (Non-Negotiable)

### Before Marking Work Complete

- [ ] Code compiles/builds
- [ ] Tests pass
- [ ] Coverage meets threshold
- [ ] No new linting errors
- [ ] Beads status updated
- [ ] HANDOFF.md updated (if session ending)

### Before Release

- [ ] AgentSET approves quality
- [ ] AgentSecurity approves security 
- [ ] AgentUX approves experience 
- [ ] Agent0 accepts work

---

## Documentation Standards (Non-Negotiable)

### Allowed MD Files

| File | Purpose |
|------|---------|
| `README.md` | Project/module overview |
| `BUILD-INSTRUCTIONS.md` | How to build |
| `TESTING-STRATEGY.md` | Test approach |
| `SECURITY-STRATEGY.md` | Security approach |
| `UX-STRATEGY.md` | UX approach |
| `HANDOFF.md` | Session/sprint handoff |
| `*-RULES.md` | Rules and policies |
| `*-STRATEGY.md` | Strategy documents |

### Forbidden MD Content

- [ ] Task lists with checkboxes
- [ ] TODO items
- [ ] Status updates
- [ ] Work sequencing
- [ ] Agent assignments

**These belong in Beads.**

---

## Git Discipline (Non-Negotiable)

### Commit Messages

```
<type>: <description>

[optional body]

[optional footer]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

### Branch Naming

```
<type>/<ticket-id>-<description>
```

Examples:
- `feat/TICKET-123-add-user-auth`
- `fix/TICKET-456-fix-login-redirect`

### Never

- Force push to main/master
- Commit secrets or credentials
- Commit large binaries
- Skip hooks without explicit approval

---

## Agent Authority (Non-Negotiable)

### Orchestration Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| Agent0 | All scope/arch decisions | No (escalates) |
| SegmentTechLead | Segment scope/arch decisions | No (escalates to Agent0) |

### Product Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| ProductManager | Roadmap/prioritization | No |
| ProgramManager | Cross-team delivery schedules | No |
| ProductOperations | Release readiness | Yes (release gates) |
| ProductMarketing | Go-to-market timing | No |

### UX Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| ProductDesigner | UX/accessibility standards | Yes (UX) |
| ProductDocumentation | Documentation standards | No |

### Engineering Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| SoftwareEngineer | Implementation details | No |
| SoftwareEngineerInTest | Quality standards | Yes (quality) |
| DevOpsEngineer | CI/CD/infrastructure | Yes (deployment) |

### Security Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| SecurityEngineer | Security standards | Yes (security) |
| SecurityResearcher | Threat assessment | No (advisory) |

### Data Layer
| Agent | Authority | Veto Power |
|-------|-----------|------------|
| DataEngineer | Data architecture | No |
| DataAnalyst | Analysis methodology | No |
| DataScientist | ML/AI model decisions | No |

**Vetoes must be respected or escalated. Never overridden.**

### Backward Compatibility
Legacy agent names map to new names:
- AgentDev → SoftwareEngineerAgent
- AgentSET → SoftwareEngineerInTestAgent
- AgentSecurity → SecurityEngineerAgent
- AgentUX → ProductDesignerAgent

---

## Anti-Patterns (Forbidden)

### All Agents

- Mixing MD and Beads content
- Working on untracked tasks
- Skipping handoffs
- Silent failures
- Assumptions without validation

### Agent0

- Becoming the bottleneck
- Micromanaging SQUAD
- Ignoring COE

### AgentDev

- Scope creep
- Skipping tests
- Ignoring patterns

### AgentSET

- No baseline before enhancing
- Estimating instead of measuring
- Blocking without alternatives

### AgentSecurity

- FUD without evidence
- Blocking without solutions
- Ignoring cost/benefit

### AgentUX

- Inconsistency
- Skipping accessibility
- Over-designing

---

## Enforcement

These rules are enforced by:

1. **Agent0** - Reviews all work
2. **COE** - Specialists review their domains
3. **Beads** - Tracks compliance
4. **Git hooks** - Automated checks
5. **CI/CD** - Build-time validation

Violations should be flagged, documented, and resolved.
Repeated violations require process review.
