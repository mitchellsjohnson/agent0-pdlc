# Testing Policy – <Your Organization Name>

This document defines the organization's testing requirements for all applications.

**Organization**: <Your Organization Name>
**Last Updated**: <Date>
**QA Team Contact**: <Contact>

---

## Testing Philosophy

<!-- CUSTOMIZE: Define your testing philosophy -->

<Describe your organization's approach to testing>

Example:
> We believe in testing at the lowest level possible where behavior can be verified reliably. We prioritize meaningful coverage over metric-driven coverage.

---

## Coverage Requirements

<!-- CUSTOMIZE: Define your coverage requirements -->

### Minimum Thresholds

| Metric | New Code | Legacy Code |
|--------|----------|-------------|
| Statements | <threshold>% | <threshold>% |
| Branches | <threshold>% | <threshold>% |
| Functions | <threshold>% | <threshold>% |
| Lines | <threshold>% | <threshold>% |

Example:
- New code: 80% minimum
- Legacy code: Don't decrease existing coverage

### Critical Paths

<!-- CUSTOMIZE: Define what must be tested -->

These areas MUST have 100% coverage:
- <Critical area 1>
- <Critical area 2>

Example:
- Authentication/authorization code
- Payment processing
- Data encryption/decryption

---

## Testing Framework Standards

<!-- CUSTOMIZE: Define approved testing frameworks -->

### Unit Testing

| Language | Approved Frameworks |
|----------|---------------------|
| JavaScript/TypeScript | <Jest / Vitest / etc.> |
| Java | <JUnit 5 / TestNG / etc.> |
| Python | <pytest / unittest / etc.> |
| Go | <testing / testify / etc.> |

### Integration Testing

| Type | Approved Frameworks |
|------|---------------------|
| API Testing | <RestAssured / Supertest / etc.> |
| Database Testing | <Testcontainers / etc.> |
| Service Testing | <etc.> |

### E2E Testing

| Platform | Approved Frameworks |
|----------|---------------------|
| Web | <Playwright / Cypress / etc.> |
| Mobile | <Detox / Appium / etc.> |
| API | <Postman / Newman / etc.> |

---

## Test Types Required

<!-- CUSTOMIZE: Define when each test type is required -->

| Test Type | When Required | Who Writes |
|-----------|---------------|------------|
| Unit Tests | Always | Developers |
| Integration Tests | API changes, DB changes | Developers |
| E2E Tests | User journey changes | QA/Developers |
| Performance Tests | High-traffic features | Performance team |
| Security Tests | Auth, data handling | Security team |

---

## Test Data Management

<!-- CUSTOMIZE: Define test data requirements -->

### Test Data Sources

| Environment | Data Source |
|-------------|-------------|
| Unit Tests | Mocked data |
| Integration | <Fixtures / Factories / etc.> |
| E2E | <Seeded database / Mock server / etc.> |

### Sensitive Data

- [ ] Never use production data in tests
- [ ] Use anonymized data for realistic testing
- [ ] Test data fixtures must be version controlled
- [ ] <Additional requirements>

---

## CI/CD Integration

<!-- CUSTOMIZE: Define CI/CD testing requirements -->

### Pipeline Stages

| Stage | Tests Run | Blocking |
|-------|-----------|----------|
| Pre-commit | <tests> | <yes/no> |
| PR | <tests> | <yes/no> |
| Merge | <tests> | <yes/no> |
| Deploy | <tests> | <yes/no> |

### Time Budgets

| Stage | Max Duration |
|-------|--------------|
| Unit Tests | <duration> |
| Integration Tests | <duration> |
| E2E Tests | <duration> |
| Full Suite | <duration> |

---

## Test Quality Standards

<!-- CUSTOMIZE: Define test quality requirements -->

### Test Naming

```
<what>_<condition>_<expected>
```

Example:
- `createUser_withValidData_returnsNewUser`
- `login_withInvalidPassword_returnsError`

### Test Structure

```
// Arrange - Setup
// Act - Execute
// Assert - Verify
```

### What to Test

- ✅ Behavior, not implementation
- ✅ Edge cases and error conditions
- ✅ User-facing functionality
- ❌ Private methods directly
- ❌ Framework code
- ❌ Trivial getters/setters

---

## Flaky Test Policy

<!-- CUSTOMIZE: Define flaky test handling -->

| Action | Timeline |
|--------|----------|
| Identify flaky test | Immediately flag |
| Fix flaky test | <timeline> |
| Quarantine if can't fix | <timeline> |
| Delete if unfixable | <timeline> |

---

## Baseline First Rule

<!-- CUSTOMIZE: This is from generic, but emphasize -->

**CRITICAL**: ALWAYS run baseline before enhancing tests.

1. Run full test suite BEFORE changes
2. Document current coverage
3. Make changes
4. Run full test suite AFTER changes
5. Compare and document improvement

**Never estimate coverage - always measure.**

---

## Agent0 PDLC Integration

### AgentSET Configuration

AgentSET should:

1. Read this policy at session start
2. Use organization-approved test frameworks
3. Enforce coverage thresholds
4. Follow baseline-first rule
5. Integrate with organization CI/CD

### Veto Conditions (Organization-Specific)

AgentSET MUST block release for:

<!-- CUSTOMIZE: Define your veto conditions -->

1. <Veto condition 1>
2. <Veto condition 2>

Example:
1. Coverage below threshold on new code
2. Failing tests in CI
3. Skipped tests without documented reason
4. Missing E2E tests for new user journeys

---

## Resources

<!-- CUSTOMIZE: Link to testing resources -->

| Resource | Link |
|----------|------|
| Testing Guide | <Link> |
| Test Framework Docs | <Link> |
| CI/CD Documentation | <Link> |
| QA Team Contact | <Contact> |
