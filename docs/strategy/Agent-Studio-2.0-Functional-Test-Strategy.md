# Agent Studio 2.0 — Functional Test Strategy / Master Test Plan

**Document Status:** Draft v0.1  
**Prepared For:** Agent Studio 2.0 Functional Testing  
**Document Type:** Functional Test Strategy / Master Test Plan  
**Last Updated:** 2026-09-15

---

## 1. Purpose

This document defines the functional testing strategy and master test approach for **Agent Studio 2.0 (AS2.0)**.

The strategy is based on the current Agent Studio 2.0 Figma designs and walkthrough, covering the major user journeys currently understood:

**Agent Studio → Tenant / Pattern Configuration → Agent Builder → Agent Configuration → Publish / Version → Agent Marketplace → Agent Runtime → Sources → Generated Output**

The purpose of this plan is to establish a reusable testing structure before detailed role-based access rules and some outstanding product decisions are finalized.

The strategy intentionally separates:

1. **Functional capability validation** — what the platform should do.
2. **Access and role validation** — who is allowed to do it.
3. **Execution variation** — under which tenant, pattern, role, state, visibility, source and version the behaviour is exercised.

This allows functional scenario design to begin immediately while the final role/accessibility matrix is still being defined.

---

## 2. Objectives

The functional testing programme will provide confidence that:

- Agent Studio 2.0 capabilities operate according to approved requirements and designs.
- Users can navigate between major platform capabilities successfully.
- Pattern tenants and use-case tenants behave correctly.
- Pattern inheritance is correctly applied to adopting tenants.
- Agents can be created, configured, tested and maintained.
- Agents cannot become generally usable merely by being created; the required publication lifecycle is enforced.
- Private and marketplace publication behave according to their intended visibility.
- Published agents can be discovered and used by eligible users.
- Agent version changes follow the expected lifecycle.
- Runtime conversations operate correctly.
- Users can add, select and use sources during agent execution.
- Generated files are produced and made available correctly.
- Tenant membership, spaces and administrative functions behave correctly.
- Permission boundaries are enforced once the official role/access matrix is available.
- Negative, validation and state-transition behaviours are covered in addition to happy paths.
- Critical end-to-end business journeys remain functional across releases.

---

## 3. Scope

### 3.1 In Scope

The initial functional scope includes the following capabilities observed in the current Agent Studio 2.0 designs.

| Capability | Functional Scope |
|---|---|
| Agent Studio Homepage | Landing page, navigation, service entry points and assistant entry |
| Tenant Management — Pattern Tenant | Pattern overview, skills/connections, rules, agents, pattern contents, review/version, members and spaces |
| Tenant Management — Use Case / Training Tenant | Tenant overview, inherited patterns, inherited tooling/agents, tenant system prompt, members and spaces |
| Agent Builder | Prompt-assisted creation, start-from-scratch creation and agent draft creation |
| Agent Configuration | Agent information, instructions, skills, tools, knowledge bases and advanced settings |
| Agent Publishing | Publish flow, private testing, marketplace testing/publication and version publishing |
| Agent Marketplace | Discovery, recently used agents, eligible agents, filtering/search and agent selection |
| Agent Runtime | Session handling, prompts, responses, agent execution and runtime interaction |
| Runtime Sources | Add source, select/deselect source and source-aware execution |
| Generated Files | Generation and retrieval of output artifacts |
| Agent Version Lifecycle | Draft change, new version publication and use of published versions |
| Tenant Administration | Members, roles and spaces |
| Governance / Access | Role-based visibility and action authorization once the role matrix is available |

### 3.2 Conditional / Pending Scope

The following features are visible in design but are not yet considered confirmed requirements:

- Agent Builder **“Pick up where you left off”**.
- Agent Builder **“View all agents / All agents”**.
- Role-specific meaning and visibility of **“All agents”**.
- Any other capability subsequently identified as design-only, exploratory or nice-to-have.

