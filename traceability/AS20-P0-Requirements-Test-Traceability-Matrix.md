# Agent Studio 2.0 — P0 Requirements / Test Traceability Matrix (RTM)

**Document Status:** Draft v0.1  
**Release Context:** Phase 1a / New Ideation — 28 Sep 2026 target  
**Coverage Wave:** P0 Wave 1  
**Scenario Catalogue:** `scenarios/Agent-Studio-2.0-Business-Scenario-Catalogue.md`  
**RBAC Baseline:** `docs/role-access/Agent-Studio-2.0-RBAC-Accessibility-Matrix.md`  
**Manual Test Definitions:** `test-definitions/manual/AS20-P0-Manual-Test-Definitions-Wave-1.md`  
**Execution Matrix:** `test-execution/AS20-P0-Execution-Matrix-Wave-1.md`

---

## 1. Purpose

This RTM provides end-to-end traceability from the available Agent Studio 2.0 test basis through business scenarios, reusable Manual Test Definitions and concrete execution variants.

The intended traceability chain is:

**Requirement / Rule → Business Scenario → Manual Test Definition → Execution Variant → Evidence / Defect**

This document focuses on release-critical P0 coverage. It is not intended to map all 144 planning scenarios yet.

---

## 2. Source Types

| Source Code | Test Basis |
|---|---|
| FLOW | Agent Hub Day 1 Operating Flow |
| ENG | Phase 1a engineering / release rules |
| FIG-TEN | Tenant Management Figma screens |
| FIG-BLD | Agent Builder Figma screens |
| FIG-MKT | Agent Marketplace Figma screens |
| FIG-RUN | Agent Runtime / Harness Figma screens |
| RAM | Official Roles & Actions Matrix |
| RULE | Cross-screen business/governance rule derived from supplied material |

---

## 3. Traceability Status

| Status | Meaning |
|---|---|
| COVERED | Requirement has scenario, definition and planned execution coverage |
| PARTIAL | Some behaviour is testable but requirement clarification is still needed |
| BLOCKED | Expected result/role/state cannot yet be frozen |
| N/A-CURRENT | Valid broader requirement but outside current pre-deployment Wave 1 scope |

---

# 4. Governance / Tenant Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-GOV-001 | Low Risk Pattern is available/enabled for the applicable tenant | ENG / FLOW | 4.3 | GOV-TEN-003 | MTD-GOV-001 | EX-GOV-001..004 | COVERED |
| REQ-GOV-002 | Tenant Owner can enable/disable Agent Patterns for tenant | RAM | 4.3 | GOV-TEN-003 | MTD-GOV-001 | EX-GOV-001 | COVERED |
| REQ-GOV-003 | Space Owner, Space Designer and Space User cannot change tenant pattern enablement | RAM | 4.3 | GOV-TEN-003 | MTD-GOV-001 | EX-GOV-002..004 | COVERED |
| REQ-GOV-004 | Tenant Owner defines which agent capabilities/types can be created | RAM / ENG | 4.4 | GOV-TEN-006, BLD-CFG-003, BLD-CFG-004 | MTD-GOV-002 | EX-GOV-005..007 | COVERED |
| REQ-GOV-005 | Lower-level users cannot expand the tenant's permitted capability set | RAM / RULE | 4.4 | BLD-CFG-003, BLD-CFG-004 | MTD-GOV-002, MTD-BLD-004 | EX-GOV-006..007, EX-BLD-012 | COVERED |
| REQ-GOV-006 | Pattern rules take priority over Tenant system prompt and Agent instructions | FIG-TEN / RULE | — | SEC-RBAC-011 | MTD-BLD-002 | EX-BLD-005 plus governed runtime | COVERED |
| REQ-GOV-007 | Inherited/shared resources are not automatically equivalent to enabled resources | FIG-TEN | — | GOV-TEN-006 | MTD-GOV-002, MTD-BLD-004 | EX-GOV-005, EX-BLD-011..012 | COVERED |
| REQ-GOV-008 | Pattern/resource inheritance does not carry credentials | FIG-TEN | — | BLD-CFG-003 | MTD-BLD-003 | EX-BLD-009 | COVERED |

