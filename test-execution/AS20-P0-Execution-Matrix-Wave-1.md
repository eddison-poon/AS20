# Agent Studio 2.0 — P0 Execution Matrix — Wave 1

**Document Status:** Draft v0.1  
**Execution Status:** Not Executed — Awaiting Environment  
**Test Definitions:** `test-definitions/manual/AS20-P0-Manual-Test-Definitions-Wave-1.md`  
**RBAC Baseline:** `docs/role-access/Agent-Studio-2.0-RBAC-Accessibility-Matrix.md`

---

## 1. Purpose

This matrix converts the reusable Wave 1 Manual Test Definitions into concrete execution variants. It makes explicit **who executes what, in which scope, and whether the action is expected to be allowed or denied**.

The goal is not to run every test definition once per role. Instead, executions are selected according to business risk and the official Roles & Actions Matrix.

---

## 2. Execution Dimensions

Each execution may vary by:

- Role.
- Tenant.
- Space.
- Membership.
- Pattern/resource assignment.
- Agent lifecycle state.
- User ownership.
- Source ownership.
- Expected authorization result.

### Expected Access Values

- **ALLOW** — user should be able to complete the action.
- **DENY** — user must not be able to complete the action.
- **VIEW ONLY** — object may be visible but mutation/execution must remain unavailable.
- **TBD** — requirement mapping not yet frozen.
- **N/A** — excluded by current release scope/environment.

---

## 3. Logical Test Users

| User ID | Role | Tenant | Space | Purpose |
|---|---|---|---|---|
| U-TO-A | Tenant Owner | Tenant A | Space A | Tenant administration and negative agent-runtime checks |
| U-SO-A | Space Owner | Tenant A | Space A | Space administration and negative agent-runtime checks |
| U-SD-A | Space Designer | Tenant A | Space A | Primary agent creator/builder |
| U-SU-A1 | Space User | Tenant A | Space A | Primary agent consumer |
| U-SU-A2 | Space User | Tenant A | Space A | Same-space second user for privacy/history checks |
| U-SU-B | Space User | Tenant A | Space B only | Cross-space isolation |
| U-SU-TB | Space User | Tenant B | Tenant B space | Cross-tenant isolation |
| U-PA | AH Platform Admin | Platform | — | Selected tenant administration / negative agent access |
| U-ENG | AH Engineer | Platform | — | Negative current-scope agent access |
| U-VR | Viewer / Requestor | Platform | — | Pattern browse / negative tenant-agent access |
| U-GOV | Governance Manager | Platform | — | Pattern/governance view / negative agent access |

Where a person holds multiple roles, test accounts should preferably be role-pure for RBAC validation. Multi-role effective-permission testing can be added separately once combination rules are confirmed.

---

# 4. Tenant & Space Governance Executions

| Exec ID | Test Definition | Matrix Ref | User / Role | Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|---|
| EX-GOV-001 | MTD-GOV-001 | 4.3 | U-TO-A / Tenant Owner | Tenant A | ALLOW | Can enable/disable applicable tenant Agent Pattern |
| EX-GOV-002 | MTD-GOV-001 | 4.3 | U-SO-A / Space Owner | Tenant A | DENY | Cannot change tenant pattern enablement |
| EX-GOV-003 | MTD-GOV-001 | 4.3 | U-SD-A / Space Designer | Tenant A | DENY | Cannot change tenant pattern enablement |
| EX-GOV-004 | MTD-GOV-001 | 4.3 | U-SU-A1 / Space User | Tenant A | DENY | Cannot change tenant pattern enablement |
| EX-GOV-005 | MTD-GOV-002 | 4.4 | U-TO-A / Tenant Owner | Tenant A | ALLOW | Can define permitted agent capabilities/types |
| EX-GOV-006 | MTD-GOV-002 | 4.4 | U-SO-A / Space Owner | Tenant A | DENY | Cannot define tenant-level agent capability/types |
| EX-GOV-007 | MTD-GOV-002 | 4.4 | U-SD-A / Space Designer | Tenant A | DENY | Cannot expand own tenant capability allowance |
| EX-GOV-008 | MTD-GOV-003 | 5.1 | U-TO-A / Tenant Owner | Tenant A | ALLOW / N/A if disabled for release | Can create Space B if feature is in release scope |
| EX-GOV-009 | MTD-GOV-003 | 5.1 | U-SO-A / Space Owner | Tenant A | DENY | Cannot create space within tenant |
| EX-GOV-010 | MTD-GOV-003 | 5.2 | U-TO-A / Tenant Owner | Space B | ALLOW / N/A | Can assign/change Space Owner |
| EX-GOV-011 | MTD-GOV-004 | 6.3 | U-SO-A / Space Owner | Space A | ALLOW | Can add space members and assign roles |
| EX-GOV-012 | MTD-GOV-004 | 6.3 | U-TO-A / Tenant Owner | Space A | DENY | Tenant Owner does not receive 6.3 action under supplied matrix |
| EX-GOV-013 | MTD-GOV-004 | 6.3 | U-SD-A / Space Designer | Space A | DENY | Cannot assign space roles |
| EX-GOV-014 | MTD-GOV-004 | 6.3 | U-SU-A1 / Space User | Space A | DENY | Cannot assign space roles |

