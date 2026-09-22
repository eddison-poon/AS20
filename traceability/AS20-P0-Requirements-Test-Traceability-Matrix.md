# Agent Studio 2.0 — P0 Requirements / Test Traceability Matrix (RTM)

**Document Status:** Draft v0.4 — Reconciled 23 Sep 2026 with implemented screens and updated RBAC  
**Release Context:** Phase 1a / New Ideation — 28 Sep 2026 target  
**Coverage Wave:** P0 Wave 1  
**Scenario Catalogue:** `scenarios/Agent-Studio-2.0-Business-Scenario-Catalogue.md`  
**Manual Test Definitions:** `test-definitions/manual/AS20-P0-Manual-Test-Definitions-Wave-1.md`  
**Execution Matrix:** `test-execution/AS20-P0-Execution-Matrix-Wave-1.md`

## 1. Purpose

This RTM proves the chain **Requirement / Rule → Business Scenario → Manual Test Definition → Execution Variant → Evidence / Defect**. `COVERED` means test coverage is designed; it does **not** mean the test has passed.

Updated baseline: **158 scenarios = 60 P0 + 72 P1 + 26 P2/TBD; 37 reusable P0 definitions; 109 explicit functional P0 execution variants; 2 dedicated E2E regression variants; 111 dashboard-managed variants; 10 smoke checks.**

### Status
- **COVERED** — scenario, definition and planned execution exist.
- **PARTIAL** — coverage exists but a rule/detail remains open.
- **BLOCKED** — expected role/state/result cannot yet be frozen.
- **N/A-CURRENT** — valid broader requirement outside this wave.

## 2. Source Codes

`FLOW` Day 1 Operating Flow · `ENG` engineering/release rules · `FIG-TEN` Tenant Figma · `FIG-BLD` Builder Figma · `FIG-MKT` Marketplace Figma · `FIG-RUN` Runtime Figma · `RAM` Roles & Actions Matrix · `RULE` cross-screen governance rule.

# 3. Pattern / Tenant / Space Governance

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-PAT-001 | Low Risk Pattern exists/is assignable | ENG/FLOW | GOV-PAT-001 | MTD-PAT-001 | EX-PAT-001 | COVERED |
| REQ-PAT-002 | SDLC Pattern exists/is assignable | ENG/FLOW | GOV-PAT-002 | MTD-PAT-001 | EX-PAT-002 | COVERED |
| REQ-PAT-003 | Shared Pattern rules govern downstream behaviour | FIG-TEN/RULE | GOV-PAT-005 | MTD-PAT-002 | EX-PAT-003..004 | COVERED |
| REQ-GOV-001 | Low Risk Pattern enabled for applicable tenant | ENG/FLOW/RAM 4.3 | GOV-TEN-003 | MTD-GOV-001 | EX-GOV-001..004 | COVERED |
| REQ-GOV-002 | Tenant Owner controls permitted capability/types | RAM 4.4 | GOV-TEN-006 | MTD-GOV-002 | EX-GOV-005..007 | COVERED |
| REQ-GOV-003 | Shared/inherited resource is not automatically enabled | FIG-TEN | GOV-TEN-006 | MTD-GOV-002/BLD-004 | EX-GOV-005, EX-BLD-011..012 | COVERED |
| REQ-GOV-004 | Resource requiring access remains unavailable until connected | FIG-TEN | GOV-TEN-010 | MTD-BLD-003/004 | EX-BLD-009..012 | COVERED |
| REQ-GOV-005 | Tenant prompt cannot override Pattern governance | FIG-TEN/RULE | GOV-TEN-011 | MTD-PAT-002/BLD-002 | EX-PAT-004, EX-BLD-005 | COVERED |
| REQ-GOV-006 | Required 10 rollout tenants exist | ENG | GOV-TEN-001 | MTD-GOV-005 | EX-GOV-015 | COVERED |
| REQ-GOV-007 | Required default Space exists for each tenant | ENG/FLOW | GOV-TEN-002 | MTD-GOV-005 | EX-GOV-016 | COVERED |
| REQ-GOV-008 | Mandatory default Space cannot be removed | FIG-TEN | GOV-SPC-001 | MTD-GOV-005 | EX-GOV-017 | COVERED |
| REQ-SPC-001 | Tenant Owner creates Space | RAM 5.1/FLOW | GOV-SPC-005 | MTD-GOV-003 | EX-GOV-008..009 | PARTIAL — release scope |
| REQ-SPC-002 | Tenant Owner assigns Space Owner | RAM 5.2 | GOV-SPC-004 | MTD-GOV-003 | EX-GOV-010 | COVERED |
| REQ-SPC-003 | Space Owner assigns members/roles from existing Tenant Members | RAM 5.5 | GOV-SPC-004/GOV-SPC-009 | MTD-GOV-004/GOV-006 | EX-GOV-011..014, EX-GOV-020..021 | COVERED |
| REQ-SPC-004 | Tenant Member has read-only tenant configuration access | RAM 4.1 | GOV-TEN-013 | MTD-GOV-006 | EX-GOV-018..019 | COVERED |
| REQ-SPC-005 | Space System Prompt participates in governance hierarchy | FIG-SPC/RULE | GOV-SPC-008 | MTD-GOV-007 | EX-GOV-022..023 | COVERED |