---

# 5. Space Governance Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-SPC-001 | Tenant has a default Space | ENG / FLOW / FIG-TEN | — | GOV-SPC-001 | MTD-E2E-001 | E2E-X01 | COVERED |
| REQ-SPC-002 | Tenant Owner can create a space within tenant | RAM / FLOW | 5.1 | GOV-SPC-005 | MTD-GOV-003 | EX-GOV-008..009 | PARTIAL |
| REQ-SPC-003 | Tenant Owner assigns/changes Space Owner | RAM / FLOW | 5.2 | GOV-SPC-004 | MTD-GOV-003 | EX-GOV-010 | COVERED |
| REQ-SPC-004 | Space Owner adds members to space and assigns roles | RAM / FLOW | 6.3 | GOV-SPC-004 | MTD-GOV-004 | EX-GOV-011..014 | COVERED |
| REQ-SPC-005 | Space configuration can be viewed by Tenant Owner, Space Owner, Space Designer and Space User | RAM | 5.5 | GOV-SPC-003 | Planned P1 detail; indirectly exercised in Wave 1 | E2E-X01 | PARTIAL |
| REQ-SPC-006 | Default Space cannot be deleted | FIG-TEN | — | GOV-SPC-002 | Planned P1 validation | — | PARTIAL |
| REQ-SPC-007 | Default Space membership/resources follow defined inheritance behaviour | FIG-TEN | — | GOV-SPC-003 | Planned P1 detail | — | PARTIAL |

**Clarification:** Additional-space creation is present in RAM 5.1 and the operating flow, while Figma text suggests one shared default Space in the initial scope. Execution EX-GOV-008 is therefore ALLOW if active for the release, otherwise N/A — Release Scope.

---

# 6. Agent Creation & Configuration Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-BLD-001 | Space Designer (Agent Creator) creates an agent | RAM / FLOW | 6.1 | BLD-CRT-001 | MTD-BLD-001 | EX-BLD-001..004 | COVERED |
| REQ-BLD-002 | Agent is created from an enabled pattern | RAM / FLOW | 6.1 | BLD-CRT-002 | MTD-BLD-001 | EX-BLD-001 | COVERED |
| REQ-BLD-003 | Low Risk Pattern is default/pre-selected for agent creation | ENG / FLOW | — | BLD-CRT-003 | MTD-BLD-001 | EX-BLD-001 | COVERED |
| REQ-BLD-004 | An agent uses exactly one pattern | ENG / FLOW | — | BLD-CRT-002 | MTD-BLD-001 | EX-BLD-001 | COVERED |
| REQ-BLD-005 | Space Designer configures prompt/logic/parameters within pattern | RAM | 6.2 | BLD-CFG-002 | MTD-BLD-002 | EX-BLD-005..008 | COVERED |
| REQ-BLD-006 | Agent instructions cannot override higher Pattern/Tenant governance | FIG-TEN / RULE | — | SEC-RBAC-011 | MTD-BLD-002 | EX-BLD-005 + runtime | COVERED |
| REQ-BLD-007 | Space Designer can attach approved MCP tools/skills | RAM / ENG | 6.5 | BLD-CFG-003, BLD-CFG-004 | MTD-BLD-003 | EX-BLD-009..010 | COVERED |
| REQ-BLD-008 | Space Designer cannot use MCPs/skills unassigned or unapproved for the applicable scope | ENG / RULE | 6.5 | BLD-CFG-003, BLD-CFG-004, SEC-RBAC-009 | MTD-BLD-004 | EX-BLD-011..012 | COVERED |
| REQ-BLD-009 | Arbitrary/unapproved APIs must not become available through agent configuration | ENG | — | SEC-RBAC-010 | MTD-BLD-004 | EX-BLD-012 | COVERED |
| REQ-BLD-010 | Space Designer is the authoritative Agent Creator role for current testing | RAM / roles diagram | 6.1/6.2 | BLD-CRT-001 | MTD-BLD-001 | EX-BLD-001 | COVERED |

