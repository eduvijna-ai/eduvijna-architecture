---
id: AIEOS-PROGRAM-RB02
title: Requirements Reconciliation & Development Capacity Preflight (Founder No-Scope-Cut)
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: draft
version: 1.0.0
created: 2026-11-04
last_updated: 2026-11-04
workday: AIEOS-PROGRAM-RB02-P01
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
| Packet | **AIEOS-PROGRAM-RB02-P01** |
| Architecture parent (`main`) | `1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30` (RB01 PR #63 merge) |
| Branch (expected) | `cursor/aieos-program-rb02-reconciliation-2488` |
| RB01 merge reviewed head (#63) | `c141edd3c68605c69ada49c6928ec8792f245abd` |

---

## B — Exact-source gate (re-verified before RB02 write)

Re-verification **2026-11-04**: `git fetch origin main`, `git ls-remote`, `gh pr view`, Backend `tools.release.common` digest helpers on shallow clone @ Backend pin.

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

**Gate:** **PASS** — RB02 write authorized.

**Architecture Actions:** `.github/workflows/.gitkeep` only — **NO CI CONFIGURED** on Architecture repo. Backend/Frontend CI **not re-run** in RB02.

---

## C — Git branch and diff scope

| Field | Value |
|-------|-------|
| Branch | `cursor/aieos-program-rb02-reconciliation-2488` |
| Sole parent commit | `1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30` (Architecture `main` @ RB01 merge) |
| Diff vs `main` | **One file only:** this document |
| Other repos / draft PRs | **Untouched** |

---

## D — Evidence pins & reconciliation conventions

**Pins (read-only):** Backend `637583f42…` · Frontend `569ef8be…` · Product `b4b3048f…` · Infrastructure `a8654e5b…`

**Disposition labels (per row):**

| Label | Meaning |
|-------|---------|
| **SOURCE_FOUND** | Reproducible GitHub source located; atomic acceptance may still be **FOUNDER_RATIFICATION_NEEDED** if authority is Draft/Vision |
| **STILL_SOURCE_REQUIRED** | Programme intent preserved under **NO_CUT**; no authoritative atomic acceptance or external conversation evidence recoverable |
| **NEEDS_FOUNDER_RATIFICATION** | Direction visible in Draft/Vision/Roadmap; not promoted to **APPROVED_AGREED** without Founder/Product Architecture sign-off |

**Privacy / quality negatives (global):** No answer-key or hint leakage (ADR-063); no Principal learner drill-down or Parent evaluation scores without forward ADR (ADR-060/061); no AIEOS roster/enrollment SoR (ADR-062 external master); tenant isolation and ContentVersion immutability unchanged (ADR-027).

**Do not rebuild:** TOS-DEV10/CX01 closed slices; AIEOS360 S01–S04; CX01 operator tooling I01R9–I07 @ Frontend pin — polish, UAT, and verification residuals only.

---

## E — Client-safe status (external)

**Policy (unchanged):** No silent scope cuts; extend dates before quality compromise.

**Real @ pin (development, not production):** Governed Teacher loop through Improve (ADR-057 / TOS-DEV10); Student S01; Principal S02; Parent S03; Admin school-context S04 (synthetic dev provider); CX01 showcase baseline I01R7–I07 with **EVIDENCE_GAP** on fresh CI rerun; ADR-063 **text only** — hint routes absent @ OpenAPI pin.

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
| **Serial governed Cursor** | One governed implementation lane; Chief review + Founder UAT serializes | RB01 §H.3 notional **25–35 workweek** V1 band remains **illustrative only**; SRC-04 blocks ratification |
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

**Summary counts (disposition):**

| Disposition | Count |
|-------------|------:|
| SOURCE_FOUND (partial — Draft/Vision/Roadmap located) | 12 |
| STILL_SOURCE_REQUIRED (atomic acceptance or external conversation) | 5 |
| NEEDS_FOUNDER_RATIFICATION | 12 |

*All twelve rows retain programme intent under **NO_CUT**; none removed.*

### I.1 — Reconciliation table

| Req-ID | Original sources (repo @ `b4b3048f…` / Architecture @ pin) | Authority | Implementation @ pin | Missing behavior & acceptance proposal | Unresolved decision | Owner / domain | Next gate | Disposition |
|--------|--------------------------------------------------------------|-----------|----------------------|----------------------------------------|---------------------|----------------|-----------|-------------|
| **RB01-TOS-LOOP** | [PA-LOOP-001 `DAILY_LEARNING_LOOP.md`](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/product-architecture/teacher-os/DAILY_LEARNING_LOOP.md) L1–41 (Prepare→Improve); [ADR-AIEOS-057](https://github.com/eduvijna-ai/eduvijna-architecture/blob/1fbbc3567f6955b11d3fa24c3bf2258b8f1c1f30/decisions/ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md) L36–44 DEV10 loop boundary; RB01 K.8 | PA loop doc **Draft**; ADR-057 **Frozen/Approved** for DEV10 boundary | TOS-DEV04–DEV10 domains @ Backend pin; FE teacher-os nav; DEV10 closeout cited RB01 K.1 | **Accept:** Product E2E proves Intent→Prepare→Teach→Assess→Improve handoffs for **one** governed scenario @ pin; **Indian-school Today’s Mission** copy/calendar/context reflects S04 fields without teacher re-entry (see TOS-IND). **Reject:** generic non-Indian mission text when school context populated; broken stage handoff | Observe as first-class nav vs inside Teach (TLM-001 OQ #4); PPT/sketch/week-plan gaps in PA loop table | Product Architecture + Teacher OS | Ratify PA-LOOP-001 + Indian mission checklist (SRC-03) | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-TOS-A11Y** | [ENG-A11Y-001 `ACCESSIBILITY_STANDARDS.md`](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/engineering/ACCESSIBILITY_STANDARDS.md) L9–36; `ENGINEERING_CONSTITUTION.md` L109 | Engineering **Draft/standards** — not frozen ADR | FE `teacher-os/teach/execution.a11y.test.tsx` @ `569ef8be…`; **EVIDENCE_GAP** for Mission/Queue axe gate on all listed surfaces | **Accept:** axe (or equivalent) in CI for Mission, Review Queue, primary nav; manual keyboard pass recorded; WCAG AA contrast on primary CTAs. **Reject:** icon-only controls without accessible names; lifecycle by colour alone | WCAG **AA vs AAA** for Indian deployments; waiver policy for polish-only changes | Frontend + Product | Approve ENG-A11Y-001 as binding for Experience Depth tranche | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-TOS-IND** | [MODEL-SCHOOL-CONTEXT-001 `context/school-context.md`](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/context/school-context.md) L18–29 calendar/curriculum/language; ADR-062 S04 dev provider @ Backend pin | Product context **Draft**; ADR-062 **Frozen** (external ERP master, dev synthetic) | `DevelopmentCoherentSchoolContextProvider` + S04 E2E @ Backend pin — **not** production Indian calendar UX | **Accept:** Teacher Prepare/Today displays inherited **term/holiday/board/medium** from school context API without manual re-entry; dates respect configured holiday week in dev fixture. **Reject:** teacher must re-type board/term for each generate | Which ERP fields are SoT (TLM-001 OQ #3); vernacular-medium P0 (OQ #7) | Product + Admin/ERP programme | SRC-03 ratification + ERP-LIVE boundary (not roster SoR) | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-STU-A11Y** | ENG-A11Y-001 applies to “All Teacher OS UI” only @ Product pin — **no Student-specific ENG doc**; Student shell @ FE pin | **SOURCE gap** for Student atomic standard; constitution principles only | Student-os routes @ FE pin; **no** dedicated student a11y spec or axe suite found @ pin | **Accept:** extend ENG-A11Y-001 scope to Student attempt/submit flows; keyboard-complete assign→submit; focus order on attempt UI; no PII in AT labels. **Reject:** trap focus in timed attempt without escape policy | Parity with Teacher WCAG target; timed assessment accommodations | Product + Frontend | Founder approves Student a11y addendum to ENG-A11Y-001 | **STILL_SOURCE_REQUIRED** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-PRI-UX** | [Principal persona](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/personas/principal.md); PA DRAFT shells — no frozen Principal PA package @ Product pin | **PA DRAFT** / roadmap family | FE `principal-os` shell + OpenAPI S02 aggregates @ pin (ADR-060) | **Accept:** Principal dashboard presents **privacy-safe** school intelligence with role-appropriate IA (no learner drill-down); loading/error/empty states; Hindi/English labels TBD in SRC-03. **Reject:** individual learner rows or scores | Drill-down forbidden unless forward ADR | Product Architecture | Experience Depth tranche after SRC-03 role-depth brief | **SOURCE_FOUND** (persona only) + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-PAR-UX** | [Parent persona](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/personas/parent.md); ADR-061 lifecycle vocabulary | **PA DRAFT** + ADR-061 **Frozen** | FE `parent-os` + S03 API @ pin | **Accept:** Parent sees ADR-061-permitted lifecycle signals with consent/access copy; multilingual message **draft** surfaces remain teacher-approved only. **Reject:** evaluation scores / existence leaks | Multilingual parent comms scope (jobs-to-be-done) vs ADR-061 | Product Architecture | SRC-03 + PAR-SCORE remain forbidden | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-EIS-CUR** | [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) post-Dec EIS family; [PRODUCT_VISION.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/vision/PRODUCT_VISION.md) **Draft** | Roadmap **Approved** family; atomic graph **not frozen** | **NOT_STARTED** — no curriculum graph SoR @ Backend pin | **Accept:** ADR defining competency graph SoR, tenant boundaries, read APIs, and **no** automatic student profiling without policy; seed import for **one** board grade pilot. **Reject:** shadow roster or cross-tenant graph leakage | Native graph vs external CMS; alignment to ADR-024 SoR rules | Architecture + Product | Forward ADR + programme charter post-V1 | **SOURCE_FOUND** (family) + **STILL_SOURCE_REQUIRED** (atomic) |
| **RB01-EIS-ALIGN** | Roadmap EIS programme; capability-mapping references — no ALIGN ADR | Roadmap **Approved** family only | **NOT_STARTED** | **Accept:** alignment job produces **reviewable** mapping report teacher approves before publish; no auto-publish. **Reject:** alignment bypassing ContentVersion review | ML vs rules-first alignment | Product + Architecture | Depends on EIS-CUR ADR | **SOURCE_FOUND** (family) + **STILL_SOURCE_REQUIRED** (atomic) |
| **RB01-EIS-ML** | [NORTH_STAR.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/vision/NORTH_STAR.md) L61 multilingual; [school-context.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/context/school-context.md) L28 language; jobs-to-be-done multilingual drafts | Vision **Draft** / SRC-03 | Model Gateway Fake/Groq @ dev — **no** governed multilingual product acceptance | **Accept:** defined list of **supported mediums** for generated artifacts + parent drafts with human review; measurable quality rubric per language. **Reject:** unchecked machine translation to parents | Which languages P0 for Indian schools | Founder + Product | SRC-03 ratification workshop | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-ECO-SDK** | TLM-001 [OPEN_QUESTIONS.md](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/reviews/review-packages/TLM-001/OPEN_QUESTIONS.md) §Ecosystem; **no** SDK spec @ Product pin | **SOURCE_REQUIRED** / Vision | **NOT_STARTED** — no public SDK package @ repos @ pin | **Accept:** documented SDK scope (read-only integrations vs write); OAuth/tenant model; versioning — **after** Founder defines ecosystem boundary. **Reject:** marketplace monetization without TO_RATIFY ADR | Staged packaging vs single narrative (OQ #17) | Founder / Product | SRC-02 evidence + ecosystem ADR | **STILL_SOURCE_REQUIRED** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-ECO-AN** | No Founder analytics spec in GitHub @ pin; Product vision mentions analytics engines reused, not Founder cockpit | **SOURCE_REQUIRED** | **NOT_STARTED** | **Accept:** role-gated Founder **read-only** operational dashboard spec (tenants, release health, education quality signals) with PII minimization. **Reject:** student-level analytics in Founder views | Overlap with existing module analytics vs new product | Founder | SRC-02 checklist item | **STILL_SOURCE_REQUIRED** + **NEEDS_FOUNDER_RATIFICATION** |
| **RB01-QA-OBS** | [ENG-OBS-001 `OBSERVABILITY_STANDARDS.md`](https://github.com/eduvijna-ai/eduvijna-product/blob/b4b3048fb7a6a1c50ae8619dc490743714f2e3e2/engineering/OBSERVABILITY_STANDARDS.md) L9–54; ADR-037 defers prod observability backend | Engineering standards **Draft**; **[PROD]** observability ADR family separate | Partial structured logging patterns @ Backend; **no** product SLO dashboards @ pin | **Accept (DEV tranche):** Teacher OS telemetry events in ENG-OBS-001 table emitted with PII-safe fields in dev; smoke on mission p95. **Accept ([PROD]):** SLO/alert contract per SRC-05 — **out of V1 dev CP**. **Reject:** PII in logs; publish-without-approved alert silence | DEV vs PROD observability boundary | Platform + **[PROD]** charter | Split acceptance: DEV instrumentation vs PROD SLO gate | **SOURCE_FOUND** + **NEEDS_FOUNDER_RATIFICATION** |

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
| Calendar / periods | school-context Draft | TOS-IND | S04 dev inheritance only |
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

### L.1 — RB02 reconciliation scorecard

| Metric | Value |
|--------|------:|
| `SOURCE_RECONCILIATION` IDs addressed | **12 / 12** |
| IDs with reproducible GitHub source (any authority) | **12** |
| IDs with **STILL_SOURCE_REQUIRED** atomic acceptance | **5** (STU-A11Y, EIS-CUR, EIS-ALIGN, ECO-SDK, ECO-AN) |
| IDs promoted to **APPROVED_AGREED** without Founder ratification | **0** |
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

**End RB02-P01 — await Chief exact-head review; no date ratified; no merge; no code authorized.**

**STOP LINE:** `RB02 SOURCE RECONCILIATION/CAPACITY PREFLIGHT DRAFT DEPOSITED / FOUNDER FULL SCOPE PRESERVED / NO EXACT DATES RATIFIED / NO PRODUCT CODE OR PR MERGE AUTHORIZED / CHIEF EXACT-HEAD REVIEW PENDING`
