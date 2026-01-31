# Sprint Handoff – <Application Name>

**Sprint**: <Sprint Name or Number>
**Agent0**: <Agent Identifier>
**Date**: <YYYY-MM-DD>

---

## 1. Sprint Summary

<!-- What was accomplished in this sprint -->

<One paragraph describing what this sprint delivered and why it matters.>

---

## 2. Scope

### Included

- <Module/Feature A>
- <Module/Feature B>

### Excluded (Explicit Non-Goals)

- <Non-goal 1>
- <Non-goal 2>

---

## 3. Current Codebase State

### Completed

- ✅ <Completed item 1>
- ✅ <Completed item 2>

### In Progress

- 🔄 <In-progress item> (Beads ID: `<id>`)

### Known Bugs

- 🐛 <Bug description> (Beads ID: `<id>`)

---

## 4. Architecture Decisions

### Key Decisions Made

1. **<Decision 1>**: <Rationale>
2. **<Decision 2>**: <Rationale>

### Technical Debt Introduced

- <Tech debt item 1>
- <Tech debt item 2>

---

## 5. SQUAD Status

| Agent | Last Task | Status |
|-------|-----------|--------|
| AgentDev1 | <task> | <completed/in-progress> |
| AgentDev2 | <task> | <completed/in-progress> |

---

## 6. COE Status

### AgentSET (Testing)

- Test coverage: <before>% → <after>%
- Tests passing: <count>
- Known gaps: <list>

### AgentSecurity (Security)

- Vulnerabilities: <before> → <after>
- Scans completed: <list>
- Accepted risks: <list>

### AgentUX (UX)

- Standards compliance: <status>
- Deviations approved: <list>
- Known gaps: <list>

---

## 7. Known Risks

1. <Risk 1>
2. <Risk 2>

---

## 8. Immediate Priorities

For next session/sprint:

1. <Priority 1>
2. <Priority 2>
3. <Priority 3>

---

## 9. Beads Status

```bash
# Current Beads state
yarn bd:list --status open,in_progress
```

- Open tasks: <count>
- In progress: <count>
- Blocked: <count>

---

## 10. Where to Look

| Topic | File |
|-------|------|
| Work Items | `yarn bd:list` |
| Build Instructions | `agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md` |
| Testing Strategy | `agent0-pdlc-<app>/TESTING-STRATEGY.md` |
| Organization Rules | `agent0-pdlc-<org>/ORGANIZATION-RULES.md` |
| Global Rules | `agent0-pdlc/GLOBAL-RULES.md` |

---

## 11. Resume Instructions

To continue from this handoff:

1. Read this document
2. Run `yarn bd:list` to see current tasks
3. Check git status for any uncommitted work
4. Bootstrap Agent0 with: "Continue from HANDOFF.md"

---

**Handoff created by**: <Agent0 identifier>
**Beads synced**: <Yes/No>
**Git pushed**: <Yes/No>
