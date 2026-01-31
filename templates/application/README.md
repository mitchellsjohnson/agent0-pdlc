# Application-Level Agent0 PDLC Template

This folder contains the template for your application-level Agent0 PDLC configuration.

---

## Setup Instructions

### 1. Create the Application Folder

In your application repository:

```bash
# Create the folder
mkdir agent0-pdlc-<app-name>

# Copy this template
cp -r <path-to-agent0-pdlc>/templates/application/* agent0-pdlc-<app-name>/

# Replace placeholders
# Replace all instances of <app-name> with your application name
```

### 2. Customize Required Files

| File | Required | What to Add |
|------|----------|-------------|
| `BUILD-INSTRUCTIONS.md` | ✅ Yes | How to build THIS application |
| `TESTING-STRATEGY.md` | ✅ Yes | Testing strategy for THIS app |
| `SECURITY-STRATEGY.md` | If security-sensitive | App-specific security notes |
| `UX-STRATEGY.md` | If UI work | App-specific UX notes |
| `agents/` | Optional | App-specific agent extensions |
| `skills/` | Optional | App-specific skills |

### 3. Ensure Framework Access

Your AI agents need access to all three tiers:

1. **Generic** (`agent0-pdlc/`) - Clone or symlink
2. **Organization** (`agent0-pdlc-<org>/`) - Clone or symlink
3. **Application** (`agent0-pdlc-<app>/`) - This folder

---

## File Structure

```
agent0-pdlc-<app-name>/
├── README.md                     # This file
├── BUILD-INSTRUCTIONS.md         # How to build this app
├── TESTING-STRATEGY.md           # Testing for this app
├── SECURITY-STRATEGY.md          # Security for this app (optional)
├── UX-STRATEGY.md                # UX for this app (optional)
│
├── agents/                       # Agent extensions (optional)
│   └── README.md                 # How to extend agents
│
├── skills/                       # App-specific skills (optional)
│   └── README.md                 # How to add skills
│
└── .beads/                       # Beads configuration
    └── config.yaml               # Beads config for this app
```

---

## Usage

### Bootstrap Agent0

When bootstrapping Agent0 for this application, it will read:

1. `agent0-pdlc/agents/AGENT0.md` (generic)
2. `agent0-pdlc-<org>/ORGANIZATION-RULES.md` (org overrides)
3. `agent0-pdlc-<app>/BUILD-INSTRUCTIONS.md` (app specifics)

### Precedence

Application config overrides Organization, which overrides Generic:

```
App > Org > Generic
```

---

## Maintenance

- Update when build process changes
- Update when testing strategy changes
- Keep in sync with application code
- Commit with application changes
