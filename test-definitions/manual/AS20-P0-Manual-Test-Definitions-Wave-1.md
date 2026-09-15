# Agent Studio 2.0 — P0 Manual Test Definitions — Wave 1

**Document Status:** Draft v0.1  
**Priority:** P0 / Release-Critical Baseline  
**Execution Status:** Design-ready / Not Executed — Awaiting Environment  
**Parent Catalogue:** `scenarios/Agent-Studio-2.0-Business-Scenario-Catalogue.md`  
**RBAC Baseline:** `docs/role-access/Agent-Studio-2.0-RBAC-Accessibility-Matrix.md`

---

## 1. Purpose

This package is the first detailed Manual Test Definition baseline for Agent Studio 2.0. It concentrates on the release-critical pre-production lifecycle currently supported by the supplied Figma designs, operating flow and official Roles & Actions Matrix.

The package deliberately does **not** expand every catalogue scenario. Wave 1 proves the highest-risk functional chain:

**Tenant/Space Governance → Space Designer Agent Creation → Agent Configuration → Same-Space Visibility → Space User Execution → Sources → Generated Output → Isolation / Negative Authorization**

Production deployment beginning with `Request deploy` is excluded from this wave.

---

## 2. Test Definition Convention

Each Test Definition contains:

- Test Definition ID.
- Business Scenario reference.
- Roles & Actions Matrix reference where applicable.
- Priority.
- Principal executing role.
- Preconditions/test data.
- Steps.
- Expected results.
- Execution variants / negative authorization coverage.

A Test Definition is reusable. Role, tenant, space, environment and test data variations should normally be captured as executions rather than duplicated definitions.

---

## 3. Common Test Data

Use the following logical data set; actual IDs/names may be substituted in the environment.

| Data | Baseline |
|---|---|
| Tenant A | Training or equivalent active use-case tenant |
| Tenant B | Second active tenant for isolation checks |
| Space A | Default Space under Tenant A |
| Space B | Second space or another independently scoped space where available |
| Pattern | Low Risk Pattern enabled for Tenant A / Space A |
| Tenant Owner | User with Tenant Owner only |
| Space Owner | User with Space Owner only |
| Space Designer A | Agent Creator assigned to Space A |
| Space User A | Consumer assigned to Space A |
| Space User B | Consumer not assigned to Space A / assigned to Space B where available |
| No-access user | User without applicable Tenant A / Space A entitlement |
| Approved Skill | Skill enabled/approved for current scope |
| Unapproved Skill | Skill not assigned/approved for current scope |
| Approved MCP/Tool | MCP/tool enabled/approved for current scope |
| Unapproved MCP/Tool | MCP/tool not assigned/approved for current scope |
| Valid Source | Supported small PDF/TXT/MD file containing known facts |
| Boundary Source | File at confirmed maximum size once environment rule is verified |
| Oversize Source | File above confirmed maximum size |
| Unsupported Source | Unsupported extension |

---

# 4. Governance & Space Baseline

## MTD-GOV-001 — Verify Low Risk Pattern is enabled for the tenant

**Scenario:** GOV-TEN-003  
**Matrix Ref:** 4.3  
**Priority:** P0  
**Principal Role:** Tenant Owner

### Preconditions

- Tenant A exists and is active.
- Tenant Owner is assigned to Tenant A.
- Low Risk Pattern exists.

### Steps

1. Sign in as Tenant Owner.
2. Open Tenant A configuration.
3. Navigate to pattern configuration/selection.
4. Locate Low Risk Pattern.
5. Enable/assign Low Risk Pattern if not already enabled.
6. Save the tenant configuration.
7. Reload/re-enter Tenant A configuration.

### Expected Results

- Tenant Owner can access the applicable tenant configuration.
- Low Risk Pattern can be enabled by Tenant Owner.
- Saved pattern assignment persists after reload.
- The pattern becomes available to the tenant according to the configured scope.
- No unrelated pattern is enabled implicitly.

### Negative Authorization

- Space Owner, Space Designer and Space User must not be able to enable/disable tenant patterns.
- If a restricted user attempts direct navigation/service invocation, the action should be rejected rather than merely hidden.

