# Agent Studio 2.0 — P0 Manual Test Definitions — Wave 1.1 Reconciliation

**Status:** Draft / Design-ready  
**Purpose:** Add the P0 definitions exposed by the 16 Sep catalogue recount. This document supplements Wave 1; together they form the reconciled **32-definition P0 baseline**.

## MTD-PAT-001 — Verify required Patterns exist and are assignable

**Scenarios:** GOV-PAT-001, GOV-PAT-002  
**Priority:** P0

**Steps:** Open the applicable Pattern catalogue/administration view; locate Low Risk and SDLC; inspect identity/status; verify each is available for intended assignment/adoption.

**Expected:** Low Risk and SDLC exist as distinct Patterns and are available according to release configuration. Missing required Pattern is release-blocking. Exact SDLC resources may remain a data clarification without invalidating Pattern existence.

## MTD-PAT-002 — Verify shared Pattern rules govern downstream behaviour

**Scenarios:** GOV-PAT-005, GOV-TEN-011, RUN-004  
**Priority:** P0

**Steps:** Establish a known Pattern rule; confirm it is inherited by adopting tenant; add a compatible tenant/agent instruction and execute; then configure a lower-level instruction that conflicts with the Pattern rule and execute a controlled prompt.

**Expected:** Shared Pattern rules persist and apply. Compatible lower-level instructions work. Conflicting tenant/agent instructions cannot override higher Pattern governance.

## MTD-GOV-005 — Verify rollout tenants, default spaces and mandatory-space protection

**Scenarios:** GOV-TEN-001, GOV-TEN-002, GOV-SPC-001  
**Priority:** P0

**Steps:** Verify Training, AME, CAIO, CIB, COO, CTO, Cyber, GF, IWPB and UK tenant records; confirm each required tenant has its default Space; for a controlled tenant inspect/attempt the supported remove/delete action for the mandatory default Space.

**Expected:** All required rollout tenants exist; each has its required default Space; a mandatory default Space cannot be removed. If deletion control is not exposed, confirm protection through the available administration/service behaviour.

## MTD-PUB-003 — Verify Private Testing publication and visibility

**Scenarios:** PUB-002, MKT-003, E2E-005  
**Priority:** P0  
**Role:** Pending final Publish-role mapping

**Steps:** Create/configure Agent A; publish a frozen version using Private Testing; verify the authorized private path; sign in as normal Marketplace consumer and search/browse for Agent A; attempt normal consumer access.

**Expected:** A frozen private version is created; it is available only through the intended private-testing scope; it is not exposed as a general Marketplace agent. Role-specific execution remains blocked until Publish ownership is confirmed.

## MTD-VER-001 — Verify frozen release and V1 → draft → V2 lifecycle

**Scenarios:** PUB-009, VER-001, VER-002, VER-003, E2E-004  
**Priority:** P0

**Steps:** Publish Agent A as V1; execute as authorized consumer and record a V1-identifying behaviour; edit the draft without publishing; execute again as consumer; publish the changed draft as V2; execute again.

**Expected:** Publication creates a frozen release. Draft edits do not silently alter V1. Before V2 publish, Marketplace/runtime continues using V1. Successful V2 publish creates a new frozen version and subsequent consumer runtime uses V2.

## MTD-MKT-001 — Verify authorized Marketplace discovery after publication

**Scenarios:** MKT-001, MKT-002  
**Priority:** P0

**Steps:** Sign in as authorized consumer; open Marketplace; verify only permitted agents are presented; publish/share Agent A to the intended Marketplace state; refresh/re-enter Marketplace; locate Agent A and open it.

**Expected:** Authorized user can open Marketplace; successful publication makes Agent A discoverable only in intended scope; selected listing opens the correct published Agent/version. Cross-space isolation remains covered by `MTD-ISO-001`.

## MTD-RUN-005 — Verify multi-turn runtime under inherited governance

**Scenarios:** RUN-003, RUN-004  
**Priority:** P0

**Steps:** Open a permitted published Agent; start a session; submit a prompt establishing known context; submit a follow-up that relies on that context; then submit a controlled prompt that would conflict with inherited Pattern/Tenant governance if followed literally.

**Expected:** Appropriate session context is retained across turns; responses remain within inherited governance and permitted capabilities; conversation context cannot be used to override higher-level restrictions.

## Existing Definition Traceability Extensions

- `MTD-BLD-003/004` → also trace `GOV-TEN-010` because inherited/selected resources requiring access must not become usable merely through assignment.
- `MTD-BLD-002` → also trace `GOV-TEN-011`.
- `MTD-SRC-001` → also trace `SRC-003`; its expected result already states the original uploaded source is not modified.
- Existing governance/build/access/runtime definitions collectively cover `SEC-RBAC-001..006`; `MTD-ISO-001` covers `SEC-RBAC-007`.

## Reconciled Definition Count

| Package | Definitions |
|---|---:|
| Original Wave 1 | 25 |
| Wave 1.1 reconciliation additions | 7 |
| **Reconciled P0 baseline** | **32** |

**End of Document**