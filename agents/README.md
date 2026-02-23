# Agent Operating Manuals

This directory contains the operating manuals for all agents in the Agent0 PDLC framework.

---

## Agent Hierarchy

```
                              Agent0
                         (Tech Lead/Orchestrator)
                                  |
    __________________________________________________________________
   |              |              |            |           |           |
Segment     Product Layer  Engineering   Security     Data         UX
Tech Leads       |            Layer        Layer      Layer       Layer
   |        _____|_____         |            |          |           |
(Multiple) |  |  |  |      ____|____    ____|____   ___|___    ____|____
segments  PM PgM PO Mkt  |    |    |  |         | |   |   |  |         |
                        SWE SET DevOps SecEng SecRes DE DA DS Designer Docs
```

---

## Agent Directory

### Orchestration Layer
| Agent | File | Role |
|-------|------|------|
| Agent0 | [orchestration/AGENT0.md](orchestration/AGENT0.md) | Tech Lead, Product Owner, Orchestrator |

### Product Layer
| Agent | File | Role |
|-------|------|------|
| ProductManager | [product/PRODUCT-MANAGER-AGENT.md](product/PRODUCT-MANAGER-AGENT.md) | Owns roadmap/prioritization |
| ProgramManager | [product/PROGRAM-MANAGER-AGENT.md](product/PROGRAM-MANAGER-AGENT.md) | Owns cross-team delivery |
| ProductOperations | [product/PRODUCT-OPERATIONS-AGENT.md](product/PRODUCT-OPERATIONS-AGENT.md) | Owns process/analytics/release readiness |
| ProductMarketing | [product/PRODUCT-MARKETING-AGENT.md](product/PRODUCT-MARKETING-AGENT.md) | Owns positioning/launch |

### UX Layer
| Agent | File | Role |
|-------|------|------|
| UXAgent | [ux/UX-AGENT.md](ux/UX-AGENT.md) | Owns UX/accessibility/design systems |
| ProductDocumentation | [ux/PRODUCT-DOCUMENTATION-AGENT.md](ux/PRODUCT-DOCUMENTATION-AGENT.md) | Owns technical writing/user docs |

### Engineering Layer
| Agent | File | Role |
|-------|------|------|
| SoftwareEngineer | [engineering/SOFTWARE-ENGINEER-AGENT.md](engineering/SOFTWARE-ENGINEER-AGENT.md) | Implements features, writes code |
| SoftwareEngineerInTest | [engineering/SOFTWARE-ENGINEER-IN-TEST-AGENT.md](engineering/SOFTWARE-ENGINEER-IN-TEST-AGENT.md) | Owns quality, test strategy |
| DevOpsEngineer | [engineering/DEVOPS-ENGINEER-AGENT.md](engineering/DEVOPS-ENGINEER-AGENT.md) | Owns CI/CD/infrastructure |
| SegmentTechLead | [engineering/SEGMENT-TECH-LEAD-AGENT.md](engineering/SEGMENT-TECH-LEAD-AGENT.md) | Segment coordinator under Agent0 |

### Security Layer
| Agent | File | Role |
|-------|------|------|
| SecurityEngineer | [security/SECURITY-ENGINEER-AGENT.md](security/SECURITY-ENGINEER-AGENT.md) | Reviews security, scans dependencies |
| SecurityResearcher | [security/SECURITY-RESEARCHER-AGENT.md](security/SECURITY-RESEARCHER-AGENT.md) | Owns threat research |

### Data Layer
| Agent | File | Role |
|-------|------|------|
| DataEngineer | [data/DATA-ENGINEER-AGENT.md](data/DATA-ENGINEER-AGENT.md) | Owns data pipelines |
| DataAnalyst | [data/DATA-ANALYST-AGENT.md](data/DATA-ANALYST-AGENT.md) | Owns analysis/reporting |
| DataScientist | [data/DATA-SCIENTIST-AGENT.md](data/DATA-SCIENTIST-AGENT.md) | Owns ML/AI models |

---

## Backward Compatibility

For backward compatibility, the following mappings apply:

| Legacy Name | New Name |
|-------------|----------|
| AgentDev | SoftwareEngineerAgent |
| AgentSET | SoftwareEngineerInTestAgent |
| AgentSecurity | SecurityEngineerAgent |
| AgentUX | UXAgent |

---

## Team Structures

### SQUAD (Delivery Team)
- Agent0 (Lead)
- SoftwareEngineer instances (1-4)
- DevOpsEngineer (as needed)

### COE (Center of Excellence)
- SoftwareEngineerInTest
- SecurityEngineer
- UXAgent

### Extended Team (as needed)
- ProductManager
- ProgramManager
- ProductOperations
- SecurityResearcher
- Data team (DE, DA, DS)
- ProductMarketing
- ProductDocumentation
