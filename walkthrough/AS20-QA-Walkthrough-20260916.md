# Agent Studio 2.0 — QA Test Approach Walkthrough

**Purpose:** Quick QA walkthrough for Agent Studio 2.0  
**Date:** 16 Sep 2026  
**Target duration:** 5–10 minutes  
**Status:** Design baseline — environment execution pending

---

# 1. Opening — What We Are Trying to Achieve

> We are applying a shift-left testing approach for Agent Studio 2.0. Because the test environment is still being built, we started test design from the available Figma flows, engineering rules, Day 1 operating flow, and the official Roles & Actions Matrix rather than waiting for the application to be fully available.

The objective is not simply to test individual screens.

Our testing model validates the complete governed lifecycle:

**Tenant / Space Governance**  
↓  
**Agent Creation & Configuration**  
↓  
**Access / Publication / Visibility**  
↓  
**Agent Runtime**  
↓  
**Sources & Generated Output**

At every layer we also validate **role authorization and Tenant/Space isolation**.

---

# 2. Test Basis

The current functional test design is based on four main sources:

1. **Day 1 Operating Flow** — how Pattern, Tenant, Space, Agent Creator and Space User interact.
2. **Engineering / release scope** — Phase 1a features and rules for the new Ideation environment.
3. **Figma designs** — Tenant Management, Agent Builder, Agent Marketplace and actual Agent Runtime behaviour.
4. **Official Roles & Actions Matrix** — authoritative role/action permissions used for RBAC testing.

Production deployment beginning from **Request deploy** is intentionally outside the current testing wave.

---

# 3. How We Structure the Testing

We use four layers rather than writing hundreds of independent test cases immediately.

```text
Requirement / Business Rule
          ↓
Business Scenario
          ↓
Manual Test Definition
          ↓
Execution Variant
          ↓
Evidence / Defect
```

### Current baseline

| Layer | Current Position |
|---|---:|
| Business Scenario Catalogue | 144 planning scenarios |
| P0 Manual Test Definitions | 25 reusable definitions |
| P0 Execution Variants | 73 planned executions |
| Initial Smoke Baseline | 10 executions |

The key point is that **25 Test Definitions do not mean only 25 tests**.

For example:

**Create Agent** is one functional Test Definition.

But according to the official role matrix:

| Role | Expected |
|---|---|
| Space Designer | ALLOW |
| Tenant Owner | DENY |
| Space Owner | DENY |
| Space User | DENY |

These become separate execution variants while still tracing back to one reusable functional definition.

This avoids duplicating nearly identical test cases while preserving full RBAC coverage.

---

# 4. Role Model — Important QA Interpretation

The official matrix gives us a much clearer role model.

### Tenant Owner

Controls Tenant-level governance and Space creation/assignment.

Examples:

- Enable/disable Agent Patterns.
- Define permitted agent capabilities/types.
- Create Space.
- Assign Space Owner.

But Tenant Owner does **not automatically create or run agents**.

### Space Owner

Controls the workspace and membership.

Examples:

- Configure Space.
- Add members and assign Space roles.
- Review applicable agent configuration requests.

But Space Owner does **not automatically create/edit/run agents**.

### Space Designer — Agent Creator

This is the primary Agent Builder role.

Examples:

- Create agent.
- Configure agent.
- Attach approved MCP tools/skills.
- Edit agent.
- Run/test agent.

### Space User

This is the primary Agent consumer.

Examples:

- View same-Space agents.
- Run agents.
- View own execution outputs/history.

This separation is important because administrative access does not automatically imply runtime access.

---

# 5. P0 Golden Journey

Our P0 testing is centred around one business journey rather than individual pages.

```text
Tenant Owner
    ↓
Enable Low Risk Pattern / permitted capabilities
    ↓
Tenant / Space setup
    ↓
Space Owner
    ↓
Assign Space Designer + Space User
    ↓
Space Designer
    ↓
Create Agent
    ↓
Configure instructions
    ↓
Attach approved MCP / Skills
    ↓
Publish / Share [mapping to be confirmed]
    ↓
Space User
    ↓
Discover Agent
    ↓
Run Agent
    ↓
Select / Upload Sources
    ↓
Receive source-aware response
    ↓
Generate output file
    ↓
Retrieve generated file
```

This becomes the backbone of our regression suite.

---

# 6. We Test Positive AND Negative Authorization

RBAC testing is not limited to checking whether a button is visible.

For high-risk actions we test both:

**Positive authorization** — the correct role can perform the operation.

**Negative authorization** — another role cannot perform the operation.

Example — Run Agent:

| Role | Matrix Expected Result |
|---|---|
| Space Designer | ALLOW |
| Space User | ALLOW |
| Tenant Owner | DENY |
| Space Owner | DENY |

Where technically possible, a DENY test should also attempt direct URL/service invocation.

A hidden button alone does not prove that authorization is enforced.

---

# 7. Tenant / Space Isolation Is P0

One of our most important security/business tests is isolation.

Example:

```text
Tenant A
 ├─ Space A
 │   └─ Agent A
 │
 └─ Space B
```

Expected:

**Space A User** → Agent A → ALLOW

**Space B-only User** → Agent A → DENY