---

# 7. Agent Visibility / Edit Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-ACC-001 | Tenant Owner can view agents within the same space | RAM | 6.6 | SEC-RBAC-003 | MTD-ACC-001 | EX-ACC-001 | COVERED |
| REQ-ACC-002 | Space Owner can view agents within the same space | RAM | 6.6 | SEC-RBAC-003 | MTD-ACC-001 | EX-ACC-002 | COVERED |
| REQ-ACC-003 | Space Designer can view agents within the same space | RAM | 6.6 | SEC-RBAC-003 | MTD-ACC-001 | EX-ACC-003 | COVERED |
| REQ-ACC-004 | Space User can view agents within the same space | RAM | 6.6 | SEC-RBAC-004 | MTD-ACC-001 | EX-ACC-004 | COVERED |
| REQ-ACC-005 | AH Platform Admin / Viewer Requestor do not gain same-space agent visibility from those roles alone | RAM | 6.6 | SEC-RBAC-005 | MTD-ACC-001 | EX-ACC-005..006 | COVERED |
| REQ-ACC-006 | Only Space Designer can edit agents within same space | RAM | 6.7 | SEC-RBAC-003, SEC-RBAC-005, SEC-RBAC-006 | MTD-ACC-002 | EX-ACC-007..011 | COVERED |
| REQ-ACC-007 | Authorization denial must protect the operation, not only hide UI controls | RULE | 6.7 | SEC-RBAC-005 | MTD-ACC-002 | EX-ACC-011 | COVERED |

---

# 8. Runtime / Harness Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-RUN-001 | Space Designer can run/execute same-space agent | RAM | 6.8/7.1 | RUN-001 | MTD-RUN-001 | EX-RUN-001 | COVERED |
| REQ-RUN-002 | Space User can run/execute same-space agent | RAM | 6.8/7.1 | RUN-001, SEC-RBAC-004 | MTD-RUN-002 | EX-RUN-002 | COVERED |
| REQ-RUN-003 | Tenant Owner cannot run agent from Tenant Owner role alone | RAM | 6.8/7.1 | SEC-RBAC-005 | MTD-RUN-003 | EX-RUN-003 | COVERED |
| REQ-RUN-004 | Space Owner cannot run agent from Space Owner role alone | RAM | 6.8/7.1 | SEC-RBAC-006 | MTD-RUN-003 | EX-RUN-004 | COVERED |
| REQ-RUN-005 | AH Platform Admin does not receive agent runtime permission from platform-admin role alone | RAM | 7.1 | SEC-RBAC-005 | MTD-RUN-003 | EX-RUN-005 | COVERED |
| REQ-RUN-006 | Direct unauthorized runtime invocation is rejected | RULE / RAM | 7.1 | SEC-RBAC-005 | MTD-RUN-003 | EX-RUN-006 | COVERED |
| REQ-RUN-007 | Space Designer and Space User can view their own execution outputs/history | RAM | 7.2 | RUN-007 | MTD-RUN-004 | EX-RUN-007..008 | COVERED |
| REQ-RUN-008 | User cannot access another user's protected execution history merely through same-space membership | RAM / RULE | 7.2 | RUN-007 | MTD-RUN-004 | EX-RUN-009..010 | COVERED |
| REQ-RUN-009 | Runtime response exposes request metadata where supported (Request ID, time, tokens, cost estimate) | FIG-RUN | — | RUN-002 | MTD-RUN-001/002 | EX-RUN-001..002 | COVERED |

---