---

# 5. Agent Build & Configuration Executions

| Exec ID | Test Definition | Matrix Ref | User / Role | Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|---|
| EX-BLD-001 | MTD-BLD-001 | 6.1 | U-SD-A / Space Designer | Tenant A / Space A | ALLOW | Creates agent from enabled Low Risk Pattern |
| EX-BLD-002 | MTD-BLD-001 | 6.1 | U-TO-A / Tenant Owner | Space A | DENY | Cannot create agent |
| EX-BLD-003 | MTD-BLD-001 | 6.1 | U-SO-A / Space Owner | Space A | DENY | Cannot create agent |
| EX-BLD-004 | MTD-BLD-001 | 6.1 | U-SU-A1 / Space User | Space A | DENY | Cannot create agent |
| EX-BLD-005 | MTD-BLD-002 | 6.2 | U-SD-A / Space Designer | Agent A | ALLOW | Can configure prompt/logic/parameters |
| EX-BLD-006 | MTD-BLD-002 | 6.2 | U-TO-A / Tenant Owner | Agent A | DENY | Cannot configure agent despite admin role |
| EX-BLD-007 | MTD-BLD-002 | 6.2 | U-SO-A / Space Owner | Agent A | DENY | Cannot configure agent |
| EX-BLD-008 | MTD-BLD-002 | 6.2 | U-SU-A1 / Space User | Agent A | DENY | Cannot configure agent |
| EX-BLD-009 | MTD-BLD-003 | 6.5 | U-SD-A / Space Designer | Agent A | ALLOW | Can attach approved MCP/skill |
| EX-BLD-010 | MTD-BLD-003 | 6.5 | U-SO-A / Space Owner | Agent A | DENY | Cannot attach MCP/skill |
| EX-BLD-011 | MTD-BLD-004 | 6.5 | U-SD-A / Space Designer | Agent A | DENY resource | Unapproved MCP/skill cannot be attached/used |
| EX-BLD-012 | MTD-BLD-004 | 4.4/6.5 | U-SD-A / Space Designer | Agent A | DENY resource | Direct attempt to bypass allowed-resource list is rejected |

---

# 6. Agent Visibility & Edit Executions

| Exec ID | Test Definition | Matrix Ref | User / Role | Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|---|
| EX-ACC-001 | MTD-ACC-001 | 6.6 | U-TO-A / Tenant Owner | Same Space A | VIEW ONLY | Can view Agent A but does not gain edit/run rights |
| EX-ACC-002 | MTD-ACC-001 | 6.6 | U-SO-A / Space Owner | Same Space A | VIEW ONLY | Can view Agent A |
| EX-ACC-003 | MTD-ACC-001 | 6.6 | U-SD-A / Space Designer | Same Space A | ALLOW | Can view Agent A |
| EX-ACC-004 | MTD-ACC-001 | 6.6 | U-SU-A1 / Space User | Same Space A | ALLOW | Can view Agent A |
| EX-ACC-005 | MTD-ACC-001 | 6.6 | U-PA / AH Platform Admin | Agent A | DENY | No same-space agent-view action from platform-admin role alone |
| EX-ACC-006 | MTD-ACC-001 | 6.6 | U-VR / Viewer Requestor | Agent A | DENY | Pattern catalogue access does not imply tenant agent visibility |
| EX-ACC-007 | MTD-ACC-002 | 6.7 | U-SD-A / Space Designer | Agent A | ALLOW | Can edit Agent A |
| EX-ACC-008 | MTD-ACC-002 | 6.7 | U-TO-A / Tenant Owner | Agent A | DENY | Cannot edit Agent A |
| EX-ACC-009 | MTD-ACC-002 | 6.7 | U-SO-A / Space Owner | Agent A | DENY | Cannot edit Agent A |
| EX-ACC-010 | MTD-ACC-002 | 6.7 | U-SU-A1 / Space User | Agent A | DENY | Cannot edit Agent A |
| EX-ACC-011 | MTD-ACC-002 | 6.7 | Unauthorized direct request | Agent A | DENY | Backend/service rejects unauthorized edit |

