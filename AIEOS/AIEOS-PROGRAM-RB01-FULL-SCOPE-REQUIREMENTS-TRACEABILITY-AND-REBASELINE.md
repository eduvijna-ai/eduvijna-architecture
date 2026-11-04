---
id: AIEOS-PROGRAM-RB01
title: Full-Scope Requirements Traceability & Programme Rebaseline (Founder No-Scope-Cut)
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: draft
version: 1.0.0
created: 2026-11-04
last_updated: 2026-11-04
workday: AIEOS-PROGRAM-RB01-P01
authorization: Founder 2026-11-04 quality-first timeline extension — planning only
parent_issue: https://github.com/eduvijna-ai/eduvijna-architecture/issues/62
---

# AIEOS-PROGRAM-RB01 — Full-Scope Requirements Traceability & Programme Rebaseline

**Governance:** **FOUNDER-APPROVED QUALITY-FIRST, NO-SILENT-SCOPE-CUT REBASELINE DIRECTION** ([Issue #62](https://github.com/eduvijna-ai/eduvijna-architecture/issues/62)). This deposit is **DESIGN / PLANNING ONLY**. It does **not** authorize product code, merges (except this Architecture draft PR), production activity, or reinterpretation of frozen ADR privacy boundaries.

**STOP (workday end-state):** `RB01-P01 PROGRAMME TRACEABILITY/REBASELINE DRAFT DEPOSITED / NO SCOPE CUT / NEW DATES PROPOSED ONLY / CHIEF REVIEW PENDING / NO PRODUCT CODE AUTHORIZED`

---

## A — Workday identity

| Field | Value |
|-------|-------|
| Programme | AIEOS-PROGRAM-RB01 |
| Packet | **AIEOS-PROGRAM-RB01-P01** — Chief Architect scoped planning workday |
| Founder authorization date | **2026-11-04** |
| Mode | Architecture-only Markdown; **no** Backend / Frontend / Product / Infrastructure writes |
| Deliverable file | `AIEOS/AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md` (this document) |

---

## B — Exact-source gate (verified before branch creation)

Verification executed **2026-11-04** against remote `origin` (methods: `git fetch`, `git ls-remote`, `gh pr view`, shallow Backend clone + `sha256sum`).

| Authority | Expected SHA / value | Verified | Result |
|-----------|----------------------|----------|--------|
| Architecture `main` | `ebd0f5c67550638852c12d32a60d1671b130ae85` | **MATCH** | `git rev-parse origin/main` |
| Product `main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | `git ls-remote` |
| Backend `main` | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | `git ls-remote` |
| Frontend `main` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** | `git ls-remote` |
| Infrastructure `main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | `git ls-remote` |
| Backend OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** | shallow clone @ Backend pin |
| Alembic head | `a360s010004` | **MATCH** | `migrations/versions/a360s010004_*.py` on Backend pin |

**Gate:** **PASS** — proceed to authorized write.

### B.1 — Architecture PR states (must not be modified)

| PR | Title (short) | State | Draft | Head OID | Merge commit (if merged) |
|----|---------------|-------|-------|----------|---------------------------|
| **#59** | ADR-AIEOS-063 Learner-Safe Instructional Hints | **MERGED** | n/a | `097caebe2a18d3cd195aa996d05e1a910200e310` | `ebd0f5c67550638852c12d32a60d1671b130ae85` |
| **#57** | SP01 PATH-STUDENT-PRACTICE discovery | **OPEN** | **YES** | `5182f99d028f32bcd55570c5d44f5c1f64ad5277` | — |
| **#55** | EX01 V1-EXPAND scope freeze | **OPEN** | **YES** | `8b1d07692e1698cf2be9d338f6d45a1707719146` | — |
| **#53** | DR01 Dec-18 gap audit | **OPEN** | **YES** | `70986a013ce776257f739eff6ab89727d6715df9` | — |
| **#51** | CX01-I08 Founder acceptance evidence | **OPEN** | **YES** | `87725067d3aa9f39dff05e634f71b05d8da85cd0` | — |

| PR (Product) | State | Draft | Head OID |
|--------------|-------|-------|----------|
| **#3** | CX01-I08-P Product acceptance draft | **OPEN** | **YES** | `90511df0358dcee1236adcde73659bfb2be95e37` |

**Note:** Draft PRs #53, #55, #57, #51 and Product #3 are **read-only references** for requirement inventory. Their bases predate post-#59 `main`; **no auto-rebase, amend, or merge** was performed in RB01-P01.

---

## C — Git branch and parent

| Field | Value |
|-------|-------|
| Branch | `cursor/aieos-program-rb01-traceability-7b2f` |
| Parent commit | `ebd0f5c67550638852c12d32a60d1671b130ae85` (Architecture `origin/main` post ADR-063 merge) |
| Diff scope | **One file only:** this Markdown document |

---

## D — Evidence pins (used in matrix)

All implementation evidence rows reference **Backend** `637583f42…`, **Frontend** `569ef8be…`, **Product** `b4b3048f…`, **Infrastructure** `a8654e5b…` unless a row cites an **historical closeout pin** (Teacher CX01, earlier DEV slices) explicitly.

**Alembic:** `a360s010004` · **OpenAPI SHA-256:** `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`

---

## E — Client-safe status message (external)

**What changed in planning policy (2026-11-04):** Calendar dates **no longer force** scope cuts or fake “complete” labels. EduVijna remains committed to **100% of agreed requirements** with verifiable evidence; if schedule pressure appears, **dates extend**, not features.

**What is already real (development slices — not full product / not production):**

- **Teacher OS** — development-ready and client-showcase-ready (TOS-DEV10, TOS-CX01).
- **AIEOS360 S01–S04** — thin Student assignment path, Principal and Parent derived intelligence, coherent **non-production** School Context — each **development slice complete**, **not** full OS products.
- **Cross-role data-plane E2E** — proven on shared PostgreSQL; **human unified client rehearsal** still has gaps ([CX01-W01](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)).

**What is not claimed:**

- **Not** “100% of original AIEOS already implemented.”
- **Not** production-ready, production ERP/SIS, Admin OS, broad Agents/MCP platform, full Educational Intelligence System, or Founder UAT complete.
- **Not** learner hints (ADR-063) — architecture **frozen on `main`**, **implementation not started** at pinned code.

**Dates:**

| Label | Meaning |
|-------|---------|
| **Historical baseline** | Nov 20 2026 showcase, Dec 18 2026 V1 dev-ready, Jan–May 2027 programme families — preserved in [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) §Locked targets |
| **New planning targets (tentative)** | AIEOS V1 development readiness **~Q1–Q2 2027**; full original functional development **~H2 2027 or later** — **PROPOSED / FOUNDER RATIFICATION PENDING** (Section H) |

---

## F — Founder decision sheet (ratification pending)

| Decision | Founder status | Chief / programme action |
|----------|----------------|---------------------------|
| No silent scope cut; extend timeline before quality compromise | **APPROVED 2026-11-04** | Binding planning policy |
| Rebaseline inventory + proposed dates from evidence | **AUTHORIZED (planning workday)** | This document |
| **New client-facing commitment dates** | **NOT YET RATIFIED** | Requires Chief independent review of this matrix + capacity assumptions |
| ADR-063 learner hints **architecture** | **FROZEN / APPROVED** (on `main` via PR #59) | Implementation requires **separate engineering workday** |
| Product code / merges / production | **NOT AUTHORIZED** by RB01-P01 | Await chartered workdays |

**NO_CUT rule:** Only the Founder may explicitly descope a requirement. Otherwise status remains **NOT DONE** (or **PARTIAL**) and the **date moves**, not the requirement.

---

## G — Quality gates (definitions)

| Gate | Definition |
|------|------------|
| **Development-ready (programme)** | All **approved** scope for the gate has real-stack E2E proof; authorization correct; no answer-key / evaluation leak to learner or Parent where forbidden; immutable ContentVersion binding; role-appropriate UX; QA without open P0/P1 functional gaps on approved scope |
| **Client showcase-ready** | Development-ready **plus** unified human rehearsal of the agreed vertical story (CX01 contract) |
| **Founder UAT** | Human acceptance **after** development completion — **not** claimed now |
| **Production-ready** | Separate infrastructure, security, ERP live integration, deployment — **not** implied by any development slice closeout |

---

## H — Programme rebaseline (historical vs proposed)

**Assumptions (explicit):** Serial Cursor throughput ~1–2 bounded implementation packets per week including review/E2E; parallel human teams would compress calendar but are **not assumed**; **+25% QA/integration buffer** on bottom-up estimates.

| Programme family | Historical target (baseline) | Preserved scope | Proposed target date | Status |
|------------------|------------------------------|-----------------|----------------------|--------|
| AIEOS 360 engineering showcase checkpoint | 2026-11-20 | Evidence checkpoint only — **not** forced readiness | **2026-11-20** (checkpoint retained) | Internal checkpoint |
| AIEOS V1 development-ready (incl. V1-EXPAND hints + CX01 gaps + EX01/DR01 reconciled backlog) | 2026-12-18 | Full agreed V1-EXPAND + showcase + matrix **PARTIAL/NOT_STARTED** items for V1 | **2027-04-17** (Fri) | **PROPOSED / FOUNDER RATIFICATION PENDING** |
| Experience Depth Complete | 2027-01-29 | Role UX depth, accessibility, Indian-school use-case fidelity | **2027-06-26** | **PROPOSED / PENDING** |
| ERP / School Operations Complete | 2027-02-26 | Real Admin OS / production ERP-SIS beyond S04 synthetic provider | **2027-08-21** | **PROPOSED / PENDING** |
| Educational Intelligence + Knowledge | 2027-03-26 | Curriculum graph, multilingual EIS | **2027-10-16** | **PROPOSED / PENDING** |
| Agentic AI + MCP + AI Engineering Platform | 2027-04-23 | Governed agents, MCP surfaces, orchestration | **2027-11-20** | **PROPOSED / PENDING** |
| Ecosystem / Founder / Developer | 2027-05-21 | SDK, analytics, marketplace-class vision | **2027-12-11** | **PROPOSED / PENDING** |
| Full Original AIEOS Development Complete | 2027-05-28 | All agreed functionality with evidence | **2027-12-18** | **PROPOSED / PENDING** |

**Critical path to first proposed V1 date (2027-04-17):** ADR-063 implementation chain (Section J) → CX01-I01…I08 showcase closure → remaining V1-EXPAND items from draft EX01/DR01 PRs → cross-role E2E hardening → explicit **NO_CUT** buffer.

---

## I — Non-omission register (`SOURCE_REQUIRED / FOUNDER RECONCILIATION`)

Requirements referenced in programme narrative but **not fully reproducible** in GitHub at RB01 pins are **not dropped**. They require Founder-supplied authoritative sources.

| Register ID | Topic | Why SOURCE_REQUIRED | Proposed reconciliation |
|-------------|-------|---------------------|-------------------------|
| SRC-01 | “Original six post-Dec feature families” exact acceptance checklists beyond roadmap table rows | Roadmap preserves **dates/names**; item-level acceptance not fully enumerated in Architecture repo alone | Founder + Product Architecture workshop; attach to Product `vision/` or chartered PA supplements |
| SRC-02 | Pre-GitHub Project conversation requirements (full AIEOS vision breadth) | Agent has **no** access to external conversation transcripts | Founder reconciliation session; map to REQ-IDs or explicit **TO_RATIFY** |
| SRC-03 | Indian-school contextual UX specifics (beyond PA drafts) | Partially in Product repo; not all marked **Approved** | Product decision pass; mark Draft vs Approved per contract |
| SRC-04 | Team capacity / FTE plan | Not in repositories | Founder / programme management input for date ratification |
| SRC-05 | Production provider spend / Groq production certification | Explicitly excluded from development slices | Separate production charter |

**TO_RATIFY (vision — not authorized coding):** Marketplace / multi-tenant ecosystem monetization, autonomous multi-agent classrooms, inferred learner personalization beyond explicit Teacher Memory, Principal learner drill-down, Parent evaluation disclosure — require **new ADR + Founder approval** before counting as agreed scope.

---

## J — ADR-063 dependency chain (post-freeze; not authorized here)

Ordered engineering packets for **`V1-EXPAND-STUDENT-LEARNER-HINTS-V1`** ([ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md)); static scenarios in [AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md](AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md).

| Step | Packet | Objective | Repos | Depends on |
|------|--------|-----------|-------|------------|
| **T0** | Teacher hint authoring + guarded append | `education.worksheet@2` authoring UI/API; O63-02 owner/class gates; review attestation | Backend, Frontend, Product E2E | ADR-063 frozen on `main` |
| **T1** | Content worksheet `@2` registry | Schema registration, append validation, semantic lint hooks | Backend | T0 |
| **T1b** | Learning `@2` projection | Learner-safe payload rules; no hint on assignment GET | Backend | T1 |
| **T1c** | Assessment `@2` convergence | No hint/answer leakage through assessment channels | Backend | T1 |
| **T2** | Semantic QA | Human review + `human_review_pass` for flagged hints | Backend, Product | T1 |
| **B** | Guarded hint GET | `GET .../learning/attempts/{id}/learner-hints[...]` with §8.2 locking | Backend OpenAPI + auth | T1b, School Context |
| **F** | Student UI | Optional in-attempt hint UX; no Parent/Principal surfaces | Frontend | B |
| **E2E** | Adversarial suite | SP02-S01…S67 HTTP negatives + happy path | Product | F |

**First separately authorized code packet (proposal):** **T0 + T1** as one Chief-chartered workday — smallest vertical that proves immutable hint-bearing ContentVersion path without yet exposing Student hint GET.

---

## K — Requirements matrix

**Legend — classification:** `DONE_VERIFIED` · `PARTIAL` · `NOT_STARTED` · `BLOCKED_ADR` (architecture approved, implementation not authorized) · `REQUIRES_PRODUCT_DECISION` · `SOURCE_REQUIRED`

**Legend — authority:** `FROZEN` · `APPROVED` · `DRAFT` · `VISION` · `PROPOSED`

### K.1 — Closed development slices (do not duplicate)

| Req-ID | Title | Source / authority | Persona / SoR | Evidence (SHA + path) | Class | Missing / notes | Phase (proposed) |
|--------|-------|-------------------|---------------|----------------------|-------|-----------------|------------------|
| RB01-TOS-DEV10 | Teacher OS development-complete experience | ADR-AIEOS-057 FROZEN | Teacher / Teaching + Content | Historical closeout SHAs in [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md); capabilities on current Backend pin under `domains/teaching/`, `domains/content/` | **DONE_VERIFIED** | Not production; not full Planner Agent | **Complete** |
| RB01-TOS-CX01 | Teacher OS client showcase | TOS-CX01-C01 APPROVED | Teacher | TOS-CX01 pins in roadmap; Frontend `ArtifactRenderer`, Model Gateway Groq showcase | **DONE_VERIFIED** | AIEOS360 cross-role shell gaps remain | **Complete** |
| RB01-S01-CORE | Student assign → attempt → submit | ADR-AIEOS-058 FROZEN | Student / Learning | Backend `637583f42…` `domains/learning/`; Frontend student-os routes @ pin | **DONE_VERIFIED** | Not full Student OS product | **Complete** |
| RB01-S01-I05 | Learner assessment intelligence → Teacher improve | ADR-AIEOS-059 FROZEN | Assessment / Teacher | Backend `LearnerAssessmentEvaluation`; Product E2E history | **DONE_VERIFIED** | No learner-facing grades | **Complete** |
| RB01-S02 | Principal school intelligence (thin) | ADR-AIEOS-060 FROZEN | Principal / derived | `GET /api/v1/principal-os/school-intelligence` @ OpenAPI pin | **DONE_VERIFIED** | No drill-down; not Principal OS product | **Complete** |
| RB01-S03 | Parent intelligence (thin) | ADR-AIEOS-061 FROZEN | Parent / derived | `GET /api/v1/parent-os/...` @ OpenAPI pin | **DONE_VERIFIED** | EVALUATION_EXISTENCE=NO; not Parent OS product | **Complete** |
| RB01-S04 | Admin/ERP school context (non-prod) | ADR-AIEOS-062 FROZEN | School Context adapter | `DevelopmentCoherentSchoolContextProvider`; S04-I03 E2E scripts referenced in CX01-W01 | **DONE_VERIFIED** | Not production ERP; not Admin OS | **Complete** |
| RB01-TOS-DEV04-09 | Prepare kit, Assign, Teach, Assess, Improve chain | ADR-052…056 FROZEN | Teacher | Implemented domains @ Backend pin | **DONE_VERIFIED** | Class-level scope limits per ADRs | **Complete** |

### K.2 — V1-EXPAND & ADR-063 (frozen architecture, zero implementation at pin)

| Req-ID | Title | Source | Class | Missing behavior | Deps | Est. | Owner lane | Phase |
|--------|-------|--------|-------|------------------|------|------|------------|-------|
| RB01-HINT-ARCH | Learner-safe hints authority | ADR-063 FROZEN on `main` | **BLOCKED_ADR** | All §5–§8 behaviors | — | 0 dev (done) | Architecture | **Complete (authority)** |
| RB01-HINT-T0 | Teacher worksheet@2 hint authoring | ADR-063 §7; SP01R1 PR #57 DRAFT | **NOT_STARTED** | Authoring UI/API, class-bound append | RB01-HINT-ARCH | L | Backend+FE | V1 **2027-Q1** |
| RB01-HINT-T1 | Content `@2` + attestation | ADR-063 §5 | **NOT_STARTED** | Registry, lint, review gates | T0 | M | Backend | V1 |
| RB01-HINT-B | Attempt-scoped hint GET | ADR-063 R1 | **NOT_STARTED** | New routes + FOR UPDATE read path | T1b | M | Backend | V1 |
| RB01-HINT-F | Student in-attempt hint UX | ADR-063 §1 | **NOT_STARTED** | UI wired to B only | B | S | Frontend | V1 |
| RB01-HINT-E2E | SP02 adversarial E2E | SP02A doc | **NOT_STARTED** | 67 scenarios automated | F | L | Product | V1 |

### K.3 — AIEOS360 client showcase gaps (from CX01-W01)

| Req-ID | Title | Source | Class | Missing | Est. | Phase |
|--------|-------|--------|-------|---------|------|-------|
| RB01-CX01-I01 | Unified showcase launcher / reseed | CX01-W01 §4 D | **NOT_STARTED** | Operator surface for CX-SCENARIO-01 | M | Pre-V1 showcase |
| RB01-CX01-I02 | Cross-role entry composition | CX01-W01 UX-01 | **NOT_STARTED** | Role → principal mapping without DEV panel | M | Pre-V1 |
| RB01-CX01-I03 | Student showcase UX polish | CX01-W01 UX-04 C | **PARTIAL** | Functional @ pin; below TOS-CX01 bar | M | Experience Depth |
| RB01-CX01-I04 | Principal/Parent showcase polish | CX01-W01 UX-04 | **PARTIAL** | Presentation layer | M | Experience Depth |
| RB01-CX01-I05 | Cross-role narrative / handoffs | CX01-W01 UX-05 | **NOT_STARTED** | Story affordances | S | Pre-V1 |
| RB01-CX01-I06 | Improve step in showcase story | CX01-W01 UX-06 | **PARTIAL** | I05 E2E exists; not in unified rehearsal | S | Pre-V1 |
| RB01-CX01-I07 | Provider mode transparency (non-Teacher) | CX01-W01 UX-07 | **NOT_STARTED** | Deterministic vs Groq labeling | S | Pre-V1 |
| RB01-CX01-I08 | Founder acceptance evidence pack | Arch PR #51 DRAFT; Product PR #3 DRAFT | **NOT_STARTED** | Formal acceptance docs merge | S | Post-showcase |

**Acceptance pattern (all CX01 packages):** direct HTTP negatives where applicable; shared PostgreSQL; **zero** `/api` Playwright mocks for integrated proofs (per CX01-W01).

### K.4 — Draft programme documents (read-only inventory)

| Req-ID | Title | Source (DRAFT PR) | Class | Notes |
|--------|-------|-------------------|-------|-------|
| RB01-DR01 | Dec-18 gap audit backlog | PR #53 head `70986a01…` | **REQUIRES_PRODUCT_DECISION** | Superseded as **deadline** by Founder 2026-11-04; backlog items remain valid input |
| RB01-EX01 | V1-EXPAND scope freeze | PR #55 head `8b1d0769…` | **REQUIRES_PRODUCT_DECISION** | Align EX01 feature list to this matrix before coding |
| RB01-SP01 | Student practice path discovery | PR #57 head `5182f99d…` | **APPROVED input** | Informed ADR-063; do not merge draft without revalidation |

### K.5 — Shared platform (selected ADR register @ main)

Each row: architecture authority on `main`; implementation at Backend pin unless noted.

| Req-ID | ADR | Theme | Authority | Class | Evidence / gap @ pin |
|--------|-----|-------|-----------|-------|----------------------|
| RB01-ADR-022 | 022 | Platform tech baseline | FROZEN | **PARTIAL** | Stack matches; not all production hardening |
| RB01-ADR-023R1 | 023R1 | Identity / tenant / security | FROZEN | **PARTIAL** | JWT dev patterns; production JWT ADR-030 separate |
| RB01-ADR-024 | 024 | Data resource SoR | FROZEN | **PARTIAL** | Core domains implemented; not all vision SoRs |
| RB01-ADR-025 | 025 | API contract baseline | FROZEN | **DONE_VERIFIED** | OpenAPI pin + contract tests history |
| RB01-ADR-026 | 026 | Workflow baseline | FROZEN | **PARTIAL** | Dev workflow; production Temporal ADR-047 not activated |
| RB01-ADR-027 | 027 | Generic Content | FROZEN | **DONE_VERIFIED** | Review queue + publish @ pin |
| RB01-ADR-028 | 028 | Security audit mutations | FROZEN | **PARTIAL** | Audit on governed mutations; full production audit plane TBD |
| RB01-ADR-029-031 | 029–031 | Production env / JWT / authz kernel | FROZEN | **NOT_STARTED** (production) | Architecture only for production path |
| RB01-ADR-033-036 | 033–036 | Asset file architecture | FROZEN | **PARTIAL** | Asset domains present; production blob plane not live |
| RB01-ADR-037-051 | 037–051 | Infra / asset production / OCI | FROZEN | **NOT_STARTED** (production) | No production deployment authorized |
| RB01-ADR-046R1 | 046R1 | Event plane publishers | FROZEN | **PARTIAL** | TeachingAssignment outbox; NATS prod **NOT_STARTED** |
| RB01-ADR-044 | 044 (legacy id) | AI platform behind services | APPROVED | **PARTIAL** | Model Gateway + Fake/Groq; Agents/MCP deferred |

*(Full ADR-AIEOS-022…063 corpus: **51** files on Architecture `main`; **8** teacher vertical ADRs 052–063 directly govern AIEOS360 + V1-EXPAND.)*

### K.6 — Post-December programme families (preserved scope)

| Req-ID | Family | Historical date | Class | Representative missing scope |
|--------|--------|-----------------|-------|------------------------------|
| RB01-PHASE-ED | Experience Depth | 2027-01-29 | **NOT_STARTED** | Accessibility, role UX parity, Indian-school workflows — **SRC-03** |
| RB01-PHASE-ERP | ERP / School Ops | 2027-02-26 | **NOT_STARTED** | Production ERP/SIS adapter; Admin OS; real roster/enrollment SoR |
| RB01-PHASE-EIS | Educational Intelligence + Knowledge | 2027-03-26 | **NOT_STARTED** | Curriculum/competency graph; multilingual; EIS engine integration |
| RB01-PHASE-AGENT | Agents / MCP / AI Engineering | 2027-04-23 | **NOT_STARTED** | Governed MCP tools; planner agents; eval/safety pipelines |
| RB01-PHASE-ECO | Ecosystem / Founder / Developer | 2027-05-21 | **SOURCE_REQUIRED** | SDK/marketplace — **SRC-02** partial in Product vision |
| RB01-PHASE-FULL | Full Original AIEOS dev complete | 2027-05-28 | **NOT_STARTED** | Aggregate of all **agreed** REQ rows with DONE_VERIFIED |

### K.7 — Explicit exclusions (unchanged without Founder descope)

| Topic | Status |
|-------|--------|
| UI-only authorization | **Forbidden** |
| Answer-key / hint leakage | **Forbidden** |
| Production ERP as S04 dev provider | **Not implemented by design** |
| Parent evaluation / mastery scores | **Forbidden** without new ADR |
| Principal learner drill-down | **Forbidden** without new ADR |
| Inferred personalization | **Deferred / TO_RATIFY** |

---

## L — Traceability summary counts

Counts are **requirement register rows** in Section K (not SP02 scenario rows).

| Classification | Count |
|----------------|------:|
| **DONE_VERIFIED** | 8 |
| **PARTIAL** | 9 |
| **NOT_STARTED** | 22 |
| **BLOCKED_ADR** | 1 |
| **REQUIRES_PRODUCT_DECISION** | 2 |
| **SOURCE_REQUIRED** (register SRC + PHASE-ECO) | 2 |
| **Total tracked REQ rows** | **44** |

**ADR corpus on `main`:** 51 × ADR-AIEOS files; **1** merged as architecture-only freeze with **NOT_STARTED** implementation (063).

**CI reality (Architecture repo):** `.github/workflows/` contains **no active CI workflows** (placeholder `.gitkeep` only). **Do not claim Architecture CI green.** Backend/Frontend CI exists on their repos at their pins — not re-run in RB01-P01.

---

## M — QA criteria for future ratification

1. Chief Architect independent **exact-head** review of this branch vs Section B gate.
2. Item-level estimate challenge — replace serial Cursor assumptions if team capacity differs (**SRC-04**).
3. Founder explicit ratification of Section H dates or revised substitutes.
4. No matrix row marked **DONE_VERIFIED** without SHA + path + test reference.
5. Privacy regression suite: Parent/Student/Principal negative HTTP cases on every learner-facing packet.

---

## N — Related documents (not modified in RB01-P01)

- [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) — historical locked dates (still on `main`; superseded for **policy** by Issue #62, not deleted)
- [AIEOS-CURRENT-STATE.md](AIEOS-CURRENT-STATE.md)
- [AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)
- [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md)

---

**End of RB01-P01 deposit — await Chief exact-head review and Founder date ratification.**