# 9. Runtime Source Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-SRC-001 | Runtime user can add a supported personal source | FIG-RUN | — | SRC-001 | MTD-SRC-001 | EX-SRC-001..002 | COVERED |
| REQ-SRC-002 | Personal source is hidden from other users | FIG-RUN | — | SRC-002 | MTD-SRC-002 | EX-SRC-003..005 | COVERED |
| REQ-SRC-003 | Agent may read a personal source at runtime but must not modify the uploaded original | FIG-RUN | — | SRC-001 | MTD-SRC-001 | EX-SRC-001..002 | COVERED |
| REQ-SRC-004 | Source selection determines active runtime source context | FIG-RUN | — | SRC-009, SRC-010, SRC-012 | MTD-SRC-003 | EX-SRC-006..008 | COVERED |
| REQ-SRC-005 | Deselected source should no longer act as selected source context | FIG-RUN | — | SRC-010 | MTD-SRC-003 | EX-SRC-007 | COVERED |
| REQ-SRC-006 | Supported upload types are restricted to the product-defined file types | FIG-RUN | — | SRC-003 | Planned P1 boundary definition | — | PARTIAL |
| REQ-SRC-007 | Maximum source file size is 10MB per current Figma | FIG-RUN | — | SRC-004 | Planned P1 boundary definition | — | PARTIAL |
| REQ-SRC-008 | PUBLIC/INTERNAL upload rule is enforced according to actual classification implementation | FIG-RUN | — | SRC-005 | Planned after classification mechanism confirmed | — | BLOCKED |

---

# 10. Generated File Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-GEN-001 | User can request an agent-generated output file | FIG-RUN | — | GEN-001 | MTD-GEN-001 | EX-GEN-001..002 | COVERED |
| REQ-GEN-002 | Generated artifact appears in Generated Files | FIG-RUN | — | GEN-001 | MTD-GEN-001 | EX-GEN-001..002 | COVERED |
| REQ-GEN-003 | Authorized user can retrieve/open generated artifact | FIG-RUN | — | GEN-002 | MTD-GEN-002 | EX-GEN-003 | COVERED |
| REQ-GEN-004 | Generated output should materially correspond to requested task/source facts | FIG-RUN / RULE | — | GEN-009 | MTD-GEN-002 | EX-GEN-003 | COVERED |
| REQ-GEN-005 | Another user must not gain unauthorized access to protected generated artifacts | RULE | — | GEN-009 | MTD-GEN-002 | EX-GEN-004..005 | PARTIAL |

Generated-file ownership/retention semantics still require confirmation; object-level unauthorized access remains a required security assertion.

---

# 11. Space / Tenant Isolation Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-ISO-001 | Agent visibility is limited to the same authorized space | ENG / FLOW / RAM | 6.6 | MKT-004, SEC-RBAC-007 | MTD-ISO-001 | EX-ISO-001..004 | COVERED |
| REQ-ISO-002 | Space B-only user cannot discover Space A agent | FLOW / RULE | 6.6 | SEC-RBAC-007 | MTD-ISO-001 | EX-ISO-002 | COVERED |
| REQ-ISO-003 | Direct cross-space agent access/invocation is rejected | RULE | 6.6/7.1 | SEC-RBAC-007 | MTD-ISO-001 | EX-ISO-003..004 | COVERED |
| REQ-ISO-004 | Tenant B-only user cannot discover/execute Tenant A restricted agent | ENG / RULE | — | SEC-RBAC-008 | MTD-ISO-002 | EX-ISO-005..007 | COVERED |
| REQ-ISO-005 | Cross-scope denial must not leak agent/configuration/session information | RULE | — | SEC-RBAC-007, SEC-RBAC-008 | MTD-ISO-001/002 | EX-ISO-003..007 | COVERED |

---

# 12. Publication / Marketplace Traceability

