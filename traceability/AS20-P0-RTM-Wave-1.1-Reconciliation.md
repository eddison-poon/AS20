# AS2.0 — P0 RTM Wave 1.1 Reconciliation

**Date:** 16 Sep 2026  
**Purpose:** Supplement the original P0 RTM after the Business Scenario Catalogue recount.

| RTM ID | P0 Requirement / Scenario | Definition | Execution | Coverage |
|---|---|---|---|---|
| RTM-R01 | GOV-PAT-001 Low Risk Pattern exists | MTD-PAT-001 | EX-PAT-001 | Covered — Design Ready |
| RTM-R02 | GOV-PAT-002 SDLC Pattern exists | MTD-PAT-001 | EX-PAT-002 | Covered — Design Ready |
| RTM-R03 | GOV-PAT-005 shared Pattern rules | MTD-PAT-002 | EX-PAT-003..004 | Covered — Design Ready |
| RTM-R04 | GOV-TEN-001 rollout tenants exist | MTD-GOV-005 | EX-GOV-015 | Covered — Design Ready |
| RTM-R05 | GOV-TEN-002 default Space exists | MTD-GOV-005 | EX-GOV-016 | Covered — Design Ready |
| RTM-R06 | GOV-TEN-010 access-required resource remains unavailable until connected | MTD-BLD-003/004 | EX-BLD-009..012 | Covered — Design Ready |
| RTM-R07 | GOV-TEN-011 Tenant prompt cannot override Pattern | MTD-BLD-002 / MTD-PAT-002 | EX-BLD-005 / EX-PAT-004 | Covered — Design Ready |
| RTM-R08 | GOV-SPC-001 mandatory default Space protected | MTD-GOV-005 | EX-GOV-017 | Covered — Design Ready |
| RTM-R09 | PUB-002 private-testing publication | MTD-PUB-003 | EX-PUB-007..009 | Partial — Publish role mapping |
| RTM-R10 | PUB-009 frozen publication | MTD-VER-001 | EX-VER-001..005 | Covered functionally; publisher role TBD |
| RTM-R11 | VER-001 edit after V1 | MTD-VER-001 | EX-VER-002..003 | Covered — Design Ready |
| RTM-R12 | VER-002 publish V2 | MTD-VER-001 | EX-VER-004 | Partial — Publish role mapping |
| RTM-R13 | VER-003 runtime switches after V2 | MTD-VER-001 | EX-VER-003..005 | Covered — Design Ready |
| RTM-R14 | MKT-001 authorized Marketplace opens | MTD-MKT-001 | EX-MKT-001 | Covered — Design Ready |
| RTM-R15 | MKT-002 published agent discoverable | MTD-MKT-001 | EX-MKT-002..003 | Partial — Marketplace scope mapping |
| RTM-R16 | MKT-003 private agent not generally exposed | MTD-PUB-003 | EX-PUB-008..009 | Covered functionally; role mapping TBD |
| RTM-R17 | RUN-003 multi-turn conversation | MTD-RUN-005 | EX-RUN-011..012 | Covered — Design Ready |
| RTM-R18 | RUN-004 runtime governance | MTD-RUN-005 / MTD-PAT-002 | EX-RUN-013..014 / EX-PAT-004 | Covered — Design Ready |
| RTM-R19 | SRC-003 personal source read-only | MTD-SRC-001 | EX-SRC-001..002 | Covered — existing expected result |
| RTM-R20 | SEC-RBAC-001..007 | Existing GOV/BLD/ACC/RUN/ISO definitions | Existing role variants | Covered — reusable mapping |
| RTM-R21 | E2E-004 V1→draft→V2 | MTD-VER-001 | E2E-X04 | Covered — Design Ready |
| RTM-R22 | E2E-005 private boundary | MTD-PUB-003 | E2E-X05 | Partial — Publish role mapping |
| RTM-R23 | E2E-006 Space isolation | MTD-ISO-001 | E2E-X03 | Covered — existing chain |

## Reconciled Baseline

- Catalogue: **153 scenarios** = 52 P0 + 75 P1 + 26 P2/TBD.
- P0 definitions: **32** = 25 original + 7 reconciliation additions.
- Explicit P0 executions: **96** = 73 original + 23 reconciliation additions.
- Smoke: **10** checks, intentionally unchanged.

This addendum should be read with `AS20-P0-Requirements-Test-Traceability-Matrix.md` until the next consolidated RTM revision.

**End of Document**