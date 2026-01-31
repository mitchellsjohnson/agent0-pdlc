# Organization Skills

This folder contains organization-specific AI skills.

---

## What Are Skills?

Skills are specialized instructions or capabilities that extend agent behavior for organization-specific tools, processes, or requirements.

---

## When to Create a Skill

Create a skill when:
- You have a tool/process unique to your organization
- You want consistent agent behavior for a specific task
- You need to encode domain knowledge

---

## Skill Structure

Each skill should be a Markdown file with:

```markdown
# Skill: <Skill Name>

## Purpose
<What this skill does>

## When to Use
<Trigger conditions>

## Instructions
<Step-by-step instructions for the agent>

## Examples
<Example usage>

## Related
<Related skills or documentation>
```

---

## Example Skills

### Internal Tool Integration

```markdown
# Skill: Internal Deployment Tool

## Purpose
Deploy applications using our internal deployment system.

## When to Use
When deploying to staging or production environments.

## Instructions
1. Verify build is successful
2. Run: `deploy-tool --env <env> --app <app>`
3. Monitor deployment dashboard at <link>
4. Verify health checks pass

## Examples
deploy-tool --env staging --app user-service

## Related
- CI/CD documentation
- Deployment runbook
```

### Organization-Specific Patterns

```markdown
# Skill: Logging Pattern

## Purpose
Use organization-standard logging patterns.

## When to Use
When adding logging to any code.

## Instructions
1. Use structured logging
2. Include correlation IDs
3. Follow log level guidelines:
   - ERROR: Failures requiring attention
   - WARN: Unexpected but handled
   - INFO: Business events
   - DEBUG: Diagnostic info

## Examples
logger.info("User created", { userId: user.id, correlationId: ctx.correlationId });

## Related
- Logging standards documentation
- Observability guide
```

---

## Adding a New Skill

1. Create a new `.md` file in this folder
2. Follow the structure above
3. Reference in agent prompts or `ORGANIZATION-RULES.md`
4. Commit and push

---

## Using Skills

Skills are loaded by agents when:
1. Referenced in bootstrap prompts
2. Listed in `ORGANIZATION-RULES.md`
3. Triggered by specific contexts

Example bootstrap prompt addition:
```
Also read these skills:
- agent0-pdlc-org/skills/deployment.md
- agent0-pdlc-org/skills/logging.md
```
