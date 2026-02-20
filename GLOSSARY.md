# Agent0 PDLC Glossary

Terms and definitions used throughout the Agent0 PDLC framework.

---

## Core Concepts

### Agent0
The orchestrating AI agent that serves as Product Owner and Technical Lead. Coordinates all other agents, plans sprints, assigns work, and manages quality. Uses the CRIT Framework to process requirements.

### PDLC
**P**roduct **D**evelopment **L**ife**c**ycle. The framework for managing the entire software development process with AI agents.

### CRIT Framework
The methodology Agent0 uses to process requirements and bootstrap sprints:
- **C**ontext: Gather background, goals, audience, constraints
- **R**ole: Determine which agents and specialists are needed
- **I**nterview: Ask clarifying questions before acting
- **T**ask: Define specific, actionable work items

Agent0 does NOT immediately act on requirements. It gathers context, interviews the user, then creates tasks.

### Beads
A distributed, git-backed graph issue tracker designed for AI agents ([steveyegge/beads](https://github.com/steveyegge/beads)). Provides persistent, structured memory for coding agents, replacing messy markdown plans with a dependency-aware graph. Tasks, status, dependencies, and assignments are tracked in Beads.

### SQUAD
The delivery team consisting of Agent0 and multiple AgentDev instances. Responsible for implementing features and fixing bugs.

### COE (Center of Excellence)
Specialist agents that ensure quality across domains:
- **AgentSET** - Software Engineer in Test
- **AgentSecurity** - Security Architect
- **AgentUX** - UX Architect

---

## Agent Types

### Orchestration Layer

#### Agent0
The orchestrating AI agent that serves as Product Owner and Technical Lead. Coordinates all other agents, plans sprints, assigns work, and manages quality.

#### SegmentTechLead
Intermediate coordinator for large organizations. Manages a segment/domain under Agent0's direction, coordinating segment-specific SQUAD and COE teams.

### Product Layer

#### ProductManager
Owns roadmap and prioritization. Defines what to build and why, manages product backlog, and coordinates with stakeholders.

#### ProgramManager
Owns cross-team delivery. Manages schedules, dependencies, and risk tracking across multiple teams and segments.

#### ProductOperations
Owns process, analytics, and release readiness. Manages release gates, metrics dashboards, and operational excellence.

#### ProductMarketing
Owns positioning and launch. Manages go-to-market strategy, messaging, and launch timing.

### UX Layer

#### UXAgent
Owns UX, accessibility, and design systems. Ensures consistent user experience and WCAG compliance. *(Also known as AgentUX)*

#### ProductDocumentation
Owns technical writing and user documentation. Manages documentation standards, user guides, and API documentation.

### Engineering Layer

#### SoftwareEngineer
Software Engineer agent. Implements features, writes code, and follows Agent0's direction. Multiple instances can work in parallel. *(Also known as AgentDev)*

#### SoftwareEngineerInTest
Software Engineer in Test. Owns quality strategy, coverage requirements, and has authority to block releases on quality grounds. *(Also known as AgentSET)*

#### DevOpsEngineer
Owns CI/CD and infrastructure. Manages pipelines, deployment strategies, and infrastructure as code.

### Security Layer

#### SecurityEngineer
Security Architect. Reviews code for security issues, scans dependencies, and has release veto authority for security vulnerabilities. *(Also known as AgentSecurity)*

#### SecurityResearcher
Owns threat research. Monitors emerging threats, researches vulnerabilities, and provides threat intelligence to the team.

### Data Layer

#### DataEngineer
Owns data pipelines. Builds and maintains ETL/ELT processes, data architecture, and data quality frameworks.

#### DataAnalyst
Owns analysis and reporting. Creates dashboards, performs data analysis, and delivers actionable insights.

#### DataScientist
Owns ML/AI models. Develops machine learning models, conducts experiments, and manages model deployment.

---

## Architecture

### Three-Tier Framework
The hierarchical structure of Agent0 PDLC:
1. **Generic Tier** - Public framework (agent0-pdlc)
2. **Organization Tier** - Org-specific policies (agent0-pdlc-<org>)
3. **Application Tier** - App-specific config (agent0-pdlc-<app>)

### Generic Tier
The public, open-source framework. Contains agent operating manuals, workflows, and templates. No organization or application-specific content.

### Organization Tier
Private repository for an organization. Contains security policies, UX standards, testing requirements, and shared skills that apply to all applications in the organization.

### Application Tier
Configuration specific to a single application. Contains build instructions, testing strategy, and app-specific skills.

---

## Communication

### Markdown (MD)
Human-readable documentation. Contains intent, requirements, decisions, and explanations. **MD is for humans.**

### Beads Tasks
Machine-readable work items. Contains tasks, status, assignments, and dependencies. **Beads is for machines.**

### The Cardinal Rule
> Read Markdown to understand the system.
> Read Beads to understand the work.
> Never rely on one to replace the other.

---

## Workflows

### Bootstrap
The process of initializing an agent with its operating manual, rules, and context. Each agent type has a specific bootstrap prompt.

### Sprint
A time-boxed period of work. Agent0 creates sprint plans in Beads, assigns tasks, and manages completion.

### Handoff
The process of ending a session and documenting state for the next session. Includes HANDOFF.md, Beads sync, and git push.

### Session
A period of work with AI agents. Sessions have a start (bootstrap or resume), work period, and end (handoff).

---

## Tools

### Cursor
An AI-powered IDE that integrates with language models. Recommended for single-developer workflows.

### Claude
An AI assistant that can run in terminal (Claude CLI). Used for multi-agent workflows with iTerm2.

### iTerm2
A terminal emulator for macOS. Used to run multiple Claude sessions in split panes for SQUAD and COE windows.

---

## Quality

### Baseline
The measured state of tests/coverage/security before making changes. Always establish baseline first.

### Coverage
The percentage of code executed by tests. Measured by statements, branches, functions, and lines.

### Veto
The authority of COE agents (SET, Security, UX) to block releases in their domain. Vetoes must be respected or escalated.

---

## Common Abbreviations

| Abbreviation | Meaning |
|--------------|---------|
| COE | Center of Excellence |
| E2E | End-to-End (testing) |
| MD | Markdown |
| PDLC | Product Development Lifecycle |
| PR | Pull Request |
| QA | Quality Assurance |
| RTL | React Testing Library |
| SAST | Static Application Security Testing |
| SET | Software Engineer in Test |
| SQUAD | Agent0 + SoftwareEngineer team |

---

## Backward Compatibility

Legacy agent names are still recognized and map to new standardized names:

| Legacy Name | New Name | Notes |
|-------------|----------|-------|
| AgentDev | SoftwareEngineerAgent | Engineering layer |
| AgentSET | SoftwareEngineerInTestAgent | Engineering layer |
| AgentSecurity | SecurityEngineerAgent | Security layer |
| AgentUX | UXAgent | UX layer |
| UX | User Experience |
