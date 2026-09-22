# Agent Studio 2.0 — Business Scenario Catalogue

**Document Status:** Draft v0.4 — Reconciled 23 Sep 2026 with implemented screens and updated RBAC  
**Release Context:** Phase 1a — New Ideation, target 28 Sep 2026  
**Parent Strategy:** `docs/strategy/Agent-Studio-2.0-Functional-Test-Strategy.md`  
**Purpose:** Define the business-level functional scenario inventory from which detailed Manual Test Definitions, RBAC executions, smoke suites and regression suites will be derived.

---

## 1. Scenario Design Principles

The catalogue is intentionally maintained at **business scenario level** rather than individual UI-control level.

Traceability model:

**Capability → Business Scenario → Manual / Automation Test Definition → Execution → Evidence / Defect**

One Business Scenario may have multiple Test Definitions. A Test Definition may then be executed using different roles, tenants, spaces, agent states, versions, publication levels and source combinations.

The role/access matrix is therefore an execution and authorization dimension without requiring the entire functional catalogue to be redesigned.

### Priority

- **P0 — Critical:** release-blocking lifecycle, governance, isolation or runtime path.
- **P1 — High:** important functional behaviour required for reliable day-to-day use.
- **P2 — Medium:** supporting functionality, usability or lower-risk management behaviour.
- **TBD:** requirement/design not yet sufficiently confirmed.

### Status

- **Design-ready:** enough information exists to derive detailed test definitions.
- **Dependency:** scenario is valid but final expected result depends on an outstanding rule.
- **Conditional:** visible in design but feature/release inclusion is not confirmed.

---

## 2. Release-Critical Golden Journey

**Pattern / Tenant / Space Governance → Agent Builder → Agent Configuration → Publish Version → Space Agent Marketplace → Authorized User Opens Agent → Select / Upload Sources → Execute Prompt → Receive Response → Generate / Retrieve Output File**

---

## 3. Scenario Summary — Updated 23 Sep 2026

| Capability | P0 | P1 | P2 / TBD | Total |
|---|---:|---:|---:|---:|
| Foundation / Pattern & Tenant Governance | **12** | **15** | **6** | **33** |
| Agent Studio Homepage & Navigation | 0 | 3 | 3 | 6 |
| Agent Builder & Configuration | **12** | **7** | **3** | 22 |
| Publication & Versioning | **8** | **7** | 2 | **17** |
| Agent Marketplace | 4 | 6 | 4 | 14 |
| Agent Runtime / Harness | 4 | 9 | 2 | 15 |
| Runtime Sources | 3 | 10 | 2 | 15 |
| Generated Files | 2 | 7 | 1 | 10 |
| Cross-Cutting RBAC / Isolation | 7 | 5 | 2 | 14 |
| End-to-End Journeys | 8 | 3 | 1 | 12 |
| **Total** | **60** | **72** | **26** | **158** |

> 23 Sep reconciliation adds five screen/RBAC-backed scenarios without decomposing every UI control into a separate case: Tenant Member visibility, Space System Prompt governance, tenant-member-only Space assignment, connection credential/setup behaviour and explicit Space Marketplace publication. Publication role/scope is now resolved to Space Designer → Agent Marketplace of the Space.

> Counts are planning counts, not a commitment to 153 manual test cases. Related scenarios are intentionally covered by reusable Test Definitions and role/scope execution variants.

---

# 4. Foundation — Pattern, Tenant & Space Governance

## 4.1 Pattern Foundation

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| GOV-PAT-001 | P0 | Low Risk Pattern exists and is available for assignment | Required Low Risk Pattern is available with its configured governance/resources | Design-ready |
| GOV-PAT-002 | P0 | SDLC Pattern exists and is available for assignment | Required SDLC Pattern is available | Design-ready; exact configuration TBD |
| GOV-PAT-003 | P1 | View pattern definition through Pattern UI | User can view pattern content according to intended read-only behaviour | Dependency: reconcile read-only Pattern UI vs editable Pattern Tenant screens |
| GOV-PAT-004 | P1 | Maintain pattern overview | Authorized administration can maintain pattern name/purpose/audience/adopter information | Dependency: exact administration role |
| GOV-PAT-005 | P0 | Maintain shared pattern rules | Pattern-level purpose/boundaries/common rules/when-unsure are saved and applied | Design-ready |
| GOV-PAT-006 | P1 | Maintain pattern skills and connections | Authorized administration can define resources made available by pattern | Exact MCP/skill list TBD |
| GOV-PAT-007 | P1 | Connection requires adopter access rather than carrying credentials | Pattern carries connection requirement but not adopter credentials | Design-ready |
| GOV-PAT-008 | P1 | Associate agents/content with pattern | Selected content is included according to pattern rules | Design-ready |
| GOV-PAT-009 | P1 | Pattern draft changes remain draft until applicable publication/review | Existing published pattern/adopted state is not silently changed by draft editing | Dependency: final pattern publication semantics |
| GOV-PAT-010 | P2 | Review pattern version information | Published/current draft information is presented accurately | Dependency |
| GOV-PAT-011 | P2 | Submit pattern for review | Submission follows intended pattern-governance workflow | Dependency: distinguish from out-of-scope agent production approval |

