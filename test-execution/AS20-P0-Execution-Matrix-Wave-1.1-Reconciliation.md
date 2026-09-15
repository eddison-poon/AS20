# Agent Studio 2.0 — P0 Execution Matrix — Wave 1.1 Reconciliation

**Status:** Not Executed — Awaiting Environment  
**Purpose:** Add explicit execution variants for the seven Wave 1.1 definitions. Together with the original 73 executions, this produces a reconciled **96-execution P0 baseline**.

| Exec ID | Test Definition | User / Role | Scope / State | Expected | Key Result |
|---|---|---|---|---|---|
| EX-PAT-001 | MTD-PAT-001 | Authorized pattern viewer/admin | Platform | ALLOW | Low Risk Pattern exists and is identifiable |
| EX-PAT-002 | MTD-PAT-001 | Authorized pattern viewer/admin | Platform | ALLOW | SDLC Pattern exists and is identifiable |
| EX-PAT-003 | MTD-PAT-002 | Authorized governance setup | Pattern/Tenant | ALLOW | Pattern rule persists/inherits |
| EX-PAT-004 | MTD-PAT-002 | Space Designer runtime | Conflicting lower instruction | DENY override | Pattern rule remains effective |
| EX-GOV-015 | MTD-GOV-005 | Tenant Owner/admin view | Rollout tenants | ALLOW | All 10 required tenants exist |
| EX-GOV-016 | MTD-GOV-005 | Tenant Owner/admin view | Default Spaces | ALLOW | Required default Space exists for each tenant |
| EX-GOV-017 | MTD-GOV-005 | Tenant Owner | Mandatory default Space | DENY removal | Required default Space protected |
| EX-PUB-007 | MTD-PUB-003 | Applicable publisher | Agent A draft → Private Testing | TBD role | Frozen private version created |
| EX-PUB-008 | MTD-PUB-003 | Authorized private user/creator | Private Agent A | ALLOW | Intended private access succeeds |
| EX-PUB-009 | MTD-PUB-003 | Normal Marketplace consumer | Private Agent A | DENY discovery | Private agent absent from general Marketplace |
| EX-VER-001 | MTD-VER-001 | Applicable publisher | Publish V1 | TBD role | Frozen V1 created |
| EX-VER-002 | MTD-VER-001 | Space Designer | Edit draft after V1 | ALLOW draft | Draft changes do not alter V1 |
| EX-VER-003 | MTD-VER-001 | Space User | Runtime before V2 publish | ALLOW V1 | Consumer still receives V1 |
| EX-VER-004 | MTD-VER-001 | Applicable publisher | Publish V2 | TBD role | Frozen V2 created |
| EX-VER-005 | MTD-VER-001 | Space User | Runtime after V2 publish | ALLOW V2 | Consumer receives V2 |
| EX-MKT-001 | MTD-MKT-001 | Space User A | Permitted Marketplace | ALLOW | Marketplace opens with permitted set |
| EX-MKT-002 | MTD-MKT-001 | Space User A | Published Agent A | ALLOW | Agent becomes discoverable after share/publish |
| EX-MKT-003 | MTD-MKT-001 | Space User A | Agent A listing | ALLOW | Correct published Agent/version opens |
| EX-MKT-004 | MTD-MKT-001 + MTD-ISO-001 | Space B-only user | Agent A | DENY | Unauthorized listing absent |
| EX-RUN-011 | MTD-RUN-005 | Space User A | Turn 1 | ALLOW | Initial prompt establishes context |
| EX-RUN-012 | MTD-RUN-005 | Space User A | Follow-up turn | ALLOW | Appropriate context retained |
| EX-RUN-013 | MTD-RUN-005 | Space User A | Governance-conflicting prompt | DENY override | Higher governance remains effective |
| EX-RUN-014 | MTD-RUN-005 | Space Designer | Same governed multi-turn flow | ALLOW within rules | Creator runtime obeys same governance |

## Count Reconciliation

| Package | Explicit Execution Variants |
|---|---:|
| Original Wave 1 | 73 |
| Wave 1.1 additions | 23 |
| **Reconciled P0 baseline** | **96** |

The E2E chains reuse explicit executions and are not double-counted.

## Additional E2E Chains

### E2E-X04 — Frozen Version Lifecycle

Publish V1 → consumer verifies V1 → edit draft → consumer still verifies V1 → publish V2 → consumer verifies V2.

### E2E-X05 — Private Publication Boundary

Publish Private Testing version → authorized private access succeeds → normal Marketplace consumer cannot discover/use the private agent.

## Smoke Suite

The existing 10-check smoke subset remains unchanged. It is an environment sanity gate, not a representation of all P0 catalogue scenarios. Version/private checks enter the wider P0 suite after Publish-role mapping is confirmed.

**End of Document**