---

## MTD-GOV-002 — Verify tenant controls permitted agent capabilities/types

**Scenario:** GOV-TEN-006 / BLD-CFG-003 / BLD-CFG-004  
**Matrix Ref:** 4.4  
**Priority:** P0  
**Principal Role:** Tenant Owner

### Steps

1. Sign in as Tenant Owner.
2. Open Tenant A configuration.
3. Define/confirm the permitted agent capability/type set.
4. Save.
5. Sign in as Space Designer A.
6. Start/configure an agent in Space A.
7. Inspect the capabilities/resources offered to the creator.

### Expected Results

- Tenant Owner can define permitted capability/types.
- Space Designer sees/uses only capabilities allowed by the applicable governance/resource configuration.
- Unapproved capability must not become usable merely because it exists globally.

---

## MTD-GOV-003 — Verify Tenant Owner creates a space and assigns Space Owner

**Scenario:** GOV-SPC-005 / GOV-SPC-004  
**Matrix Ref:** 5.1, 5.2  
**Priority:** P0  
**Principal Role:** Tenant Owner

### Preconditions

- Additional-space creation is enabled in the test environment.

### Steps

1. Sign in as Tenant Owner.
2. Open Tenant A.
3. Create a new Space B.
4. Assign a Space Owner to Space B.
5. Save.
6. Sign in as the assigned Space Owner.
7. Open Space B.

### Expected Results

- Tenant Owner can create the space.
- Tenant Owner can assign/change its Space Owner.
- Assigned Space Owner can access the space according to role permissions.
- Other users do not gain membership implicitly unless required by inheritance rules.

### Scope Note

The official matrix confirms the actions exist, but earlier Figma wording around one shared default Space remains a release-scope clarification. If additional spaces are disabled for 28 Sep, record this definition as **Not Applicable — Release Scope** rather than Failed.

---

## MTD-GOV-004 — Verify Space Owner assigns members and roles

**Scenario:** GOV-SPC-004  
**Matrix Ref:** 6.3  
**Priority:** P0  
**Principal Role:** Space Owner

### Steps

1. Sign in as Space Owner for Space A.
2. Open member/role management.
3. Add Space Designer A to Space A with Space Designer role.
4. Add Space User A to Space A with Space User role.
5. Save changes.
6. Sign in separately as each assigned user.

### Expected Results

- Space Owner can add members and assign roles.
- Membership/role changes persist.
- Space Designer and Space User receive the access appropriate to their assigned roles.
- Tenant Owner, Space Designer and Space User must not gain the 6.3 action merely from their other permissions.

---

# 5. Agent Creation & Configuration

## MTD-BLD-001 — Create an agent from an enabled pattern

**Scenario:** BLD-CRT-001 / BLD-CRT-002 / BLD-CRT-003  
**Matrix Ref:** 6.1  
**Priority:** P0  
**Principal Role:** Space Designer

### Preconditions

- Space Designer A is assigned to Space A.
- Low Risk Pattern is enabled for the applicable tenant/space.

### Steps

1. Sign in as Space Designer A.
2. Enter Space A.
3. Open Agent Builder.
4. Start agent creation.
5. Confirm the enabled/default pattern behaviour.
6. Create an agent using valid minimum data.
7. Save/create the draft.

### Expected Results

- Space Designer can initiate agent creation.
- Low Risk Pattern is the default/pre-selected pattern where required by the release rule.
- Agent is associated with exactly one pattern.
- Valid input produces a draft agent.
- Agent belongs to Space A/current scope.

### Negative Authorization

Repeat the creation-entry check using Tenant Owner, Space Owner and Space User.

Expected: none of these roles can perform action 6.1 unless they also hold Space Designer through an explicitly supported multi-role model.

---

## MTD-BLD-002 — Configure agent instructions within pattern governance

**Scenario:** BLD-CFG-002 / SEC-RBAC-011  
**Matrix Ref:** 6.2  
**Priority:** P0  
**Principal Role:** Space Designer

### Steps