## 4.2 Tenant Creation & Assignment

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| GOV-TEN-001 | P0 | Required rollout tenants exist | Training, AME, CAIO, CIB, COO, CTO, Cyber, GF, IWPB and UK tenants are available | Design-ready |
| GOV-TEN-002 | P0 | Default space exists for each tenant | Every created tenant receives its required default space | Design-ready |
| GOV-TEN-003 | P0 | Low Risk Pattern assigned to tenant/all applicable spaces | Low Risk governance is available throughout the intended tenant scope | Design-ready |
| GOV-TEN-004 | P1 | Tenant can inherit multiple patterns where supported | Tenant displays all assigned/inherited patterns | Dependency: Training design shows Research while engineering scope says Low Risk + SDLC |
| GOV-TEN-005 | P1 | Review inherited patterns/rules | Adopting tenant can review inherited governance but cannot improperly override it | Design-ready |
| GOV-TEN-006 | P0 | Inherited resource is not automatically enabled merely because it is shared | Tenant explicitly selects permitted subset of inherited tooling/agents | Design-ready |
| GOV-TEN-007 | P1 | Enable selected inherited agents | Selected inherited agents become enabled for Training/use-case tenant | Design-ready |
| GOV-TEN-008 | P1 | Enable selected inherited skills | Selected inherited skills become enabled | Design-ready |
| GOV-TEN-009 | P1 | Enable selected inherited connections | Selected inherited connections become enabled subject to access state | Design-ready |
| GOV-TEN-010 | P0 | Resource requiring access remains unavailable until connection established | Inherited/selected connection does not imply usable credentials/access | Design-ready |
| GOV-TEN-011 | P0 | Tenant system prompt respects pattern governance | Tenant prompt adds local context but cannot override higher-priority pattern rules | Design-ready |
| GOV-TEN-012 | P1 | Tenant system prompt applies across tenant spaces | Saved local context applies to applicable tenant agent calls | Design-ready |
| GOV-TEN-013 | P0 | Tenant Member can view tenant configuration without administration rights | Tenant Member receives read-only tenant context but cannot change configuration/patterns/membership | Design-ready; updated RAM 4.1–4.5 |

## 4.3 Space & Membership Governance

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| GOV-SPC-001 | P0 | Default space cannot be removed when defined as mandatory | Platform protects required default space | Design-ready |
| GOV-SPC-002 | P1 | Default-space membership/resources inherit/update correctly | Default space remains aligned with tenant inheritance rules | Design-ready |
| GOV-SPC-003 | P1 | Add tenant member and assign space/role | Membership is created with intended space and role | Design-ready; role matrix received |
| GOV-SPC-004 | P1 | Space owner manages space access/roles | Authorized Space Owner can maintain space membership | Design-ready; RAM 6.3 |
| GOV-SPC-005 | P2 | Create additional space | Additional space can be created where Day-1 scope permits | Dependency: design wording conflicts with optional-space flow |
| GOV-SPC-006 | P2 | Separate spaces maintain independent membership/resource scope | Space-level boundaries are maintained | Dependency: additional-space confirmation |
| GOV-SPC-007 | P2 | Membership changes propagate according to inheritance rules | Add/remove/change is reflected at intended tenant/space level | Dependency: final inheritance semantics |
| GOV-SPC-008 | P0 | Space System Prompt extends governance without overriding higher rules | Space prompt persists and applies below Pattern/Tenant governance and above Agent instructions | Design-ready from implemented Space Management screen |
| GOV-SPC-009 | P1 | Space membership is selected from existing Tenant Members | Space Owner can assign eligible Tenant Members; non-tenant identities cannot be directly added to Space | Design-ready; updated RAM 5.5 |

