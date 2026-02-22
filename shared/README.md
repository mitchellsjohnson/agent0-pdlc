# Shared Resources (Organization-Wide)

This directory contains resources shared across **all agents** and **all products** in your organization.

## Structure

```
shared/
├── policies/           # Organization-wide standards
│   ├── SECURITY-POLICY.md
│   ├── UX-STANDARDS.md
│   ├── TESTING-POLICY.md
│   └── TECH-STACK.md
│
├── integrations/       # Tool integrations (Jira, CI/CD, SCA, etc.)
│   └── README.md
│
├── mcp/                # MCP server configurations
│   └── README.md
│
├── skills/             # Cross-functional skills by agent role
│   ├── security/       # Skills for SecurityEngineer agents
│   ├── ux/             # Skills for UX agents
│   ├── set/            # Skills for SET agents
│   └── engineering/    # Skills for SoftwareEngineer agents
│
└── templates/          # Shared templates (PR, handoff, etc.)
```

## Three Scopes

| Scope | Location | Description |
|-------|----------|-------------|
| **Organization** | `shared/integrations/`, `shared/mcp/`, `shared/policies/` | Every agent, every product |
| **Agent Role** | `shared/skills/{role}/` | Specific role, any product |
| **Product** | `products/{product}/skills/` | Any role, specific product |

## Customization

When creating your organization's config (`agent0-pdlc-<yourorg>/`), populate these directories with your organization-specific content. See the template READMEs in each subdirectory for guidance.