1. Open the draft agent as Space Designer.
2. Configure valid agent instructions.
3. Save.
4. Reload the agent.
5. Confirm instructions persist.
6. Add an instruction that conflicts with a known Pattern/Tenant rule.
7. Save and execute/test the draft where supported.

### Expected Results

- Space Designer can configure the agent.
- Valid instructions persist.
- Agent-specific instructions do not override higher-priority governance.
- Runtime behaviour remains within inherited Pattern/Tenant restrictions.

### Negative Authorization

Tenant Owner, Space Owner and Space User must not be able to edit agent configuration under 6.2/6.7 solely because they can view the agent.

---

## MTD-BLD-003 — Attach approved MCP tool / skill to an agent

**Scenario:** BLD-CFG-003 / BLD-CFG-004  
**Matrix Ref:** 6.5  
**Priority:** P0  
**Principal Role:** Space Designer

### Steps

1. Open draft agent as Space Designer.
2. Open Skills/Tools configuration.
3. Select an approved Skill.
4. Select an approved MCP/tool.
5. Save.
6. Reload the agent.
7. Test the agent using the selected capability where practical.

### Expected Results

- Approved resources are selectable.
- Selection persists.
- Agent can use the resources according to their configured access.
- No credentials are exposed through pattern inheritance.

---

## MTD-BLD-004 — Prevent use of unapproved MCP / skill

**Scenario:** BLD-CFG-003 / BLD-CFG-004 / SEC-RBAC-009 / SEC-RBAC-010  
**Matrix Ref:** 6.5 plus governance 4.4  
**Priority:** P0  
**Principal Role:** Space Designer

### Steps

1. Open draft agent as Space Designer.
2. Inspect Skills/Tools available for attachment.
3. Search for an unapproved/unassigned Skill or MCP.
4. Attempt selection if the UI exposes it.
5. Where technically possible, attempt direct service/API submission of an unapproved resource identifier.

### Expected Results

- Unapproved resource is absent, disabled or clearly unavailable.
- Agent cannot save/use an unapproved resource.
- Direct invocation must be rejected by authorization/governance controls.
- No arbitrary unapproved API access is introduced.

---

# 6. Same-Space Visibility & Editing

## MTD-ACC-001 — Verify permitted roles can view agents within the same space

**Scenario:** SEC-RBAC-003 / SEC-RBAC-004  
**Matrix Ref:** 6.6  
**Priority:** P0  
**Principal Roles:** Tenant Owner, Space Owner, Space Designer, Space User

### Preconditions

- Agent A exists in Space A.
- Each test user has legitimate Space A scope where required.

### Steps

1. Sign in as each role separately.
2. Navigate to the applicable agent listing/marketplace/view.
3. Locate Agent A.
4. Open its permitted view.

### Expected Results

- All four roles listed as Yes for 6.6 can view agents within the same space.
- View permission does not automatically provide edit or execute permission.
- AH Platform Admin, AH Engineer, Viewer/Requestor and Governance Manager do not receive 6.6 access from those roles alone.

---

## MTD-ACC-002 — Verify only Space Designer can edit same-space agent

**Scenario:** SEC-RBAC-003 / SEC-RBAC-005 / SEC-RBAC-006  
**Matrix Ref:** 6.7  
**Priority:** P0  
**Principal Role:** Space Designer

### Steps

1. Open Agent A as Space Designer.
2. Modify an editable configuration value and save.
3. Confirm persistence.
4. Repeat edit attempt as Tenant Owner.
5. Repeat as Space Owner.
6. Repeat as Space User.
7. Attempt direct edit endpoint/request for at least one unauthorized role where possible.

### Expected Results

- Space Designer can edit and save.
- Tenant Owner, Space Owner and Space User cannot edit under the supplied role matrix.
- Unauthorized direct request is rejected.
- Unauthorized attempts do not alter the agent.

---

# 7. Agent Runtime

## MTD-RUN-001 — Space Designer executes a same-space agent

**Scenario:** RUN-001 / RUN-002  
**Matrix Ref:** 6.8, 7.1  
**Priority:** P0  
**Principal Role:** Space Designer

