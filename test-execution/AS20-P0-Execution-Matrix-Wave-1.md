# Agent Studio 2.0 — P0 Execution Matrix — Wave 1

**Document Status:** Draft v0.2 — Reconciled 16 Sep 2026  
**Execution Status:** Not Executed — Awaiting Environment  
**Test Definitions:** `test-definitions/manual/AS20-P0-Manual-Test-Definitions-Wave-1.md`  
**RBAC Baseline:** `docs/role-access/Agent-Studio-2.0-RBAC-Accessibility-Matrix.md`

## 1. Purpose

This consolidated matrix expands the **32 reusable P0 Manual Test Definitions** into **96 explicit execution variants**. It records who executes what, in which scope/state, and whether the operation is expected to be allowed or denied.

Expected access: **ALLOW**, **DENY**, **VIEW ONLY**, **TBD**, or **N/A**.

## 2. Logical Test Users

| User ID | Role | Tenant / Space |
|---|---|---|
| U-TO-A | Tenant Owner | Tenant A / Space A |
| U-SO-A | Space Owner | Tenant A / Space A |
| U-SD-A | Space Designer | Tenant A / Space A |
| U-SU-A1 | Space User | Tenant A / Space A |
| U-SU-A2 | Space User | Tenant A / Space A |
| U-SU-B | Space User | Tenant A / Space B only |
| U-SU-TB | Space User | Tenant B only |
| U-PA | AH Platform Admin | Platform |
| U-ENG | AH Engineer | Platform |
| U-VR | Viewer / Requestor | Platform |
| U-GOV | Governance Manager | Platform |

Prefer role-pure accounts for RBAC validation. Multi-role effective-permission testing remains a clarification.

# 3. Pattern / Tenant / Space Governance Executions

| Exec ID | Definition | Matrix Ref | User / Role | Scope | Expected | Key Result |
|---|---|---|---|---|---|---|
| EX-PAT-001 | MTD-PAT-001 | — | Authorized pattern viewer/admin | Platform | ALLOW | Low Risk Pattern exists/identifiable |
| EX-PAT-002 | MTD-PAT-001 | — | Authorized pattern viewer/admin | Platform | ALLOW | SDLC Pattern exists/identifiable |
| EX-PAT-003 | MTD-PAT-002 | — | Authorized governance setup | Pattern/Tenant | ALLOW | Pattern rule persists/inherits |
| EX-PAT-004 | MTD-PAT-002 | — | Space Designer runtime | Conflicting lower instruction | DENY override | Pattern rule remains effective |
| EX-GOV-001 | MTD-GOV-001 | 4.3 | U-TO-A | Tenant A | ALLOW | Can enable/disable Pattern |
| EX-GOV-002 | MTD-GOV-001 | 4.3 | U-SO-A | Tenant A | DENY | Cannot change Pattern enablement |
| EX-GOV-003 | MTD-GOV-001 | 4.3 | U-SD-A | Tenant A | DENY | Cannot change Pattern enablement |
| EX-GOV-004 | MTD-GOV-001 | 4.3 | U-SU-A1 | Tenant A | DENY | Cannot change Pattern enablement |
| EX-GOV-005 | MTD-GOV-002 | 4.4 | U-TO-A | Tenant A | ALLOW | Defines permitted capability/types |
| EX-GOV-006 | MTD-GOV-002 | 4.4 | U-SO-A | Tenant A | DENY | Cannot define tenant capabilities |
| EX-GOV-007 | MTD-GOV-002 | 4.4 | U-SD-A | Tenant A | DENY | Cannot expand allowance |
| EX-GOV-008 | MTD-GOV-003 | 5.1 | U-TO-A | Tenant A | ALLOW / N/A | Creates Space B if in scope |
| EX-GOV-009 | MTD-GOV-003 | 5.1 | U-SO-A | Tenant A | DENY | Cannot create Space |
| EX-GOV-010 | MTD-GOV-003 | 5.2 | U-TO-A | Space B | ALLOW / N/A | Assign/change Space Owner |
| EX-GOV-011 | MTD-GOV-004 | 6.3 | U-SO-A | Space A | ALLOW | Add members/assign roles |
| EX-GOV-012 | MTD-GOV-004 | 6.3 | U-TO-A | Space A | DENY | Does not receive 6.3 |
| EX-GOV-013 | MTD-GOV-004 | 6.3 | U-SD-A | Space A | DENY | Cannot assign roles |
| EX-GOV-014 | MTD-GOV-004 | 6.3 | U-SU-A1 | Space A | DENY | Cannot assign roles |
| EX-GOV-015 | MTD-GOV-005 | — | Tenant Owner/admin view | Rollout tenants | ALLOW | All 10 required tenants exist |
| EX-GOV-016 | MTD-GOV-005 | — | Tenant Owner/admin view | Default Spaces | ALLOW | Required default Space exists for each tenant |
| EX-GOV-017 | MTD-GOV-005 | — | Tenant Owner | Mandatory default Space | DENY removal | Required default Space protected |