---

# 5. Agent Studio Homepage & Navigation

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| NAV-001 | P1 | Open Agent Studio homepage | Homepage loads with permitted services/navigation | Design-ready |
| NAV-002 | P1 | Navigate to Agent Builder | Correct Agent Builder entry opens | Design-ready |
| NAV-003 | P1 | Navigate to Agent Marketplace | Correct marketplace opens | Design-ready |
| NAV-004 | P2 | Navigate to Tenant/Space Management | Management page opens when entitled | Design-ready against RAM; exact navigation semantics remain clarification |
| NAV-005 | P2 | Navigate to other in-scope modules | Evaluation/MCP/Skill/Registry/Agentic Flow links open applicable capability | Dependency: detailed scope/screens incomplete |
| NAV-006 | TBD | Use homepage assistant/service cards | Assistant/card behaviour matches confirmed release design | Conditional |

---

# 6. Agent Builder & Configuration

## 6.1 Agent Creation

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| BLD-CRT-001 | P0 | Authorized Space Designer enters assigned space and starts agent creation | Creator can create only within assigned scope | Design-ready; Space Designer = Agent Creator |
| BLD-CRT-002 | P0 | Low Risk Pattern is default during agent creation | Low Risk is pre-selected/default as required | Design-ready; UI location TBD |
| BLD-CRT-003 | P0 | Agent is associated with exactly one pattern | Multiple simultaneous patterns cannot be assigned to one agent | Design-ready |
| BLD-CRT-004 | P0 | Create agent through natural-language idea | Builder captures idea and initiates assisted creation | Design-ready |
| BLD-CRT-005 | P0 | Builder asks focused follow-up question(s) | Required setup information is collected before draft creation | Design-ready |
| BLD-CRT-006 | P0 | Create agent from scratch | Valid name/details produce a new draft agent | Design-ready |
| BLD-CRT-007 | P0 | Validate required creation fields | Missing required data prevents invalid draft creation | Design-ready |
| BLD-CRT-008 | P0 | Cancel agent creation | No unintended agent is created | Design-ready |
| BLD-CRT-009 | P2 | Recover from assisted-generation failure | User receives controlled failure/retry behaviour | Implementation dependent |
| BLD-CRT-010 | TBD | Resume recently edited agent | User can pick up prior work according to access rules | Conditional / nice-to-have |
| BLD-CRT-011 | TBD | View All Agents | List contains only agents permitted for user's role/scope | Conditional; definition pending |

## 6.2 Agent Configuration

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| BLD-CFG-001 | P1 | Maintain Agent Info | Changes save and persist | Design-ready |
| BLD-CFG-002 | P0 | Maintain Agent Instructions under inherited governance | Agent-specific instructions persist but cannot override higher governance | Design-ready |
| BLD-CFG-003 | P0 | Select only skills permitted to current scope | Unassigned/unapproved skill cannot be attached/used | Design-ready |
| BLD-CFG-004 | P0 | Select only tools/MCPs permitted to current scope | Unassigned/unapproved tool cannot be attached/used | Design-ready |
| BLD-CFG-005 | P1 | Configure Knowledge Bases | Permitted knowledge-base configuration saves correctly | Design-ready |
| BLD-CFG-006 | P1 | Configure Advanced Settings | Supported settings save/persist | Detailed fields TBD |
| BLD-CFG-007 | P1 | Remove previously selected configurable capability | Removal persists and affects subsequent draft runtime as intended | Design-ready |
| BLD-CFG-008 | P1 | Reload configured draft | Saved configuration remains consistent | Design-ready |
| BLD-CFG-009 | P1 | Test/chat with draft during configuration | Space Designer can run the draft from the debug window without Marketplace publication | Design-ready; updated RAM 6.7 |
| BLD-CFG-010 | P0 | Configure approved connection/tool and required personal access | Designer can select approved connection/tool; required personal credentials/access are established or explicitly deferred before use | Design-ready from implemented connection screens |
| BLD-CFG-011 | P1 | Select permitted Knowledge Base configuration | Designer can select only Knowledge Bases available to the current scope and selection persists | Design-ready from implemented Builder screen |

---

# 7. Agent Publication & Versioning