### Steps

1. Sign in as Space Designer A.
2. Open a runnable Agent A in Space A.
3. Start a new session.
4. Submit a valid prompt.
5. Wait for completion.

### Expected Results

- Agent opens successfully.
- Prompt is accepted.
- Agent executes.
- Response is displayed.
- Execution remains within permitted agent capabilities/governance.
- Execution metadata is displayed where supported.

---

## MTD-RUN-002 — Space User executes a same-space agent

**Scenario:** RUN-001 / RUN-002 / SEC-RBAC-004  
**Matrix Ref:** 6.8, 7.1  
**Priority:** P0  
**Principal Role:** Space User

### Steps

1. Sign in as Space User A.
2. Locate/open Agent A within Space A through the permitted discovery path.
3. Start a session.
4. Submit a valid prompt.
5. Wait for completion.

### Expected Results

- Space User can discover/view the same-space agent as permitted.
- Space User can execute it.
- Space User cannot edit the agent configuration.
- Successful response is returned.

---

## MTD-RUN-003 — Prevent Tenant Owner / Space Owner from executing agent

**Scenario:** SEC-RBAC-005 / SEC-RBAC-006  
**Matrix Ref:** 6.8, 7.1  
**Priority:** P0  
**Principal Negative Roles:** Tenant Owner, Space Owner

### Steps

1. Sign in as Tenant Owner with visibility to Agent A.
2. Open/view Agent A.
3. Attempt to run/execute the agent.
4. Repeat as Space Owner.
5. Where possible, attempt direct runtime/service invocation.

### Expected Results

- Both roles may view Agent A under 6.6 when within same space.
- Neither role can execute Agent A under 6.8/7.1 unless separately granted Space Designer/User through a supported multi-role model.
- UI prevents execution appropriately.
- Direct invocation is rejected.
- No execution record is created from denied attempts.

---

## MTD-RUN-004 — Verify own execution output/history isolation

**Scenario:** RUN-007 / SEC-RBAC-004  
**Matrix Ref:** 7.2  
**Priority:** P0  
**Principal Roles:** Space Designer, Space User

### Steps

1. Execute Agent A as Space User A and record the execution/session.
2. Open own execution outputs/history as Space User A.
3. Confirm the execution is present.
4. Sign in as another Space User in the same space.
5. Attempt to locate/access Space User A's execution output/history.
6. Repeat equivalent check between Space Designer and Space User where relevant.

### Expected Results

- User can view their own execution outputs/history.
- Another user cannot access private execution history merely because they share the space.
- Direct URL/identifier access to another user's protected execution is rejected where applicable.

---

# 8. Runtime Sources

## MTD-SRC-001 — Upload and use a valid personal source

**Scenario:** SRC-001 / E2E-007  
**Priority:** P0  
**Principal Role:** Space User or Space Designer

### Steps

1. Open Agent A runtime.
2. Select Add Source.
3. Upload Valid Source containing known test facts.
4. Confirm upload succeeds.
5. Select the uploaded source.
6. Ask a question whose answer is contained in the source.

### Expected Results

- Supported source uploads successfully.
- Source appears in the user's source list.
- Source can be selected.
- Agent execution can use the selected source as runtime context.
- Original uploaded file is not modified by the agent.

---

## MTD-SRC-002 — Verify personal source is isolated from another user

**Scenario:** SRC-002  
**Priority:** P0  
**Principal Roles:** Space User A and second user

### Steps

1. Upload Personal Source as Space User A.
2. Confirm it appears for Space User A.
3. Sign out.
4. Sign in as another user with access to the same agent/space.
5. Inspect available sources.
6. Attempt direct access using any known source identifier/URL where feasible.

### Expected Results

- Personal Source is not visible to the second user.
- Second user cannot select/read/download the source.
- Direct access is denied.

---

## MTD-SRC-003 — Verify source selection changes runtime context

**Scenario:** SRC-009 / SRC-010 / SRC-012  
**Priority:** P0  
**Principal Role:** Space User or Space Designer

### Test Data

Use sources A, B and C containing distinguishable known facts.

