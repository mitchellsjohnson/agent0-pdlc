# Testing Strategy – <Application Name>

**Application**: <Application Name>
**Last Updated**: <Date>
**Maintained By**: <Team/Person>

---

## Overview

<!-- CUSTOMIZE: Your testing philosophy for this app -->

<Describe the testing approach for this specific application>

---

## Test Types

<!-- CUSTOMIZE: Which test types apply to this app -->

| Test Type | Used | Framework | Location |
|-----------|------|-----------|----------|
| Unit Tests | <Yes/No> | <Framework> | <Path> |
| Integration Tests | <Yes/No> | <Framework> | <Path> |
| E2E Tests | <Yes/No> | <Framework> | <Path> |
| API Tests | <Yes/No> | <Framework> | <Path> |
| Performance Tests | <Yes/No> | <Framework> | <Path> |

---

## Test Commands

<!-- CUSTOMIZE: All test commands -->

### Unit Tests

```bash
# Run all unit tests
<command>

# Run with coverage
<command with coverage>

# Run specific test file
<command for specific file>

# Run tests in watch mode
<watch mode command>
```

### Integration Tests

```bash
# Run integration tests
<command>

# Run specific integration test
<command for specific test>
```

### E2E Tests

```bash
# Run E2E tests
<command>

# Run specific E2E test
<command for specific test>

# Run E2E in headed mode (for debugging)
<headed mode command>
```

### All Tests

```bash
# Run entire test suite
<command for all tests>
```

---

## Coverage Requirements

<!-- CUSTOMIZE: Coverage thresholds for this app -->

### Thresholds

| Metric | New Code | Existing Code |
|--------|----------|---------------|
| Statements | <threshold>% | <threshold>% |
| Branches | <threshold>% | <threshold>% |
| Functions | <threshold>% | <threshold>% |
| Lines | <threshold>% | <threshold>% |

### Critical Paths (100% Required)

<!-- CUSTOMIZE: What must have 100% coverage -->

- <Critical path 1>
- <Critical path 2>

---

## Test Data

<!-- CUSTOMIZE: How test data works in this app -->

### Fixtures Location

```
<path to test fixtures>
```

### Test Database

<!-- CUSTOMIZE: If applicable -->

| Setting | Value |
|---------|-------|
| Type | <In-memory / Docker / etc.> |
| Setup | <How to set up> |
| Teardown | <How to tear down> |

### Mock Data

<!-- CUSTOMIZE: How mocking works -->

```
<path to mock data or setup>
```

---

## Known Constraints

<!-- CUSTOMIZE: App-specific testing constraints -->

### Framework Limitations

<!-- Document any testing framework limitations -->

| Component | Issue | Workaround |
|-----------|-------|------------|
| <Component> | <Issue> | <Workaround> |

### Environment Requirements

<!-- CUSTOMIZE: What's needed to run tests -->

- <Requirement 1>
- <Requirement 2>

---

## Test Patterns

<!-- CUSTOMIZE: Patterns specific to this app -->

### Component Test Pattern

```typescript
// Example test structure for this app
<example test code>
```

### API Test Pattern

```typescript
// Example API test for this app
<example test code>
```

---

## CI/CD Integration

<!-- CUSTOMIZE: How tests run in CI -->

### Pipeline Stages

| Stage | Tests Run | Timeout | Blocking |
|-------|-----------|---------|----------|
| Pre-commit | <tests> | <timeout> | <yes/no> |
| PR | <tests> | <timeout> | <yes/no> |
| Merge | <tests> | <timeout> | <yes/no> |

### Running Tests Locally Like CI

```bash
# Simulate CI test run locally
<command>
```

---

## Debugging Tests

<!-- CUSTOMIZE: How to debug in this app -->

### Unit Tests

```bash
# Run with debugger
<debug command>
```

### E2E Tests

```bash
# Run with visual browser
<headed command>

# Run with Playwright inspector
<inspector command>
```

### Viewing Test Reports

```bash
# Generate and view report
<report command>
```

**Report location**: <path>

---

## Agent0 PDLC Notes

### For AgentSET

When testing this application:

1. **Always run baseline first** - Document coverage before changes
2. **Use these exact commands** - They're configured for this app
3. **Check CI/CD config** - Tests may differ locally vs CI
4. **Report coverage delta** - Before/after comparison

### Coverage Tool

```bash
# Generate coverage report
<coverage command>

# View coverage report
<view coverage command>
```

### Test Infrastructure Issues

<!-- CUSTOMIZE: Common test infra issues -->

If tests fail to run:
1. <Common fix 1>
2. <Common fix 2>

---

## Appendix: Test File Conventions

<!-- CUSTOMIZE: Naming conventions -->

| Type | Pattern | Example |
|------|---------|---------|
| Unit Test | <pattern> | <example> |
| Integration | <pattern> | <example> |
| E2E | <pattern> | <example> |
