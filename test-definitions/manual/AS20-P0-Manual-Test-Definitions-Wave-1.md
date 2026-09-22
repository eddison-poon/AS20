# Agent Studio 2.0 — P0 Manual Test Definitions — Wave 1

**Document Status:** Draft v0.4 — Reconciled 23 Sep 2026 with implemented screens and updated RBAC  
**Priority:** P0 / Release-Critical Baseline  
**Execution Status:** Design-ready / Not Executed — Awaiting Environment  
**Parent Catalogue:** `scenarios/Agent-Studio-2.0-Business-Scenario-Catalogue.md`  
**RBAC Baseline:** `docs/role-access/Agent-Studio-2.0-RBAC-Accessibility-Matrix.md`

## 1. Purpose

This consolidated Wave 1 baseline contains **37 reusable P0 Manual Test Definitions**. It covers the release-critical pre-production lifecycle from Pattern/Tenant/Space governance through Agent creation, publication, Marketplace/runtime, sources, generated output and isolation. Production deployment beginning with `Request deploy` is excluded.

A Test Definition is reusable; role, tenant, space, state and data permutations belong in the Execution Matrix rather than being duplicated as separate definitions.

## 2. Common Test Data

| Data | Baseline |
|---|---|
| Tenant A | Training or equivalent active use-case tenant |
| Tenant B | Second active tenant for isolation checks |
| Space A | Default Space under Tenant A |
| Space B | Second independently scoped space where available |
| Patterns | Low Risk and SDLC |
| Tenant Owner | Role-pure Tenant Owner |
| Tenant Member | Role-pure Tenant Member under Tenant A |
| Space Owner | Role-pure Space Owner |
| Space Designer A | Agent Creator assigned to Space A |
| Space User A / A2 | Two consumers assigned to Space A |
| Space User B | Consumer assigned only to Space B |
| Approved / Unapproved Skill | Scope-controlled skill test data |
| Approved / Unapproved MCP | Scope-controlled MCP/tool test data |
| Valid Source | Supported small file containing known facts |

# 3. Pattern / Tenant / Space Governance

## MTD-PAT-001 — Verify required Patterns exist and are assignable
**Scenarios:** GOV-PAT-001, GOV-PAT-002  
**Priority:** P0

**Steps:** Open applicable Pattern catalogue/administration; locate Low Risk and SDLC; inspect identity/status; verify each is available for intended assignment/adoption.

**Expected:** Both required Patterns exist as distinct Patterns and are available according to release configuration. Exact SDLC resources may remain a test-data clarification.

## MTD-PAT-002 — Verify shared Pattern rules govern downstream behaviour
**Scenarios:** GOV-PAT-005, GOV-TEN-011, RUN-004  
**Priority:** P0

**Steps:** Establish/identify a known Pattern rule; confirm it is inherited; add a compatible lower-level instruction and execute; then use a controlled lower-level instruction that conflicts with the Pattern rule.

**Expected:** Pattern rules persist and apply. Compatible lower-level instructions work; conflicting Tenant/Agent instructions cannot override higher Pattern governance.

## MTD-GOV-001 — Verify Low Risk Pattern is enabled for the tenant
**Scenario:** GOV-TEN-003  
**Matrix Ref:** 4.3  
**Principal Role:** Tenant Owner

**Steps:** Open Tenant A pattern configuration; enable/confirm Low Risk; save and reload.

**Expected:** Tenant Owner can enable the Pattern; assignment persists; Space Owner/Designer/User cannot change tenant Pattern enablement, including through direct operation where testable.

## MTD-GOV-002 — Verify tenant controls permitted agent capabilities/types
**Scenarios:** GOV-TEN-006, BLD-CFG-003, BLD-CFG-004  
**Matrix Ref:** 4.4  
**Principal Role:** Tenant Owner

**Steps:** Define/confirm permitted capability set; save; sign in as Space Designer; inspect resources offered during Agent configuration.