---

# 7. Agent Runtime Executions

| Exec ID | Test Definition | Matrix Ref | User / Role | Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|---|
| EX-RUN-001 | MTD-RUN-001 | 6.8/7.1 | U-SD-A / Space Designer | Agent A / Space A | ALLOW | Agent executes successfully |
| EX-RUN-002 | MTD-RUN-002 | 6.8/7.1 | U-SU-A1 / Space User | Agent A / Space A | ALLOW | Agent executes successfully |
| EX-RUN-003 | MTD-RUN-003 | 6.8/7.1 | U-TO-A / Tenant Owner | Agent A / Space A | DENY | Can view but cannot execute |
| EX-RUN-004 | MTD-RUN-003 | 6.8/7.1 | U-SO-A / Space Owner | Agent A / Space A | DENY | Can view but cannot execute |
| EX-RUN-005 | MTD-RUN-003 | 7.1 | U-PA / AH Platform Admin | Agent A | DENY | Platform administration does not grant agent runtime access |
| EX-RUN-006 | MTD-RUN-003 | 7.1 | Unauthorized direct request | Agent A | DENY | Runtime service rejects invocation |
| EX-RUN-007 | MTD-RUN-004 | 7.2 | U-SU-A1 / Space User | Own history | ALLOW | Can view own outputs/history |
| EX-RUN-008 | MTD-RUN-004 | 7.2 | U-SD-A / Space Designer | Own history | ALLOW | Can view own outputs/history |
| EX-RUN-009 | MTD-RUN-004 | 7.2 | U-SU-A2 / Space User | U-SU-A1 history | DENY | Cannot view another user's protected history |
| EX-RUN-010 | MTD-RUN-004 | 7.2 | Direct history URL/ID | Other user's execution | DENY | Object-level authorization prevents access |

---

# 8. Runtime Source Executions

| Exec ID | Test Definition | User / Role | Source Variant | Expected Access | Key Expected Result |
|---|---|---|---|---|---|
| EX-SRC-001 | MTD-SRC-001 | U-SU-A1 / Space User | Valid supported source | ALLOW | Upload/select/use succeeds |
| EX-SRC-002 | MTD-SRC-001 | U-SD-A / Space Designer | Valid supported source | ALLOW | Creator can use source during permitted runtime |
| EX-SRC-003 | MTD-SRC-002 | U-SU-A1 | Personal Source A | ALLOW | Owner can see/use own personal source |
| EX-SRC-004 | MTD-SRC-002 | U-SU-A2 | Personal Source A owned by U-SU-A1 | DENY | Same-space second user cannot see/use it |
| EX-SRC-005 | MTD-SRC-002 | Direct source URL/ID as U-SU-A2 | Other user's source | DENY | Object-level access rejected |
| EX-SRC-006 | MTD-SRC-003 | U-SU-A1 | Sources A+B+C selected | ALLOW | Active context reflects selected set |
| EX-SRC-007 | MTD-SRC-003 | U-SU-A1 | B deselected | ALLOW | B no longer acts as selected context |
| EX-SRC-008 | MTD-SRC-003 | U-SU-A1 | New Source D selected | ALLOW | Context updates to new selected set |

---

# 9. Generated File Executions

