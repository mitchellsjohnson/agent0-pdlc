# Build Instructions – <Application Name>

**Application**: <Application Name>
**Last Updated**: <Date>
**Maintained By**: <Team/Person>

---

## Overview

<!-- CUSTOMIZE: Describe your application -->

<Brief description of what this application does and its architecture>

---

## Prerequisites

<!-- CUSTOMIZE: List all prerequisites -->

### Required Software

| Tool | Version | Purpose | Installation |
|------|---------|---------|--------------|
| <Tool> | <Version> | <Purpose> | <Install command> |

Example:
| Tool | Version | Purpose | Installation |
|------|---------|---------|--------------|
| Node.js | 22.x | Runtime | `brew install node@22` |
| Java | 17+ | Backend | `brew install openjdk@17` |
| Docker | Latest | Containers | `brew install docker` |

### Environment Setup

<!-- CUSTOMIZE: List environment requirements -->

```bash
# Required environment variables
export <VAR_NAME>=<value>
```

---

## Initial Setup

<!-- CUSTOMIZE: First-time setup steps -->

### 1. Clone Repository

```bash
git clone <repository-url>
cd <app-directory>
```

### 2. Install Dependencies

```bash
# <Your install commands>
```

### 3. Configure Environment

```bash
# <Your config commands>
```

---

## Build Commands

<!-- CUSTOMIZE: All build commands -->

### Development Build

```bash
# <Development build command>
```

**Time**: <expected time>
**Output**: <what gets built>

### Production Build

```bash
# <Production build command>
```

**Time**: <expected time>
**Output**: <what gets built>

### Incremental Build

```bash
# <Incremental build command - for quick iteration>
```

**Time**: <expected time>
**When to use**: <when this is appropriate>

---

## Running the Application

<!-- CUSTOMIZE: How to run -->

### Development Mode

```bash
# <Run in development>
```

**URL**: <local URL>
**Credentials**: <default credentials>

### Production Mode

```bash
# <Run in production mode locally>
```

---

## Development Workflow

<!-- CUSTOMIZE: Day-to-day development -->

### Making Changes

1. <Step 1>
2. <Step 2>
3. <Step 3>

### Hot Reload / Watch Mode

```bash
# <Watch mode command if available>
```

**Supported**: <what gets hot reloaded>
**Not Supported**: <what requires restart>

---

## Testing

<!-- CUSTOMIZE: Link to testing strategy or summarize -->

See `TESTING-STRATEGY.md` for full details.

### Quick Test Commands

```bash
# Unit tests
<unit test command>

# Integration tests
<integration test command>

# E2E tests
<e2e test command>
```

---

## Common Issues

<!-- CUSTOMIZE: Document common problems -->

### Issue: <Common Issue 1>

**Symptoms**: <what you see>

**Solution**:
```bash
# <fix command>
```

### Issue: <Common Issue 2>

**Symptoms**: <what you see>

**Solution**:
```bash
# <fix command>
```

---

## Project Structure

<!-- CUSTOMIZE: Key directories -->

```
<app-root>/
├── <dir1>/           # <purpose>
├── <dir2>/           # <purpose>
├── <dir3>/           # <purpose>
└── <config-files>    # <purpose>
```

---

## Key Technologies

<!-- CUSTOMIZE: Tech stack summary -->

| Layer | Technology | Documentation |
|-------|------------|---------------|
| Frontend | <tech> | <link> |
| Backend | <tech> | <link> |
| Database | <tech> | <link> |
| Testing | <tech> | <link> |

---

## Agent0 PDLC Notes

### For Agents

When working on this application:

1. **Always run incremental builds** unless told otherwise
2. **Check for running processes** before starting servers
3. **Use the test commands** specified above
4. **Reference this file** for any build-related questions

### Data Protection

<!-- CUSTOMIZE: Critical data to protect -->

**NEVER delete these without confirmation:**
- <directory or file 1>
- <directory or file 2>

### Build After Maven/Gradle/etc.

<!-- CUSTOMIZE: Post-build steps if any -->

```bash
# <Any required post-build steps>
```

---

## Support

For build issues:
- <Contact/channel>
- <Documentation link>