## 7.1 Publication

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| PUB-001 | P0 | Draft agent is not generally available before publication | Normal users cannot discover/use unpublished draft | Design-ready |
| PUB-002 | P0 | Space Designer publishes initial Agent version to Space Marketplace | Publish v1 creates a frozen release and makes it available through the Agent Marketplace of the Space | Design-ready; updated RAM 6.8 + implemented Publish v1 screen |
| PUB-003 | P0 | Published Agent remains constrained to its Space Marketplace | Publication does not grant cross-Space discovery or execution | Design-ready; updated RAM 6.8/7.1 |
| PUB-004 | P1 | Provide What's New/version notes | Publication metadata saves against version | Design-ready |
| PUB-005 | P1 | Generate What's New text | Generated release-note assistance behaves correctly where enabled | Design-ready |
| PUB-006 | P1 | Set category | Published version retains selected category | Design-ready |
| PUB-007 | P1 | Set tags | Published version retains selected tags | Design-ready |
| PUB-008 | P1 | Cancel publication | Current published/draft state remains unchanged | Design-ready |
| PUB-009 | P0 | Publication creates frozen release | Published runtime is separated from mutable draft configuration | Design-ready |
| PUB-010 | P0 | Marketplace publication respects Space visibility boundary | Agent is exposed only in the Agent Marketplace of its intended Space | Design-ready; updated RAM 6.8 resolves earlier tenant-shared ambiguity |

## 7.2 Version Lifecycle

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| VER-001 | P0 | Modify agent after Version N is published | New edits remain draft and Version N remains active | Design-ready |
| VER-002 | P0 | Publish Version N+1 | New frozen version is created from approved draft state | Design-ready functionally; publisher role confirmed as Space Designer |
| VER-003 | P0 | Marketplace/runtime switches to newly published version | Eligible users receive Version N+1 only after successful publish | Design-ready |
| VER-004 | P1 | Failed publication preserves existing published version | Version N remains usable and uncorrupted | Design-ready |
| VER-005 | P1 | Version metadata/history remains coherent | Version number/notes/state align with lifecycle | Design-ready |
| VER-006 | TBD | Unpublish/retire agent | Agent leaves discovery/runtime according to lifecycle | Conditional; not yet defined |
| VER-007 | TBD | Production release request/approval | Production change control works | Explicitly out of 28 Sep scope; future only |

---

# 8. Agent Marketplace

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| MKT-001 | P0 | Authorized user opens marketplace | Marketplace shows agents user is permitted to discover | Design-ready |
| MKT-002 | P0 | Published marketplace agent becomes discoverable | Successful publication results in marketplace availability | Design-ready; exact marketplace scope pending |
| MKT-003 | P0 | Unpublished draft is not exposed in Agent Marketplace | Draft remains in Builder and does not appear as a consumable Marketplace Agent | Design-ready; implemented Draft/Active state + RAM 6.8 |
| MKT-004 | P0 | Cross-space/cross-tenant unauthorized agent is not discoverable | Isolation boundary is enforced | Dependency: final marketplace scope |
| MKT-005 | P1 | Search by agent name/description | Matching permitted agents returned | Design-ready |
| MKT-006 | P1 | Filter by category | Results respect category and authorization | Design-ready |
| MKT-007 | P1 | Filter by tag | Results respect tag and authorization | Design-ready |
| MKT-008 | P1 | Open selected marketplace agent | Correct agent/version opens in runtime | Design-ready |
| MKT-009 | P1 | Recently used list reflects user's activity | Relevant permitted recent agents displayed | Design-ready |
| MKT-010 | P1 | My Private Agent area shows permitted private agents | Private-agent discovery respects ownership/access | Dependency: role/access semantics |
| MKT-011 | P2 | Bookmark/unbookmark agent | User preference persists | Supporting feature |
| MKT-012 | P2 | Grid/list view | Presentation changes without altering permitted result set | Supporting feature |
| MKT-013 | P2 | Pagination | Navigation preserves correct filtered/authorized result set | Supporting feature |
| MKT-014 | P2 | Quick prompt using selected agent | Prompt launches/runs selected permitted agent | Supporting feature |

---

