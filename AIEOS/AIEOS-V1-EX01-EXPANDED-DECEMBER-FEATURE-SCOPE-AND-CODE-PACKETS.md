---
id: AIEOS-V1-EX01
title: V1-EXPAND December Feature Scope Freeze & First Code Packets
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: ex01r1 — source facts reconciled; founder product selection pending
version: 1.1.0
created: 2026-11-02
last_updated: 2026-11-02
reviewers:
  - Founder / Product Architecture
  - Chief AI Enterprise Architect
---

# AIEOS-V1-EX01 — V1-EXPAND December Feature Scope & First Code Packets

**Identity:** `AIEOS-V1-EX01` (+ **EX01R1** Chief exact-head correction)  
**Mode:** Architecture evidence, candidate de-duplication, and honest scope/blocker record — **no application code**  
**Founder direction:** [`V1-EXPAND` selected 2026-11-02](https://github.com/eduvijna-ai/eduvijna-architecture/issues/52#issuecomment-6575261649) — **direction only**; **no named December P0 ratified**  
**Terminal target (EX01R1):** `AIEOS-V1-EX01R1 — SOURCE FACTS RECONCILED / V1-EXPAND GENUINE FEATURE SCOPE PROPOSED OR EXPLICIT ADR DECISION BLOCK / PR OPEN-DRAFT-NOT-MERGED`

**Primary authority (read-only):**

- [Issue #54 — master 12-task workday](https://github.com/eduvijna-ai/eduvijna-architecture/issues/54)
- [EX01 PR #55](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) (OPEN / DRAFT / NOT MERGED)
- [DR01 PR #53](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53) (OPEN / DRAFT, base `491295c3…`)
- [W01 showcase gap baseline](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md) (frozen on Architecture `main`)
- Frozen ADR-AIEOS-052…062 under [`decisions/`](../decisions/)

**Non-claims (binding):** Development Slice Complete ≠ Client Showcase Ready ≠ Production Ready ≠ Founder UAT. No production deployment, no paid provider calls, no REAL_AI success assertion in standard CI, no new Business SoRs, and no silent promotion of 2027 programme items into December without explicit Founder scope change. **Do not treat operator rehearsal convenience as ratified V1-EXPAND product-development scope.**

---

## EX01R1 — Chief Architect reconciliation (F1–F4)

**Reviewed PR:** [#55](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) at parent commit `013856aaf071b9226ff2f6fa7f6f31af0c49063b` (EX01 initial). **EX01R1** adds one additive commit on that parent — no amend/rebase/force.

| Finding | Disposition | EX01R1 correction |
|---------|-------------|-------------------|
| **F1** Student post-submit “next step” copy as missing P0 | **ACCEPTED** | EX-C02 learner-safe “what happens next” **copy** → **`ALREADY_IMPLEMENTED`**. Withdraw **`V1-EXPAND-PKG-S02A`** as P0. |
| **F2** S05 assumed browser `status.mjs` polling + four DEV panels | **ACCEPTED** | Withdraw browser-status design; **`V1-EXPAND-PKG-S05`** → **`OPTIONAL_OPERATOR_UX`** (not December end-user P0). **`WD01-S05` NOT authorized.** |
| **F3** Proposed P0 list ≠ V1-EXPAND product scope | **ACCEPTED** | **Zero** `SOURCE_VERIFIED_MISSING` + **`NO_ADR_NEEDED`** **end-user education** P0 packets at current Frontend HEAD. **First code workday = BLOCKED** pending Founder product/ADR choice. |
| **F4** Governance / source pins | **PASS** | Re-verified all five mains + OpenAPI/Alembic before EX01R1 edit (§A). Architecture CI: **NO CI CONFIGURED**. |

---

## A. Authority gate (EX01-01 / EX01R1 F4) — PASS

Re-verified **2026-11-02 (EX01R1)** against remote `origin/main`.

| Authority | Required `origin/main` | Verified SHA | Method |
|-----------|------------------------|--------------|--------|
| Architecture | `491295c3cf0a151f31686a6a2e1a2176cd92c782` | **MATCH** | `git fetch origin main` |
| Product | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | shallow clone + `git fetch` |
| Backend | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | shallow clone + `git fetch` |
| Frontend | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** | shallow clone + `git fetch` |
| Infrastructure | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | shallow clone + `git fetch` |
| OpenAPI SHA-256 | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** | `sha256sum` on Backend pin |
| Alembic head | `a360s010004` | **MATCH** | Backend migrations |

| Governance item | Verified |
|-----------------|----------|
| Founder `V1-EXPAND` direction | Issue #52 comment [`6575261649`](https://github.com/eduvijna-ai/eduvijna-architecture/issues/52#issuecomment-6575261649) |
| CX01-I07 on Frontend `main` | Merge `569ef8b`; Actions success at pin |
| DR01 #53 / I08 #51 / Product #3 | OPEN / DRAFT / NOT MERGED |
| Founder UAT | **DEFERRED** |
| Architecture GitHub Actions | [`.github/workflows/.gitkeep`](../.github/workflows/.gitkeep) only → **NO CI CONFIGURED** |

**Gate result:** **PASS** for Architecture-only EX01R1 document edit.

---

## B. Programme dates vs original vision (EX01-02)

Unchanged from EX01 — **2026-12-18** = major integrated persona experiences under **ratified named scope**; **2027-01-29 through 2027-05-28** programme items **preserved and not silently moved into December**.

---

## C. Candidate evidence matrix (EX01-03 / EX01-05) — EX01R1 revised

| ID | Summary | Classification (EX01R1) | ADR gate | Source evidence at Frontend `569ef8be…` |
|----|---------|-------------------------|----------|----------------------------------------|
| **EX-C01** | REAL_AI **integrated** generation → ContentVersion → Publish/Assign proof on I07 substrate | **`SOURCE_VERIFIED_MISSING`** (operator / proof segment only) | **`FOUNDER_PROVIDER_APPROVAL_REQUIRED`**; not mandatory CI; **`NO_ADR_NEEDED`** only for non-semantic wiring/docs | I07 matrix REAL_AI row **PENDING**; I06 mode scripts; deterministic I07 guard remains authoritative |
| **EX-C02** | Student practice / feedback beyond current thin journey | **Copy / “what happens next”:** **`ALREADY_IMPLEMENTED`**. **Genuine new learner practice or response-level feedback:** **`NEW_ADR_REQUIRED`** (not evidenced as missing without ADR) | ADR-058 one attempt; ADR-059 Teacher-side evaluation; ADR-061 Parent deny evaluation | Persistent submitted banner + no-grade copy: [`AttemptPage.tsx` L266–280](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/student-os/attempts/AttemptPage.tsx#L266-L280). Showcase handoff to Teacher Assess: [L341–350](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/student-os/attempts/AttemptPage.tsx#L341-L350). Transient `"Work submitted."` is auxiliary only. |
| **EX-C03** | Teacher Assess intelligence → Improve UX | **`MOSTLY_ALREADY_IMPLEMENTED`** | **`NO_ADR_NEEDED`** for polish only | S01-I05-F1 + Assess showcase Improve link + launcher **Improve** stage |
| **EX-C04** | Principal/Parent presentation within allowlists | **`MOSTLY_ALREADY_IMPLEMENTED`** | **`NO_ADR_NEEDED`** for polish only | Presentation modules + showcase continuity |
| **EX-C05** | Showcase operator continuity (four memory-only bearer tabs) | **Operator friction:** **`OPTIONAL_OPERATOR_UX`** — **not** a missing core December **end-user** capability. **Not** `SOURCE_VERIFIED_MISSING` as education product. | Any **browser-visible** hint projection beyond existing `public/aieos360-showcase-runtime.json` needs **explicit allowlist + lifecycle contract** (not assumed in EX01) | Preflight documents manual per-tab DEV connect ([`AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md)). **Operator CLI** [`status.mjs`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/scripts/aieos360-cx01-i01r9-showcase-rehearsal/status.mjs) reads private `tmp/` — **not** an HTTP API. Launcher [`Aieos360ShowcaseLauncherPage.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/aieos360-showcase/Aieos360ShowcaseLauncherPage.tsx) has **no status polling**. Browser runtime truth: **only** [`/aieos360-showcase-runtime.json`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/aieos360-showcase/showcaseRuntimeTruth.ts) via [`ShowcaseModeTruthPanel`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/aieos360-showcase/ShowcaseModeTruthPanel.tsx). [`emit_manifest.py`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/scripts/aieos360-cx01-i01r9-showcase-rehearsal/emit_manifest.py) already emits sanitized operator-local `tenant_id`, role principal IDs, and `role_urls` — **must not** expose fixture paths, DB reports, or bearer material to browsers. Shared [`DevSessionPanel.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/teacher-os/shell/DevSessionPanel.tsx) is used across Teacher/Student/Principal/Parent shells — **no auto-impersonation** fixes four-tab memory-only requirement. |
| **EX-C06** | Educational quality v1 | **`ALREADY_IMPLEMENTED`** | **`DEFER_2027`** for EIS depth | DEV04/DEV10 baseline |

**Post-I07 de-duplication:** CX01-I01R9–I07 at Frontend pin closes W01 **deterministic integrated rehearsal** gaps. Remaining W01 **UX-03** (Teacher dual chrome) stays **2027-01-29 Experience Depth** unless explicitly promoted.

---

## D. Product benefit & acceptance (EX01-04) — withdrawn / reclassified packets

### Withdrawn — `V1-EXPAND-PKG-S02A` (EX01 F1)

**Reason:** Proposed benefit duplicated existing UX. **Do not ratify.**

### Downgraded — `V1-EXPAND-PKG-S05` (EX01 F2–F3)

| Field | EX01R1 truth |
|-------|----------------|
| **Nature** | Operator rehearsal convenience — **not** new education capability |
| **Safe default** | Improve **operator-only** preflight/docs/checklists referencing existing **`tmp/…-manifest.json`** on the operator machine |
| **Not authorized without new contract** | Browser polling of orchestrator status, `presenter_role_hints` on CLI JSON served to UI, or cross-port “prefill” that bypasses memory-only bearer rules |
| **Classification** | **`OPTIONAL_OPERATOR_UX`** — P2/backlog unless Founder explicitly prioritizes operator tooling over product features |

### Optional — `V1-EXPAND-PKG-REAL-AI-360` (EX-C01)

| Field | Content |
|-------|---------|
| **Nature** | Optional **provider-gated proof** segment — **not** established mandatory December **product** functionality |
| **Gate** | Separate **Founder provider-spend authorization**; **not** a required CI lane |
| **Classification** | **`OPTIONAL_PROOF_CANDIDATE`** — not a defensible default P0 education packet |

### Genuine product expansion paths (require Founder choice — not pre-ratified)

| Path ID | User-visible intent | Classification | Feasibility |
|---------|---------------------|----------------|-------------|
| **PATH-STUDENT-PRACTICE** | New student practice/review/response feedback beyond one attempt + current banner | **`NEW_ADR_REQUIRED`** | Needs ADR-058/059 forward design; real-stack negatives for Parent/Principal non-disclosure |
| **PATH-REAL-AI-360** | Live provider generation through Publish/Assign on same substrate as I07 | **`SOURCE_VERIFIED_MISSING`** (proof) + **provider approval** | Operator-only; deterministic CI unchanged |
| **PATH-ACCEPT-BASELINE** | Treat Dec18 expand as **integrated baseline already at pin** + defer depth to 2027 | **Programme choice** | No code until Founder names a **different** bounded function |

---

## E. Cross-role composition (EX01-06)

Unchanged: `AIEOS360-CX-SCENARIO-01` spine with ADR-060/061 privacy negatives and I07 tenant negatives. **No proposed P0 packet** is authorized to alter Backend DTO allowlists at this time.

---

## F. Named scope (EX01-07) — EX01R1 honest proposal

**Do not force a minimum 2–3 P0 count.** At Frontend `569ef8be…`, after EX01R1 reconciliation:

| Tier | Count | Content |
|------|-------|---------|
| **Ratified P0 (end-user education, NO_ADR_NEEDED, SOURCE_VERIFIED_MISSING)** | **0** | **None defensible** at current HEAD |
| **First code workday** | **BLOCKED** | See §G |

| Tier | Package / path | Maps | Note |
|------|----------------|------|------|
| **Optional proof** | `V1-EXPAND-PKG-REAL-AI-360` | EX-C01 | Provider approval; not default sprint |
| **Optional operator** | `V1-EXPAND-PKG-S05-DOC` | EX-C05 | Docs/checklist only unless browser projection contract approved |
| **ADR-gated product** | `PATH-STUDENT-PRACTICE` | EX-C02 (real function) | **`NEW_ADR_REQUIRED`** |
| **P1 polish** | C03/C04/UX-03 residuals | EX-C03/04, W01 | Experience Depth default **2027-01-29** |
| **Deferred** | ERP, EIS, Agents, Admin OS | Programme | 2027 dates preserved |

**Programme statement:** Founder selected **`V1-EXPAND` direction**, **not** any named P0 list. **`DEC18 REQUIRED`** cannot attach to S05, S02A, or REAL-AI-360 until explicitly ratified with corrected classifications.

---

## G. First REAL code workday (EX01-08) — BLOCKED

**Status:** **`V1-EXPAND REAL PRODUCT FUNCTION SELECTION / NEW ADR REQUIRED`**

The former **`AIEOS-V1-EXPAND-WD01-S05`** twelve-task packet is **withdrawn** (EX01 F2–F3). It assumed non-existent browser status transport and misclassified operator friction as December product P0.

**Smallest Founder / Product Architecture choices (pick one before any feature PR):**

1. **Authorize `PATH-REAL-AI-360`** as the named expand differentiator — explicit provider budget + operator-only proof acceptance criteria (deterministic I07 remains CI authority).  
2. **Authorize ADR work** for **`PATH-STUDENT-PRACTICE`** — define bounded learner-visible behaviour under ADR-058/059/061 before coding.  
3. **Declare functional baseline sufficient** for Dec18 core integrated loop at current pins and move depth to **2027-01-29 Experience Depth** — V1-EXPAND then means **programme/record reconciliation** (`AIEOS-V1-C01`) plus optional operator docs — **not** duplicate UX.  
4. **Name a different bounded function** with fresh source proof — must show `SOURCE_VERIFIED_MISSING` + ADR feasibility + real-stack negatives in a follow-on Architecture packet.

**Until one choice is recorded:** **no implementation PR**, **no WD01-S05**, **no merge of #55** as scope freeze.

---

## H. Parallelization (EX01-09)

Not applicable while §G is **BLOCKED**. When a path is ratified, apply [AIEOS-GOV-CI01](https://github.com/eduvijna-ai/eduvijna-architecture/issues/49) and keep Frontend/Backend lanes non-overlapping on the same authority.

---

## I. Delivery cut lines (EX01-10)

| Date | EX01R1 expectation |
|------|-------------------|
| **2026-11-20** | Deterministic I07 + I01R9 substrate is the engineering showcase authority; presenter manual DEV connect remains an **operator** constraint, not a missing student/teacher **feature** |
| **2026-12-18** | Requires **named** genuine product scope or honest baseline + 2027 depth — **not** the withdrawn EX01 P0 trio |
| **2027 programme** | Unchanged |

---

## J. ADR / SoR summary (EX01-05)

| Item | SoR impact |
|------|------------|
| Withdrawn S02A | **N/A** — already implemented UX |
| S05-DOC / operator UX | **None** if documentation-only |
| Browser hint projection (if ever proposed) | **Architecture contract required** before code — not authorized in EX01 |
| PATH-STUDENT-PRACTICE | **New ADR** before API/UI |
| REAL-AI-360 | Operational provider invocation — **no** silent schema/SoR change |

---

## K. Evidence & documentation check (EX01-11)

| Check | Result |
|-------|--------|
| Writable scope | Only this file (EX01R1 additive commit) |
| Relative links | ADR + W01 targets verified on branch |
| Secret scan | No credentials in document |
| Architecture CI | **NO CI CONFIGURED** — 0 checks is not PASS |

---

## L. Branch, PR, STOP (EX01-12 / EX01R1)

| Item | Value |
|------|-------|
| **PR** | [#55](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) — **DRAFT / OPEN / NOT MERGED** |
| **Branch** | `cursor/aieos-v1-ex01-expand-scope-287c` |
| **Base (`main`)** | `491295c3cf0a151f31686a6a2e1a2176cd92c782` |
| **EX01 initial HEAD** | `013856aaf071b9226ff2f6fa7f6f31af0c49063b` |
| **EX01R1 HEAD** | *(commit after push — single additive correction)* |
| **Commits** | EX01 initial + **one** EX01R1 correction (parent = `013856a…`) |

### Founder ratification request (revised)

Please record **one explicit product decision** from §G (paths 1–4). **Do not** ratify withdrawn packages **`V1-EXPAND-PKG-S02A`** or **`V1-EXPAND-PKG-S05`** as December P0 education scope.

**STOP** after push — await Chief exact-head **re-review** of PR #55. No merge, no feature code, no provider calls.

---

## Related

- [AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)
- [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) · [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)
- [Issue #54](https://github.com/eduvijna-ai/eduvijna-architecture/issues/54) · [DR01 PR #53](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53)