| Exec ID | Test Definition | User / Role | Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|
| EX-GEN-001 | MTD-GEN-001 | U-SU-A1 / Space User | Own session | ALLOW | Generated artifact is created |
| EX-GEN-002 | MTD-GEN-001 | U-SD-A / Space Designer | Own session | ALLOW | Generated artifact is created |
| EX-GEN-003 | MTD-GEN-002 | U-SU-A1 / Space User | Own generated file | ALLOW | File retrieves/opens successfully |
| EX-GEN-004 | MTD-GEN-002 | U-SU-A2 / Space User | U-SU-A1 generated file | DENY / TBD ownership semantics | No unauthorized generated-file access |
| EX-GEN-005 | MTD-GEN-002 | Direct artifact URL/ID | Other user's artifact | DENY | Object-level access protection applies |

---

# 10. Space & Tenant Isolation Executions

| Exec ID | Test Definition | User / Role | Object Scope | Expected Access | Key Expected Result |
|---|---|---|---|---|---|
| EX-ISO-001 | MTD-ISO-001 | U-SU-A1 / Space User | Agent A in Space A | ALLOW | Same-space consumer can view/run |
| EX-ISO-002 | MTD-ISO-001 | U-SU-B / Space User | Agent A in Space A | DENY | Space B-only user cannot discover Agent A |
| EX-ISO-003 | MTD-ISO-001 | U-SU-B direct URL | Agent A in Space A | DENY | Direct cross-space access rejected |
| EX-ISO-004 | MTD-ISO-001 | U-SU-B direct runtime request | Agent A in Space A | DENY | Cross-space execution rejected |
| EX-ISO-005 | MTD-ISO-002 | U-SU-A1 | Tenant A Agent A | ALLOW | Authorized Tenant A user can use agent |
| EX-ISO-006 | MTD-ISO-002 | U-SU-TB / Tenant B user | Tenant A Agent A | DENY | Cross-tenant discovery blocked |
| EX-ISO-007 | MTD-ISO-002 | U-SU-TB direct request | Tenant A Agent A | DENY | Cross-tenant invocation blocked |

---

# 11. Publication / Marketplace Executions — Pending Clarification

| Exec ID | Test Definition | Candidate Role | State | Expected Access | Status |
|---|---|---|---|---|---|
| EX-PUB-001 | MTD-PUB-001 | U-SD-A creates draft | Unpublished draft | ALLOW creator test as supported | Design-ready |
| EX-PUB-002 | MTD-PUB-001 | U-SU-A1 | Unpublished draft | DENY general consumption | Design-ready |
| EX-PUB-003 | MTD-PUB-002 | Space Designer? | Figma Publish — Private Testing | TBD | Blocked — role mapping |
| EX-PUB-004 | MTD-PUB-002 | Space Designer? / Tenant Owner? | Figma Publish — Marketplace Testing | TBD | Blocked — role mapping |
| EX-PUB-005 | MTD-PUB-002 | U-TO-A / Tenant Owner | Matrix 6.9 Promote to tenant-shared | ALLOW per matrix | Design-ready as matrix action; mapping to Figma TBD |
| EX-PUB-006 | MTD-PUB-002 | U-SD-A / Space Designer | Matrix 6.9 Promote to tenant-shared | DENY per matrix | Design-ready as matrix action; mapping to Figma TBD |

Do not merge `Publish`, `Marketplace Testing`, and `Promote to tenant-shared` into one state transition until product ownership confirms the intended model.

---

# 12. E2E Execution Chains

## E2E-X01 — Governed Build-to-Run Chain

| Sequence | User | Action | Matrix Ref | Expected |
|---:|---|---|---|---|
| 1 | Tenant Owner | Enable Low Risk Pattern | 4.3 | ALLOW |
| 2 | Tenant Owner | Confirm permitted capability/types | 4.4 | ALLOW |
| 3 | Tenant Owner | Create/confirm Space A | 5.1 | ALLOW / N/A if default space pre-exists |
| 4 | Tenant Owner | Assign Space Owner | 5.2 | ALLOW |
| 5 | Space Owner | Add Space Designer + Space User | 6.3 | ALLOW |
| 6 | Space Designer | Create Agent A | 6.1 | ALLOW |
| 7 | Space Designer | Configure Agent A | 6.2 | ALLOW |
| 8 | Space Designer | Attach approved MCP/skill | 6.5 | ALLOW |
| 9 | Space Designer | Attempt unapproved MCP/skill | 6.5 + governance | DENY resource |
| 10 | Applicable role | Publish/share transition | TBD / candidate 6.9 | TBD until clarified |
| 11 | Space User | View Agent A | 6.6 | ALLOW |
| 12 | Space User | Run Agent A | 6.8/7.1 | ALLOW |
| 13 | Tenant Owner | Attempt run Agent A | 6.8/7.1 | DENY |
| 14 | Space Owner | Attempt run Agent A | 6.8/7.1 | DENY |

