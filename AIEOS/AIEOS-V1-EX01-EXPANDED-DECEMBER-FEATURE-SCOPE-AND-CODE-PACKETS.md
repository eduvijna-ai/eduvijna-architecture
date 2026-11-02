---
id: AIEOS-V1-EX01
title: V1-EXPAND December Feature Scope Freeze & First Code Packets
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: proposed — founder ratification pending
version: 1.0.0
created: 2026-11-02
last_updated: 2026-11-02
reviewers:
  - Founder / Product Architecture
  - Chief AI Enterprise Architect
---

# AIEOS-V1-EX01 — V1-EXPAND December Feature Scope & First Code Packets

**Identity:** `AIEOS-V1-EX01`  
**Mode:** Architecture evidence, candidate de-duplication, named P0/P1 proposal, and **first genuine code workday handoff** — **no application code in this workday**  
**Founder direction:** [`V1-EXPAND` selected 2026-11-02](https://github.com/eduvijna-ai/eduvijna-architecture/issues/52#issuecomment-6575261649) — **direction only**; **named December features remain `PROPOSED — FOUNDER RATIFICATION PENDING`**  
**Terminal target:** `AIEOS-V1-EX01 — V1-EXPAND DIRECTION ACCEPTED / NAMED FEATURE SCOPE PROPOSED / REAL CODE WORKDAY READY FOR FOUNDER APPROVAL / NOT MERGED`

**Primary authority (read-only):**

- [Issue #54 — master 12-task workday](https://github.com/eduvijna-ai/eduvijna-architecture/issues/54)
- [DR01 PR #53](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53) (OPEN / DRAFT, base `491295c3…`)
- [W01 showcase gap baseline](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md) (frozen on Architecture `main`)
- Frozen ADR-AIEOS-052…062 under [`decisions/`](../decisions/)
- Governed application repos at pins in §A (read-only verification)

**Non-claims (binding):** Development Slice Complete ≠ Client Showcase Ready ≠ Production Ready ≠ Founder UAT. No production deployment, no paid provider calls, no REAL_AI success assertion in standard CI, no new Business SoRs, and no silent promotion of 2027 programme items into December without explicit Founder scope change.

---

## A. Authority gate (EX01-01) — PASS

Verified **2026-11-02** against remote `origin/main` (not local cache alone).

| Authority | Required `origin/main` | Verified SHA | Method |
|-----------|------------------------|--------------|--------|
| Architecture | `491295c3cf0a151f31686a6a2e1a2176cd92c782` | **MATCH** | `git fetch origin main` + `git rev-parse origin/main` |
| Product | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | shallow clone + `git fetch` |
| Backend | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | shallow clone + `git fetch` |
| Frontend | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** | shallow clone + `git fetch` |
| Infrastructure | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | shallow clone + `git fetch` |
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** | `sha256sum` on Backend pin |
| Alembic head | `a360s010004` | **MATCH** | `migrations/versions/a360s010004_*.py` on Backend pin |

**Architecture worktree:** clean tracked tree at `491295c3…` before branch creation. **EX01 branch:** `cursor/aieos-v1-ex01-expand-scope-287c` (parent = exact pin above).

| Governance item | Required state | Verified |
|-----------------|----------------|----------|
| Founder `V1-EXPAND` decision | Recorded on Issue #52 | **PASS** — [`eduvijna` comment 2026-11-02](https://github.com/eduvijna-ai/eduvijna-architecture/issues/52#issuecomment-6575261649) |
| CX01-I07 integrated rehearsal | Merged + green CI on Frontend `main` | **PASS** — merge `569ef8b` ([Frontend PR #47](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/47)); GitHub Actions `conclusion: success` at `569ef8be…` |
| DR01 PR #53 | OPEN / DRAFT, base `491295c3…` | **PASS** — `headRefOid` `70986a013ce776257f739eff6ab89727d6715df9` |
| I08 Architecture PR #51 | OPEN / DRAFT | **PASS** — title `AIEOS360-CX01-I08 — Founder acceptance evidence…` |
| Product PR #3 (I08-P) | OPEN / DRAFT | **PASS** |
| Architecture GitHub Actions | No workflow configured | **PASS (honest)** — [`.github/workflows/.gitkeep`](../.github/workflows/.gitkeep) only → **NO CI CONFIGURED**, not claimed green |
| Other governed PRs modified in EX01 | None | **PASS** |

**Gate result:** **PASS** — proceed with Architecture-only document on new branch.

---

## B. Programme dates vs original vision (EX01-02)

| Milestone | Date | Meaning for this proposal |
|-----------|------|---------------------------|
| **AIEOS 360 Client Showcase (engineering)** | **2026-11-20** | Cross-role NON_PRODUCTION rehearsal quality; CX01-I01R9–I07 substrate largely satisfies deterministic integrated proof at Frontend pin |
| **AIEOS v1 development readiness** | **2026-12-18** | Major persona experiences **functional and integrated** under ratified V1-EXPAND named scope — **not** full original AIEOS architecture |
| Experience Depth Complete | 2027-01-29 | **Preserved — deferred** |
| ERP / School Operations Complete | 2027-02-26 | **Preserved — deferred** |
| Educational Intelligence + Knowledge | 2027-03-26 | **Preserved — deferred** |
| Agentic AI + MCP + AI Engineering Platform | 2027-04-23 | **Preserved — deferred** |
| Ecosystem | 2027-05-21 | **Preserved — deferred** |
| Full Original AIEOS Development Complete | 2027-05-28 | **Preserved — deferred** |

**Distinction:** Items in §C marked `PROPOSED` are **illustrative engineering packets** until Founder ratifies named scope. **`AIEOS-V1-C01` (Architecture closeout record)** is documentation reconciliation — **not** a December feature code packet.

---

## C. Candidate evidence matrix (EX01-03 / EX01-05)

Legend: **Classification** = de-duplication outcome; **ADR gate** = feasibility for December code without new ADR bodies.

| ID | Summary | Classification | ADR gate | Source evidence (Frontend `569ef8be…` / Backend `637583f42…` unless noted) |
|----|---------|----------------|----------|-------------------------------------------------------------------------------|
| **EX-C01** | REAL_AI generation → ContentVersion → Publish/Assign **integrated** showcase proof | **`SOURCE_VERIFIED_MISSING`** (operator segment) | **`NO_ADR_NEEDED`** for wiring/docs/guard; **`FOUNDER_PROVIDER_APPROVAL_REQUIRED`** before any paid call or REAL_AI CI assertion | I06 mode scripts (`scripts/aieos360-cx01-i06-showcase-ai-mode/`); I07 matrix row REAL_AI = **PENDING** ([`docs/AIEOS360-CX01-I07-COVERAGE-MATRIX.md`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-COVERAGE-MATRIX.md)); TOS-CX01 Teacher-only historic Real-AI proof unchanged |
| **EX-C02** | Student practice / feedback v1 (no mastery, no Parent evaluation) | **`SOURCE_VERIFIED_MISSING`** (bounded UX only) | **`NO_ADR_NEEDED`** if **presentation-only** learner-safe copy; **`NEW_ADR_REQUIRED`** if learner-visible scores/evaluation feedback | ADR-AIEOS-058 one-attempt; ADR-AIEOS-061 Parent `EVALUATION_EXISTENCE = NO`; Student submit UX ends at `"Work submitted."` ([`AttemptPage.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/student-os/attempts/AttemptPage.tsx)) — no learner evaluation surface |
| **EX-C03** | Teacher Assessment Intelligence → deliberate Improve explanatory UX | **`MOSTLY_ALREADY_IMPLEMENTED`** | **`NO_ADR_NEEDED`** for residual polish | S01-I05-F1 intelligence presentation + Assess UI; showcase Improve link ([`AssessPage.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/teacher-os/assess/AssessPage.tsx)); launcher story stage **Improve** ([`roleUrls.ts`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/aieos360-showcase/roleUrls.ts)); I07 step 6 automated guard |
| **EX-C04** | Principal/Parent explanatory presentation within DTO allowlists | **`MOSTLY_ALREADY_IMPLEMENTED`** | **`NO_ADR_NEEDED`** | CX01-I04 Student presentation tests; Principal/Parent presentation modules + showcase handoffs ([`schoolIntelligencePresentation.ts`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/principal-os/school-intelligence/schoolIntelligencePresentation.ts), [`parentPresentation.ts`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/parent-os/parentPresentation.ts)); ADR-060 aggregate-only / ADR-061 lifecycle vocabulary |
| **EX-C05** | NON_PRODUCTION showcase operator continuity (no credential shortcuts) | **`SOURCE_VERIFIED_MISSING`** | **`NO_ADR_NEEDED`** | I01R9 managed stack + launcher exist; preflight still requires **manual per-tab DEV session** ([`docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md) §Steps 5–6, §Limitation) |
| **EX-C06** | Educational quality v1 gap | **`ALREADY_IMPLEMENTED`** | **`DEFER_2027`** for EIS depth | DEV04/DEV10 + OpenAPI `EducationalQuality`; [`qualityPresentation.ts`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/teacher-os/work/qualityPresentation.ts) |

**W01 de-duplication note:** W01 (at Architecture `491295c3…`) classified unified launcher / cross-role rehearsal as gap **D**. CX01-I01R9–I07 on Frontend `569ef8be…` **closes the deterministic integrated substrate** (launcher, continuity, mode truth, 10/10 same-run guard). W01 rows **UX-03** (Teacher dual chrome) and deep Experience Depth polish remain **2027-01-29** unless explicitly pulled into a ratified V1-EXPAND packet.

---

## D. Product benefit & acceptance (EX01-04)

### Proposed P0-1 — `V1-EXPAND-PKG-S05` (EX-C05)

| Field | Content |
|-------|---------|
| **User problem** | Presenters lose time and make connection errors wiring four role tabs before a client rehearsal. |
| **Visible impact** | Launcher + orchestrator expose a **credential-free role connection checklist** tied to the coherent showcase fixture; DEV session fields can be prefilled from localhost-only hints (tenant / role labels) while bearer paste stays memory-only. |
| **Minimal feature** | NON_PRODUCTION presenter continuity helper — **not** SSO, not token-in-URL, not production identity. |
| **Success** | Operator completes four-tab preflight with fewer steps; sanitized manifest/status JSON still contains **no bearer tokens**; I07 deterministic rehearse unchanged. |
| **Failure / negative** | Any token in URL/query/localStorage; cross-tenant hint leakage; production ERP/Admin OS semantics. |

### Proposed P0-2 — `V1-EXPAND-PKG-S02A` (EX-C02 bounded)

| Field | Content |
|-------|---------|
| **User problem** | After submit, students see only `"Work submitted."` with no learner-safe explanation of what happens next. |
| **Visible impact** | Post-submit panel explains **teacher review / school process** vocabulary without scores, mastery, or evaluation payloads. |
| **Minimal feature** | Frontend presentation + copy tests only — **no new API fields**. |
| **Success** | Submitted attempt view shows bounded next-step copy; Parent/Principal surfaces unchanged; ADR-061 constraints preserved in tests. |
| **Failure / negative** | Any learner-visible evaluation score; recommendation engine copy; new Backend SoR. |

### Proposed P0-3 (conditional) — `V1-EXPAND-PKG-REAL-AI-360` (EX-C01)

| Field | Content |
|-------|---------|
| **User problem** | Client story cannot demonstrate live provider generation through Publish/Assign on the **same** cross-role substrate as deterministic I07. |
| **Visible impact** | Optional operator-only REAL_AI rehearsal segment with provenance labels on Teacher Prepare → ContentVersion lineage. |
| **Gate** | **`FOUNDER NAMED-SCOPE + PROVIDER APPROVAL PENDING`** — no mandatory REAL_AI in default CI; deterministic I07 remains authoritative guard. |
| **Failure / negative** | Provider secrets in repo/CI; automatic paid calls in GitHub Actions; Fake gateway bypass in standard CI. |

---

## E. Cross-role composition (EX01-06)

**Canonical scenario:** `AIEOS360-CX-SCENARIO-01` / ADR-AIEOS-062 coherent NON_PRODUCTION facts ([ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)).

**Spine (unchanged):** Teacher Prepare/Publish/Assign → Student Attempt/Submit → explicit learner evaluation (Teacher Assess intelligence) → Teacher Improve (deliberate) → Principal aggregate read → Parent authorized-child lifecycle read.

**Privacy negatives (must remain in all packet tests):**

- Student B / wrong-tenant assignment or attempt **deny** (existing I07 tenant negative + S04 patterns).
- Parent: **`EVALUATION_EXISTENCE = NO`** — no child scores ([ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)).
- Principal: **aggregate-only** — no learner drill-down ([ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md)).

Proposed P0 packets **must not** alter Backend DTO allowlists or evaluation SoR.

---

## F. Recommended named scope (EX01-07) — `PROPOSED — FOUNDER RATIFICATION PENDING`

**Constraint:** ≤3 P0 December code packets; each independently testable.

| Priority | Package ID | Maps | Repo | Effort | ADR | Value |
|----------|------------|------|------|--------|-----|-------|
| **P0** | **`V1-EXPAND-PKG-S05`** | EX-C05 | Frontend (+ I01R9 orchestrator scripts) | **M** | NO_ADR_NEEDED | Closes largest **honest** Nov/Dec rehearsal friction without security shortcuts |
| **P0** | **`V1-EXPAND-PKG-S02A`** | EX-C02 (bounded) | Frontend | **S** | NO_ADR_NEEDED (presentation-only) | Student journey completeness without forbidden evaluation disclosure |
| **P0 (conditional)** | **`V1-EXPAND-PKG-REAL-AI-360`** | EX-C01 | Frontend + Backend config/docs | **L** | NO_ADR_NEEDED + **provider approval** | Optional client differentiation — **not** default first sprint |

| Priority | Package ID | Maps | Note |
|----------|------------|------|------|
| **P1** | **`V1-EXPAND-PKG-C03-POLISH`** | EX-C03 residual | Assess → Improve presenter handoff copy / showcase external handoff parity — polish only |
| **P1** | **`V1-EXPAND-PKG-C04-POLISH`** | EX-C04 residual | Principal/Parent narrative continuity vs Teacher CX01 bar — polish only |
| **P1** | **`V1-EXPAND-PKG-UX03`** | W01 UX-03 | Teacher dual chrome cleanup — defer to **2027-01-29 Experience Depth** unless Founder promotes |
| **Deferred** | EIS / ERP / Agents / Admin OS | EX-C06 / programme | Locked 2027 dates in §B |

**Critical path (if Founder ratifies P0-1 → P0-2 → optional P0-3):**

1. Ratify named list (this document).  
2. **`V1-EXPAND-PKG-S05`** — unblocks reliable human rehearsal for Nov20 engineering milestone.  
3. **`V1-EXPAND-PKG-S02A`** — parallel Frontend lane after S05 launcher/orchestrator contract frozen.  
4. **`V1-EXPAND-PKG-REAL-AI-360`** — only after explicit provider + scope approval; does not block deterministic Dec18 baseline.

**No `DEC18 REQUIRED` label** applies until Founder accepts the **named** packet list above.

---

## G. First REAL code workday (EX01-08)

**Recommended first implementation workday (if Founder ratifies P0-1):** **`V1-EXPAND-PKG-S05`** — highest NO_ADR_NEEDED value, no provider cost, preserves ADR-062 and memory-only bearer rules.

**Workday ID (proposed):** `AIEOS-V1-EXPAND-WD01-S05`  
**Status:** **`FOUNDER NAMED-SCOPE APPROVAL PENDING`**

### WD01-S05 task list (12 tasks)

| # | Task | Owner / paths | Acceptance |
|---|------|---------------|------------|
| 1 | **Freeze presenter continuity contract** — document allowed hints vs forbidden secrets | Frontend `docs/AIEOS360-V1-EXPAND-S05-PRESENTER-CONTINUITY.md` | Explicit ban: token in URL, `localStorage`, `VITE_*` secrets |
| 2 | **Extend sanitized manifest schema** with per-role `{ role, tenant_id, principal_label, dev_session_field_map }` | `scripts/aieos360-cx01-i01r9-showcase-rehearsal/` emitters | `tmp/…-manifest.json` still **no bearer**; unit selftest |
| 3 | **Localhost-only status field** `presenter_role_hints` on managed showcase status JSON | `scripts/aieos360-cx01-i01r9-showcase-rehearsal/status.mjs` (or successor) | Bound to `127.0.0.1`; rejected on non-local bind |
| 4 | **Launcher UI: Role connection checklist** | `src/features/aieos360-showcase/Aieos360ShowcaseLauncherPage.tsx` + CSS | Renders hints from status poll; no fetch of fixture file from browser |
| 5 | **DEV session panel: optional “Apply showcase hints”** for `?showcase=1` | `src/features/teacher-os/shell/DevSessionPanel.tsx` + student/principal/parent equivalents if not shared | Prefills tenant only; bearer paste remains manual; memory-only |
| 6 | **Cross-port safety** — document that hints do not auto-sync bearer across origins | docs + launcher copy | Aligns with preflight §Limitation without claiming SSO |
| 7 | **Unit tests** — manifest sanitization regression | `src/aieos360Cx01I01R9Showcase.safety.test.ts` | Fails if bearer appears in manifest/status fixtures |
| 8 | **Launcher test** — checklist renders from mocked status | `src/features/aieos360-showcase/aieos360ShowcaseLauncher.test.tsx` | Snapshot of labels only |
| 9 | **Update preflight / cue sheet** cross-links | `docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md`, `docs/AIEOS360-CX01-I07-FOUNDER-CUE-SHEET.md` | Credential-free evidence |
| 10 | **I07 rehearse lifecycle selftest** — status schema backward compatible | `scripts/aieos360-cx01-i07-integrated-rehearsal/rehearse_lifecycle.selftest.mjs` | No change to deterministic proof policy |
| 11 | **Security negatives** — grep gate: no `Bearer` in showcase URLs | CI script / pin test | Fails closed on regression |
| 12 | **Product E2E pin consistency** | `src/aieos360Cx01I01R9Showcase.pins.test.ts` | Records Backend/Frontend SHA pins |

**API surface:** none required (orchestrator JSON + existing DEV session connector only).

**If Founder rejects P0-1:** smallest alternatives — (a) ratify **P0-2 S02A** only as first workday; (b) ratify **REAL-AI-360** with provider approval; (c) declare **`FIRST CODE WORKDAY BLOCKED`** until ADR scope change for learner feedback beyond presentation-only.

---

## H. Parallelization (EX01-09)

| Lane | Scope | Depends on | Conflict guard |
|------|-------|------------|----------------|
| **Frontend A** | WD01-S05 orchestrator + launcher + DEV panel hints | I01R9 status contract | Single writer to `aieos360-cx01-i01r9-showcase-rehearsal/` per PR |
| **Frontend B** | WD02-S02A Student post-submit copy | None (presentation) | Avoid same PR as S05 unless sequenced after task 2 freeze |
| **Backend** | Idle for P0-1/P0-2 | — | **No Backend changes** unless REAL-AI-360 ratified |
| **Architecture** | Record-only follow-ups | Founder ratification | No ADR body edits without separate workday |

Apply [AIEOS-GOV-CI01](https://github.com/eduvijna-ai/eduvijna-architecture/issues/49) two-failure rule on all subsequent code workdays.

---

## I. Delivery cut lines (EX01-10)

| Date | Expectation | Risk if P0 not ratified |
|------|-------------|-------------------------|
| **2026-11-20** | Engineering showcase rehearsal credible on deterministic I07 substrate | Presenter friction (EX-C05) remains a **demo risk** even when automated guard is green |
| **2026-12-18** | Ratified V1-EXPAND P0 slices integrated + tested | Without named scope, programme stays **`DEC18 V1 SCOPE DECISION REQUIRED`** per DR01 |
| **2027-01-29+** | Full Experience Depth / ERP / EIS / Agents | **Unchanged** — not silently collapsed into December |

**Effort realism:** P0-1 + P0-2 fit December if ratified promptly; P0-3 REAL-AI is **optional** and may slip post-Dec18 without blocking deterministic v1 development readiness.

---

## J. ADR / SoR mapping summary (EX01-05 condensed)

| Package | ADR-AIEOS-052…062 touchpoints | SoR impact |
|---------|-------------------------------|------------|
| S05 | 062 (school context facts unchanged); 057 (Teacher OS UX); dev-only composition | **None** — UX + orchestrator metadata |
| S02A | 058 (attempt/submit); 059 (evaluation remains Teacher-side); 061 (Parent deny evaluation) | **None** — copy only |
| REAL-AI-360 | 052 (PreparationKit lineage); 044 platform behind services; I06 mode governance | **None** if no schema change — provider invocation is operational |

---

## K. Evidence & documentation check (EX01-11)

| Check | Result |
|-------|--------|
| Single new Architecture artifact | **`AIEOS/AIEOS-V1-EX01-EXPANDED-DECEMBER-FEATURE-SCOPE-AND-CODE-PACKETS.md`** (this file) |
| Avoided edits | `AIEOS-CURRENT-STATE.md`, `AIEOS-ROADMAP.md`, `CHANGELOG.md`, ADR bodies, W01 baseline — **not modified** |
| Relative Markdown links to in-repo ADRs / W01 | Verified targets under `decisions/` and `AIEOS/` |
| External GitHub links | Use full commit paths for Frontend/Backend evidence |
| Credential-free | No tokens, keys, or fixture bearer material in this document |
| Architecture CI | **NO CI CONFIGURED** — no false green claim |

---

## L. EX01-12 — Branch, PR, and STOP

| Item | Value |
|------|-------|
| **Branch** | `cursor/aieos-v1-ex01-expand-scope-287c` |
| **Base** | `491295c3cf0a151f31686a6a2e1a2176cd92c782` (`main`) |
| **Head** | *(commit after push — Architecture doc only)* |
| **Changed files** | `AIEOS/AIEOS-V1-EX01-EXPANDED-DECEMBER-FEATURE-SCOPE-AND-CODE-PACKETS.md` |
| **PR state** | **DRAFT / OPEN / NOT MERGED** |
| **Application code PRs** | **None authorized** until Founder ratifies named P0 list |

### Founder ratification request

Please confirm **one** of:

1. **Ratify P0 list:** `V1-EXPAND-PKG-S05`, `V1-EXPAND-PKG-S02A`, and optionally `V1-EXPAND-PKG-REAL-AI-360` (with separate provider approval for REAL_AI); **first code workday = WD01-S05**, or  
2. **Substitute / shrink** the P0 list (name exact package IDs), or  
3. **Reject** presentation-only expansion and require **`NEW_ADR_REQUIRED`** scope (e.g., learner-visible feedback) before any code workday.

**Awaiting:** Founder “Cursor completed” + Chief exact-head review on this DRAFT PR.

---

## Related

- [AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)
- [ADR-AIEOS-052](../decisions/ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md) … [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)
- [Issue #54 — EX01 master tasklist](https://github.com/eduvijna-ai/eduvijna-architecture/issues/54)
- [DR01 PR #53 — development readiness backlog (DRAFT)](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53)