| Req ID | Requirement / Rule | Source | RAM Ref | Scenario Ref | Test Definition | Execution Ref | Status |
|---|---|---|---|---|---|---|---|
| REQ-PUB-001 | Created agent must transition to an appropriate shared/marketplace state before normal consumer use | FLOW / FIG-BLD / FIG-MKT | Candidate 6.9 | PUB-001, PUB-003 | MTD-PUB-001/002 | EX-PUB-001..006 | PARTIAL |
| REQ-PUB-002 | Figma Publish supports Private Testing visibility | FIG-BLD | — | PUB-002 | MTD-PUB-002 | EX-PUB-003 | BLOCKED |
| REQ-PUB-003 | Figma Publish supports Marketplace Testing visibility | FIG-BLD | — | PUB-003 | MTD-PUB-002 | EX-PUB-004 | BLOCKED |
| REQ-PUB-004 | Matrix 6.9 allows Tenant Owner to promote an agent to tenant-shared | RAM | 6.9 | PUB-010 | MTD-PUB-002 | EX-PUB-005..006 | COVERED as RAM rule; mapping BLOCKED |
| REQ-PUB-005 | Unpublished draft is not generally consumable by Space User | FLOW / FIG-BLD | — | PUB-001 | MTD-PUB-001 | EX-PUB-001..002 | COVERED |
| REQ-PUB-006 | Published/shared agent visibility must respect intended space/tenant scope | ENG / FLOW / FIG-BLD | — | PUB-003, MKT-004 | MTD-PUB-002, MTD-ISO-001 | EX-PUB-004..005, EX-ISO-001..004 | PARTIAL |
| REQ-PUB-007 | Unpublished edits must not silently alter the currently published runtime version | FIG-BLD / RULE | — | PUB-006 | Planned P1 versioning definition | — | PARTIAL |
| REQ-PUB-008 | A newly published version becomes the intended consumer runtime version | FIG-BLD / FIG-MKT | — | PUB-007 | Planned P1 versioning definition | — | PARTIAL |

**Blocking clarification:** Product ownership must confirm the relationship among `Publish`, `Private Testing`, `Marketplace Testing`, and RAM `6.9 Promote an agent to tenant-shared`, including which role owns each transition and whether marketplace visibility is Space-scoped or Tenant-scoped.

---

# 13. P0 End-to-End Journey Traceability

| Journey | Requirement Chain | Test Definition | Execution Chain | Status |
|---|---|---|---|---|
| E2E-01 Governed Build-to-Run | Pattern → Space → Role → Build → Tooling → Share → View → Run | MTD-E2E-001 | E2E-X01 | PARTIAL — publish mapping |
| E2E-02 Source-to-Artifact | Run → Personal Source → Source-grounded response → Generate → Retrieve → Privacy | MTD-E2E-002 | E2E-X02 | COVERED, generated ownership detail pending |
| E2E-03 Space Isolation | Same-space discover/run → cross-space search/direct access/direct runtime denial | MTD-ISO-001 | E2E-X03 | COVERED |

---

# 14. Roles & Actions Matrix Coverage — Current Wave

This section makes gaps in official RBAC coverage visible.