# 4. Agent Creation & Configuration

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-BLD-001 | Space Designer creates Agent | RAM 6.1/FLOW | BLD-CRT-001 | MTD-BLD-001 | EX-BLD-001..004 | COVERED |
| REQ-BLD-002 | Low Risk is default/pre-selected | ENG/FLOW | BLD-CRT-002 | MTD-BLD-001 | EX-BLD-001 | COVERED |
| REQ-BLD-003 | Agent uses exactly one Pattern | ENG/FLOW | BLD-CRT-003 | MTD-BLD-001 | EX-BLD-001 | COVERED |
| REQ-BLD-008 | Natural-language idea starts assisted creation | FIG-BLD | BLD-CRT-004 | MTD-BLD-005 | EX-BLD-013 | COVERED |
| REQ-BLD-009 | Builder asks focused follow-up questions | FIG-BLD | BLD-CRT-005 | MTD-BLD-005 | EX-BLD-014 | COVERED |
| REQ-BLD-010 | Space Designer can create Agent from scratch | FIG-BLD/RAM 6.1 | BLD-CRT-006 | MTD-BLD-006 | EX-BLD-015 | COVERED |
| REQ-BLD-011 | Required creation fields prevent invalid draft | FIG-BLD/RULE | BLD-CRT-007 | MTD-BLD-006 | EX-BLD-016 | COVERED |
| REQ-BLD-012 | Cancelling creation creates no unintended Agent | FIG-BLD/RULE | BLD-CRT-008 | MTD-BLD-007 | EX-BLD-017 | COVERED |
| REQ-BLD-004 | Space Designer configures Agent | RAM 6.2 | BLD-CFG-002 | MTD-BLD-002 | EX-BLD-005..008 | COVERED |
| REQ-BLD-005 | Agent instructions cannot override higher governance | RULE | BLD-CFG-002 | MTD-BLD-002 | EX-BLD-005 + governed runtime | COVERED |
| REQ-BLD-006 | Designer attaches approved MCP/skills | RAM 6.4 | BLD-CFG-003/004 | MTD-BLD-003 | EX-BLD-009..010 | COVERED |
| REQ-BLD-007 | Unapproved MCP/skills/API cannot be used | ENG/RULE | BLD-CFG-003/004, SEC-RBAC-009/010 | MTD-BLD-004 | EX-BLD-011..012 | COVERED |
| REQ-BLD-013 | Approved connection/tool selection and personal access setup are enforced | FIG-BLD/RAM 6.4 | BLD-CFG-010 | MTD-BLD-003 | EX-BLD-018..019 | COVERED |

# 5. Agent Visibility / Edit / RBAC

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-ACC-001 | TO/SO/Designer/User can view same-Space Agents | RAM 6.5 | SEC-RBAC-001..004 | MTD-ACC-001 | EX-ACC-001..004 | COVERED |
| REQ-ACC-002 | Platform Admin/Viewer do not gain same-Space Agent view | RAM 6.5 | SEC-RBAC-005 | MTD-ACC-001 | EX-ACC-005..006 | COVERED |
| REQ-ACC-003 | Only Space Designer edits same-Space Agent | RAM 6.6 | SEC-RBAC-003/005/006 | MTD-ACC-002 | EX-ACC-007..011 | COVERED |
| REQ-ACC-004 | Authorization denial protects operation, not only UI | RULE | SEC-RBAC-006 | MTD-ACC-002/RUN-003/ISO-001 | direct-request variants | COVERED where service testable |

