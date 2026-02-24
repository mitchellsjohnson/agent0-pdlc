# Model Cost Optimization

Agent0 uses this skill during the CRIT Role phase to assign model tiers to each agent. The goal is to minimize cost without sacrificing quality where it matters.

## Tiers

| Tier | Purpose | When to Use |
|------|---------|-------------|
| **Orchestrator** | Agent0 only | Architecture decisions, sprint planning, cross-agent coordination |
| **High** | Judgment-intensive work | Security review with veto authority, complex multi-step reasoning, architecture |
| **Mid** | Standard development | Implementation, code review, test writing, most SQUAD/COE work |
| **Fast** | Routine tasks | Documentation, exploration, boilerplate, formatting, simple refactoring |

## Decision Rules

1. **Agent0**: Always Orchestrator tier (orchestration requires best reasoning)
2. **COE with veto authority** (SecurityEngineer reviewing critical code): High
3. **COE advisory** (UX, SET, Security on routine scans): Mid
4. **SQUAD implementation** (SoftwareEngineer): Mid default
5. **Downgrade to Fast when**:
    - Task is documentation-only
    - Task is exploration/research (many parallel cheap searches > one expensive one)
    - Task is boilerplate generation or simple refactoring
    - Task is test data creation or formatting

## Agent Strategy Format

When declaring your Agent Strategy, include model tier for each agent:

```
## Agent Strategy

### Core COE
| Agent | Tier | Rationale |
|-------|------|-----------|
| SecurityEngineer | High | Auth review, veto authority |
| UXAgent | Mid | Design system compliance |
| SET | Mid | Test strategy, coverage |

### SQUAD
| Agent | Tier | Rationale |
|-------|------|-----------|
| Dev1 (backend) | Mid | API implementation |
| Dev2 (frontend) | Mid | React components |
| Dev3 (docs) | Fast | Documentation generation |

Estimated cost: ~X% of all-Orchestrator baseline
```

## Tier Escalation

An agent may request a tier upgrade mid-sprint if:
- Task complexity was underestimated
- Agent is producing low-quality output at current tier
- Security-critical code path discovered during implementation

Agent0 approves or denies tier upgrades. Document the change in the sprint log.

## Provider Requirements

The organization config (`agent0-pdlc-<org>/shared/skills/orchestration/model-cost-optimization.md`) maps tiers to approved model providers and specific models. Only models from approved providers may be used.