**Expected:** Tenant Owner controls the permitted set; lower roles cannot expand it; inherited/shared does not automatically mean enabled.

## MTD-GOV-003 — Verify Tenant Owner creates a space and assigns Space Owner
**Scenarios:** GOV-SPC-005, GOV-SPC-004  
**Matrix Ref:** 5.1, 5.2

**Steps:** If additional-space creation is enabled, create Space B, assign Space Owner and verify access.

**Expected:** Tenant Owner can create/assign; Space Owner cannot create Space. If additional Spaces are disabled for the release, record **N/A — Release Scope**.

## MTD-GOV-004 — Verify Space Owner assigns members and roles
**Scenarios:** GOV-SPC-004, GOV-SPC-009  
**Matrix Ref:** 5.5

**Steps:** Confirm candidate identities already exist as Tenant Members; Space Owner adds Space Designer and Space User to Space A and assigns roles; attempt an identity that is not a Tenant Member; save; sign in separately as each.

**Expected:** Membership/roles persist; only Space Owner receives the 5.5 action; Space assignment is constrained to existing Tenant Members.

## MTD-GOV-005 — Verify rollout tenants, default spaces and mandatory-space protection
**Scenarios:** GOV-TEN-001, GOV-TEN-002, GOV-SPC-001  
**Priority:** P0

**Steps:** Verify Training, AME, CAIO, CIB, COO, CTO, Cyber, GF, IWPB and UK; confirm each required tenant has its default Space; inspect/attempt supported removal of a mandatory default Space.

**Expected:** All required rollout tenants/default Spaces exist and mandatory default Space cannot be removed.

## MTD-GOV-006 — Verify Tenant Member read-only tenant access and Space eligibility
**Scenarios:** GOV-TEN-013, GOV-SPC-009  
**Matrix Ref:** 4.1, 5.5  
**Principal Roles:** Tenant Member, Space Owner

**Steps:** Sign in as a role-pure Tenant Member and view Tenant A configuration; attempt tenant configuration changes; as Space Owner, select that Tenant Member for Space assignment; attempt to assign a non-Tenant-Member identity.

**Expected:** Tenant Member can view tenant configuration but cannot administer it. Space Owner can assign eligible Tenant Members to a Space; direct Space assignment of an identity outside tenant membership is prevented.

## MTD-GOV-007 — Verify Space System Prompt governance hierarchy
**Scenarios:** GOV-SPC-008, GOV-TEN-011, BLD-CFG-002, RUN-004  
**Matrix Ref:** 5.3, 5.6, 6.2  
**Principal Roles:** Space Owner / Tenant Owner for Space configuration; Space Designer for Agent validation

**Steps:** Save a distinguishable Space System Prompt; reload; create/configure an Agent in the Space; verify compatible Space context applies; then introduce controlled conflicts at Space and Agent levels and execute.

**Expected:** Space System Prompt persists and applies to Agents in the Space. Governance precedence remains **Pattern > Tenant > Space > Agent**; lower-level instructions cannot override higher-level rules.

# 4. Agent Creation & Configuration

## MTD-BLD-001 — Create an agent from an enabled pattern
**Scenarios:** BLD-CRT-001, BLD-CRT-002, BLD-CRT-003  
**Matrix Ref:** 6.1  
**Principal Role:** Space Designer

**Steps:** Enter assigned Space; start Agent Builder; confirm enabled/default Pattern; create with valid minimum data.

**Expected:** Space Designer can create; Low Risk is default where required; exactly one Pattern is associated; draft belongs to current scope. Tenant Owner, Space Owner and Space User cannot perform 6.1 from those roles alone.

## MTD-BLD-005 — Create agent through assisted natural-language idea
**Scenarios:** BLD-CRT-004, BLD-CRT-005  
**Priority:** P0  
**Principal Role:** Space Designer

**Steps:** Enter Agent Builder; provide a valid natural-language agent idea; verify the builder interprets the idea and asks focused follow-up question(s); provide the requested information and continue toward draft creation.