# 6. Runtime / Harness

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-RUN-001 | Designer can run same-Space Agent | RAM 6.7/7.1 | RUN-001 | MTD-RUN-001 | EX-RUN-001 | COVERED |
| REQ-RUN-002 | Space User can run same-Space Agent | RAM 7.1 | RUN-001/SEC-RBAC-004 | MTD-RUN-002 | EX-RUN-002 | COVERED |
| REQ-RUN-003 | Tenant Owner cannot run from TO role alone | RAM 7.1 | SEC-RBAC-005 | MTD-RUN-003 | EX-RUN-003 | COVERED |
| REQ-RUN-004 | Space Owner cannot run from SO role alone | RAM 7.1 | SEC-RBAC-006 | MTD-RUN-003 | EX-RUN-004 | COVERED |
| REQ-RUN-005 | Unauthorized direct runtime invocation rejected | RULE | SEC-RBAC-006 | MTD-RUN-003 | EX-RUN-005..006 | COVERED |
| REQ-RUN-006 | User can view own execution outputs/history | RAM 7.2 | RUN-007 | MTD-RUN-004 | EX-RUN-007..010 | COVERED |
| REQ-RUN-007 | Multi-turn conversation retains appropriate context | FIG-RUN | RUN-003 | MTD-RUN-005 | EX-RUN-011..012 | COVERED |
| REQ-RUN-008 | Runtime respects inherited governance | ENG/RULE | RUN-004 | MTD-RUN-005/PAT-002 | EX-RUN-013..014, EX-PAT-004 | COVERED |
| REQ-RUN-009 | Runtime exposes request metadata where supported | FIG-RUN | RUN-002 | MTD-RUN-001/002 | EX-RUN-001..002 | COVERED |

# 7. Runtime Sources

| Req ID | Requirement / Rule | Source | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-SRC-001 | Add supported personal source | FIG-RUN | SRC-001 | MTD-SRC-001 | EX-SRC-001..002 | COVERED |
| REQ-SRC-002 | Personal source hidden from other users | FIG-RUN | SRC-002 | MTD-SRC-002 | EX-SRC-003..005 | COVERED |
| REQ-SRC-003 | Personal source is read-only to Agent | FIG-RUN | SRC-003 | MTD-SRC-001 | EX-SRC-001..002 | COVERED |
| REQ-SRC-004 | Source selection determines active context | FIG-RUN | SRC-009/010/012 | MTD-SRC-003 | EX-SRC-006..008 | COVERED |
| REQ-SRC-005 | Supported types / 10MB boundary | FIG-RUN | SRC-004..007 | Planned P1 detail | — | PARTIAL |
| REQ-SRC-006 | PUBLIC/INTERNAL classification restriction | FIG-RUN | related source validation | Pending mechanism | — | BLOCKED |

# 8. Generated Files

| Req ID | Requirement / Rule | Source | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-GEN-001 | Generate output artifact | FIG-RUN | GEN-001 | MTD-GEN-001 | EX-GEN-001..002 | COVERED |
| REQ-GEN-002 | Retrieve/open artifact | FIG-RUN | GEN-002 | MTD-GEN-002 | EX-GEN-003 | COVERED |
| REQ-GEN-003 | Output materially corresponds to request/source | RULE | GEN-009 | MTD-GEN-002 | EX-GEN-003 | COVERED |
| REQ-GEN-004 | Unauthorized user cannot access protected artifact | RULE | GEN-007/009 | MTD-GEN-002 | EX-GEN-004..005 | PARTIAL — ownership semantics |

# 9. Space / Tenant Isolation

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-ISO-001 | Agent visibility limited to authorized same Space | ENG/FLOW/RAM 6.5 | MKT-004/SEC-RBAC-007 | MTD-ISO-001 | EX-ISO-001..004 | COVERED |
| REQ-ISO-002 | Cross-Tenant unauthorized discovery/use denied | RULE | MKT-004/SEC-RBAC-008 | MTD-ISO-002 | EX-ISO-005..007 | COVERED |

# 10. Publication / Marketplace / Versioning