These items should be tagged **TBD / Design Dependency** and should not be treated as release-blocking requirements until confirmed.

### 3.3 Out of Scope for This Functional Strategy

Unless separately requested, this document does not define detailed approaches for:

- Performance/load testing.
- Security penetration testing.
- Vulnerability assessment.
- Infrastructure resilience testing.
- Disaster recovery.
- Production monitoring.
- Model quality benchmarking beyond functional acceptance.
- Full accessibility/usability certification.

These areas may have functional touchpoints but should have dedicated strategies where required.

---

## 4. Current Product Model

### 4.1 High-Level Lifecycle

The current functional lifecycle is understood as:

1. User enters **Agent Studio**.
2. Authorized users configure or manage **tenants/patterns**.
3. Authorized users use **Agent Builder** to create an agent.
4. The agent is configured with required information, instructions and capabilities.
5. The agent remains a draft until the appropriate **publish** process occurs.
6. Publishing creates a usable version with an appropriate visibility level.
7. Eligible users discover published agents through **Agent Marketplace** or private-agent mechanisms.
8. Users open the agent runtime.
9. Users optionally provide/select sources.
10. Users submit prompts and receive agent responses.
11. Where requested/supported, the agent creates generated files.
12. Agent changes require a subsequent version to be published before the updated version becomes available.

### 4.2 Publication Principle

A created agent is not assumed to be generally available to normal users.

The expected lifecycle is:

**Create → Configure → Test → Publish → Discover / Access → Use**

When changes are made:

**Published Version N → Modify Draft → Validate → Publish Version N+1 → New Version Available**

Publication may be:

- **Private testing / private visibility**, or
- **Marketplace-level visibility**.

Detailed authorization rules for each publication level remain subject to the final role/access matrix.

---

## 5. Test Design Model

Testing will follow a four-level model.

### Level 1 — Capability

Examples:
- Tenant Management
- Agent Builder
- Agent Marketplace
- Agent Runtime

### Level 2 — Business Scenario

Examples:
- Create an agent.
- Configure an agent.
- Publish an agent.
- Update and republish an existing agent.
- Discover a marketplace agent.
- Use an agent with uploaded sources.
- Generate an output file.

### Level 3 — Test Definition

Each Business Scenario may have multiple Test Definitions covering:
- Happy path.
- Negative path.
- Field/input validation.
- State transition.
- Integration behaviour.
- Permission/RBAC behaviour.
- Boundary conditions.
- Error/recovery behaviour.

### Level 4 — Execution Variant

The same Test Definition may be executed using different:
- Roles.
- Tenant types.
- Patterns.
- Spaces.
- Agent states.
- Publication visibility.
- Agent versions.
- Source combinations.
- Test data.
- Environments.

This prevents unnecessary duplication of Business Scenarios while allowing broad execution coverage.

---

## 6. Proposed Traceability Structure

The preferred relationship is:

**Capability → Business Scenario → Manual/Automation Test Definition → Execution → Evidence / Defect**

A Business Scenario may therefore have **multiple Test Definitions**, and a Test Definition may have **multiple Executions**.

Role is primarily treated as an execution/access dimension unless the role changes the business behaviour sufficiently to require a dedicated permission Test Definition.

| Scenario | Test Definition | Execution Role | Expected Access | Expected Outcome |
|---|---|---|---|---|
| Create Agent | Create valid agent | Authorized creator | Allow | Draft agent created |
| Create Agent | Verify unauthorized creation | Normal user | Deny | Creation unavailable/rejected |
| Publish Agent | Publish valid version | Publisher | Allow | Version published |
| Publish Agent | Verify publish restriction | Creator without publish authority | Deny | Publish unavailable/rejected |

---

## 7. Test Layers

### 7.1 Smoke Testing

A compact release-health suite should prove that the major platform path is operational.

Suggested smoke journey:

