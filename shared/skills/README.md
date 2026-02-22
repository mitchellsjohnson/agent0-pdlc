# Cross-Functional Skills (Template)

Skills are specialized instructions that extend agent behavior for organization-specific tools and processes.

## Structure

Organize skills by the **agent role** that uses them:

```
shared/skills/
├── security/           # Skills for SecurityEngineer agents
│   └── skill-name/
│       └── SKILL.md
├── ux/                 # Skills for UX agents
│   └── skill-name/
│       └── SKILL.md
├── set/                # Skills for SoftwareEngineerInTest agents
│   └── skill-name/
│       └── SKILL.md
└── engineering/        # Skills for all SoftwareEngineer agents
    └── skill-name/
        └── SKILL.md
```

## Skill Format (Cursor SKILL.md)

Each skill follows the Cursor SKILL.md format with YAML frontmatter:

```markdown
---
name: skill-name
description: What it does and when to use it. Be specific.
---

# Skill Title

## Instructions

Step-by-step guidance for the agent.
```

### Key Principles

- **Under 500 lines** per SKILL.md
- **Concise**: Only include info the agent doesn't already know
- **Specific description**: Include both WHAT and WHEN
- **Progressive disclosure**: Link to reference files for details

## Example Skills

| Role | Skill | Purpose |
|------|-------|---------|
| Security | `lifecycle-scan` | SCA scanning and remediation |
| Security | `threat-modeling` | STRIDE threat modeling |
| UX | `figma-review` | Design-to-code review |
| UX | `accessibility-audit` | WCAG compliance checking |
| SET | `test-strategy` | Test planning and quality gates |
| Engineering | `secure-coding` | Secure coding patterns |