# 9. Agent Runtime / Harness

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| RUN-001 | P0 | Open published permitted agent | Runtime opens correct agent and published version | Design-ready |
| RUN-002 | P0 | Submit prompt and receive response | Agent completes normal execution successfully | Design-ready |
| RUN-003 | P0 | Execute multi-turn conversation | Follow-up retains appropriate session context | Design-ready |
| RUN-004 | P0 | Runtime respects inherited governance and permitted capabilities | Agent cannot bypass Pattern/Tenant/Space restrictions at execution | Design-ready |
| RUN-005 | P1 | Create new session | New independent conversation starts | Design-ready |
| RUN-006 | P1 | Reopen prior session | User can access permitted prior session with correct history | Design-ready |
| RUN-007 | P1 | Session isolation between users | One user's conversation is not exposed to another | Design-ready |
| RUN-008 | P1 | Clear chat/session | Conversation state changes according to intended semantics | Dependency: exact clear behaviour TBD |
| RUN-009 | P1 | Runtime displays Request ID | Execution identifier is presented and corresponds to request | Design-ready |
| RUN-010 | P1 | Runtime displays Time Spent | Execution timing metadata is presented consistently | Design-ready |
| RUN-011 | P1 | Runtime displays token usage | Total token metadata is presented consistently | Design-ready |
| RUN-012 | P1 | Runtime displays cost estimate | Cost estimate is presented consistently | Design-ready |
| RUN-013 | P1 | Runtime handles controlled execution failure | User receives understandable failure without corrupting session | Implementation dependent |
| RUN-014 | P2 | Runtime handles long/boundary input | Input limits produce defined behaviour | Limits TBD |
| RUN-015 | P2 | Suggested questions execute correctly | Suggested prompt is submitted to intended agent | Supporting feature |

---

# 10. Runtime Sources

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| SRC-001 | P0 | Upload valid personal source | Supported file is added and available to user/agent runtime | Design-ready |
| SRC-002 | P0 | Personal source remains hidden from other users | User A's personal file is not discoverable by User B | Design-ready |
| SRC-003 | P0 | Agent treats personal source as read-only | Runtime cannot modify original personal source | Design-ready |
| SRC-004 | P1 | Upload each supported file type | Supported TXT/MD/Word/Excel/PDF/PNG/JPG/CSV formats are accepted | Confirm exact extensions |
| SRC-005 | P1 | Upload file at maximum permitted size | Boundary file is accepted | Current design says 10MB; confirm implementation |
| SRC-006 | P1 | Upload file exceeding maximum size | Upload is rejected with clear validation | Current design says >10MB |
| SRC-007 | P1 | Upload unsupported file type | Upload is rejected safely | Design-ready |
| SRC-008 | P1 | Upload empty/corrupted file | Controlled validation/error occurs | Implementation dependent |
| SRC-009 | P1 | Select one source | Selected source participates in runtime context | Design-ready |
| SRC-010 | P1 | Select multiple sources | All selected sources participate appropriately | Design-ready |
| SRC-011 | P1 | Select all sources | All available permitted sources become active | Design-ready |
| SRC-012 | P1 | Deselect source | Deselected source no longer acts as selected context | Design-ready |
| SRC-013 | P1 | Execute with no source selected | Agent follows defined no-source behaviour | Design-ready |
| SRC-014 | P2 | Duplicate source upload | Duplicate handling follows intended rule | Rule TBD |
| SRC-015 | P2 | Source persistence across sessions | Sources persist/reset according to intended scope | Dependency: persistence rule TBD |

---

# 11. Generated Files

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| GEN-001 | P0 | Request agent to generate an output file | Agent successfully creates supported artifact | Design-ready |
| GEN-002 | P0 | Retrieve/download generated file | Generated artifact is accessible to authorized user and opens successfully | Design-ready |
| GEN-003 | P1 | Generated Files panel updates after creation | Newly created artifact appears with correct association | Design-ready |
| GEN-004 | P1 | Generated content reflects request/source context | Output is materially aligned to requested task and selected context | Design-ready; quality criteria may vary |
| GEN-005 | P1 | Generate multiple files in one session | Artifacts remain distinguishable and retrievable | Design-ready |
| GEN-006 | P1 | Generate new file after follow-up request | Subsequent artifact is created without corrupting prior output | Design-ready |
| GEN-007 | P1 | Generated file remains private to permitted user/session scope | Unauthorized user cannot retrieve artifact | Dependency: exact ownership scope |
| GEN-008 | P1 | Handle file-generation failure | Controlled error occurs and session remains usable | Implementation dependent |
| GEN-009 | P1 | Generated file is structurally valid | File can be opened/read in expected format | Design-ready |
| GEN-010 | P2 | Generated-file lifecycle/expiry | File availability follows retention rule | Retention rule TBD |