# 4. Agent Build & Configuration Executions

| Exec ID | Definition | Matrix Ref | User / Role | Scope | Expected | Key Result |
|---|---|---|---|---|---|---|
| EX-BLD-001 | MTD-BLD-001 | 6.1 | U-SD-A | Space A | ALLOW | Creates Agent from enabled Low Risk |
| EX-BLD-002 | MTD-BLD-001 | 6.1 | U-TO-A | Space A | DENY | Cannot create Agent |
| EX-BLD-003 | MTD-BLD-001 | 6.1 | U-SO-A | Space A | DENY | Cannot create Agent |
| EX-BLD-004 | MTD-BLD-001 | 6.1 | U-SU-A1 | Space A | DENY | Cannot create Agent |
| EX-BLD-005 | MTD-BLD-002 | 6.2 | U-SD-A | Agent A | ALLOW | Configure Agent |
| EX-BLD-006 | MTD-BLD-002 | 6.2 | U-TO-A | Agent A | DENY | Cannot configure |
| EX-BLD-007 | MTD-BLD-002 | 6.2 | U-SO-A | Agent A | DENY | Cannot configure |
| EX-BLD-008 | MTD-BLD-002 | 6.2 | U-SU-A1 | Agent A | DENY | Cannot configure |
| EX-BLD-009 | MTD-BLD-003 | 6.5 | U-SD-A | Agent A | ALLOW | Attach approved MCP/skill |
| EX-BLD-010 | MTD-BLD-003 | 6.5 | U-SO-A | Agent A | DENY | Cannot attach MCP/skill |
| EX-BLD-011 | MTD-BLD-004 | 6.5 | U-SD-A | Unapproved resource | DENY resource | Cannot attach/use |
| EX-BLD-012 | MTD-BLD-004 | 4.4/6.5 | U-SD-A direct attempt | Agent A | DENY resource | Bypass rejected |

# 5. Agent Visibility & Edit Executions

| Exec ID | Definition | Matrix Ref | User / Role | Scope | Expected | Key Result |
|---|---|---|---|---|---|---|
| EX-ACC-001 | MTD-ACC-001 | 6.6 | U-TO-A | Same Space A | VIEW ONLY | Can view, not edit/run |
| EX-ACC-002 | MTD-ACC-001 | 6.6 | U-SO-A | Same Space A | VIEW ONLY | Can view |
| EX-ACC-003 | MTD-ACC-001 | 6.6 | U-SD-A | Same Space A | ALLOW | Can view |
| EX-ACC-004 | MTD-ACC-001 | 6.6 | U-SU-A1 | Same Space A | ALLOW | Can view |
| EX-ACC-005 | MTD-ACC-001 | 6.6 | U-PA | Agent A | DENY | No 6.6 from platform role |
| EX-ACC-006 | MTD-ACC-001 | 6.6 | U-VR | Agent A | DENY | Catalogue access ≠ Agent visibility |
| EX-ACC-007 | MTD-ACC-002 | 6.7 | U-SD-A | Agent A | ALLOW | Can edit |
| EX-ACC-008 | MTD-ACC-002 | 6.7 | U-TO-A | Agent A | DENY | Cannot edit |
| EX-ACC-009 | MTD-ACC-002 | 6.7 | U-SO-A | Agent A | DENY | Cannot edit |
| EX-ACC-010 | MTD-ACC-002 | 6.7 | U-SU-A1 | Agent A | DENY | Cannot edit |
| EX-ACC-011 | MTD-ACC-002 | 6.7 | Unauthorized direct request | Agent A | DENY | Backend rejects edit |

# 6. Agent Runtime Executions