**Expected:** Assisted creation starts from the supplied idea, collects the information required to create a usable draft, and does not silently invent or omit required setup information.

## MTD-BLD-006 — Create agent from scratch with required-field validation
**Scenarios:** BLD-CRT-006, BLD-CRT-007  
**Priority:** P0  
**Principal Role:** Space Designer

**Steps:** Start from scratch; first attempt to continue/create with required information missing; verify validation; then provide valid required name/details and create the draft.

**Expected:** Invalid/incomplete creation is prevented with usable validation; valid required data creates one new draft Agent in the assigned scope.

## MTD-BLD-007 — Cancel agent creation without side effects
**Scenario:** BLD-CRT-008  
**Priority:** P0  
**Principal Role:** Space Designer

**Steps:** Start Agent creation and enter distinguishable draft information; cancel before creation is completed; return to the applicable Agent list/recent work and search for the cancelled Agent.

**Expected:** Creation is cancelled cleanly; no unintended Agent/draft is created or exposed as a usable Agent.

## MTD-BLD-002 — Configure agent instructions within Pattern governance
**Scenarios:** BLD-CFG-002, GOV-TEN-011, SEC-RBAC-011  
**Matrix Ref:** 6.2

**Steps:** Configure valid instructions; save/reload; add a controlled instruction conflicting with higher governance and test.

**Expected:** Instructions persist but cannot override Pattern/Tenant governance. Non-Designer roles cannot edit solely because they can view.

## MTD-BLD-003 — Attach approved MCP tool / skill
**Scenarios:** BLD-CFG-003, BLD-CFG-004, GOV-TEN-010  
**Matrix Ref:** 6.4

**Steps:** Select an approved Skill and MCP/connection/tool; select the required tool where applicable; complete personal credential/access setup or choose the supported setup-later path; save/reload; test use where practical.

**Expected:** Approved resources persist. Connection/tool selection is retained; personal credentials/access are user-specific and are not carried by Pattern inheritance. A connection requiring access cannot be used until setup is complete.

## MTD-BLD-004 — Prevent unapproved MCP / skill / API use
**Scenarios:** BLD-CFG-003, BLD-CFG-004, GOV-TEN-010, SEC-RBAC-009, SEC-RBAC-010  
**Matrix Ref:** 4.4, 6.4

**Steps:** Search/select an unapproved resource; attempt direct submission/invocation where possible.

**Expected:** Unapproved resource cannot be saved/used; direct bypass is rejected; arbitrary unapproved API access is not introduced.

# 5. Same-Space Visibility & Editing

## MTD-ACC-001 — Verify permitted roles can view same-space agents
**Scenarios:** SEC-RBAC-003, SEC-RBAC-004  
**Matrix Ref:** 6.5

**Steps:** Test Tenant Owner, Space Owner, Space Designer and Space User separately against Agent A.

**Expected:** All four can view within same Space; view does not imply edit/run. Platform Admin, Engineer, Viewer/Requestor and Governance Manager do not gain 6.6 from those roles alone.

## MTD-ACC-002 — Verify only Space Designer can edit same-space agent
**Scenarios:** SEC-RBAC-003, SEC-RBAC-005, SEC-RBAC-006  
**Matrix Ref:** 6.6

**Steps:** Designer edits and saves; repeat as Tenant Owner, Space Owner and Space User; attempt direct unauthorized edit.

**Expected:** Designer succeeds; other roles/direct unauthorized requests are denied and do not alter the Agent.

# 6. Agent Runtime

## MTD-RUN-001 — Space Designer executes a same-space agent
**Scenarios:** RUN-001, RUN-002  
**Matrix Ref:** 6.7, 7.1

**Expected:** Designer opens/runs permitted Agent successfully within governance; runtime metadata appears where supported.

## MTD-RUN-002 — Space User executes a same-space agent
**Scenarios:** RUN-001, RUN-002, SEC-RBAC-004  
**Matrix Ref:** 7.1

