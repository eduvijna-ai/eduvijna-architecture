---
id: AIEOS-PROGRAM-RB02
title: Requirements Reconciliation & Development Capacity Preflight (Founder No-Scope-Cut)
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: draft
version: 1.0.1
created: 2026-11-04
last_updated: 2026-11-04
workday: AIEOS-PROGRAM-RB02-P01R1
authorization: Founder 2026-11-04 — planning only (Issue #64; post RB01 PR #63 merge)
parent_issue: https://github.com/eduvijna-ai/eduvijna-architecture/issues/64
parent_register: AIEOS/AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md @ 1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30
---

# AIEOS-PROGRAM-RB02 — Requirements Reconciliation & Capacity Preflight

**Governance:** **FOUNDER-APPROVED QUALITY-FIRST, NO-SILENT-SCOPE-CUT** ([Issue #64](https://github.com/eduvijna-ai/eduvijna-architecture/issues/64)). **DESIGN / PLANNING ONLY.** No product code, merge of other PRs, production spend, UAT, or exact-date ratification authorized by this deposit.

**Primary upstream:** [RB01 @ `main` `1fbbc356…`](https://github.com/eduvijna-ai/eduvijna-architecture/blob/1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30/AIEOS/AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md) — **12** matrix rows remain **`SOURCE_RECONCILIATION`** until this supplement is Chief-reviewed.

**STOP (RB02 end-state):** `RB02 SOURCE RECONCILIATION/CAPACITY PREFLIGHT DRAFT DEPOSITED / FOUNDER FULL SCOPE PRESERVED / NO EXACT DATES RATIFIED / NO PRODUCT CODE OR PR MERGE AUTHORIZED / CHIEF EXACT-HEAD REVIEW PENDING`

---

## A — Workday identity

| Field | Value |
|-------|-------|
| Programme | AIEOS-PROGRAM-RB02 |
| Founder authorization | **2026-11-04** (“ok, go ahead” after RB01 #63 verified merge) |
| Mode | **Read-only** investigation on five pinned `main` trees + linked Product/PA/EBP/ADR sources; **write only this file** |
| Packet | **AIEOS-PROGRAM-RB02-P01R1** — narrow evidence/accounting correction (Chief review F1–F3) |
| Prior deposit (P01) | `99ca38e7a5dca6c14e21ef879a07b2e0059c5198` on [PR #65](https://github.com/eduvijna-ai/eduvijna-architecture/pull/65) |
| Architecture parent (`main`) | `1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30` (RB01 PR #63 merge) |
| Branch | `cursor/aieos-program-rb02-reconciliation-2488` |
| RB01 merge reviewed head (#63) | `c141edd3c68605c69ada49c6928ec8792f245abd` |

---

## B — Exact-source gate (re-verified before P01R1 write)

Re-verification **2026-11-04 (P01R1)**: `git fetch origin main`, `git ls-remote`, `gh pr view` — all five pins and PR #65 base/head unchanged before this correction.

| Authority | Expected | Verified |
|-----------|----------|----------|
| Architecture `main` | `1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30` | **MATCH** |
| Product `main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** |
| Backend `main` | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** |
| Frontend `main` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** |
| Infrastructure `main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** |
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** |
| Alembic head | `a360s010004` | **MATCH** (single head + `readiness.py` coherence) |

### B.1 — PR states (unchanged; not modified)

| PR | State | Draft | Head OID | Notes |
|----|-------|-------|----------|-------|
| Arch **#63** RB01 | **MERGED** | — | Review `c141edd3…` → merge `1fbbc356…` | Upstream register |
| Arch **#59** ADR-063 | **MERGED** | — | Merge `ebd0f5c67550638852c12d32a60d1671b130ae85` | Hint **architecture** frozen |
| Arch **#57** SP01 | OPEN | YES | `5182f99d028f32bcd55570c5d44f5c1f64ad5277` | Unchanged |
| Arch **#55** EX01 | OPEN | YES | `8b1d07692e1698cf2be9d338f6d45a1707719146` | Unchanged |
| Arch **#53** DR01 | OPEN | YES | `70986a013ce776257f739eff6ab89727d6715df9` | Unchanged |
| Arch **#51** CX01 pack | OPEN | YES | `87725067d3aa9f39dff05e634f71b05d8da85cd0` | Unchanged |
| Product **#3** | OPEN | YES | `90511df0358dcee1236adcde73659bfb2be95e37` | Unchanged |
| Arch **#65** RB02 (this deposit) | OPEN | YES | Head `99ca38e…`; base `1fbbc356…` | Owner-open draft; P01R1 moves tip only |

**Gate:** **PASS** — P01R1 write authorized.

**Architecture Actions:** `.github/workflows/.gitkeep` only — **NO CI CONFIGURED** on Architecture repo. Backend/Frontend CI **not re-run** in RB02.

---

## C — Git branch and diff scope

| Field | Value |
|-------|-------|
| Branch | `cursor/aieos-program-rb02-reconciliation-2488` |
| P01 sole parent | `1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30` |
| **P01R1 sole direct parent** | `99ca38e7a5dca6c14e21ef879a07b2e0059c5198` |
| Diff vs `main` | **One file only:** this document (P01 + P01R1 additive edits) |
| Other repos / draft PRs | **Untouched** |

---

## D — Evidence pins & reconciliation conventions

**Pins (read-only):** Backend `637583f42…` · Frontend `569ef8be…` · Product `b4b3048f…` · Infrastructure `a8654e5b…`

**Independently counted reconciliation flags (§I.0 — not interchangeable):**

| Flag | Meaning |
|------|---------|
| **ID_ADDRESSED** | One §I.1 register block exists for the RB01 `SOURCE_RECONCILIATION` ID (**12/12** required) |
| **RELATED_SOURCE_FOUND (RSF)** | Reproducible **related** GitHub source (Draft/Vision/Roadmap/persona/standards) — **does not** certify an atomic agreed contract |
| **NO_MATCHING_ATOMIC_SOURCE (NMAS)** | No authoritative atomic acceptance spec at pin (may still have RSF=Y for family/draft material) |
| **FOUNDER_DECISION_PENDING (FDP)** | Cannot bind **APPROVED_AGREED** until Founder/Product Architecture and/or forward ADR — sub-reason per row |

**Size column:** S/M/L/XL/**UNKNOWN** + **confidence** (`RB01-aligned` / `hypothesis` / `UNKNOWN`) — **planning hypotheses only** while SRC-04 is empty; **not** calendar forecasts.

**Privacy / quality negatives (global):** No answer-key or hint leakage (ADR-063); no Principal learner drill-down or Parent evaluation scores without forward ADR (ADR-060/061); no AIEOS roster/enrollment SoR (ADR-062 external master); tenant isolation and ContentVersion immutability unchanged (ADR-027).

**Do not rebuild:** TOS-DEV10/CX01 closed slices; AIEOS360 S01–S04; CX01 operator tooling I01R9–I07 @ Frontend pin — polish, UAT, and verification residuals only.

---

## E — Client-safe status (external)

**Policy (unchanged):** No silent scope cuts; extend dates before quality compromise.

**Real @ pin (development, not production):** Governed Teacher loop through Improve (ADR-057 / TOS-DEV10); Student S01; Principal S02; Parent S03; Admin school-context S04 (**four current-authority ports only** @ ADR-062 — not calendar/board/medium read model); CX01 showcase baseline **I01R9–I07** with **EVIDENCE_GAP** on fresh CI rerun; ADR-063 **text only** — hint routes absent @ OpenAPI pin.

**Not claimed:** 100% original agreed AIEOS; Indian-school UX depth; role OS parity; EIS graph/alignment/ML; ecosystem SDK; production observability SLOs; certified staffing throughput.

**Dates:** Nov/Dec 2026 and Jan–May 2027 programme rows in [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) / RB01 §H.1 remain **historical comparison baselines**. V1 **Q1–Q2 2027** and full-original **H2 2027+** remain **tentative planning bands** — **NOT RATIFIED** pending SRC-04 and RB03 bottom-up estimation.

---

## F — Founder decision sheet (reconciliation outcomes)

| Item | RB02 disposition |
|------|------------------|
| No-scope-cut / quality-first | **APPROVED 2026-11-04** (unchanged) |
| 12 `SOURCE_RECONCILIATION` IDs | **Partially reconciled** — see §I; **0/12** promoted to full **APPROVED_AGREED** atomic contracts without ratification |
| SRC-01 post-Dec family checklists | **Atomic candidates mapped** — acceptance checklists **NEEDS_FOUNDER_RATIFICATION** |
| SRC-02 external conversations | **Not provable from GitHub** — evidence checklist §J.2 |
| SRC-03 Indian-school fidelity | **Draft Product sources found** — thresholds **NEEDS_FOUNDER_RATIFICATION** |
| SRC-04 capacity | **No authoritative FTE roster in repos** — Founder input checklist §J.4 |
| SRC-05 production spend | **Separate [PROD] gate** — not dev-ready scope |
| ADR-063 implementation | **PK-HINT-A proposal only** (§H) — **NOT AUTHORIZED** |
| RB03 bottom-up estimation | **Proposed gate** §H.2 — **NOT AUTHORIZED today** |

---

## G — Quality gates (unchanged definitions)

| Gate | RB02 note |
|------|-----------|
| Architecture review | This deposit |
| Real-stack development | Blocked without separate code authorization |
| Client showcase | CX01 residuals + I08 acceptance pack (draft PRs #51 / Product #3) |
| Founder human UAT | **DEFERRED** on showcase rows per RB01 K.3 |
| Production readiness | **[PROD]** ADR rows; provider/spend (SRC-05) |

---

## H — Capacity preflight & RB03 handoff

### H.1 — Documented capacity evidence (@ pinned repos)

| Evidence type | Finding |
|---------------|---------|
| Named FTE / role roster in Architecture, Product, Backend, Frontend, Infra @ pin | **NOT FOUND** — no headcount or dedicated lane assignments in governed docs |
| Engineering ownership fields | Discovery templates use `technical_owner: ""` / UNKNOWN pattern — not staffing truth |
| Closed slice closeouts (roadmap) | Named **merge SHAs** and programme IDs (TOS-DEV04…DEV10, S01–S04, CX01) prove **historical delivery events**, not sustainable throughput or future calendar |
| Cursor Cloud Agent cadence | **Explicitly excluded** as capacity proof per Issue #64 / SRC-04 |
| Cross-PR review latency | **UNKNOWN** — not recorded in Git |
| Integration test environment | Backend/Frontend CI exists; Architecture **NO CI**; **no RB02 re-run receipt** |

### H.2 — Conditional capacity scenarios (**not dates**)

| Scenario | Assumption | Effect on planning (qualitative) |
|----------|------------|-----------------------------------|
| **Serial governed Cursor** | One governed implementation lane; **Chief architecture/PR review** serializes merge-ready packets on the dev critical path | RB01 §H.3 notional **25–35 workweek** V1 band remains **illustrative only**; SRC-04 blocks ratification. **Founder human UAT is a separate subsequent gate** (deferred until after development completion) — **not** a prerequisite to *development readiness* |
| **Bounded two-lane team** | Two non-colliding lanes (e.g. Backend hint DAG ∥ Frontend CX01 verification) where DAG allows | May reduce **eligible** parallel M-equivalents; integration/E2E still serializes; **not** guaranteed 2× calendar speed |

**RB03 proposed acceptance gate (planning stage — not authorized):**

1. Founder completes SRC-04 checklist (§J.4).
2. Chief + Product Architecture ratify atomic acceptance for each row still **NEEDS_FOUNDER_RATIFICATION**.
3. Bottom-up packet list with dependencies (ADR-063 DAG, EX01/DR01 reconciliation, CX01 I08) sized in **S/M/L/XL** with **named owners** — no calendar until steps 1–2 complete.
4. Explicit **[PROD]** charter separated (SRC-05).

### H.3 — PK-HINT-A first code candidate (**proposal — NOT AUTHORIZED**)

Per RB01 §J / ADR-063: **Backend-only** `education.worksheet@2` registration, guarded append + fail-closed HTTP negatives, staged review attestation hooks — **excludes** Student hint GET, Teacher UI, published hint-bearing client use. Requires **separate Founder code authorization**; RB02 does not authorize merge.

---

## I — Twelve `SOURCE_RECONCILIATION` reconciliations (RB01 §K.0)

### I.0 — Independent accounting (recounted from §I.1 — labels may overlap)

| Metric | Count | Rule |
|--------|------:|------|
| **ID_ADDRESSED** | **12** | Every RB01 `SOURCE_RECONCILIATION` ID has exactly one §I.1 block |
| **RELATED_SOURCE_FOUND (RSF=Y)** | **9** | Rows with reproducible related GitHub source — **not** 12 atomic contracts |
| **NO_MATCHING_ATOMIC_SOURCE (NMAS=Y)** | **6** | TOS-IND, STU-A11Y, EIS-CUR, EIS-ALIGN, ECO-SDK, ECO-AN |
| **FOUNDER_DECISION_PENDING (FDP=Y)** | **12** | All rows remain `SOURCE_RECONCILIATION` bind until ratified |
| FDP — Product / Experience ratification | **10** | Rows marked **FDP: Product ratify** in §I.1 |
| FDP — Forward ADR + programme acceptance (atomic) | **2** | EIS-CUR, EIS-ALIGN (**FDP: Forward ADR**) |
| Promoted to **APPROVED_AGREED** without ratification | **0** | |

**Count interpretation:** RSF, NMAS, and FDP are independent, overlapping flags. **Three** requirements (TOS-IND, EIS-CUR, EIS-ALIGN) need a forward architecture decision; **two** (EIS-CUR, EIS-ALIGN) use Forward ADR as their *primary* FDP category, while TOS-IND's primary FDP category is Product ratification with an additional forward-ADR dependency.

**Forbidden misread:** **12 ID_ADDRESSED ≠ 12 RSF=Y ≠ 12 atomic contracts.** Teacher ENG-A11Y does **not** establish Student a11y; TLM packaging OQ does **not** establish SDK; no Founder analytics spec @ pin.

### I.1 — Per-requirement register (Issue #64 fields)

#### RB01-TOS-LOOP

| Field | Value |
|-------|-------|
| Original sources | [PA-LOOP-001 `DAILY_LEARNING_LOOP.md`](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/product-architecture/teacher-os/DAILY_LEARNING_LOOP.md) L1–41; [ADR-AIEOS-057](../decisions/ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md) L36–44; RB01 K.8 |
| Authority | PA loop **Draft**; ADR-057 **Frozen/Approved** (DEV10 boundary only) |
| Code / test @ pin | Backend `src/aieos/domains/teaching/` (DEV04–DEV10); tests e.g. `tests/domains/teaching/test_tos_dev10_i04_http_postgres.py` @ `637583f42…`; FE teacher-os shell @ `569ef8be…`; **EVIDENCE_GAP:** loop-complete Product E2E not re-run @ RB02 pin |
| Acceptance (+ negatives) | **Accept:** named Product E2E or closeout replay proves Intent→Prepare→Teach→Assess→Improve for one governed scenario; tenant-safe; no cross-class leakage. **Reject:** broken stage handoff; answer-key surfacing in teacher primary UI |
| Size | **M** · confidence **RB01-aligned** |
| Prerequisite / next packet | Ratify PA-LOOP-001; SRC-03 Indian mission brief; Experience Depth tranche |
| Unresolved | Observe nav (TLM-001 OQ #4); PPT/sketch/week-plan gaps in PA table |
| Owner / domain | Product Architecture · Teacher OS |
| Next gate | Founder SRC-03 + PA sign-off |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify** |

#### RB01-TOS-A11Y

| Field | Value |
|-------|-------|
| Original sources | [ENG-A11Y-001](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/engineering/ACCESSIBILITY_STANDARDS.md) L9–36; [ENGINEERING_CONSTITUTION.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/engineering/ENGINEERING_CONSTITUTION.md) L109 |
| Authority | Engineering standards **Draft** — not frozen ADR |
| Code / test @ pin | FE `src/features/teacher-os/teach/execution.a11y.test.tsx` (TOS-DEV07-I03 Teach); docs cite `tosDev02.a11y.test.tsx` — **EVIDENCE_GAP:** Mission + Review Queue + primary nav axe CI @ pin **NOT_CHECKED** in RB02 |
| Acceptance (+ negatives) | **Accept:** ENG-A11Y surfaces pass axe in CI + keyboard pass recorded; WCAG AA contrast on primary CTAs. **Reject:** icon-only controls without names; lifecycle by colour alone |
| Size | **M** · **RB01-aligned** |
| Prerequisite / next packet | Approve ENG-A11Y-001 as binding; FE CI axe expansion packet |
| Unresolved | AA vs AAA; waiver policy |
| Owner / domain | Frontend + Product |
| Next gate | Product Architecture approves ENG-A11Y-001 |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify** |

#### RB01-TOS-IND

| Field | Value |
|-------|-------|
| Original sources | [school-context.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/context/school-context.md) L18–29 (**Draft** — calendar/board/medium); [ADR-AIEOS-062 §4](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) **four ports only** |
| Authority | Product context **Draft**; ADR-062 **Frozen** — **does not** authorize calendar/board/medium API |
| Code / test @ pin | Backend [`DevelopmentCoherentSchoolContextProvider`](https://github.com/eduvijna-ai/eduvijna-aieos-backend/blob/637583f42b7c475ef83f6f99bca7e65e665a253d/src/aieos/development/coherent_school_context.py) — ClassRef / membership / Principal scope / Parent learner access only; tests `tests/development/test_aieos360_s04_i01_coherent_school_context.py`, `test_aieos360_s04_i02_architecture.py` @ `637583f42…` — **no** term/holiday/board/medium contract |
| Acceptance (+ negatives) | **Future (post forward ADR/port):** governed **institutional read-model** (or ERP-LIVE adapter) exposes term/holiday/board/medium to Teacher OS without widening ADR-062 four ports; teacher does not re-type institutional facts. **Reject:** silently extending S04 ports; competing roster SoR (ADR-062 external master). **Today @ pin:** assert only four-port coherence — **not** Indian calendar UX complete |
| Size | **M** · **hypothesis** (UX) + **XL** if new port/adapter (**UNKNOWN** split until ADR) |
| Prerequisite / next packet | SRC-03 ratification → **separate** architecture decision for institutional read-model / ERP-LIVE; **not** S04 port expansion by implication |
| Unresolved | ERP field SoT (TLM-001 OQ #3); vernacular-medium P0 (OQ #7) |
| Owner / domain | Product + Architecture (Admin/ERP programme) |
| Next gate | Forward ADR for read-model; ERP-LIVE charter |
| RSF / NMAS / FDP | **Y** (Draft product intent) / **Y** (no atomic port spec) / **Y — Product ratify + forward ADR** |

#### RB01-STU-A11Y

| Field | Value |
|-------|-------|
| Original sources | ENG-A11Y-001 scope = Teacher OS only @ Product pin; **no** Student ENG-A11Y addendum |
| Authority | **No matching atomic standard** — constitution principles only |
| Code / test @ pin | FE `src/features/student-os/` routes @ `569ef8be…`; **EVIDENCE_GAP:** no `*.a11y.test.tsx` under student-os @ pin; **NOT_CHECKED** |
| Acceptance (+ negatives) | **Accept:** Student assign→attempt→submit keyboard-complete; focus order; no PII in AT labels; timed-attempt policy documented. **Reject:** focus trap without policy; hint/answer leakage via AT (ADR-063 posture) |
| Size | **M** · **hypothesis** |
| Prerequisite / next packet | Founder approves Student scope on ENG-A11Y-001 + FE axe tests |
| Unresolved | Parity target with Teacher; accommodation rules |
| Owner / domain | Product + Frontend |
| Next gate | Product Architecture addendum |
| RSF / NMAS / FDP | **N** / **Y** / **Y — Product ratify** |

#### RB01-PRI-UX

| Field | Value |
|-------|-------|
| Original sources | [personas/principal.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/personas/principal.md) (**Draft**); ADR-060 frozen aggregates |
| Authority | Persona **Draft**; S02 API **Frozen** |
| Code / test @ pin | FE `src/features/principal-os/school-intelligence/` + `school-intelligence.page.test.tsx`; Backend principal-os OpenAPI @ pin; S02 programme closeout cited RB01 K.1 — **EVIDENCE_GAP:** UX-depth UAT @ pin |
| Acceptance (+ negatives) | **Accept:** privacy-safe school intelligence IA; empty/error states; **no** learner drill-down rows. **Reject:** individual learner identifiers/scores (ADR-060); cross-tenant scope bleed |
| Size | **M** · **RB01-aligned** |
| Prerequisite / next packet | SRC-03 role-depth brief → Experience Depth FE packet |
| Unresolved | Hindi/English copy (SRC-03) |
| Owner / domain | Product Architecture · Principal OS |
| Next gate | SRC-03 ratification |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify** |

#### RB01-PAR-UX

| Field | Value |
|-------|-------|
| Original sources | [personas/parent.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/personas/parent.md); ADR-061 |
| Authority | Persona **Draft**; ADR-061 **Frozen** |
| Code / test @ pin | FE `src/features/parent-os/` + `parent-home.page.test.tsx`, `parent-child.page.test.tsx`; S03 API @ pin — **EVIDENCE_GAP:** consent/copy depth vs persona |
| Acceptance (+ negatives) | **Accept:** ADR-061-permitted lifecycle vocabulary only; teacher-approved comms drafts. **Reject:** `EVALUATION_EXISTENCE=NO` violations; score disclosure |
| Size | **M** · **RB01-aligned** |
| Prerequisite / next packet | SRC-03 multilingual/comms scope → Experience Depth |
| Unresolved | Multilingual parent drafts vs ADR-061 |
| Owner / domain | Product Architecture · Parent OS |
| Next gate | SRC-03 + PAR-SCORE remains forbidden |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify** |

#### RB01-EIS-CUR

| Field | Value |
|-------|-------|
| Original sources | [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) EIS family; [PRODUCT_VISION.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/vision/PRODUCT_VISION.md) **Draft** |
| Authority | Roadmap family **Approved**; competency graph **not frozen** |
| Code / test @ pin | **NOT_STARTED** @ Backend pin — no curriculum graph SoR module; **EVIDENCE_GAP** |
| Acceptance (+ negatives) | **Accept (post ADR):** tenant-scoped graph SoR; import for one board/grade pilot; no shadow roster. **Reject:** cross-tenant graph reads; auto student profiling without policy |
| Size | **XL** · **RB01-aligned** |
| Prerequisite / next packet | Forward ADR (SoR + API) → EIS programme charter post-V1 |
| Unresolved | Native graph vs external CMS; ADR-024 SoR alignment |
| Owner / domain | Architecture + Product |
| Next gate | **Forward ADR** + Founder programme acceptance |
| RSF / NMAS / FDP | **Y** (family) / **Y** / **Y — Forward ADR** |

#### RB01-EIS-ALIGN

| Field | Value |
|-------|-------|
| Original sources | Roadmap EIS programme; capability-mapping references — **no** ALIGN ADR or atomic spec @ pin |
| Authority | Roadmap family only |
| Code / test @ pin | **NOT_STARTED** — **EVIDENCE_GAP** |
| Acceptance (+ negatives) | **Accept:** alignment output is reviewable report; teacher approval before publish; ContentVersion path enforced. **Reject:** auto-publish; bypass review queue |
| Size | **XL** · **hypothesis** |
| Prerequisite / next packet | EIS-CUR ADR → ALIGN engine programme |
| Unresolved | ML vs rules-first |
| Owner / domain | Product + Architecture |
| Next gate | **Forward ADR** after EIS-CUR |
| RSF / NMAS / FDP | **Y** (family) / **Y** / **Y — Forward ADR** |

#### RB01-EIS-ML

| Field | Value |
|-------|-------|
| Original sources | [NORTH_STAR.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/vision/NORTH_STAR.md) L61; school-context language layer (**Draft**) |
| Authority | Vision **Draft** / SRC-03 |
| Code / test @ pin | Backend `StructuredModelGateway` (Fake/Groq dev paths) — **no** governed multilingual product tests @ pin; **EVIDENCE_GAP** |
| Acceptance (+ negatives) | **Accept:** explicit supported-medium list; human-reviewed parent/artifact language quality rubric. **Reject:** unchecked MT to parents; cross-tenant language profile leakage |
| Size | **L** · **hypothesis** |
| Prerequisite / next packet | SRC-03 workshop → content/policy ADR or Product standard |
| Unresolved | P0 languages for Indian schools |
| Owner / domain | Founder + Product |
| Next gate | SRC-03 ratification |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify** |

#### RB01-ECO-SDK

| Field | Value |
|-------|-------|
| Original sources | [TLM-001 OPEN_QUESTIONS §Ecosystem](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/reviews/review-packages/TLM-001/OPEN_QUESTIONS.md) — **no** SDK spec |
| Authority | Open question only — **not** an SDK contract |
| Code / test @ pin | **NOT_STARTED** — no SDK package in Backend/Frontend/Product @ pin |
| Acceptance (+ negatives) | **Accept (post scope ADR):** documented SDK boundary, OAuth/tenant model, versioning. **Reject:** marketplace monetization without TO_RATIFY ADR; write access without authz kernel |
| Size | **XL** · **UNKNOWN** |
| Prerequisite / next packet | SRC-02 evidence → ecosystem ADR |
| Unresolved | Packaging narrative (OQ #17) |
| Owner / domain | Founder / Product |
| Next gate | SRC-02 checklist |
| RSF / NMAS / FDP | **N** / **Y** / **Y — Product ratify + SRC-02** |

#### RB01-ECO-AN

| Field | Value |
|-------|-------|
| Original sources | **SOURCE_NOT_ACCESSIBLE** @ pin — no Founder analytics spec in governed repos |
| Authority | **SOURCE_REQUIRED** |
| Code / test @ pin | **NOT_STARTED** — **EVIDENCE_GAP** |
| Acceptance (+ negatives) | **Accept (post spec):** Founder read-only ops dashboard; tenant-level aggregates; PII minimization. **Reject:** student-level rows in Founder views |
| Size | **L** · **UNKNOWN** |
| Prerequisite / next packet | SRC-02 Founder evidence → Product Architecture brief |
| Unresolved | Overlap with module analytics |
| Owner / domain | Founder |
| Next gate | SRC-02 item |
| RSF / NMAS / FDP | **N** / **Y** / **Y — SRC-02 + Product ratify** |

#### RB01-QA-OBS

| Field | Value |
|-------|-------|
| Original sources | [ENG-OBS-001](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/engineering/OBSERVABILITY_STANDARDS.md); ADR-037 defers prod observability backend |
| Authority | ENG standards **Draft**; **[PROD]** SLOs separate |
| Code / test @ pin | Backend audit/correlation patterns (e.g. `platform/security/audit/`); **EVIDENCE_GAP:** `mission.viewed` / ENG-OBS event table emission **NOT_CHECKED** @ pin; no product SLO dashboards |
| Acceptance (+ negatives) | **DEV:** emit ENG-OBS Teacher OS events PII-safe in dev; smoke latency budgets. **PROD ([PROD] gate):** SLO/alert contract per SRC-05 — out of V1 dev CP. **Reject:** PII in logs; silent publish-without-approved |
| Size | **M** (DEV instrumentation) · **L** ([PROD] SLO) · **hypothesis** |
| Prerequisite / next packet | DEV telemetry packet ∥ **[PROD]** observability charter (SRC-05) |
| Unresolved | DEV vs PROD boundary |
| Owner / domain | Platform engineering |
| Next gate | Split DEV vs PROD acceptance |
| RSF / NMAS / FDP | **Y** / **N** / **Y — Product ratify (DEV) + [PROD] charter** |

*All twelve rows retain programme intent under **NO_CUT**; none removed.*

---

## J — SRC register dispositions (five topics)

### J.1 — SRC-01 Post-December programme families

| Family | RB01 anchor | Atomic candidates (non-exhaustive — **NO_CUT**) | Approved vs conditional | Unresolved subdecisions |
|--------|-------------|---------------------------------------------------|-------------------------|-------------------------|
| Experience Depth | RB01-PHASE-ED; K.8–K.10 | TOS-LOOP/A11Y/IND; STU-A11Y; PRI/PAR-UX; polish CX01 I03–I04 | Loop **partial** @ DEV10; depth rows **Draft/SRC** | SRC-03 thresholds; Observe nav; Student a11y addendum |
| ERP / School Ops | RB01-PHASE-ERP; K.11 | ADM-OS; ERP-LIVE adapter; **not** ERP-ROSTER (forbidden) | S04 **DONE** synthetic; live ERP **NOT_STARTED** | External SoT precedence; production credentials (SRC-05) |
| EIS + Knowledge | RB01-PHASE-EIS; K.12 | EIS-CUR; EIS-ALIGN; EIS-ML; STU-MAST (**VISION**) | EIS-DET **DONE** bounded; graph **NOT_STARTED** | Graph SoR; ML vs rules; mastery TO_RATIFY |
| Agents / MCP / AI Eng | RB01-PHASE-AGENT; K.13 | AGT-MCP; AGT-ORCH; TOS-PLAN | Gateway **PARTIAL**; MCP **deferred** | MCP scope; multi-agent TO_RATIFY |
| Ecosystem / Developer | RB01-PHASE-ECO; K.14 | ECO-SDK; ECO-AN; ECO-XPLAT (**VISION**) | **SOURCE_REQUIRED** / Vision | Packaging narrative; SDK boundary |

**Disposition:** **SOURCE_FOUND** for roadmap + matrix mapping; family-level acceptance checklists **NEEDS_FOUNDER_RATIFICATION** before RB03 sizing.

### J.2 — SRC-02 External vision / conversations

**Provable from GitHub @ pin:** Product vision/PA/EBP markdown; Architecture ADRs; closed programme closeouts in [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md); Issue #62/#64 programme authorization text.

**Not provable (no access in this workday):** Private Founder chat transcripts; oral scope agreements; vendor commitments; staffing agreements.

**Founder evidence-request checklist (minimal):**

1. Any written scope **outside GitHub** for ecosystem SDK, Founder analytics, marketplace/monetization, or multi-agent classroom — deposit redacted summary or authorize Product Architecture review minutes repo path.
2. Confirm whether **PA-001 / TLM-001** review packages were **Accepted** beyond front-matter `status: draft` (roadmap labels “Approved (product docs)” — reconcile explicit sign-off date/owner).
3. List Indian-school reference schools or board packs intended as **acceptance fixtures** (CBSE/ICSE/state — no inference).
4. Confirm **P0 persona segment** (TLM-001 OQ #6–#8) for Experience Depth acceptance.

**Disposition:** **STILL_SOURCE_REQUIRED** for ECO-* and any conversation-only scope; **NO** invented transcripts or marketplace SoR.

### J.3 — SRC-03 Indian-school fidelity cross-map

| Theme | Product authority @ pin | Linked Req-IDs | RB02 note |
|-------|-------------------------|----------------|-----------|
| Daily loop / Mission | PA-LOOP Draft; vision TEACHER_OS Draft | TOS-LOOP | DEV10 implements generic loop; Indian contextual mission **not ratified** |
| Calendar / periods | school-context Draft | TOS-IND | **Not** implemented as S04 calendar API — requires **forward ADR** read-model / ERP-LIVE |
| Language / medium | school-context; NORTH_STAR Draft | EIS-ML, PAR-UX (comms) | No governed multilingual acceptance |
| Board / curriculum | school-context; journeys academic-year Draft | TOS-IND, EIS-CUR | No graph SoR |
| Accessibility | ENG-A11Y Draft | TOS-A11Y, STU-A11Y | Teacher partial test; Student standard missing |
| Role UX depth | personas Draft; PA shells partial | PRI-UX, PAR-UX | Aggregates frozen; UX depth open |

**Disposition:** **SOURCE_FOUND** (Draft corpus); atomic thresholds **NEEDS_FOUNDER_RATIFICATION**.

### J.4 — SRC-04 Development capacity

**Confirmed:** Programme delivery history exists as **named closed slices** with merge SHAs (roadmap table).

**Unknown (require Founder input):**

| # | Question |
|---|----------|
| 1 | Available engineering headcount (Frontend, Backend, full-stack, QA) and **FTE** fractions |
| 2 | Dedicated educational / Product Architecture review capacity for ContentVersion and hint attestation |
| 3 | Planned leave/blackout through tentative V1 band |
| 4 | Typical Chief Architect + Founder review latency (days) per governed PR |
| 5 | Shared integration environment availability (who maintains; refresh cadence) |
| 6 | Whether a **second human lane** is actually staffed vs serial Cursor-only |

**Disposition:** Capacity model in §H remains **conditional** — **blocks date ratification**.

### J.5 — SRC-05 Production provider / spend

**Confirmed:** ADR-AIEOS-029…051 **[PROD]** rows in RB01 K.5; ADR-037 observability vendor deferred; Groq/OpenAI/Fake are **dev/showcase** paths — not production spend authorization.

**Disposition:** **Separate production gate** — must not mark RB01-QA-OBS or AGT-GW **DONE** as production readiness; no procurement authorized in RB02.

---

## K — Original full AIEOS product-family map (non-omission)

| Family | Representative RB01 IDs | Approved / frozen @ pin | Conditional / draft / source-missing |
|--------|-------------------------|---------------------------|--------------------------------------|
| Teacher OS | TOS-DEV10, CX01, TOS-LOOP, TOS-A11Y, TOS-IND, HINT-* | DEV10/CX01 **DONE/PARTIAL**; ADR-052–057 frozen | Loop depth, a11y, Indian UX **SRC-03**; hints **NOT_STARTED** |
| Student | S01, STU-A11Y, STU-HINT, STU-FB, STU-MAST | S01 **DONE**; hints ADR-063 frozen text | A11y, feedback, mastery **ratify/defer** |
| Principal | S02, PRI-UX, PRI-DRILL | Aggregates **DONE** | UX depth draft; drill **FORBIDDEN** |
| Parent | S03, PAR-UX, PAR-SCORE | Aggregates **DONE** | UX draft; scores **FORBIDDEN** |
| Admin / ERP | S04, ADM-OS, ERP-LIVE, ERP-ROSTER | S04 **DONE** dev synthetic | Live ERP **NOT_STARTED**; roster SoR **FORBIDDEN** |
| EIS / Knowledge | EIS-DET, EIS-CUR, EIS-ALIGN, EIS-ML | Deterministic quality **DONE** bounded | Graph/align/ML **NOT_STARTED / SRC** |
| Agents / MCP / AI | AGT-GW, AGT-MCP, AGT-ORCH, TOS-PLAN | Gateway **PARTIAL** | MCP/orchestration **deferred / vision** |
| Founder / Developer / Ecosystem | ECO-SDK, ECO-AN, ECO-XPLAT | Preserved in matrix | **SOURCE_REQUIRED / vision** |
| Platform / Quality | ADR-022…063, QA-E2E, QA-CI, QA-OBS | Many **PARTIAL**; ADR-063 arch **DONE** authority only | **[PROD]** ADRs off V1 dev CP; OBS product SLOs unset |

**Overlap rule:** Do not double-count K.2 hint rollup with atomic hint rows; do not treat 100 matrix rows as % complete.

---

## L — Traceability summary, blockers, STOP

### L.1 — RB02 reconciliation scorecard (aligned with §I.0)

| Metric | Value |
|--------|------:|
| **ID_ADDRESSED** | **12 / 12** |
| **RELATED_SOURCE_FOUND (RSF=Y)** | **9 / 12** |
| **NO_MATCHING_ATOMIC_SOURCE (NMAS=Y)** | **6 / 12** |
| **FOUNDER_DECISION_PENDING (FDP=Y)** | **12 / 12** (10 Product ratify · 2 Forward ADR) |
| Promoted to **APPROVED_AGREED** without ratification | **0** |
| Silent scope removals | **0** |
| Exact delivery dates ratified | **0** |
| Product code authorized | **0** |
| Architecture CI | **NO CI CONFIGURED** |

### L.2 — SRC blockers for “100% agreed inventory certified”

1. **SRC-02** — external conversation evidence for ecosystem/Founder analytics.
2. **SRC-03** — Indian-school atomic acceptance (calendar, medium, board, a11y).
3. **SRC-04** — staffed lanes and review latency.
4. **PA package status drift** — roadmap “Approved (product docs)” vs review-package YAML `status: draft`.
5. **EX01 / DR01 / SP01** draft PRs — product decisions still open (RB01 K.4).

### L.3 — ADR-063 reminder

Architecture **FROZEN** on `main` @ merge `ebd0f5c…`; implementation **NOT STARTED** @ OpenAPI pin — PK-HINT-A remains **proposal only** (§H.3).

### L.4 — Related documents (not modified)

[AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md](AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md) · [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) · [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) · [Issue #64](https://github.com/eduvijna-ai/eduvijna-architecture/issues/64)

---

**End RB02-P01R1 — await Chief exact-head re-review; no date ratified; no merge; no code authorized.**

**STOP LINE:** `RB02-P01R1 EVIDENCE ACCOUNTING CORRECTED / FULL SCOPE PRESERVED / NO EXACT DATES RATIFIED / NO PRODUCT CODE OR PR MERGE AUTHORIZED / CHIEF EXACT-HEAD REVIEW PENDING`