| Req ID | Requirement / Rule | Source / RAM | Scenario | Definition | Execution | Status |
|---|---|---|---|---|---|---|
| REQ-PUB-001 | Unpublished draft not generally consumable; Designer may debug | FIG-BLD/RAM 6.7 | PUB-001 | MTD-PUB-001 | EX-PUB-001..002 | COVERED |
| REQ-PUB-002 | Space Designer publishes Agent to Agent Marketplace of the Space | RAM 6.8/FIG-BLD | PUB-002/003 | MTD-PUB-002 | EX-PUB-003..006 | COVERED |
| REQ-PUB-003 | Publication remains within intended Space boundary | RAM 6.8/7.1 | PUB-003/010 | MTD-PUB-003 | EX-PUB-007..009 | COVERED |
| REQ-PUB-004 | Publication creates frozen release with version metadata | FIG-BLD/RULE | PUB-004/006/007/009 | MTD-PUB-002/VER-001 | EX-PUB-003..004, EX-VER-001..005 | COVERED |
| REQ-VER-001 | Draft edits after V1 do not alter V1 | FIG-BLD/RULE | VER-001 | MTD-VER-001 | EX-VER-002..003 | COVERED |
| REQ-VER-002 | Space Designer publishes V2 as new frozen version | RAM 6.8/FIG-BLD | VER-002 | MTD-VER-001 | EX-VER-004 | COVERED |
| REQ-VER-003 | Consumer switches to V2 only after publish | FIG-MKT/RULE | VER-003 | MTD-VER-001 | EX-VER-003..005 | COVERED |
| REQ-MKT-001 | Authorized consumer opens Space Agent Marketplace | FIG-MKT/RAM 7.1 | MKT-001 | MTD-MKT-001 | EX-MKT-001 | COVERED |
| REQ-MKT-002 | Published Agent becomes discoverable in intended Space | FIG-MKT/RAM 6.8 | MKT-002 | MTD-MKT-001 | EX-MKT-002..003 | COVERED |
| REQ-MKT-003 | Cross-Space user cannot discover/run published Agent | RAM 6.8/7.1/RULE | MKT-004 | MTD-PUB-003/ISO-001 | EX-PUB-009, EX-MKT-004, EX-ISO-002..004 | COVERED |

# 11. P0 E2E Traceability

| E2E Scenario | Definition / Chain | Coverage |
|---|---|---|
| E2E-001 Governed lifecycle | MTD-E2E-001 / EX-E2E-001 / E2E-X01 | COVERED |
| E2E-002 Inheritance/capability boundary | MTD-E2E-001 / EX-E2E-001 | COVERED |
| E2E-003 V1 first publication | MTD-E2E-001 + MTD-VER-001 / EX-E2E-001 | COVERED |
| E2E-004 V1 → draft → V2 | MTD-VER-001 / E2E-X04 | COVERED functionally |
| E2E-005 Space publication boundary | MTD-PUB-003 / E2E-X05 | COVERED |
| E2E-006 Space isolation | MTD-ISO-001 / E2E-X03 | COVERED |
| E2E-007 Source-grounded runtime | MTD-E2E-002 + MTD-SRC-001/003 / EX-E2E-002 / E2E-X02 | COVERED |
| E2E-008 Runtime-to-artifact | MTD-E2E-002 + MTD-GEN-001/002 / EX-E2E-002 / E2E-X02 | COVERED |

# 12. Current P0 Coverage Position

The reconciled catalogue has **60 P0 scenarios** within **158 total scenarios**. These intentionally map into **37 reusable P0 definitions**, not one-to-one cases. The functional definitions expand to **109 role/scope/state execution variants**. Two dedicated E2E regression variants bring the dashboard-managed baseline to **111 variants**. The **10 smoke checks** remain the initial environment sanity gate.

The updated matrix and implemented screen resolve the prior publication ambiguity for this release: **Space Designer publishes to the Agent Marketplace of the Space under RAM 6.8**. Production deployment remains out of scope.

# 13. Open Requirement Clarifications

1. Additional-Space rollout scope beyond the required default Space.
4. Pattern names/configuration: engineering Low Risk + SDLC vs Training Figma Low Risk + Research.
5. Pattern UI read-only vs privileged Pattern administration.
4. RAM 6.3 Review agent configuration request flow.
7. Source PUBLIC/INTERNAL classification mechanism.
8. Generated-file ownership/retention.
9. Multi-role effective permissions.
10. Agentic Workflow 2.0 detailed functional basis.

# 14. Traceability Maintenance Rule

When a requirement changes: update its source/rule → identify affected Scenario IDs → review affected Manual Test Definitions → update only impacted execution variants → preserve historical evidence against the requirement version used during execution.

**End of Document**