**Expected:** Space User discovers/views/runs permitted Agent but cannot edit configuration.

## MTD-RUN-003 — Prevent Tenant Owner / Space Owner from executing agent
**Scenarios:** SEC-RBAC-005, SEC-RBAC-006  
**Matrix Ref:** 7.1

**Steps:** Attempt execution as Tenant Owner and Space Owner, including direct invocation where possible.

**Expected:** They may view under 6.6 but cannot run from those roles alone; no execution record is created from denied attempts.

## MTD-RUN-004 — Verify own execution output/history isolation
**Scenario:** RUN-007  
**Matrix Ref:** 7.2

**Steps:** User A executes and views own history; User A2 attempts to locate/access it, including direct ID where feasible.

**Expected:** User can view own outputs/history; another user cannot access protected history merely through same-Space membership.

## MTD-RUN-005 — Verify multi-turn runtime under inherited governance
**Scenarios:** RUN-003, RUN-004  
**Priority:** P0

**Steps:** Start session; submit prompt establishing known context; submit context-dependent follow-up; then a controlled governance-conflicting prompt.

**Expected:** Appropriate session context is retained; responses remain within inherited governance/permitted capabilities; conversation context cannot override higher restrictions.

# 7. Runtime Sources

## MTD-SRC-001 — Upload and use a valid personal source
**Scenarios:** SRC-001, SRC-003, E2E-007

**Steps:** Upload valid source; select it; ask a source-grounded question.

**Expected:** Upload/select/use succeeds; Agent can read source at runtime; original uploaded source is not modified.

## MTD-SRC-002 — Verify personal source is isolated from another user
**Scenario:** SRC-002

**Steps:** User A uploads source; User A2 inspects sources and attempts direct access.

**Expected:** Other user cannot see/select/read/download source; direct access denied.

## MTD-SRC-003 — Verify source selection changes runtime context
**Scenarios:** SRC-009, SRC-010, SRC-012

**Steps:** Select distinguishable A+B+C; test context; deselect B and retest; add/select D and retest.

**Expected:** Active context follows selected set and no cross-user source is introduced.

# 8. Generated Output

## MTD-GEN-001 — Generate output file
**Scenarios:** GEN-001, E2E-008

**Expected:** Valid request creates a new artifact in Generated Files associated with permitted session/user.

## MTD-GEN-002 — Retrieve and validate generated output
**Scenarios:** GEN-002, GEN-009

**Steps:** Retrieve/open artifact; validate basic structure and content against request/known source facts.

**Expected:** Authorized retrieval succeeds; file is structurally valid and materially corresponds to request.

# 9. Space / Tenant Isolation

## MTD-ISO-001 — Prevent cross-space agent visibility/access
**Scenarios:** MKT-004, SEC-RBAC-007, E2E-006

**Steps:** Space A user confirms access; Space B-only user searches, opens direct URL and attempts runtime invocation.

**Expected:** Same-Space access succeeds; cross-Space discovery/direct access/invocation denied with no data leakage. Exact Marketplace wording remains clarification.

## MTD-ISO-002 — Prevent cross-tenant agent access
**Scenarios:** MKT-004, SEC-RBAC-008

**Expected:** Tenant B-only user cannot discover/execute Tenant A restricted Agent; direct invocation denied.

# 10. Publication, Marketplace & Versioning

The updated matrix and implemented Publish screen resolve the earlier publisher ambiguity: **Space Designer publishes an Agent to the Agent Marketplace of the Space (6.8)**. Production deployment remains outside this baseline.

## MTD-PUB-001 — Unpublished draft unavailable to normal consumer
**Scenario:** PUB-001

**Expected:** Draft remains in the Designer's draft context and is not exposed through the Space Agent Marketplace. Space Designer may validate it through the debug path (6.7); Space User cannot consume it before publication.