---

# 12. Cross-Cutting RBAC, Governance & Isolation

The official Roles & Actions Matrix is now the authorization baseline. Role permutations remain in the separate RBAC and execution artifacts rather than being duplicated in this business catalogue.

| ID | Pri | Business Scenario | Expected Business Outcome | Status / Dependency |
|---|---|---|---|---|
| SEC-RBAC-001 | P0 | Tenant Owner performs permitted tenant administration | Authorized actions succeed | Design-ready against RAM |
| SEC-RBAC-002 | P0 | Space Owner performs permitted space administration | Authorized actions succeed only within assigned scope | Design-ready against RAM |
| SEC-RBAC-003 | P0 | Space Designer performs permitted agent lifecycle actions | Create/configure/test access matches approved model | Design-ready against RAM; publish mapping separate |
| SEC-RBAC-004 | P0 | Space User uses permitted marketplace agent | Runtime access succeeds without administrative capability | Design-ready against RAM |
| SEC-RBAC-005 | P0 | Unauthorized role cannot perform restricted action through UI | Restricted control is hidden/disabled/read-only as designed | Design-ready against RAM |
| SEC-RBAC-006 | P0 | Unauthorized role cannot bypass UI using direct URL/service request | Server-side authorization rejects restricted operation | Design-ready where direct service is testable |
| SEC-RBAC-007 | P0 | Space 2-only user cannot discover/use Space 1-only agent | Cross-space isolation is enforced | Design-ready; final marketplace scope confirmation |
| SEC-RBAC-008 | P1 | Cross-tenant user cannot discover/use unauthorized tenant agent | Tenant isolation is enforced | Design-ready |
| SEC-RBAC-009 | P1 | Creator cannot use unassigned MCP/skill | Capability assignment boundary enforced | Design-ready |
| SEC-RBAC-010 | P1 | Creator cannot consume unapproved arbitrary API | Platform prevents bypass of approved capability model | Design-ready |
| SEC-RBAC-011 | P1 | Lower-level agent instruction cannot override tenant/pattern governance | Instruction precedence is enforced at runtime | Design-ready |
| SEC-RBAC-012 | P1 | Tenant prompt cannot override inherited pattern governance | Pattern remains highest applicable rule layer | Design-ready |
| SEC-RBAC-013 | TBD | Map Agent Creator vs Space Designer vs Agent Owner terminology | Space Designer = Agent Creator for current test baseline; Agent Owner terminology still to be reconciled where used | Partially resolved |
| SEC-RBAC-014 | TBD | Multi-role user receives correct effective permissions | Combined role semantics follow approved model | Dependency |

---

# 13. End-to-End Scenario Catalogue

| ID | Pri | End-to-End Journey | Expected Business Outcome | Status |
|---|---|---|---|---|
| E2E-001 | P0 | Pattern → Tenant → Agent → Publish → Marketplace → Runtime | Complete governed agent lifecycle succeeds | Design-ready; publish-role mapping pending |
| E2E-002 | P0 | Pattern inheritance → Tenant subset enablement → Agent uses only permitted capability | Inheritance and enablement boundaries remain intact end-to-end | Design-ready |
| E2E-003 | P0 | Create Agent → Publish V1 → Marketplace runs V1 | First publication reaches authorized consumers | Design-ready functionally; publish-role mapping pending |
| E2E-004 | P0 | V1 published → Edit draft → Marketplace still V1 → Publish V2 → Marketplace runs V2 | Frozen-version lifecycle is proven | Design-ready functionally |
| E2E-005 | P0 | Publish private agent → authorized private access → normal marketplace user cannot discover | Private visibility boundary is proven | Dependency: exact private-access/publisher roles |
| E2E-006 | P0 | Publish marketplace agent in Space 1 → Space 1 user can use → Space 2-only user cannot discover/use | Space isolation is proven | Dependency: marketplace scope conflict |
| E2E-007 | P0 | Open published agent → upload/select source → source-grounded response | Runtime source chain succeeds | Design-ready |
| E2E-008 | P0 | Open agent → use source → request generated artifact → retrieve file | Full runtime-to-output chain succeeds | Design-ready |
| E2E-009 | P1 | Connection inherited but access not established → attempt use | Capability remains unavailable with controlled guidance/error | Design-ready |
| E2E-010 | P1 | Pattern rule conflicts with tenant/agent instruction → execute agent | Higher-level governance wins | Design-ready |
| E2E-011 | P1 | Member/role assignment → permitted operation → restricted operation | RBAC works through full user journey | Design-ready against RAM |
| E2E-012 | TBD | Additional space creation → membership/resource assignment → isolated agent publication/use | Additional-space lifecycle works | Conditional pending Day-1 confirmation |