**Login / Enter Studio → Agent Builder → Create Agent → Configure Minimum Required Data → Publish → Marketplace / Private Access → Open Agent → Submit Prompt → Receive Response**

Where feasible, include a basic source upload/use case.

### 7.2 Functional Capability Testing

Detailed validation of each capability and its controls, rules, validations and expected states.

### 7.3 Integration Testing

Validate functional boundaries between capabilities, particularly:
- Pattern → Tenant.
- Tenant → Agent Builder.
- Agent Builder → Agent draft.
- Agent configuration → Publication.
- Publication → Marketplace/private availability.
- Marketplace → Runtime.
- Runtime → Sources.
- Runtime → Generated files.
- Agent update → Version publication.

### 7.4 End-to-End Testing

Validate complete user/business journeys rather than isolated pages.

### 7.5 Regression Testing

Maintain a stable suite of high-value scenarios covering critical paths, previously defective areas, cross-capability integrations, governance, publication/versioning, runtime and source handling.

### 7.6 Role / Access Testing

Once the role matrix is available, test both positive authorization and negative authorization. Validation must go beyond UI visibility. Where technically possible, restricted actions should also be rejected by the underlying service/API rather than merely hidden in the interface.

---

## 8. Capability Test Coverage

### 8.1 Agent Studio Homepage

Validate homepage loading, entitlement-based navigation, major module entry points, assistant input where confirmed, and correct service-card navigation.

### 8.2 Tenant Management — Pattern Tenant

Validate pattern overview, skills/connections, pattern rules, agents, pattern contents, review/version lifecycle, members/roles and spaces.

Important assertions include persistence, downstream inheritance, connected versus access-required connection state, default-space behaviour and restrictions where specified.

### 8.3 Tenant Management — Use Case / Training Tenant

Validate tenant overview, inherited patterns, inherited tooling/agents, tenant system prompt, members/roles and spaces.

A key distinction is:

**Available from inherited pattern ≠ enabled/selected for the tenant.**

Validate the intended precedence model:

**Pattern Rules → Tenant System Prompt → Agent Instructions**

Inherited governance must not be silently overridden by lower-level configuration if the design prohibits it.

---

## 9. Agent Builder Strategy

### 9.1 Agent Builder Main Page

Validate prompt-based entry, suggested ideas, start-from-scratch entry, navigation and page state.

### 9.2 Prompt-Assisted Agent Creation

Validate idea submission, follow-up questions, captured choices, draft creation, cancel/back behaviour, invalid/empty input handling and generation failure/retry behaviour.

### 9.3 Start From Scratch

Validate agent name, optional description, required-field validation, duplicate/invalid name handling where applicable, cancel and create.

### 9.4 Unconfirmed Agent Listing Features

The following remain **TBD**:
- Pick up where you left off.
- View all agents.
- Definition of All Agents by role.

Test cases may be drafted but should remain inactive until product decisions are finalized.

---

## 10. Agent Configuration Strategy

Once an agent is created, validate configuration areas including:
- Agent Info.
- Instructions.
- Skills.
- Tools.
- Knowledge Bases.
- Advanced Settings.

For each configuration area validate load/display, add/change, save, persistence, validation, removal where supported, permission and runtime effect where applicable.

Configuration testing should distinguish between draft configuration, published configuration and changes made after publication.

---

## 11. Agent Publication and Versioning Strategy

Publication is a critical control point and should receive dedicated state-transition coverage.

### 11.1 Initial Publication

Validate **Draft → Publish Setup → Published Version**, including required fields, version information, release notes, visibility, category, tags, cancel and publish.

### 11.2 Visibility

Validate at least:
- **Private Testing** — agent is available only through the intended private scope.
- **Marketplace Testing / Marketplace Publication** — agent becomes discoverable according to permissions.

### 11.3 Version Update

Validate:

**Version N Published → Agent Modified → Draft Changes → Publish Version N+1**