## MTD-PUB-002 — Publish Agent version to the Space Agent Marketplace
**Scenarios:** PUB-002, PUB-003, PUB-010  
**Matrix Ref:** 6.8  
**Principal Role:** Space Designer

**Steps:** Open a valid draft; open Publish; verify version shown; enter What's New where applicable; choose Category; add Tags; publish v1; return to Agent Builder/Marketplace.

**Expected:** Space Designer can publish; a frozen version is created; publication metadata persists; the Agent becomes available through the intended Space Marketplace only after successful publication. Non-Designer roles cannot publish from their role alone.

## MTD-PUB-003 — Verify publication does not cross Space boundary
**Scenarios:** PUB-003, PUB-010, MKT-003, MKT-004  
**Matrix Ref:** 6.8, 7.1  
**Principal Roles:** Space Designer, Space User

**Steps:** Publish Agent A from Space A; verify an authorized Space A user can discover/run it; verify a Space B-only user cannot discover/open/run it, including direct access where feasible.

**Expected:** Publication is scoped to the Agent Marketplace of Space A and does not create cross-Space visibility or execution rights.

## MTD-VER-001 — Verify frozen release and V1 → draft → V2 lifecycle
**Scenarios:** PUB-009, VER-001, VER-002, VER-003, E2E-004  
**Matrix Ref:** 6.8  
**Principal Role:** Space Designer

**Steps:** Publish V1 and record identifying behaviour; edit draft without publishing; consumer executes again; publish V2; consumer executes again.

**Expected:** V1 is frozen; draft edits do not alter V1; runtime remains V1 until successful V2 publish; thereafter consumer receives V2.

## MTD-MKT-001 — Verify authorized Space Marketplace discovery after publication
**Scenarios:** MKT-001, MKT-002

**Steps:** Authorized Space User opens Agent Marketplace; Space Designer publishes Agent A; refresh/re-enter; locate/open Agent A.

**Expected:** Marketplace contains only the permitted Space set; successful publication makes Agent A discoverable in the intended Space; listing opens the correct published Agent/version.

# 11. End-to-End Regression Definitions

## MTD-E2E-001 — Governed agent build and consumption
**Scenarios:** E2E-001, E2E-002, E2E-003

**Flow:** Tenant governance → Space roles → Designer creates/configures → approved capability → unapproved capability denied → applicable publish/share → Space User discovers/runs → governance enforced.

## MTD-E2E-002 — Runtime with personal source and generated artifact
**Scenarios:** E2E-007, E2E-008

**Flow:** User opens Agent → uploads/selects source → source-grounded response → generated artifact → retrieve/open → second user cannot access first user's personal source.

# 12. Coverage Summary

| Area | Definitions |
|---|---:|
| Pattern / Tenant / Space Governance | 9 |
| Agent Build / Configuration | 7 |
| Same-Space Access / Editing | 2 |
| Runtime | 5 |
| Sources | 3 |
| Generated Files | 2 |
| Space / Tenant Isolation | 2 |
| Publication / Marketplace / Versioning | 5 |
| E2E Regression | 2 |
| **Total** | **37** |

The **37 definitions** cover the updated **60 P0 business scenarios** through reuse; the functional definitions expand into **109 explicit execution variants** in the Execution Matrix. The two E2E definitions are additionally represented by dedicated dashboard-managed regression executions, giving **111 dashboard-managed variants** for the AS20 bundle.

# 13. Execution Status Values

- **Design-ready**
- **Not Executed — Awaiting Environment**
- **Blocked — Requirement Clarification**
- **Pass / Fail**
- **Blocked — Environment**
- **Not Applicable — Release Scope**

# 14. Current Follow-Up

1. Confirm additional-Space rollout scope beyond the required default Space.
3. Confirm source extensions and 10MB boundary semantics.
4. Confirm generated-file ownership/retention.
5. Confirm multi-role effective permissions.
6. Expand P1 detailed definitions after P0 baseline review.

**End of Document**