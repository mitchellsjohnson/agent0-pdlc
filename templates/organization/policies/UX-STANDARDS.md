# UX Standards – <Your Organization Name>

This document defines the organization's UX/UI standards for all applications.

**Organization**: <Your Organization Name>
**Last Updated**: <Date>
**Design Team Contact**: <Contact>

---

## Design System Reference

<!-- CUSTOMIZE: Link to your design system -->

**Design System**: <Link to your design system documentation>
**Component Library**: <Link to component library / Storybook>
**Figma/Sketch Files**: <Link if applicable>

---

## Core Principles

<!-- CUSTOMIZE: Define your UX principles -->

### 1. <Principle 1>
<Description>

### 2. <Principle 2>
<Description>

### 3. <Principle 3>
<Description>

Example:
1. **Consistency First** - Same patterns, same behavior across all products
2. **Accessibility Always** - WCAG 2.1 AA compliance minimum
3. **User-Centered** - Design for user needs, validated by research

---

## Component Library

<!-- CUSTOMIZE: Define your component library -->

### Primary Component Library

| Library | Use For | Documentation |
|---------|---------|---------------|
| <Library Name> | <All apps / Web / Mobile / etc.> | <Link> |

Example:
- React Shared Components (RSC) for web applications
- Radix UI for new products
- Material UI for internal tools

### When to Use Which

<!-- CUSTOMIZE: Define when to use different libraries -->

| Scenario | Use |
|----------|-----|
| <Scenario 1> | <Library> |
| <Scenario 2> | <Library> |

---

## Typography

<!-- CUSTOMIZE: Define your typography standards -->

| Element | Font | Size | Weight |
|---------|------|------|--------|
| Headings | <Font> | <Sizes> | <Weights> |
| Body | <Font> | <Size> | <Weight> |
| Code | <Font> | <Size> | <Weight> |

---

## Color System

<!-- CUSTOMIZE: Define your color system -->

### Primary Colors

| Color | Hex | Usage |
|-------|-----|-------|
| <Color Name> | <#hex> | <Usage> |

### Status Colors

| Status | Hex | Usage |
|--------|-----|-------|
| Success | <#hex> | Positive actions, confirmations |
| Warning | <#hex> | Caution, pending states |
| Error | <#hex> | Errors, destructive actions |
| Info | <#hex> | Informational messages |

### Accessibility

- Text contrast ratio: minimum 4.5:1
- Large text contrast ratio: minimum 3:1
- UI component contrast ratio: minimum 3:1

---

## Layout Standards

<!-- CUSTOMIZE: Define your layout standards -->

### Grid System

| Breakpoint | Width | Columns | Gutter |
|------------|-------|---------|--------|
| Mobile | <width> | <cols> | <gutter> |
| Tablet | <width> | <cols> | <gutter> |
| Desktop | <width> | <cols> | <gutter> |

### Spacing Scale

| Token | Value | Usage |
|-------|-------|-------|
| space-1 | <px> | <Usage> |
| space-2 | <px> | <Usage> |
| space-3 | <px> | <Usage> |

---

## Accessibility Requirements

<!-- CUSTOMIZE: Define your accessibility requirements -->

### Minimum Standard

**WCAG Version**: <2.1 / 2.2>
**Conformance Level**: <A / AA / AAA>

### Required Checks

- [ ] Keyboard navigation works for all interactions
- [ ] Focus indicators visible (min 2px)
- [ ] All images have alt text
- [ ] Form labels properly associated
- [ ] Color is not the only indicator
- [ ] Touch targets minimum 44x44px
- [ ] Screen reader tested

### Testing Tools

| Tool | Use For |
|------|---------|
| <Tool 1> | <Purpose> |
| <Tool 2> | <Purpose> |

Example:
- axe DevTools for automated checks
- Lighthouse for accessibility score
- VoiceOver/NVDA for screen reader testing

---

## Testability Requirements

<!-- CUSTOMIZE: Define testability requirements -->

### data-testid Convention

```
{page}-{element-type}-{identifier}
```

Example:
- `users-page` - Page container
- `users-list` - List component
- `users-button-create` - Create button
- `users-input-email` - Email input

### Required Attributes

All forms must include:
- `data-testid` on all interactive elements
- `data-loading` for loading states
- `data-dirty` for unsaved changes
- `data-valid` for form validation

---

## Responsive Design

<!-- CUSTOMIZE: Define responsive requirements -->

### Supported Breakpoints

| Name | Width | Priority |
|------|-------|----------|
| <Mobile> | <width> | <Required/Optional> |
| <Tablet> | <width> | <Required/Optional> |
| <Desktop> | <width> | <Required/Optional> |

### Mobile-First vs Desktop-First

<Specify your approach>

---

## Dark Mode

<!-- CUSTOMIZE: Define dark mode requirements -->

| Requirement | Details |
|-------------|---------|
| Support Required | <Yes / No / Future> |
| Default Mode | <Light / Dark / System> |
| Toggle Location | <Describe> |

---

## Agent0 PDLC Integration

### AgentUX Configuration

AgentUX should:

1. Read this document at session start
2. Enforce component library usage
3. Check accessibility compliance
4. Verify testability patterns

### Veto Conditions (Organization-Specific)

AgentUX MUST block release for:

<!-- CUSTOMIZE: Define your veto conditions -->

1. <Veto condition 1>
2. <Veto condition 2>

Example:
1. Accessibility violations (WCAG AA failures)
2. Missing data-testid on interactive elements
3. Custom components where shared exist
4. Color contrast failures

---

## Resources

<!-- CUSTOMIZE: Link to design resources -->

| Resource | Link |
|----------|------|
| Design System Docs | <Link> |
| Component Library | <Link> |
| Figma/Design Files | <Link> |
| Accessibility Guide | <Link> |
| UX Team Contact | <Contact> |