| Exec ID | Definition | Matrix Ref | User / Role | Scope | Expected | Key Result |
|---|---|---|---|---|---|---|
| EX-RUN-001 | MTD-RUN-001 | 6.8/7.1 | U-SD-A | Agent A | ALLOW | Executes successfully |
| EX-RUN-002 | MTD-RUN-002 | 6.8/7.1 | U-SU-A1 | Agent A | ALLOW | Executes successfully |
| EX-RUN-003 | MTD-RUN-003 | 6.8/7.1 | U-TO-A | Agent A | DENY | View but cannot execute |
| EX-RUN-004 | MTD-RUN-003 | 6.8/7.1 | U-SO-A | Agent A | DENY | View but cannot execute |
| EX-RUN-005 | MTD-RUN-003 | 7.1 | U-PA | Agent A | DENY | Platform admin ≠ runtime |
| EX-RUN-006 | MTD-RUN-003 | 7.1 | Unauthorized direct request | Agent A | DENY | Service rejects invocation |
| EX-RUN-007 | MTD-RUN-004 | 7.2 | U-SU-A1 | Own history | ALLOW | Own history visible |
| EX-RUN-008 | MTD-RUN-004 | 7.2 | U-SD-A | Own history | ALLOW | Own history visible |
| EX-RUN-009 | MTD-RUN-004 | 7.2 | U-SU-A2 | A1 history | DENY | Other history protected |
| EX-RUN-010 | MTD-RUN-004 | 7.2 | Direct history URL/ID | Other execution | DENY | Object authorization |
| EX-RUN-011 | MTD-RUN-005 | — | U-SU-A1 | Turn 1 | ALLOW | Establish context |
| EX-RUN-012 | MTD-RUN-005 | — | U-SU-A1 | Follow-up | ALLOW | Context retained |
| EX-RUN-013 | MTD-RUN-005 | — | U-SU-A1 | Governance conflict | DENY override | Higher governance effective |
| EX-RUN-014 | MTD-RUN-005 | — | U-SD-A | Governed multi-turn | ALLOW within rules | Creator obeys same governance |

# 7. Runtime Source Executions

| Exec ID | Definition | User / Role | Variant | Expected | Key Result |
|---|---|---|---|---|---|
| EX-SRC-001 | MTD-SRC-001 | U-SU-A1 | Valid source | ALLOW | Upload/select/use; original read-only |
| EX-SRC-002 | MTD-SRC-001 | U-SD-A | Valid source | ALLOW | Creator runtime source works |
| EX-SRC-003 | MTD-SRC-002 | U-SU-A1 | Own personal source | ALLOW | Owner sees/uses |
| EX-SRC-004 | MTD-SRC-002 | U-SU-A2 | A1 source | DENY | Cannot see/use |
| EX-SRC-005 | MTD-SRC-002 | Direct source ID as A2 | A1 source | DENY | Object access rejected |
| EX-SRC-006 | MTD-SRC-003 | U-SU-A1 | A+B+C selected | ALLOW | Context reflects selected set |
| EX-SRC-007 | MTD-SRC-003 | U-SU-A1 | B deselected | ALLOW | B no longer selected context |
| EX-SRC-008 | MTD-SRC-003 | U-SU-A1 | D selected | ALLOW | Context updates |

# 8. Generated File Executions

| Exec ID | Definition | User / Role | Scope | Expected | Key Result |
|---|---|---|---|---|---|
| EX-GEN-001 | MTD-GEN-001 | U-SU-A1 | Own session | ALLOW | Artifact created |
| EX-GEN-002 | MTD-GEN-001 | U-SD-A | Own session | ALLOW | Artifact created |
| EX-GEN-003 | MTD-GEN-002 | U-SU-A1 | Own file | ALLOW | Retrieves/opens |
| EX-GEN-004 | MTD-GEN-002 | U-SU-A2 | A1 file | DENY / TBD | No unauthorized access |
| EX-GEN-005 | MTD-GEN-002 | Direct artifact ID | Other file | DENY | Object protection |

# 9. Space & Tenant Isolation Executions

| Exec ID | Definition | User / Role | Object | Expected | Key Result |
|---|---|---|---|---|---|
| EX-ISO-001 | MTD-ISO-001 | U-SU-A1 | Agent A / Space A | ALLOW | Same-Space view/run |
| EX-ISO-002 | MTD-ISO-001 | U-SU-B | Agent A | DENY | Cross-Space discovery blocked |
| EX-ISO-003 | MTD-ISO-001 | U-SU-B direct URL | Agent A | DENY | Direct access rejected |
| EX-ISO-004 | MTD-ISO-001 | U-SU-B direct runtime | Agent A | DENY | Execution rejected |
| EX-ISO-005 | MTD-ISO-002 | U-SU-A1 | Tenant A Agent | ALLOW | Authorized use |
| EX-ISO-006 | MTD-ISO-002 | U-SU-TB | Tenant A Agent | DENY | Cross-Tenant discovery blocked |
| EX-ISO-007 | MTD-ISO-002 | U-SU-TB direct request | Tenant A Agent | DENY | Invocation blocked |

# 10. Publication / Marketplace / Version Executions