### Steps

1. Add/select Sources A + B + C.
2. Ask a prompt requiring information from all selected sources.
3. Deselect Source B.
4. Submit a controlled follow-up/new-session prompt designed to test whether B remains active context.
5. Add/select Source D if available and repeat.

### Expected Results

- Selected sources participate in the active runtime context according to product behaviour.
- Deselected source is no longer treated as selected source context.
- Source-selection UI state matches the execution context.
- No cross-user source is introduced.

---

# 9. Generated Output

## MTD-GEN-001 — Generate an output file from an agent session

**Scenario:** GEN-001 / E2E-008  
**Priority:** P0  
**Principal Role:** Space User or Space Designer

### Steps

1. Open Agent A and start a valid session.
2. Provide/select source context where needed.
3. Ask the agent to generate a supported shareable output file.
4. Wait for completion.
5. Inspect Generated Files.

### Expected Results

- Generation request is accepted.
- Agent completes the request successfully.
- A new artifact appears in Generated Files.
- Generated artifact is associated with the current permitted session/user.
- Existing generated artifacts are not corrupted.

---

## MTD-GEN-002 — Retrieve and validate generated output file

**Scenario:** GEN-002 / GEN-009  
**Priority:** P0  
**Principal Role:** Space User or Space Designer

### Steps

1. Locate the artifact created by MTD-GEN-001.
2. Download/retrieve it.
3. Open the file using an appropriate application/viewer.
4. Check basic structure/readability.
5. Compare content against the requested task and known source facts.

### Expected Results

- Authorized user can retrieve the artifact.
- File opens successfully and is structurally valid.
- File materially corresponds to the requested output.
- Where source-grounded generation was requested, output does not contradict the controlled known source facts.

---

# 10. Space / Tenant Isolation

## MTD-ISO-001 — Prevent cross-space agent visibility/access

**Scenario:** MKT-004 / SEC-RBAC-007 / E2E-006  
**Priority:** P0  
**Principal Roles:** Space User A / Space User B

### Preconditions

- Agent A belongs to Space A.
- Space User A is authorized for Space A.
- Space User B is not authorized for Space A.

### Steps

1. Sign in as Space User A and confirm Agent A is visible/usable.
2. Sign out and sign in as Space User B.
3. Search/browse for Agent A.
4. Attempt direct navigation to Agent A using known identifier/URL where feasible.
5. Attempt runtime invocation where technically possible.

### Expected Results

- Space User A can access Agent A.
- Space User B cannot discover Agent A through normal same-space discovery.
- Direct access/invocation by Space User B is rejected.
- No Agent A data/configuration/session information is leaked.

### Clarification

The official matrix says `View agents within the same space`; this strongly supports space isolation. The exact relationship to Figma's tenant marketplace wording remains open and should be confirmed before marketplace-publication expected results are frozen.

---

## MTD-ISO-002 — Prevent cross-tenant agent access

**Scenario:** MKT-004 / SEC-RBAC-008  
**Priority:** P0  
**Principal Roles:** Tenant A user / Tenant B user

### Steps

1. Confirm Agent A is available to an authorized Tenant A / Space A consumer.
2. Sign in as a user scoped only to Tenant B.
3. Search/browse for Agent A.
4. Attempt direct access/invocation where feasible.

### Expected Results

- Tenant B-only user cannot discover or execute Tenant A's restricted agent.
- Direct invocation is rejected.
- Tenant/agent metadata is not improperly exposed.

---

# 11. Publication / Marketplace — Controlled Placeholder Definitions

The Figma flow clearly includes **Publish → Private Testing / Marketplace Testing**, but the official Roles & Actions Matrix does not yet provide an exact equivalent pre-production publish action. Matrix 6.9 states **Tenant Owner: Promote an agent to tenant-shared**.

For this reason, publication is retained as P0 functional coverage but role ownership is not frozen until product clarification.

## MTD-PUB-001 — Unpublished draft is unavailable to normal consumer

**Scenario:** PUB-001  
**Priority:** P0  
**Role:** Space Designer creates draft; Space User validates consumer visibility

### Steps