## E2E-X02 — Runtime Source-to-Artifact Chain

| Sequence | User | Action | Expected |
|---:|---|---|---|
| 1 | Space User A1 | Open/run Agent A | ALLOW |
| 2 | Space User A1 | Upload Personal Source A | ALLOW |
| 3 | Space User A1 | Select Source A | ALLOW |
| 4 | Space User A1 | Ask source-grounded question | Response uses selected context |
| 5 | Space User A1 | Request generated file | Artifact created |
| 6 | Space User A1 | Retrieve generated file | ALLOW |
| 7 | Space User A2 | Search for Personal Source A | DENY |
| 8 | Space User A2 | Attempt direct source access | DENY |
| 9 | Space User A2 | Attempt another user's protected generated artifact | DENY / confirm ownership semantics |

## E2E-X03 — Space Isolation Chain

| Sequence | User | Action | Expected |
|---:|---|---|---|
| 1 | Space User A1 | Discover Agent A in Space A | ALLOW |
| 2 | Space User A1 | Execute Agent A | ALLOW |
| 3 | Space User B | Search Agent A from Space B-only scope | DENY |
| 4 | Space User B | Open direct Agent A URL | DENY |
| 5 | Space User B | Invoke Agent A directly | DENY |

---

# 13. Execution Count

| Area | Planned Executions |
|---|---:|
| Governance / Space | 14 |
| Agent Build / Configuration | 12 |
| Visibility / Edit | 11 |
| Runtime | 10 |
| Sources | 8 |
| Generated Files | 5 |
| Space / Tenant Isolation | 7 |
| Publication / Marketplace | 6 |
| **Total explicit execution variants** | **73** |

The three E2E chains reuse the above executions and are not added to the 73 to avoid double counting.

---

# 14. Recommended Smoke Subset

For an initial environment/build sanity check, execute this compact chain before the full Wave 1 suite:

| Smoke ID | Execution | Reason |
|---|---|---|
| SMK-01 | EX-GOV-001 | Tenant governance available |
| SMK-02 | EX-GOV-011 | Space role administration works |
| SMK-03 | EX-BLD-001 | Space Designer can create agent |
| SMK-04 | EX-BLD-009 | Approved capability can be attached |
| SMK-05 | EX-ACC-004 | Space User can view same-space agent |
| SMK-06 | EX-RUN-002 | Space User can execute agent |
| SMK-07 | EX-RUN-003 | Tenant Owner cannot execute |
| SMK-08 | EX-SRC-001 | Source upload/runtime works |
| SMK-09 | EX-GEN-001 | Generated artifact works |
| SMK-10 | EX-ISO-002 | Cross-space visibility is blocked |

Publication/share should be inserted between SMK-04 and SMK-05 once its exact state/role mapping is confirmed.

---

# 15. Evidence Expectations

For each execution, record as applicable:

- Execution ID.
- Date/build/environment.
- Tester and executing test user/role.
- Tenant and Space.
- Agent/version.
- Actual result.
- Pass/Fail/Blocked/N/A.
- Screenshot or screen recording reference.
- Request/Execution ID for runtime cases.
- Relevant service response/error for authorization-negative cases where available.
- Defect ID.

For DENY cases, evidence should prove **the protected operation did not occur**, not only that a button was absent.

---

# 16. Current Blockers / Clarifications

1. Exact mapping among Figma `Publish`, `Private Testing`, `Marketplace Testing`, and matrix `6.9 Promote an agent to tenant-shared`.
2. Whether additional-space creation is active in the 28 Sep release or only part of the broader role model.
3. Exact source extensions and maximum-size boundary semantics.
4. Generated-file ownership/retention semantics.
5. Multi-role effective-permission rules if users may hold more than one role concurrently.

---

**End of Document**