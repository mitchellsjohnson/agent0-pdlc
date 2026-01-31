# Organization-Level Agent0 PDLC Template

This folder contains the template for your organization-level Agent0 PDLC configuration.

---

## Setup Instructions

### 1. Create Your Organization Repo

```bash
# Create repo
mkdir agent0-pdlc-<your-org>
cd agent0-pdlc-<your-org>
git init

# Copy this template
cp -r <path-to-agent0-pdlc>/templates/organization/* .

# Rename placeholders
# Replace all instances of <your-org> with your organization name
```

### 2. Customize Required Files

| File | Required | What to Add |
|------|----------|-------------|
| `ORGANIZATION-RULES.md` | ✅ Yes | Your org's non-negotiable rules |
| `policies/SECURITY-POLICY.md` | ✅ Yes | Link to or embed your security policy |
| `policies/UX-STANDARDS.md` | If UI work | Link to your design system |
| `policies/TESTING-POLICY.md` | ✅ Yes | Your testing requirements |
| `policies/TECH-STACK.md` | Optional | Approved languages/frameworks |
| `skills/` | Optional | Organization-specific AI skills |

### 3. Connect to Generic Framework

Ensure your org repo references the generic `agent0-pdlc`:

```yaml
# In .beads/config.yaml
extends:
  - https://github.com/mitchellsjohnson/agent0-pdlc
```

### 4. Push to Your Git Host

```bash
git add -A
git commit -m "Initial organization framework"
git remote add origin <your-git-host>/agent0-pdlc-<your-org>
git push -u origin main
```

---

## File Structure

```
agent0-pdlc-<your-org>/
├── README.md                     # This file
├── ORGANIZATION-RULES.md         # Org-wide rules (extends generic)
│
├── policies/
│   ├── SECURITY-POLICY.md        # Security requirements
│   ├── UX-STANDARDS.md           # UX/Design standards
│   ├── TESTING-POLICY.md         # Testing requirements
│   └── TECH-STACK.md             # Approved technologies
│
├── agents/
│   └── extensions/               # Agent extensions (optional)
│       ├── AGENTUX-ORG.md        # Org-specific UX rules
│       └── AGENTSECURITY-ORG.md  # Org-specific security rules
│
├── skills/                       # Organization skills
│   └── README.md                 # How to add skills
│
└── resources/                    # Shared resources
    ├── personas/                 # User personas (if defined)
    └── references/               # Reference documentation links
```

---

## Usage by Application Teams

Application teams should:

1. Clone or reference this org repo
2. Give AI agents access to this repo
3. Create their app-level configuration

AI agents will read:
1. Generic `agent0-pdlc/` first
2. Your org repo second (overrides generic)
3. App-level config third (overrides org)

---

## Maintenance

- Review quarterly or when policies change
- Notify all teams of breaking changes
- Version significant changes with tags