We test this at multiple levels:

- Marketplace/discovery.
- Direct Agent URL.
- Runtime invocation where possible.
- Source/session/object access.

We also repeat the principle across Tenant boundaries.

---

# 8. Runtime Testing Goes Beyond “Agent Returned an Answer”

For Agent runtime, a successful response alone is not enough.

Our runtime coverage includes:

### Execution

- Correct published/permitted Agent opens.
- Prompt executes successfully.
- Multi-turn behaviour.
- Runtime remains inside inherited governance.
- Request ID / execution metadata where available.

### Sources

- Upload supported personal source.
- Select/deselect source.
- Selected sources affect runtime context.
- Personal source remains private to the owning user.
- Agent can read but must not modify the original personal source.

### Generated Files

- Agent creates requested output artifact.
- Artifact appears in Generated Files.
- Authorized user can retrieve/open it.
- Generated content corresponds to the request and controlled source facts.
- Unauthorized user must not gain access to another user's protected artifact.

This gives us a complete **prompt → source → execution → output** validation chain.

---

# 9. Traceability

Every release-critical test can be traced back to its source requirement.

Example:

```text
Roles Matrix 6.1
Create an agent from enabled pattern
        ↓
BLD-CRT-001
Business Scenario
        ↓
MTD-BLD-001
Manual Test Definition
        ↓
EX-BLD-001
Space Designer → ALLOW

EX-BLD-002
Tenant Owner → DENY

EX-BLD-003
Space Owner → DENY

EX-BLD-004
Space User → DENY
```

The RTM therefore allows us to answer:

- Which requirement are we testing?
- Which scenario covers it?
- Which test definition validates it?
- Which roles/scopes are executed?
- What evidence/defect came from the execution?

---

# 10. Initial Smoke Test When Environment Arrives

We do not intend to execute all 73 variants immediately when the environment first becomes available.

The initial smoke baseline is approximately 10 critical checks:

1. Tenant Owner can manage required Pattern governance.
2. Space Owner can manage required Space roles.
3. Space Designer can create an Agent.
4. Space Designer can attach an approved capability.
5. Space User can view the permitted same-Space Agent.
6. Space User can execute the Agent.
7. Tenant Owner cannot execute the Agent from Tenant Owner role alone.
8. Runtime source upload/use works.
9. Generated output file works.
10. Cross-Space Agent visibility is blocked.

After smoke passes, we expand into the complete P0 execution matrix.

---

# 11. Known Clarifications — Not Hidden Assumptions

There are a few design/requirement points we deliberately have **not guessed**.

### Publish / Marketplace Model

Figma currently shows:

**Publish → Private Testing / Marketplace Testing**

The official Roles & Actions Matrix separately defines:

**6.9 Tenant Owner → Promote an agent to tenant-shared**

We need confirmation of how these states/actions map together and which role owns each transition.

### Marketplace Scope

Some material describes same-Space visibility while some Figma wording refers to a Tenant Marketplace.

We currently treat Space isolation as a critical requirement but will freeze the exact Marketplace expected result after confirmation.

### Additional Spaces

The operating flow and role matrix support Space creation, while some Figma wording says one shared default Space for the initial scope.

The test is already designed and can be marked **N/A — Release Scope** if additional Space creation is disabled for this release.

Other tracked clarifications include source classification, generated-file ownership/retention and multi-role effective permissions.

---

# 12. Current QA Readiness

Even though the environment is not yet ready, QA is not waiting for Day 1 of execution.

We already have:

**Test Strategy**  
↓  
**Business Scenario Catalogue**  
↓  
**Official RBAC Accessibility Model**  
↓  
**P0 Manual Test Definitions**  
↓  
**P0 Execution Matrix**  
↓  
**Requirements Traceability Matrix**  
↓  
**Initial Smoke Baseline**

Once the environment becomes available, we can move from **Design-ready / Not Executed** into execution without redesigning the whole suite.

---

# 13. Suggested Closing

> The main principle of our approach is that we're not treating Agent Studio as a collection of screens. We're testing it as a governed Agent lifecycle. We start from Tenant and Space controls, verify who can build and configure an Agent, validate who can see and run it, and then test the actual runtime including sources and generated outputs. The role matrix is applied as execution variants, so we test both what a user is allowed to do and what they must not be able to do. Everything is traceable back to the original requirement, and unresolved product decisions are recorded as clarifications rather than being built into the test cases as assumptions.

---

# 14. If Time Is Very Short — 2 Minute Version

If the meeting only allows a very quick QA update, cover these four points:

**1. Shift-left**  
QA design started from Figma + engineering flow + official role matrix before the environment is ready.

**2. Risk-based structure**  
144 business scenarios have been identified, with the first release-critical wave reduced to 25 reusable P0 definitions and 73 role/scope execution variants.

**3. Golden lifecycle**  
Tenant/Space Governance → Agent Build → Access/Share → Space User Runtime → Sources → Generated Output, with RBAC and isolation tested throughout.

**4. Execution readiness**  
A 10-check smoke baseline is ready for the first usable environment, followed by the full P0 execution matrix. Open requirement questions such as Publish/Marketplace mapping are explicitly tracked rather than assumed.

---

**End of Walkthrough**