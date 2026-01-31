# Organization Rules – <Your Organization Name>

This document extends `agent0-pdlc/GLOBAL-RULES.md` with organization-specific rules.

**Organization**: <Your Organization Name>
**Last Updated**: <Date>
**Maintained By**: <Team/Person>

---

## Organization Overview

<!-- CUSTOMIZE: Describe your organization -->

<Your organization description here. What does your organization do? What are your core values regarding software development?>

---

## Extends Generic Rules

This document extends, but does not replace, the rules in `agent0-pdlc/GLOBAL-RULES.md`.

**All generic rules apply unless explicitly overridden here.**

---

## Organization-Specific Rules

### Compliance Requirements

<!-- CUSTOMIZE: Add your compliance requirements -->

| Requirement | Description | Applies To |
|-------------|-------------|------------|
| <Requirement 1> | <Description> | <All apps / Specific apps> |
| <Requirement 2> | <Description> | <All apps / Specific apps> |

Example:
- SOC 2 compliance required for all customer-facing applications
- HIPAA compliance required for healthcare applications
- GDPR compliance required for EU data handling

### Legal Requirements

<!-- CUSTOMIZE: Add legal requirements -->

- <Legal requirement 1>
- <Legal requirement 2>

Example:
- All code must include copyright headers
- Third-party licenses must be reviewed before use
- No GPL-licensed code in proprietary products

### Process Requirements

<!-- CUSTOMIZE: Add process requirements -->

- <Process requirement 1>
- <Process requirement 2>

Example:
- All PRs require two approvals
- Security review required for authentication code
- Accessibility review required for UI changes

---

## Technology Constraints

<!-- CUSTOMIZE: Define what's allowed/forbidden -->

### Approved Technologies

See `policies/TECH-STACK.md` for the full list.

**Summary:**
- Languages: <list approved languages or "any">
- Frameworks: <list approved frameworks or "any">
- Databases: <list approved databases or "any">
- Cloud Providers: <list approved providers or "any">

### Forbidden Technologies

<!-- CUSTOMIZE: List forbidden technologies -->

- <Technology 1>: <Reason>
- <Technology 2>: <Reason>

Example:
- jQuery: Use React instead
- MongoDB: Use PostgreSQL for consistency

---

## Security Policy Reference

See `policies/SECURITY-POLICY.md` for the full security policy.

**Key Points:**
- <!-- CUSTOMIZE: List key security requirements -->
- Dependency scanning required before release
- No secrets in code (use vault)
- All endpoints require authentication

---

## UX Standards Reference

See `policies/UX-STANDARDS.md` for the full UX standards.

**Key Points:**
- <!-- CUSTOMIZE: List key UX requirements -->
- WCAG 2.1 AA compliance required
- Use organization design system
- Responsive design required

---

## Testing Policy Reference

See `policies/TESTING-POLICY.md` for the full testing policy.

**Key Points:**
- <!-- CUSTOMIZE: List key testing requirements -->
- 80% code coverage minimum on new code
- E2E tests for critical user journeys
- Performance testing for high-traffic endpoints

---

## Ticketing System Integration

<!-- CUSTOMIZE: Define your ticketing system -->

| Setting | Value |
|---------|-------|
| System | <Jira / GitHub Issues / Linear / etc.> |
| Project Format | <Project key format> |
| Required Fields | <List required fields> |

Example:
- System: Jira
- Project: All projects use format `<TEAM>-<NUMBER>`
- Required: Priority, Component, Sprint

---

## Source Control Standards

<!-- CUSTOMIZE: Define your source control standards -->

| Setting | Value |
|---------|-------|
| Host | <GitHub / GitLab / Bitbucket / etc.> |
| Branch Strategy | <GitFlow / Trunk-based / etc.> |
| PR Requirements | <List requirements> |

Example:
- Host: GitHub Enterprise
- Branch Strategy: Trunk-based with feature branches
- PR Requirements: 2 approvals, CI passing, no conflicts

---

## CI/CD Requirements

<!-- CUSTOMIZE: Define CI/CD requirements -->

- <CI/CD requirement 1>
- <CI/CD requirement 2>

Example:
- All repos must have CI pipeline
- Deployments require approval for production
- Automated security scanning in pipeline

---

## Agent Extensions

<!-- CUSTOMIZE: Reference any agent extensions -->

Custom agent behaviors for this organization:

| Agent | Extension | Purpose |
|-------|-----------|---------|
| AgentUX | `agents/extensions/AGENTUX-ORG.md` | <Purpose> |
| AgentSecurity | `agents/extensions/AGENTSECURITY-ORG.md` | <Purpose> |

---

## Skills

<!-- CUSTOMIZE: List organization skills -->

Available organization skills in `skills/`:

| Skill | File | Purpose |
|-------|------|---------|
| <Skill 1> | `skills/<skill>.md` | <Purpose> |

---

## Contact

<!-- CUSTOMIZE: Add contact information -->

For questions about these rules:
- <Contact person/team>
- <Contact email/channel>
