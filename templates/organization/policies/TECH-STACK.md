# Technology Stack – <Your Organization Name>

This document defines the approved technology stack for the organization.

**Organization**: <Your Organization Name>
**Last Updated**: <Date>
**Architecture Team Contact**: <Contact>

---

## Overview

<!-- CUSTOMIZE: Define your tech stack philosophy -->

<Describe your organization's approach to technology choices>

Example:
> We maintain a curated technology stack to ensure consistency, reduce maintenance burden, and enable knowledge sharing across teams.

---

## Languages

<!-- CUSTOMIZE: Define approved languages -->

### Approved Languages

| Language | Version | Use For | Notes |
|----------|---------|---------|-------|
| <Language> | <Version> | <Use cases> | <Notes> |

Example:
| Language | Version | Use For | Notes |
|----------|---------|---------|-------|
| TypeScript | 5.x | Frontend, Node.js services | Preferred for all JS work |
| Java | 17+ | Backend services | Spring Boot preferred |
| Python | 3.11+ | Data, scripting, ML | For specialized use cases |
| Go | 1.21+ | High-performance services | For infrastructure |

### Not Approved

| Language | Reason | Exception Process |
|----------|--------|-------------------|
| <Language> | <Reason> | <Process> |

---

## Frameworks

<!-- CUSTOMIZE: Define approved frameworks -->

### Frontend

| Framework | Version | Use For | Documentation |
|-----------|---------|---------|---------------|
| <Framework> | <Version> | <Use case> | <Link> |

Example:
| Framework | Version | Use For | Documentation |
|-----------|---------|---------|---------------|
| React | 18+ | Web applications | <link> |
| Next.js | 14+ | Full-stack web | <link> |
| React Native | 0.72+ | Mobile apps | <link> |

### Backend

| Framework | Version | Use For | Documentation |
|-----------|---------|---------|---------------|
| <Framework> | <Version> | <Use case> | <Link> |

Example:
| Framework | Version | Use For | Documentation |
|-----------|---------|---------|---------------|
| Spring Boot | 3.x | Java microservices | <link> |
| Express | 4.x | Node.js APIs | <link> |
| FastAPI | 0.100+ | Python APIs | <link> |

---

## Databases

<!-- CUSTOMIZE: Define approved databases -->

| Database | Version | Use For | Managed Service |
|----------|---------|---------|-----------------|
| <Database> | <Version> | <Use case> | <AWS RDS / etc.> |

Example:
| Database | Version | Use For | Managed Service |
|----------|---------|---------|-----------------|
| PostgreSQL | 15+ | Primary relational | AWS RDS |
| Redis | 7+ | Caching, sessions | AWS ElastiCache |
| Elasticsearch | 8.x | Search, logging | AWS OpenSearch |
| MongoDB | 6+ | Document storage | MongoDB Atlas |

---

## Cloud & Infrastructure

<!-- CUSTOMIZE: Define cloud requirements -->

### Cloud Provider

| Provider | Use For | Notes |
|----------|---------|-------|
| <Provider> | <Use case> | <Notes> |

Example:
- Primary: AWS (all production workloads)
- Secondary: GCP (ML/AI workloads)

### Container Platform

| Platform | Version | Use For |
|----------|---------|---------|
| <Platform> | <Version> | <Use case> |

Example:
- Docker: Container runtime
- Kubernetes: Orchestration (EKS preferred)

### CI/CD

| Tool | Use For | Documentation |
|------|---------|---------------|
| <Tool> | <Use case> | <Link> |

Example:
- GitHub Actions: CI/CD pipelines
- ArgoCD: GitOps deployments

---

## Package Management

<!-- CUSTOMIZE: Define package management -->

| Ecosystem | Manager | Registry |
|-----------|---------|----------|
| JavaScript | <npm / yarn / pnpm> | <Registry> |
| Java | <Maven / Gradle> | <Registry> |
| Python | <pip / poetry> | <Registry> |

---

## Security Tools

<!-- CUSTOMIZE: Reference security policy or list here -->

See `SECURITY-POLICY.md` for approved security tools.

---

## Observability

<!-- CUSTOMIZE: Define observability stack -->

| Type | Tool | Notes |
|------|------|-------|
| Logging | <Tool> | <Notes> |
| Metrics | <Tool> | <Notes> |
| Tracing | <Tool> | <Notes> |
| APM | <Tool> | <Notes> |

Example:
| Type | Tool | Notes |
|------|------|-------|
| Logging | Datadog Logs | Centralized logging |
| Metrics | Datadog Metrics | Infrastructure & app metrics |
| Tracing | Datadog APM | Distributed tracing |
| Alerting | PagerDuty | On-call management |

---

## Exception Process

<!-- CUSTOMIZE: Define exception process -->

To request an exception to use a non-approved technology:

1. <Step 1>
2. <Step 2>
3. <Step 3>

Example:
1. Document the use case and why approved alternatives won't work
2. Submit RFC to architecture team
3. Get approval from architecture review board
4. Document decision and maintenance plan

---

## Sunset Technologies

<!-- CUSTOMIZE: List technologies being phased out -->

| Technology | Status | Migration Deadline | Replacement |
|------------|--------|-------------------|-------------|
| <Tech> | <Deprecated/Sunset> | <Date> | <Replacement> |

---

## Agent0 PDLC Integration

### How Agents Use This

- AgentDev references for technology choices
- AgentSecurity validates dependencies against approved list
- Agent0 ensures architectural compliance

### Violations

Technology choices outside this list should be:
1. Flagged by agents
2. Escalated to Agent0
3. Exception process followed if needed
