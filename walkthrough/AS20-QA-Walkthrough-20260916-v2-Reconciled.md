# Agent Studio 2.0 — QA Test Approach Walkthrough — Reconciled v2

**Date:** 16 Sep 2026  
**Target duration:** 5–10 minutes  
**Status:** Design baseline — environment execution pending

## 1. Opening

We are applying shift-left testing. The environment is still being built, so QA design started from the Day 1 operating flow, engineering/release rules, Figma and the official Roles & Actions Matrix.

We are testing Agent Studio as a governed lifecycle, not a collection of screens:

**Tenant / Space Governance → Agent Build & Configuration → Publication / Visibility → Marketplace → Runtime → Sources → Generated Output**

RBAC and Tenant/Space isolation apply across the lifecycle.

## 2. Test Structure

**Requirement / Rule → Business Scenario → Manual Test Definition → Execution Variant → Evidence / Defect**

### Reconciled baseline

| Layer | Current Position |
|---|---:|
| Business Scenario Catalogue | **153 planning scenarios** |
| P0 Business Scenarios | **52** |
| P1 Business Scenarios | **75** |
| P2 / TBD Business Scenarios | **26** |
| P0 Manual Test Definitions | **32 reusable definitions** |
| P0 Explicit Execution Variants | **96 planned executions** |
| Initial Smoke Baseline | **10 executions** |

The catalogue count was reconciled row-by-row on 16 Sep. The previous 144/49-P0 summary was stale.

The key design principle remains: **52 P0 scenarios do not require 52 separate test definitions.** Related business scenarios can be covered by one reusable definition, while role/scope combinations become execution variants.

Example:

`BLD-CRT-001 → MTD-BLD-001 → EX-BLD-001..004`

Space Designer is expected to create an agent; Tenant Owner, Space Owner and Space User are negative authorization variants.

## 3. Role Model

**Tenant Owner** controls Tenant governance and Space creation/assignment but does not automatically create/run agents.

**Space Owner** controls Space configuration/membership but does not automatically create/edit/run agents.

**Space Designer (Agent Creator)** creates/configures agents, attaches approved capabilities, edits and runs/tests agents.

**Space User** consumes permitted same-Space agents and views own execution outputs/history.

Administrative visibility does not automatically imply runtime permission.

## 4. P0 Golden Journey

Tenant Owner enables required governance → Space Owner establishes membership → Space Designer creates/configures Agent → approved capabilities only → publish/share transition → Space User discovers permitted Agent → runs Agent → uploads/selects source → receives source-aware response → generates/retrieves output.

The P0 suite also verifies required Patterns/tenants/default Spaces, frozen version behaviour, Marketplace discovery, multi-turn runtime and negative authorization/isolation.

## 5. Positive and Negative Authorization

For high-risk actions we test both ALLOW and DENY. A hidden button alone is not sufficient proof of authorization; where the product exposes an appropriate service path, denied operations should also be proven not to occur.

Example Run Agent expectation:

| Role | Expected |
|---|---|
| Space Designer | ALLOW |
| Space User | ALLOW |
| Tenant Owner | DENY |
| Space Owner | DENY |

## 6. Isolation

A Space A consumer can use Space A Agent A. A Space B-only consumer must not discover or execute Agent A. Equivalent isolation is checked across Tenant boundaries and protected runtime objects such as personal sources/history.

## 7. Publication and Versioning

P0 now explicitly covers the frozen version lifecycle:

**Publish V1 → consumer runs V1 → edit draft → consumer still runs V1 → publish V2 → consumer runs V2.**

Private Testing is also explicitly covered: the intended private user can access the private version while a normal Marketplace consumer cannot discover it.

The remaining requirement clarification is **who owns each Publish transition** and how Figma Private/Marketplace Testing maps to RAM 6.9 `Promote agent to tenant-shared`.

## 8. Runtime

Runtime validation includes normal execution, multi-turn context, inherited governance, personal sources, source selection, generated artifacts, own-history/privacy checks and execution metadata where supported.

A successful answer alone is not sufficient. We validate the complete **prompt → governed execution → source context → response → generated output** chain.

## 9. Traceability

Every P0 scenario is now either directly mapped to a reusable definition/execution, mapped through an E2E chain, or explicitly identified as partial/blocked where the product requirement is not frozen.

The 16 Sep reconciliation added seven definitions for previously underrepresented P0 areas: required Patterns, Pattern rules, rollout tenant/default-Space foundation, Private Testing, frozen version lifecycle, Marketplace discovery and multi-turn governed runtime.

## 10. Smoke When Environment Arrives

The initial smoke remains intentionally compact at **10 checks**. It validates basic environment health: Tenant governance, Space role administration, Agent creation, approved capability attachment, consumer visibility/runtime, negative Tenant Owner runtime, source upload, generated artifact and cross-Space isolation.

After smoke passes, execute the wider **96-variant P0 baseline**. Publication/version variants that depend on unresolved role mapping can be recorded as Blocked — Requirement Clarification rather than failed.

## 11. Known Clarifications

Primary open items remain Publish/Marketplace role and scope mapping, additional-Space release inclusion, source classification/boundary semantics, generated-file ownership/retention and multi-role effective permissions.

Production deployment beginning from **Request deploy** remains outside the current scope.

## 12. Suggested Closing

> We are not treating Agent Studio as a set of screens. We are testing a governed Agent lifecycle. The catalogue now contains 153 business scenarios, of which 52 are P0. Those P0 scenarios are implemented through 32 reusable definitions and 96 role/scope execution variants, rather than duplicating a test case for every scenario and role. A 10-check smoke suite is ready for the first usable environment, and unresolved product decisions are tracked as clarifications instead of being converted into assumptions.

## 13. Two-Minute Version

**Shift-left:** design started before the environment using Figma, engineering flow and the official role matrix.

**Coverage:** **153 scenarios → 52 P0 scenarios → 32 reusable P0 definitions → 96 P0 executions → 10 smoke checks.**

**Golden lifecycle:** Governance → Build → Publish/Visibility → Marketplace → Runtime → Sources → Generated Output, with RBAC/isolation throughout.

**Readiness:** tests are design-ready; environment execution can begin with smoke and then expand into the P0 matrix. Publish/Marketplace mapping remains explicitly tracked rather than assumed.

**End of Walkthrough**