Confirm that draft changes do not unintentionally alter the active published version, new version metadata is correct, marketplace/runtime resolves the expected version, version history remains coherent, and failed/cancelled publication does not corrupt the current published version.

---

## 12. Agent Marketplace Strategy

Validate marketplace loading, recently used agents, bookmarks where supported, private-agent area, eligible marketplace agents, search, filters, presentation options, pagination, metadata/version, agent selection and runtime launch.

Critical governance assertion:

> An agent should only be discoverable where its publication visibility and the user's authorization permit it.

---

## 13. Agent Runtime Strategy

### 13.1 Session

Validate new session, session history, session selection, clear chat and session isolation.

### 13.2 Prompt and Response

Validate prompt submission, processing, response presentation, completion/error state, retry/recovery where supported, multi-turn conversation, boundary handling and relevant metadata where exposed.

### 13.3 Published Version

Validate that runtime uses the intended published agent version and does not unintentionally expose unpublished draft changes.

---

## 14. Runtime Source Strategy

Validate source addition, supported/unsupported files, multiple files, cancel, duplicates, empty files, maximum-size boundary, oversized files, upload failure and malformed/corrupted files where applicable.

Validate source selection using one, multiple, all, deselection and no-source execution.

Runtime assertions include:
- Selected sources are available to the agent.
- Unselected sources are not treated as selected runtime context.
- Sources are not exposed improperly to another user/session.
- Source state is handled correctly across sessions.

Current design text indicates supported file types and a maximum size, but these values must be confirmed against final requirements before they become authoritative acceptance criteria.

---

## 15. Generated File Strategy

Where an agent can generate an output artifact, validate request, successful creation, Generated Files update, metadata, retrieval/download, content relevance, multiple files, regeneration, failure handling, session association, permission and lifecycle where defined.

Separate:
1. **Functional generation validation** — file exists, opens and is structurally valid.
2. **Content-quality validation** — output meets business/agent-specific acceptance criteria.

---

## 16. End-to-End Business Journeys

### E2E-01 — Pattern to Published Agent
**Configure Pattern → Configure Tenant → Create Agent → Configure Agent → Publish → Discover → Run**

### E2E-02 — Training Tenant Inheritance
**Pattern Published → Training Tenant Inherits Pattern → Select Shared Tooling/Agents → Configure Tenant Prompt → Use Tenant Capability**

### E2E-03 — Agent Creation to Marketplace
**Create Agent → Configure → Test → Publish Marketplace Version → Search Marketplace → Open → Execute**

### E2E-04 — Private Agent
**Create Agent → Configure → Private Publish → Authorized User Access → Unauthorized User Cannot Discover/Access**

### E2E-05 — Agent Version Upgrade
**Use Version N → Modify Agent → Publish Version N+1 → Marketplace Reflects New Version → Runtime Uses Version N+1**

### E2E-06 — Source-Grounded Runtime
**Open Agent → Add Sources → Select Sources → Ask Question → Receive Source-Aware Response**

### E2E-07 — Generated Artifact
**Open Agent → Add/Select Sources if needed → Request Output File → Agent Generates File → User Retrieves File**

### E2E-08 — Governance
**Tenant/Pattern Setup → Assign Role → Verify Permitted Operations → Verify Restricted Operations**

This becomes fully executable when the role/access matrix is available.

---

## 17. Role-Based Access Control Test Model

The role matrix is a known dependency but does not block functional design.

When received, convert it into an execution matrix with fields such as:

| Field | Purpose |
|---|---|
| Capability | Functional area |
| Action | Operation under test |
| Role | Assigned user role |
| Tenant Type | Pattern/use-case/etc. |
| Space | Applicable space |
| Expected UI Visibility | Visible/hidden/read-only |
| Expected Action Access | Allow/deny |
| Expected Data Scope | Objects user may access |
| Expected Service Result | Success/authorization failure |
| Test Definition ID | Traceability |
| Execution Result | Pass/fail |