| Exec ID | Definition | User / Role | State / Scope | Expected | Status / Result |
|---|---|---|---|---|---|
| EX-PUB-001 | MTD-PUB-001 | U-SD-A | Unpublished draft | ALLOW creator test as supported | Design-ready |
| EX-PUB-002 | MTD-PUB-001 | U-SU-A1 | Unpublished draft | DENY general consumption | Design-ready |
| EX-PUB-003 | MTD-PUB-002 | Space Designer? | Figma Private Testing | TBD | Role mapping blocked |
| EX-PUB-004 | MTD-PUB-002 | Designer?/Tenant Owner? | Marketplace Testing | TBD | Role mapping blocked |
| EX-PUB-005 | MTD-PUB-002 | U-TO-A | RAM 6.9 tenant-shared | ALLOW per RAM | Mapping to Figma TBD |
| EX-PUB-006 | MTD-PUB-002 | U-SD-A | RAM 6.9 tenant-shared | DENY per RAM | Mapping to Figma TBD |
| EX-PUB-007 | MTD-PUB-003 | Applicable publisher | Draft → Private Testing | TBD role | Frozen private version created |
| EX-PUB-008 | MTD-PUB-003 | Authorized private user/creator | Private Agent A | ALLOW | Intended private access |
| EX-PUB-009 | MTD-PUB-003 | Normal Marketplace consumer | Private Agent A | DENY discovery | Not in general Marketplace |
| EX-VER-001 | MTD-VER-001 | Applicable publisher | Publish V1 | TBD role | Frozen V1 created |
| EX-VER-002 | MTD-VER-001 | U-SD-A | Edit draft after V1 | ALLOW draft | V1 unchanged |
| EX-VER-003 | MTD-VER-001 | U-SU-A1 | Runtime before V2 | ALLOW V1 | Still receives V1 |
| EX-VER-004 | MTD-VER-001 | Applicable publisher | Publish V2 | TBD role | Frozen V2 created |
| EX-VER-005 | MTD-VER-001 | U-SU-A1 | Runtime after V2 | ALLOW V2 | Receives V2 |
| EX-MKT-001 | MTD-MKT-001 | U-SU-A1 | Permitted Marketplace | ALLOW | Opens permitted set |
| EX-MKT-002 | MTD-MKT-001 | U-SU-A1 | Published Agent A | ALLOW | Discoverable after publish/share |
| EX-MKT-003 | MTD-MKT-001 | U-SU-A1 | Agent A listing | ALLOW | Correct version opens |
| EX-MKT-004 | MTD-MKT-001 + MTD-ISO-001 | U-SU-B | Agent A | DENY | Unauthorized listing absent |

# 11. E2E Execution Chains

**E2E-X01 — Governed Build-to-Run:** Tenant Owner governance → Space Owner role assignment → Designer build/configure → approved capability → unapproved capability denied → publish/share TBD → Space User view/run → Tenant/Space Owner run denied.

**E2E-X02 — Runtime Source-to-Artifact:** Space User run → personal source upload/select → grounded question → generated file → retrieve → second-user source/artifact access denied as applicable.

**E2E-X03 — Space Isolation:** Space A user discover/run ALLOW → Space B-only search/direct URL/direct invocation DENY.

**E2E-X04 — Frozen Version Lifecycle:** Publish V1 → consumer verifies V1 → edit draft → consumer still V1 → publish V2 → consumer verifies V2.

**E2E-X05 — Private Publication Boundary:** Publish Private Testing → authorized private access → normal Marketplace consumer cannot discover/use.

# 12. Execution Count

| Area | Planned Executions |
|---|---:|
| Pattern / Governance / Space | 21 |
| Agent Build / Configuration | 12 |
| Visibility / Edit | 11 |
| Runtime | 14 |
| Sources | 8 |
| Generated Files | 5 |
| Space / Tenant Isolation | 7 |
| Publication / Marketplace / Version | 18 |
| **Total explicit execution variants** | **96** |

E2E chains reuse the explicit variants and are not double-counted.

# 13. Recommended Smoke Subset

| Smoke ID | Execution | Reason |
|---|---|---|
| SMK-01 | EX-GOV-001 | Tenant governance available |
| SMK-02 | EX-GOV-011 | Space role administration |
| SMK-03 | EX-BLD-001 | Designer creates Agent |
| SMK-04 | EX-BLD-009 | Approved capability attached |
| SMK-05 | EX-ACC-004 | Space User views Agent |
| SMK-06 | EX-RUN-002 | Space User executes |
| SMK-07 | EX-RUN-003 | Tenant Owner execution denied |
| SMK-08 | EX-SRC-001 | Runtime source works |
| SMK-09 | EX-GEN-001 | Generated artifact works |
| SMK-10 | EX-ISO-002 | Cross-Space visibility blocked |

Publication/share is inserted between SMK-04 and SMK-05 once exact state/role mapping is confirmed.

# 14. Evidence Expectations

Record Execution ID, build/environment, tester/user/role, Tenant/Space, Agent/version, actual result, Pass/Fail/Blocked/N/A, screenshot/recording, request/execution ID, authorization service response where available, and defect ID. For DENY cases, prove the protected operation did not occur rather than only showing a hidden button.

# 15. Current Clarifications

1. Publish / Private Testing / Marketplace Testing / RAM 6.9 mapping.
2. Additional-Space release scope.
3. Source extensions and maximum-size boundary.
4. Generated-file ownership/retention.
5. Multi-role effective permissions.

**End of Document**