---

# 14. Requirement / Design Clarifications to Carry Forward

| ID | Clarification | Impact |
|---|---|---|
| CLAR-001 | Roles diagram says seven roles while official matrix includes Governance Manager as an eighth role | Role documentation alignment |
| CLAR-002 | Matrix 1.1 `Navigation (Read-Only)` semantics | Navigation/access expected results |
| CLAR-003 | Pattern UI is described as read-only while Pattern Tenant designs expose editing | Pattern administration scope |
| CLAR-004 | Training design shows Low Risk + Research Pattern while engineering scope names Low Risk + SDLC | Test data and expected inheritance |
| CLAR-005 | Publish UI says tenant Agent Marketplace while engineering rule says marketplace of that space only | Critical marketplace isolation expected result |
| CLAR-006 | Design says one shared default Space in initial scope while Create Space and operating flow allow additional spaces | Additional-space scope |
| CLAR-007 | Pattern Review/Versions/Submit for Review vs future agent production release approval | Avoid conflating pattern governance with out-of-scope production change control |
| CLAR-008 | Low Risk default and single-pattern selection are not yet visible in supplied Agent Builder screens | Exact UI/API validation path |
| CLAR-009 | Exact Low Risk/SDLC MCP and Skill lists | Test-data baseline |
| CLAR-010 | Definition of All Agents and recent-agent visibility by role | Conditional Agent Builder listing scenarios |
| CLAR-011 | Source persistence across session/user/agent | Source lifecycle expected results |
| CLAR-012 | Exact source extensions and 10MB boundary semantics | Upload boundary cases |
| CLAR-013 | Generated-file ownership/retention | Privacy and lifecycle cases |
| CLAR-014 | Detailed Agentic Workflow 2.0, Agent Inventory/Registry and Agent Harness requirements beyond supplied runtime screens | Additional scenario catalogue expansion |
| CLAR-015 | RAM 6.4 Review agent configuration request — whether this is an active current-scope gate | Agent lifecycle expected flow |
| CLAR-016 | Mapping among Figma Publish, Private Testing, Marketplace Testing and RAM 6.9 Promote to tenant-shared | P0 publication role/state coverage |
| CLAR-017 | Token/cost section numbering duplicates section 8 and skips 8.4 | Requirement reference hygiene |
| CLAR-018 | Multi-role effective permission model | Combined-role RBAC testing |

---

# 15. P0 Detailed Test-Definition Baseline

The updated catalogue contains **57 P0 business scenarios**. They do not map one-to-one to test definitions: related scenarios share reusable definitions where they form one coherent behaviour.

The current detailed P0 baseline is **35 reusable Manual Test Definitions** with **101 explicit functional execution variants**. Two dedicated E2E regression executions bring the AS20 dashboard-managed baseline to **103 variants**.

Explicit P0 coverage includes required Patterns and Pattern rules; rollout tenants/default Spaces; Tenant/Space governance; assisted and from-scratch Agent creation including required-field validation and cancellation; Agent configuration; private and marketplace publication; frozen V1→V2 versioning; Marketplace discovery; governed runtime/multi-turn; personal sources; generated files; RBAC; Space/Tenant isolation; and P0 E2E journeys.

The 10-check smoke suite remains intentionally smaller than full P0 coverage and is used only as the initial environment/build sanity gate.

---

# 16. Catalogue Maintenance Rule

This catalogue is a **living test-design index**.

- Do not silently rewrite an existing scenario's meaning.
- Update status/dependency or add a new scenario where business behaviour changes materially.
- Preserve IDs once detailed Test Definitions or executions reference them.
- Resolve `TBD` items only when an authoritative requirement or implemented behaviour is available.
- Maintain role permutations in the RBAC/execution artifacts rather than duplicating them here.
- Recalculate the summary from detailed rows whenever scenarios or priorities change.

---

**End of Document**