Important principle:

**Hidden UI alone is not sufficient evidence of authorization.**

For high-risk actions, service-side authorization should be validated wherever feasible.

---

## 18. State-Transition Testing

Potential agent states include new, draft, ready for review/testing, private published, marketplace published, modified draft after publication, new published version and retired/unavailable if supported.

Potential tenant/pattern states include draft, configuration incomplete, ready for review, submitted, published and updated draft after publication.

Detailed state names must be aligned with final implementation. Test design should validate both valid and invalid transitions.

---

## 19. Negative and Boundary Testing

Each major capability should include negative coverage such as missing required fields, invalid/duplicate values, unsupported state transitions, unauthorized operations, missing resources, concurrent update where relevant, invalid/oversized sources, upload interruption, publication failure, runtime failure, generated-file failure, timeout where applicable, and refresh/navigation during incomplete operations.

---

## 20. Test Data Strategy

Maintain reusable test data covering:

### Users
- One user per defined role.
- Multi-role user where supported.
- No-access user.
- Cross-tenant user where relevant.

### Tenants
- Pattern tenant.
- Training/use-case tenant.
- Tenant with one inherited pattern.
- Tenant with multiple inherited patterns.
- Tenant with incomplete configuration.

### Agents
- Draft agent.
- Private published agent.
- Marketplace published agent.
- Agent with multiple versions.
- Agent with skills/tools/KB.
- Minimal agent.
- Invalid/incomplete draft where possible.

### Sources
- Small valid files.
- Multiple supported formats.
- Maximum-boundary files.
- Oversized files.
- Empty files.
- Invalid/unsupported files.
- Duplicate files.

### Generated Outputs
- Single output.
- Multiple outputs.
- Output based on sources.
- Output without sources where supported.

---

## 21. Environment Strategy

Expected functional environments should be confirmed, but the testing model should support DEV, SIT, UAT, PPD/pre-production where applicable, and PROD validation only where explicitly approved.

Test Definitions should remain environment-independent wherever possible, while Executions record the actual environment.

---

## 22. Entry Criteria

A functional test cycle may begin when the build is deployed, required services are available, core test users are provisioned, required tenant/test data exists, testable requirements/designs are available, major blockers are identified and environment health checks pass.

Features with unresolved requirements may enter exploratory/design validation but should not receive definitive pass/fail acceptance criteria until clarified.

---

## 23. Exit Criteria

A release/cycle may be considered functionally acceptable when critical smoke and E2E suites pass, required functional and role/access scenarios are executed, no blocker or unacceptable critical/high-severity defects remain, regression meets agreed thresholds, known limitations are accepted and evidence/results are traceable.

Exact numerical thresholds should be agreed with programme stakeholders.

---

## 24. Defect Strategy

Defects should capture capability, scenario/Test Definition, environment, user role, tenant, agent/version, preconditions, steps, actual/expected result, evidence, severity, reproducibility and requirement/design reference.

Access defects should additionally identify whether the issue concerns UI visibility, UI action control, service/API authorization or data visibility/scope.

---

## 25. Evidence Strategy

Evidence should be captured for critical E2E flows, publication/version transitions, role/access validation, defects and high-risk negative scenarios.

Evidence may include screenshots, permitted request/response details, logs, generated files, timestamps, agent version and tenant/role context.

---

## 26. Automation Strategy

Automation should be prioritized after functional behaviour stabilizes.

### High Priority
- Homepage/navigation smoke.
- Agent creation happy path.
- Agent configuration persistence.
- Publish flow.
- Marketplace search/discovery.
- Runtime basic prompt/response.
- Version lifecycle regression.
- High-value RBAC checks.
- Source upload/select flow.

### Lower Priority / Selective Automation
- Highly dynamic AI-generated content assertions.
- Design-exploration features.
- Rapidly changing configuration UI.
- Subjective response-quality checks.

