# Agent Studio 2.0 — RBAC / Accessibility Matrix

**Document Status:** Draft v0.1  
**Source:** Agent Hub Tenant Management — Roles & Actions diagram and Roles & Actions Matrix supplied 15 Sep 2026  
**Current Test Scope:** Pre-production-deployment flow. Production deployment actions are excluded from the current detailed test-definition wave.

---

## 1. Purpose

This document converts the supplied Roles & Actions Matrix into a testable authorization baseline for Agent Studio 2.0.

The matrix should be used with the Business Scenario Catalogue to derive positive and negative Manual Test Definitions.

Authorization validation must cover both UI behaviour and, where technically possible, server-side/service authorization. A hidden button alone is not sufficient evidence that access is protected.

---

## 2. Official Roles

| Role | Working Description |
|---|---|
| Tenant Owner | Project / tenant administrator |
| Space Owner | Workspace administrator |
| Space Designer (Agent Creator) | Agent builder / creator |
| Space User | Agent consumer |
| AH Platform Admin | Platform control / administration |
| AH Engineer | Fulfilment and operations |
| Viewer / Requestor | Read/request-oriented role |
| Governance Manager (Platform) | Platform governance role |

**Terminology resolution:** The supplied matrix explicitly labels **Space Designer (Agent Creator)**. For current testing, `Agent Creator` should therefore map to the official **Space Designer** role unless a later requirement states otherwise.

---

## 3. Current Scope Boundary

Primary AS2.0 functional/RBAC coverage for the current wave:

- 1.x Platform access & navigation — relevant read/browse behaviour.
- 4.x Tenant configuration.
- 5.x Space management.
- 6.x Agent build & configuration.
- 7.x Agent execution/testing in non-production.

Not included in the current detailed test-definition wave:

- 2.x Tenant onboarding request.
- 3.x Request review & fulfilment.
- Production deployment 8.x.
- Token/cost management, monitoring/audit and support except where later requested as AS2.0 functional scope.

The excluded actions remain useful as reference but should not distract from the current Agent Studio lifecycle.

---

## 4. Testable Permission Matrix — Relevant Actions

Legend: **Y = permitted**, **N = not permitted**.

| Ref | Action | Tenant Owner | Space Owner | Space Designer | Space User | AH Platform Admin | AH Engineer | Viewer / Requestor | Governance Manager |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1.1 | Navigation (Read-Only) | N | N | N | N | N | N | Y | N |
| 1.2 | Browse Marketplace pattern catalogue | Y | Y | Y | Y | Y | Y | Y | Y |
| 1.3 | View pattern detail (Agents / MCPs / Skills, AIRCo ID) | Y | Y | Y | Y | Y | Y | Y | Y |
| 4.1 | View tenant configuration (read only) | Y | Y | N | N | Y | Y | N | Y |
| 4.2 | Change tenant configuration | Y | N | N | N | Y | N | N | N |
| 4.3 | Enable / disable Agent Patterns for tenant | Y | N | N | N | N | N | N | N |
| 4.4 | Define which agent capabilities / types can be created | Y | N | N | N | N | N | N | N |
| 4.5 | Add / remove tenant member | Y | N | N | N | N | N | N | N |
| 4.6 | Adjust token limit (tenant) | Y | N | N | N | N | N | N | N |
| 4.7 | Re-assign project admin for orphan tenant | N | N | N | N | Y | N | N | N |
| 4.8 | Inactivate tenant | Y | N | N | N | Y | N | N | N |
| 4.9 | Reactivate tenant | Y | N | N | N | Y | N | N | N |
| 5.1 | Create space within tenant | Y | N | N | N | N | N | N | N |
| 5.2 | Assign / change Space Admin (Space Owner) | Y | N | N | N | N | N | N | N |
| 5.3 | Configure space settings (pattern subset, guardrails) | Y | Y | N | N | N | N | N | N |
| 5.4 | Set / change space token limit | Y | Y | N | N | N | N | N | N |
| 5.5 | View configuration of space | Y | Y | Y | Y | N | N | N | N |
| 5.6 | Inactivate a space | Y | N | N | N | N | N | N | N |
| 5.7 | Reactivate a space | Y | N | N | N | N | N | N | N |
| 6.1 | Create an agent from enabled pattern | N | N | Y | N | N | N | N | N |
| 6.2 | Configure agent (prompt, logic, parameters) within pattern | N | N | Y | N | N | N | N | N |
| 6.3 | Add members to space and assign roles | N | Y | N | N | N | N | N | N |
| 6.4 | Review agent configuration request | N | Y | N | N | N | N | N | N |
| 6.5 | Attach approved MCP tools / skills to an agent | N | N | Y | N | N | N | N | N |
| 6.6 | View agents within the same space | Y | Y | Y | Y | N | N | N | N |
| 6.7 | Edit agents within the same space | N | N | Y | N | N | N | N | N |
| 6.8 | Run agents within the same space | N | N | Y | Y | N | N | N | N |
| 6.9 | Promote an agent to tenant-shared | Y | N | N | N | N | N | N | N |
| 6.10 | Create / schedule an automated workflow | N | Y | Y | N | N | N | N | N |
| 6.11 | Inactivate an agent | Y | Y | Y | N | N | N | N | N |
| 6.12 | Reactivate an agent | Y | Y | Y | N | N | N | N | N |
| 7.1 | Execute / run an agent | N | N | Y | Y | N | N | N | N |
| 7.2 | View own execution outputs and history | N | N | Y | Y | N | N | N | N |

---

## 5. Role-Centric Interpretation

### Tenant Owner

