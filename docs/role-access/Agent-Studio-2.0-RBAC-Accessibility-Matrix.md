# Agent Studio 2.0 — RBAC / Accessibility Matrix

**Document Status:** Draft v0.2 — Reconciled 23 Sep 2026  
**Source:** Updated Agent Hub Tenant Management — Roles & Actions diagram and Roles & Actions Matrix supplied 22 Sep 2026  
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
| Tenant Member | Tenant-level member eligible for Space assignment; read-only tenant configuration |
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

Legend: **Y = permitted**, **N = not permitted**. The current release prioritizes Tenant Owner, Tenant Member, Space Owner, Space Designer and Space User. Platform Admin, Engineer, Viewer/Requestor and Governance Manager remain reference roles and are not multiplied into P0 variants unless a critical authorization boundary requires them.

| Ref | Action | Tenant Owner | Tenant Member | Space Owner | Space Designer | Space User | AH Platform Admin | AH Engineer | Viewer / Requestor |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1.1 | Navigation (Read-Only) | N | N | N | N | N | N | N | Y |
| 1.2 | Browse Marketplace pattern catalogue | Y | Y | Y | Y | Y | Y | Y | Y |
| 1.3 | View pattern detail (Agents / MCPs / Skills, AIRCo ID) | Y | Y | Y | Y | Y | Y | Y | Y |
| 4.1 | View tenant configuration (read only) | Y | Y | Y | N | N | Y | Y | N |
| 4.2 | Change tenant configuration | Y | N | N | N | N | Y | N | N |
| 4.3 | Enable / disable Agent Patterns for tenant | Y | N | N | N | N | N | N | N |
| 4.4 | Define which agent capabilities / types can be created | Y | N | N | N | N | N | N | N |
| 4.5 | Add / remove tenant member | Y | N | N | N | N | N | N | N |
| 4.6 | Set / change token limit for tenant | Y | N | N | N | N | N | N | N |
| 4.7 | Re-assign tenant owner (orphan tenant only) | N | N | N | N | N | Y | N | N |
| 4.8 | Inactivate tenant | Y | N | N | N | N | Y | N | N |
| 4.9 | Reactivate tenant | Y | N | N | N | N | Y | N | N |
| 5.1 | Create space within tenant | Y | N | N | N | N | N | N | N |
| 5.2 | Assign / change the Space Owner | Y | N | N | N | N | N | N | N |
| 5.3 | Configure space settings (pattern subset, guardrails) | Y | N | Y | N | N | N | N | N |
| 5.4 | Set / change token limit for space | Y | N | Y | N | N | N | N | N |
| 5.5 | Add / remove members from space and assign roles (tenant members only) | N | N | Y | N | N | N | N | N |
| 5.6 | View configuration of the space | Y | N | Y | Y | Y | N | N | N |
| 5.7 | Inactivate a space | Y | N | N | N | N | N | N | N |
| 5.8 | Reactivate a space | Y | N | N | N | N | N | N | N |
| 6.1 | Create an agent from enabled pattern | N | N | N | Y | N | N | N | N |
| 6.2 | Configure agent (prompt, logic, parameters) within the pattern | N | N | N | Y | N | N | N | N |
| 6.3 | Review agent configuration request | N | N | Y | N | N | N | N | N |
| 6.4 | Attach approved MCP tools / skills to an agent | N | N | N | Y | N | N | N | N |
| 6.5 | View agents within the same space | Y | N | Y | Y | Y | N | N | N |
| 6.6 | Edit agents within the same space | N | N | N | Y | N | N | N | N |
| 6.7 | Run agents from debug window | N | N | N | Y | N | N | N | N |
| 6.8 | Publish an agent to Agent Marketplace of the space | N | N | N | Y | N | N | N | N |
| 6.9 | Create / schedule an automated workflow | N | N | N | Y | N | N | N | N |
| 6.10 | Inactivate an agent | Y | N | Y | Y | N | N | N | N |
| 6.11 | Reactivate an agent | Y | N | Y | Y | N | N | N | N |
| 7.1 | Execute / run an agent from Agent Marketplace of a space | N | N | N | Y | Y | N | N | N |
| 7.2 | View own execution outputs and history | N | N | N | Y | Y | N | N | N |

> The supplied updated screenshot does not show the Governance Manager column in full. Its earlier governance/monitoring responsibilities are retained as reference only and are not used to derive new P0 variants from this update.
---

## 5. Role-Centric Interpretation

### Tenant Owner

Key current-scope permissions include tenant administration, pattern enablement, tenant membership, space creation/assignment/configuration, viewing agents in the same space, promotion to tenant-shared, and agent/space/tenant inactivation/reactivation where specified.

Important negative assertions include that Tenant Owner **does not create/configure/edit/run an agent** under actions 6.1, 6.2, 6.7, 6.8 and 7.1.

### Tenant Member

Tenant Member is now an explicit role. It can view tenant configuration under 4.1 but does not administer the tenant, space or Agent. Space membership assignment under 5.5 selects from tenant members.

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
3. Only **Space Designer** can attach approved MCP tools/skills (6.4).
4. Only **Space Designer** can run from the Builder debug window (6.7); **Space Designer + Space User** can execute from the Space Agent Marketplace (7.1).
5. Tenant Owner and Space Owner may view same-space agents but must not gain execution rights merely because they administer the tenant/space.
6. Same-space visibility must not imply cross-space visibility.
7. Only **Space Owner** can add/remove Space members and assign roles from existing Tenant Members (5.5).
8. Only **Tenant Owner** can create spaces and assign/change the Space Owner (5.1, 5.2).
9. Tenant Owner and Space Owner can configure space settings; Space Designer/User can view configuration under 5.6 but cannot change it.
10. Only **Tenant Owner** can enable/disable patterns and define permitted agent capability/types for the tenant (4.3, 4.4).
11. Only Space Designer publishes an Agent to the Agent Marketplace of the Space (6.8).
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

## 8. Reconciliation with Updated Screens / Flow

### Resolved

- **Tenant Member** is now an explicit role and is the source population from which Space Owner assigns Space members.
- **Agent Creator = Space Designer** remains confirmed.
- **Publish is now explicit:** Space Designer publishes an Agent to the **Agent Marketplace of the Space** under action **6.8**.
- Builder debug execution is action **6.7** and belongs to Space Designer.
- Marketplace execution is action **7.1** and belongs to Space Designer + Space User.
- Space membership/role administration moved to **5.5** and belongs to Space Owner.
- Production deployment begins after the non-production testing flow and remains outside this release scope.

### Still Requiring Clarification

1. Exact effective-permission semantics for users holding multiple roles.
2. Additional-space rollout scope beyond the required default Space.
3. Exact connection/credential setup semantics for each MCP/connection.
4. Source PUBLIC/INTERNAL classification mechanism.
5. Generated-file ownership/retention.
6. Detailed Agentic Workflow 2.0 functional screens beyond action 6.9.
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