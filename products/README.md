# Product-Specific Configurations (Template)

This directory contains configurations specific to individual products in your organization.

## Structure

Create a subdirectory for each product:

```
products/
├── product-name/
│   ├── README.md           # Product overview
│   ├── skills/             # Developer skills for this product
│   │   └── skill-name/
│   │       └── SKILL.md
│   ├── integrations/       # Product-specific integrations
│   │   └── README.md
│   ├── mcp/                # Product-specific MCP servers
│   │   └── README.md
│   ├── Initiatives/        # Feature specs and requirements
│   └── Teams/              # Team-specific sprint history
```

## Scope

Resources here apply to **any agent role** working on **this specific product**. They complement (not replace) the organization-wide resources in `shared/`.

| Resource Type | Organization-wide (`shared/`) | Product-specific (`products/`) |
|--------------|------------------------------|-------------------------------|
| Policies | Security, UX, Testing standards | Product-specific overrides |
| Integrations | Jira, GitHub, CI/CD | Product-specific APIs, tools |
| MCP | Dependency scanning, project tracking | Product-specific tooling |
| Skills | Cross-functional (by role) | Product developer skills |

## Example

```
products/
├── my-web-app/
│   ├── skills/
│   │   └── api-patterns/SKILL.md     # How to write APIs for this app
│   ├── integrations/
│   │   └── STRIPE.md                 # Stripe payment integration
│   └── Teams/
│       └── team-alpha/               # Sprint history for team alpha
└── my-data-service/
    └── skills/
        └── databricks/SKILL.md       # Databricks usage for this product
```