1. Space Designer creates/configures Agent A but does not perform Publish/Promote action.
2. Sign in as Space User A.
3. Search the normal consumer discovery path for Agent A.
4. Attempt direct consumer runtime access if an identifier is known.

### Expected Results

- Draft is not exposed as a generally consumable marketplace/shared agent.
- Direct consumer invocation of an unpublished/non-shared draft is rejected unless the product explicitly supports a separate authorized testing path.

---

## MTD-PUB-002 — Publish/promote agent to permitted consumer scope

**Scenario:** PUB-003 / PUB-010  
**Matrix Ref:** Candidate mapping 6.9  
**Priority:** P0  
**Role:** **TBD pending clarification**

### Expected Functional Outcome

- A valid approved agent/version can transition from creator-only/testing state to the intended shared/marketplace state.
- Consumer visibility changes only after the successful transition.
- Visibility is limited to the intended space/tenant scope.
- Published/shared runtime uses the intended frozen version.

### Execution Status

**Blocked for role-specific expected result — clarification required.**

Do not fail the product solely because the Figma Publish control and matrix 6.9 terminology differ; first establish the intended mapping.

---

# 12. Wave 1 End-to-End Regression Definitions

## MTD-E2E-001 — Governed agent build and consumption

**Scenario:** E2E-001 / E2E-002 / E2E-003  
**Priority:** P0

### Flow

1. Tenant Owner enables Low Risk Pattern / permitted capabilities.
2. Tenant Owner creates/validates required space and Space Owner assignment.
3. Space Owner assigns Space Designer and Space User.
4. Space Designer creates Agent A from enabled pattern.
5. Space Designer configures instructions and approved tools/skills.
6. Validate unauthorized resources cannot be attached.
7. Complete applicable publish/share transition when clarified.
8. Space User discovers/views Agent A within permitted scope.
9. Space User executes Agent A.
10. Confirm successful response and governance enforcement.

### Expected Result

The complete governed lifecycle succeeds with each action performed only by an authorized role and with no scope leakage.

---

## MTD-E2E-002 — Agent runtime with personal source and generated artifact

**Scenario:** E2E-007 / E2E-008  
**Priority:** P0

### Flow

1. Space User opens permitted Agent A.
2. Upload a valid personal source.
3. Select the source.
4. Ask a source-grounded question.
5. Validate response against known source facts.
6. Request a shareable output file.
7. Retrieve/open the generated artifact.
8. Sign in as a second user and verify the first user's personal source is not exposed.

### Expected Result

Source upload, source-aware execution, output generation and user privacy operate correctly through one complete runtime journey.

---

# 13. Wave 1 Coverage Summary

| Area | Test Definitions |
|---|---:|
| Governance / Space | 4 |
| Agent Build / Configuration | 4 |
| Same-Space Access / Editing | 2 |
| Runtime | 4 |
| Sources | 3 |
| Generated Files | 2 |
| Space / Tenant Isolation | 2 |
| Publication Placeholders | 2 |
| E2E Regression | 2 |
| **Total** | **25** |

These 25 definitions intentionally cover substantially more than 25 executions because authorization and scope variants are attached to reusable definitions.

---

# 14. Execution Status Values

Use:

- **Design-ready** — definition can be reviewed now.
- **Not Executed — Awaiting Environment** — expected default before AS2.0 environment is ready.
- **Blocked — Requirement Clarification** — expected result cannot yet be frozen.
- **Pass**.
- **Fail**.
- **Blocked — Environment**.
- **Not Applicable — Release Scope**.

---

# 15. Immediate Follow-Up

After Wave 1 review:

1. Resolve Publish/Promote/Marketplace role mapping.
2. Confirm whether additional spaces are enabled for the 28 Sep release.
3. Confirm exact source file extensions and 10MB boundary semantics.
4. Expand P1 definitions for field validation, sessions, marketplace search/filter, version metadata and controlled failures.
5. Build an execution sheet/matrix that maps the 25 reusable definitions to actual role + tenant + space combinations.
6. Select the compact smoke subset for each deployment/build.

---

**End of Document**