| RAM Ref | Action | Wave 1 Coverage | Notes |
|---|---|---|---|
| 1.1 | Navigation (Read-Only) | P1 | Viewer/Requestor-specific navigation not release-critical build/run chain |
| 1.2 | Browse Marketplace pattern catalogue | P1 | Planned navigation/catalogue coverage |
| 1.3 | View pattern detail | P1 | Planned pattern catalogue coverage |
| 4.1 | View tenant configuration | Indirect / P1 detail | Exercised during governance setup |
| 4.2 | Change tenant configuration | Indirect / P1 detail | Current P0 targets specific 4.3/4.4 controls |
| 4.3 | Enable/disable Agent Patterns | P0 COVERED | MTD-GOV-001 |
| 4.4 | Define agent capabilities/types | P0 COVERED | MTD-GOV-002 |
| 4.5 | Add/remove tenant member | P1 | Space-role path prioritized in Wave 1 |
| 4.6 | Adjust tenant token limit | P1 / conditional | Token/cost functional expansion |
| 4.7 | Re-assign orphan project admin | N/A-CURRENT | Platform administration |
| 4.8 | Inactivate tenant | P1 | State-transition coverage |
| 4.9 | Reactivate tenant | P1 | State-transition coverage |
| 5.1 | Create space | P0 PARTIAL | Release-scope clarification |
| 5.2 | Assign/change Space Owner | P0 COVERED | MTD-GOV-003 |
| 5.3 | Configure space settings | P1 | Detailed space configuration expansion |
| 5.4 | Set/change space token limit | P1 / conditional | Token/cost expansion |
| 5.5 | View space configuration | Indirect / P1 detail | Role view assertions to expand |
| 5.6 | Inactivate space | P1 | State transition |
| 5.7 | Reactivate space | P1 | State transition |
| 6.1 | Create agent | P0 COVERED | MTD-BLD-001 |
| 6.2 | Configure agent | P0 COVERED | MTD-BLD-002 |
| 6.3 | Add space members/roles | P0 COVERED | MTD-GOV-004 |
| 6.4 | Review agent configuration request | P1 / clarification | Exact UI/state transition required |
| 6.5 | Attach approved MCP/skills | P0 COVERED | MTD-BLD-003/004 |
| 6.6 | View same-space agents | P0 COVERED | MTD-ACC-001 |
| 6.7 | Edit same-space agents | P0 COVERED | MTD-ACC-002 |
| 6.8 | Run same-space agents | P0 COVERED | MTD-RUN-001/002/003 |
| 6.9 | Promote agent to tenant-shared | P0 rule captured / mapping blocked | Publication clarification |
| 6.10 | Create/schedule automated workflow | P1 / dependent | Agentic Workflow 2.0 detail required |
| 6.11 | Inactivate agent | P1 | State-transition coverage |
| 6.12 | Reactivate agent | P1 | State-transition coverage |
| 7.1 | Execute/run agent | P0 COVERED | MTD-RUN-001/002/003 |
| 7.2 | View own execution outputs/history | P0 COVERED | MTD-RUN-004 |
| Production deployment | Request deploy onward | N/A-CURRENT | Explicitly excluded by current scope direction |

---

# 15. Coverage Summary

### P0 Wave 1 Position

- Core Tenant/Space governance: covered for release-critical actions.
- Agent create/configure/resource controls: covered.
- Same-space view/edit RBAC: covered.
- Runtime positive/negative authorization: covered.
- Own execution history isolation: covered.
- Personal source/runtime context: covered.
- Generated file flow: covered, ownership detail partially open.
- Cross-space/cross-tenant isolation: covered.
- Publish/Marketplace: functional requirement retained but role/state mapping remains the primary blocker.
- Production deployment: intentionally excluded.

### Why some requirements remain P1

P0 is intentionally risk-based. Lower-risk navigation, detailed field validation, lifecycle state transitions, search/filter behaviour, token limits, monitoring and full Agentic Workflow coverage should be expanded after the golden lifecycle and authorization model are stable.

---

# 16. Open Requirement Clarifications Affecting Traceability

1. **Publish model:** Figma `Publish / Private Testing / Marketplace Testing` vs RAM `6.9 Promote to tenant-shared`.
2. **Marketplace scope:** same Space only vs Tenant marketplace/tenant-shared wording.
3. **Additional spaces:** Day 1 flow/RAM support creation; Figma initial-scope wording suggests one shared default Space.
4. **Pattern names:** engineering basis says Low Risk + SDLC; Training Figma shows Low Risk + Research Pattern.
5. **Pattern UI:** engineering says Pattern UI read-only while Pattern Tenant screens show editable management controls; distinguish consumer Pattern UI from privileged pattern administration.
6. **Review agent configuration request 6.4:** exact UI/state transition not yet mapped.
7. **Source classification:** how PUBLIC/INTERNAL restriction is technically represented/enforced.
8. **Generated files:** ownership, retention and cross-user access semantics.
9. **Multi-role users:** effective-permission rule if one user holds multiple roles.
10. **Agentic Workflow 2.0:** detailed functional basis/screens needed for complete 6.10 coverage.

---

# 17. Traceability Maintenance Rule

When a requirement changes:

1. Update the requirement/rule entry and source reference.
2. Identify affected Business Scenario IDs.
3. Review affected Manual Test Definitions.
4. Update only the execution variants whose role/scope/expected result changed.
5. Preserve historical execution evidence against the version of the requirement used at execution time.

This prevents requirement changes from forcing wholesale duplication of test cases.

---

**End of Document**