Automation assertions for AI responses should prefer deterministic properties rather than exact natural-language matching.

---

## 27. AI-Specific Functional Testing Considerations

Distinguish deterministic platform behaviour (agent saved, version published, user denied, source uploaded, file generated, marketplace entry visible) from non-deterministic agent behaviour (response wording, summaries, prompt interpretation).

Deterministic behaviours should normally have strict expected results. Non-deterministic behaviours should use acceptance criteria based on required properties, constraints and business correctness rather than exact-text matching.

---

## 28. Requirement / Design Dependency Register

| ID | Dependency / Question | Current Treatment |
|---|---|---|
| DEP-001 | Final role/accessibility matrix | Pending; RBAC executions added later |
| DEP-002 | Definition of “All agents” by role | TBD; feature not treated as confirmed |
| DEP-003 | Pick-up/recent-agent feature confirmation | Nice-to-have / pending confirmation |
| DEP-004 | Final supported source file rules | Confirm before acceptance criteria freeze |
| DEP-005 | Final pattern/tenant inheritance rules | Validate against implementation/spec |
| DEP-006 | Final role permitted publication levels | Pending role matrix |
| DEP-007 | Final environment list | Confirm with programme |
| DEP-008 | Final API/service authorization behaviour | Required for deeper RBAC validation |
| DEP-009 | Agent retirement/unpublish lifecycle if supported | To be confirmed |
| DEP-010 | Final scope of Evaluation, MCP Marketplace, Skill Marketplace, Agentic Flow and Agent Registry | To be confirmed |

---

## 29. Proposed Test Repository Structure

```text
AS20/
├── README.md
├── docs/
│   ├── strategy/
│   │   └── Agent-Studio-2.0-Functional-Test-Strategy.md
│   ├── requirements/
│   ├── role-access/
│   ├── test-data/
│   └── decisions/
├── scenarios/
│   ├── homepage/
│   ├── tenant-management/
│   ├── agent-builder/
│   ├── agent-marketplace/
│   └── agent-runtime/
├── test-definitions/
│   ├── manual/
│   └── automation/
├── executions/
├── evidence/
└── reports/
```

The structure may evolve as AS2.0 testing matures.

---

## 30. Recommended Delivery Phases

### Phase 1 — Strategy & Test Model
- Master Test Plan.
- Capability map.
- Dependency register.
- Repository structure.

### Phase 2 — Business Scenario Catalogue
Derive Business Scenarios from the approved capabilities and Figma flows.

### Phase 3 — Manual Test Definitions
Create detailed Test Definitions for prioritized Business Scenarios.

### Phase 4 — Role / Access Matrix Integration
Map official roles to scenarios and expected allow/deny outcomes.

### Phase 5 — E2E & Regression Baseline
Identify smoke, E2E and regression suites.

### Phase 6 — Automation Candidates
Prioritize stable high-value tests for automation.

### Phase 7 — Execution & Reporting
Execute by environment/release and publish traceable results.

---

## 31. Immediate Next Steps

1. Review and approve this strategy.
2. Establish the **AS20** repository.
3. Commit this document as the functional-testing baseline.
4. Create the first **Capability / Business Scenario Catalogue**.
5. Mark unconfirmed Figma features as TBD rather than assuming expected behaviour.
6. Incorporate the official role/access matrix when available.
7. Convert prioritized Business Scenarios into Manual Test Definitions.
8. Identify the initial smoke and E2E baseline.
9. Begin execution once an appropriate AS2.0 environment/build is available.

---

## 32. Strategy Principle

> **Design the functional behaviour first, apply authorization as a controlled execution dimension, and validate the complete lifecycle from configuration through publication to real agent usage.**

This allows testing to start before every governance detail is finalized while preserving a clear path to comprehensive role-based, end-to-end and regression coverage.

---

**End of Document**