Key current-scope permissions include tenant administration, pattern enablement, tenant membership, space creation/assignment/configuration, viewing agents in the same space, promotion to tenant-shared, and agent/space/tenant inactivation/reactivation where specified.

Important negative assertions include that Tenant Owner **does not create/configure/edit/run an agent** under actions 6.1, 6.2, 6.7, 6.8 and 7.1.

### Space Owner

Key permissions include space configuration, member/role assignment, reviewing agent configuration requests, viewing same-space agents, automated workflow creation/scheduling, and agent inactivation/reactivation.

Important negative assertions include that Space Owner **does not create/configure/edit/run an agent** under 6.1, 6.2, 6.7, 6.8 and 7.1.

### Space Designer (Agent Creator)

This is the principal agent-building role. It can create, configure, attach approved tools/skills, view/edit/run same-space agents, create/schedule automated workflows, inactivate/reactivate agents, execute agents and view its own execution outputs/history.

It cannot perform tenant or space administration unless another role is also assigned.

### Space User

This is the principal agent-consumer role. It can view same-space configuration/agents, run same-space agents, execute agents and view its own execution outputs/history.

It cannot create/configure/edit agents or administer tenant/space membership.

### AH Platform Admin

Within the current functional areas it has selected tenant-level administrative capabilities, including tenant view/change, orphan-admin reassignment and tenant inactivation/reactivation. It is not an agent creator or runtime consumer under the supplied matrix.

### AH Engineer

Within the current AS2.0 build/runtime scope it has limited direct access. Its main responsibilities are in provisioning/operations and later deployment activities.

### Viewer / Requestor

Primarily onboarding/request-oriented. It can browse the pattern catalogue and pattern details but has no current tenant/space/agent build/runtime permissions in sections 4–7.

### Governance Manager (Platform)

Can browse/view pattern information and has selected governance/monitoring responsibilities outside the current detailed build/runtime scope. It is not an agent builder/consumer under sections 4–7.

---

## 6. High-Risk Authorization Assertions

The following should be treated as P0/P1 RBAC controls when detailed Test Definitions are produced:

1. Only **Space Designer** can create an agent from an enabled pattern (6.1).
2. Only **Space Designer** can configure/edit an agent (6.2, 6.7).
3. Only **Space Designer** can attach approved MCP tools/skills (6.5).
4. Only **Space Designer + Space User** can run/execute agents (6.8, 7.1).
5. Tenant Owner and Space Owner may view same-space agents but must not gain execution rights merely because they administer the tenant/space.
6. Same-space visibility must not imply cross-space visibility.
7. Only **Space Owner** can add members to a space and assign roles (6.3).
8. Only **Tenant Owner** can create spaces and assign/change the Space Owner (5.1, 5.2).
9. Tenant Owner and Space Owner can configure space settings, but Space Designer/User are read-only for space configuration (5.3 vs 5.5).
10. Only **Tenant Owner** can enable/disable patterns and define permitted agent capability/types for the tenant (4.3, 4.4).
11. Tenant Owner can promote an agent to tenant-shared; Space Designer cannot self-promote (6.9).
12. Runtime history access under 7.2 is explicitly **own execution outputs and history** and should be tested for cross-user isolation.

---

## 7. Execution Design Rule

Detailed tests should avoid multiplying every functional case by all eight roles.

Use two complementary patterns:

### Functional Test Definition

Valid business action using the principal authorized role.

Example:

`Create agent from enabled pattern — Space Designer — expected Allow`.

### Authorization Test Definition / Execution Matrix

For high-risk actions, execute representative unauthorized roles according to the supplied matrix.

Example:

| Action | Positive Role | Representative Negative Roles |
|---|---|---|
| 6.1 Create agent | Space Designer | Tenant Owner, Space Owner, Space User |
| 6.3 Assign space roles | Space Owner | Tenant Owner, Space Designer, Space User |
| 6.7 Edit agent | Space Designer | Tenant Owner, Space Owner, Space User |
| 7.1 Execute agent | Space Designer, Space User | Tenant Owner, Space Owner |

Where service/API access is available, at least one negative execution should attempt direct invocation rather than relying solely on hidden UI.

---

## 8. Important Reconciliation with Earlier Figma / Flow Assumptions

### Resolved

- **Agent Creator = Space Designer** is now explicitly supported by the official matrix.
- Space User is an agent consumer and can execute agents.
- Tenant Owner and Space Owner are administrators but are not automatically agent runners.

### Still Requiring Clarification

1. Figma/operating-flow language previously implied Agent Creator could publish to the marketplace. The supplied current matrix does not expose a pre-production `Publish to Marketplace` action; 6.9 instead says Tenant Owner can `Promote an agent to tenant-shared`. The exact mapping between Figma Publish/Private/Marketplace and matrix action 6.9 must be clarified.
2. Engineering/Figma space-specific marketplace visibility must still be reconciled with wording that says tenant marketplace/tenant-shared.
3. Additional-space scope remains subject to the earlier design discrepancy, although action 5.1 now explicitly confirms Tenant Owner has a `Create space within the tenant` action in the broader role model.
4. `Review agent configuration request` (6.4) should be mapped to the exact UI/state transition once available.
5. Automated workflow 6.10 is present but detailed Agentic Workflow 2.0 screens/requirements are still needed for comprehensive functional definitions.

---

## 9. Traceability Convention

Every detailed authorization test should record:

- Roles & Actions reference, e.g. `6.1`.
- Business Scenario ID, e.g. `BLD-CRT-001`.
- Test Definition ID.
- Executing role.
- Tenant.
- Space.
- Expected UI state.
- Expected action result: Allow / Deny.
- Expected data scope.
- Expected service result where observable.
- Evidence.

---

**End of Document**