# AS2.0 Business Scenario Catalogue — Reconciliation

**Date:** 16 Sep 2026  
**Applies to:** `Agent-Studio-2.0-Business-Scenario-Catalogue.md`

A row-by-row recount found that the v0.1 summary table is stale. The detailed scenario rows are the source of truth until the summary in the parent catalogue is replaced.

| Capability | P0 | P1 | P2 / TBD | Total |
|---|---:|---:|---:|---:|
| Foundation / Pattern & Tenant Governance | **10** | **14** | **6** | **30** |
| Agent Studio Homepage & Navigation | 0 | 3 | 3 | 6 |
| Agent Builder & Configuration | **6** | **11** | **3** | 20 |
| Publication & Versioning | **8** | **7** | 2 | **17** |
| Agent Marketplace | 4 | 6 | 4 | 14 |
| Agent Runtime / Harness | 4 | 9 | 2 | 15 |
| Runtime Sources | 3 | 10 | 2 | 15 |
| Generated Files | 2 | 7 | 1 | 10 |
| Cross-Cutting RBAC / Isolation | 7 | 5 | 2 | 14 |
| End-to-End Journeys | 8 | 3 | 1 | 12 |
| **Total** | **52** | **75** | **26** | **153** |

## Differences from the stale summary

- Foundation: 8/10/5/23 → **10/14/6/30**.
- Agent Builder: 6/10/4/20 → **6/11/3/20**.
- Publication & Versioning: 7/6/2/15 → **8/7/2/17**.
- Other capability counts are unchanged.
- Grand total: 49/69/26/144 → **52/75/26/153**.

## P0 detailed-coverage audit

The existing 25 Wave 1 definitions cover much of the highest-risk lifecycle, but the recount exposed P0 catalogue scenarios that were not explicitly represented as first-class Wave 1 definitions. These must be added to the P0 baseline rather than silently treated as P1.

Additional P0 coverage required:

| Coverage Group | P0 Scenario IDs | Required Addition |
|---|---|---|
| Pattern foundation | GOV-PAT-001, GOV-PAT-002 | Verify required Low Risk and SDLC patterns exist/are assignable |
| Pattern rules | GOV-PAT-005 | Verify shared pattern rules are present and govern adoption/runtime |
| Rollout tenant foundation | GOV-TEN-001, GOV-TEN-002 | Verify required tenants and default spaces exist |
| Connection/access boundary | GOV-TEN-010 | Explicitly trace inherited resource access requirement |
| Tenant prompt hierarchy | GOV-TEN-011 | Explicitly trace to governance test |
| Mandatory default space | GOV-SPC-001 | Verify mandatory default space protection |
| Private publication | PUB-002 | Explicit private-testing publication coverage |
| Frozen publication | PUB-009 | Verify publication creates frozen release |
| Version lifecycle | VER-001, VER-002, VER-003 | V1 remains active during draft edit; V2 only after publish |
| Marketplace baseline | MKT-001, MKT-002, MKT-003 | Authorized discovery, published visibility and private isolation |
| Multi-turn runtime | RUN-003 | Verify follow-up session context |
| Runtime governance | RUN-004 | Explicit runtime governance enforcement |
| Read-only personal source | SRC-003 | Explicit traceability to source definition |
| RBAC P0 | SEC-RBAC-001..007 | Existing functional definitions cover these; improve explicit traceability |
| E2E version/private | E2E-004, E2E-005 | Add version/private chains; E2E-006 already covered by isolation chain |

## Revised Wave 1 design target

The corrected P0 baseline should retain reusable definitions. We do **not** need 52 separate test definitions for 52 P0 scenarios. Related P0 scenarios can share one definition where they form one coherent behaviour.

Recommended revised target after reconciliation:

- Existing reusable definitions: 25.
- Additional reusable definitions: 7.
- **Reconciled P0 Manual Test Definitions: 32.**
- Existing explicit executions: 73.
- Additional explicit executions: 23.
- **Reconciled explicit execution variants: 96.**
- Smoke suite remains **10** checks; it is intentionally a compact environment sanity subset rather than full P0 coverage.

The seven added definitions are:

1. `MTD-PAT-001` — Required Patterns exist and are assignable (`GOV-PAT-001/002`).
2. `MTD-PAT-002` — Shared Pattern rules govern downstream behaviour (`GOV-PAT-005`, reinforces `GOV-TEN-011/RUN-004`).
3. `MTD-GOV-005` — Required rollout tenants/default spaces exist and mandatory default space is protected (`GOV-TEN-001/002`, `GOV-SPC-001`).
4. `MTD-PUB-003` — Private-testing publication and private visibility (`PUB-002`, `MKT-003`, `E2E-005`).
5. `MTD-VER-001` — Frozen publication and V1→draft→V2 lifecycle (`PUB-009`, `VER-001/002/003`, `E2E-004`).
6. `MTD-MKT-001` — Authorized Marketplace discovery after publication (`MKT-001/002`).
7. `MTD-RUN-005` — Multi-turn runtime under inherited governance (`RUN-003/004`).

Existing definitions are explicitly extended in traceability as follows:

- `MTD-BLD-003/004` also cover the P0 connection/access boundary `GOV-TEN-010`.
- `MTD-BLD-002` covers `GOV-TEN-011` governance hierarchy.
- `MTD-SRC-001` explicitly includes `SRC-003` read-only source behaviour.
- Existing governance/build/access/runtime/isolation definitions collectively cover `SEC-RBAC-001..007`.

**End of reconciliation.**