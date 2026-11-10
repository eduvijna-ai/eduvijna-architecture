---
id: AIEOS-PROGRAM-RB03
title: Bottom-Up Delivery Packets & Capacity-Gated Rebaseline (Founder No-Scope-Cut)
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: draft
version: 1.0.1
created: 2026-11-09
last_updated: 2026-11-10
workday: AIEOS-PROGRAM-RB03-P01R1
authorization: Founder "RB03 Authorized" — 2026-11-09 (Issue #66)
parent_issue: https://github.com/eduvijna-ai/eduvijna-architecture/issues/66
parent_register:
  - AIEOS/AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md @ a4edadc979248d7abedc4d7c679b348033c57eb5
  - AIEOS/AIEOS-PROGRAM-RB02-REQUIREMENTS-RECONCILIATION-AND-CAPACITY-PREFLIGHT.md @ a4edadc979248d7abedc4d7c679b348033c57eb5
---

# AIEOS-PROGRAM-RB03 — Bottom-Up Delivery Packets & Capacity-Gated Rebaseline

**Governance:** **FOUNDER-APPROVED QUALITY-FIRST, NO-SILENT-SCOPE-CUT** ([Issue #66](https://github.com/eduvijna-ai/eduvijna-architecture/issues/66)). **DESIGN / PLANNING / PACKETIZATION ONLY.** No product code, merge of this or other PRs, production spend, UAT execution, exact-date ratification, or Founder atomic-scope promotion authorized by this deposit.

**Upstream (merged @ Architecture `main` `a4edadc…`):** [RB01](AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md) · [RB02](AIEOS-PROGRAM-RB02-REQUIREMENTS-RECONCILIATION-AND-CAPACITY-PREFLIGHT.md) (PR #65 reviewed head `8793ab81f987fd8d4adc9fa19669479085c1a667`).

**STOP (RB03 end-state):** `RB03 BOTTOM-UP PLAN DEPOSITED / FULL AGREED SCOPE PRESERVED / CAPACITY & FOUNDER RATIFICATION PENDING / NO DATES RATIFIED / NO PRODUCT CODE / NO PR MERGE / CHIEF EXACT-HEAD REVIEW PENDING`

---

## A — Workday identity

| Field | Value |
|-------|-------|
| Programme | AIEOS-PROGRAM-RB03 |
| Founder authorization | **2026-11-09** — "RB03 Authorized" |
| Mode | Read-only on five pinned `main` trees + linked Product/ADR/draft PRs; **write only this file** |
| Packet | **AIEOS-PROGRAM-RB03-P01** |
| Architecture parent (`main`) | `a4edadc979248d7abedc4d7c679b348033c57eb5` (RB02 PR #65 merge) |
| Branch | `cursor/aieos-program-rb03-bottom-up-delivery-rebaseline-437e` |
| Issue | [#66](https://github.com/eduvijna-ai/eduvijna-architecture/issues/66) (workday — not a PR) |
| Draft PR (this deposit) | [#67](https://github.com/eduvijna-ai/eduvijna-architecture/pull/67) @ HEAD `21aa9f3193c7653630fa061e9532f3a725bc05c5` |

---

## B — Exact-source gate (re-verified before P01R1 write)

Re-verification **2026-11-10 (P01R1)**: `git fetch origin main`, `gh pr view 65`, `gh pr view 67`, `gh api` commit SHAs, OpenAPI SHA-256 check.

| Authority | Expected | Verified |
|-----------|----------|----------|
| Architecture `main` | `a4edadc979248d7abedc4d7c679b348033c57eb5` | **MATCH** |
| Product `main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** |
| Backend `main` | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** |
| Frontend `main` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** |
| Infrastructure `main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** |
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** |
| Alembic head | `a360s010004` | **MATCH** (per RB02 / ADR pin tables @ Backend `637583f42…`) |

### B.1 — PR states (unchanged; not modified)

| PR | State | Draft | Head OID | RB03 role |
|----|-------|-------|----------|-----------|
| Arch **#65** RB02 | **MERGED** | — | Review `8793ab81…` → merge `a4edadc…` | Upstream reconciliation |
| Arch **#63** RB01 | **MERGED** | — | Into `1fbbc356…` chain | Register |
| Arch **#59** ADR-063 | **MERGED** | — | ADR frozen on `main` | Hint authority |
| Arch **#57** SP01 | OPEN | YES | `5182f99d028f32bcd55570c5d44f5c1f64ad5277` | Decision dependency — not auto-merge |
| Arch **#55** EX01 | OPEN | YES | `8b1d07692e1698cf2be9d338f6d45a1707719146` | Decision dependency |
| Arch **#53** DR01 | OPEN | YES | `70986a013ce776257f739eff6ab89727d6715df9` | Decision dependency |
| Arch **#51** CX01 pack | OPEN | YES | `87725067d3aa9f39dff05e634f71b05d8da85cd0` | Acceptance dependency (I08) |
| Product **#3** | OPEN | YES | `90511df0358dcee1236adcde73659bfb2be95e37` | Acceptance dependency |
| Arch **#67** RB03 (this deposit) | OPEN | YES | `21aa9f3193c7653630fa061e9532f3a725bc05c5` | Planning only — **not merged** |

**Gate:** **PASS** — RB03 P01R1 correction write authorized.

**Architecture Actions:** `.github/workflows/.gitkeep` only — **NO CI CONFIGURED**. Backend/Frontend CI **not re-run** in RB03.

---

## C — Git branch and diff scope

| Field | Value |
|-------|-------|
| Branch | `cursor/aieos-program-rb03-bottom-up-delivery-rebaseline-437e` |
| Sole parent | `a4edadc979248d7abedc4d7c679b348033c57eb5` |
| Diff vs `main` | **One file only:** this document |
| Other repos / files / draft PRs / ADRs | **Untouched** |

---

## D — Evidence ledger (frozen read-only pins)

| Artifact | Path / reference @ pin |
|----------|-------------------------|
| RB01 register | `AIEOS/AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md` @ `a4edadc…` |
| RB02 supplement | `AIEOS/AIEOS-PROGRAM-RB02-REQUIREMENTS-RECONCILIATION-AND-CAPACITY-PREFLIGHT.md` @ `a4edadc…` |
| ADR-063 | `decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md` |
| ADR-057…062 | `decisions/` @ Architecture `main` |
| OpenAPI contract | Backend `contracts/openapi/aieos-v1.json` @ `637583f42…` |
| Showcase baseline | FE `569ef8be…` — `src/features/aieos360-showcase/`, `scripts/aieos360-cx01-*` |
| Issue #66 workday | Controlling RB03 scope and STOP line |

**Global privacy / authority negatives (unchanged):** No answer-key or hint leakage (ADR-063); no Principal learner drill-down or Parent evaluation scores without forward ADR (ADR-060/061); **no AIEOS roster/enrollment SoR** (ADR-062 external master); tenant isolation and ContentVersion immutability (ADR-027).

**Do not rebuild closed slices:** TOS-DEV10/CX01; S01–S04; CX01 I01R9–I07 baseline @ Frontend pin — verification, polish, UAT residuals only (RB01 K.1 / RB02 D).

---

## E — Normalized atomic deliverables & overlap accounting (RB01 §K)

### E.1 — Why 100 matrix rows ≠ 100 independent features

| Layer | Count | Rule |
|-------|------:|------|
| RB01 matrix REQ rows (§K.1–K.6, K.8–K.15) | **100** | Discovery register |
| **ROLLUP_NON_ADDITIVE** | **7** | e.g. `RB01-STU-HINT`, `RB01-PHASE-*` — **exclude** from unique work denominator |
| **ARCHITECTURE_AUTHORITY_ONLY** | **1** | `RB01-HINT-ARCH` — frozen text, not implementation |
| **FORBIDDEN_CURRENT_AUTHORITY** | **1** | `RB01-ERP-ROSTER` — **not** missing agreed work |
| **APPROVED_AGREED** bind | **69** | Commitment-eligible when ratified |
| **APPROVED_AGREED [PROD]** (K.5) | **18** | Off V1 dev critical path |
| **APPROVED_AGREED [DEV]** | **51** | V1 / dev CP denominator (RB01 §L.2) |
| **`DONE_VERIFIED` ∩ [DEV] APPROVED_AGREED** | **17** | Closed dev evidence @ pin |
| **Uncompleted [DEV] APPROVED_AGREED** | **34** | Primary packetization target (51 − 17) |
| **`SOURCE_RECONCILIATION`** | **12** | Programme intent preserved — **DECISION_BLOCKED** packets, not approved execution |
| **`DISCOVERY_DRAFT`** | **3** | DR01/EX01/SP01 — reconcile before counting as execution |
| **`VISION_TO_RATIFY`** | **5** | Conditional / not authorized coding |
| **`FUTURE_CONDITIONAL_ADR`** | **2** | PRI-DRILL, PAR-SCORE — forbidden today |

**Forbidden completion math:** Never cite `17/51`, `17/100`, or hint rollup + atomic hint rows as a single completion percentage.

### E.2 — Atomic status lens (planning — not Class replacement)

| Status | Meaning in RB03 packets |
|--------|---------------------------|
| **DONE_VERIFIED** | Closed @ pin — packet = verification-only or **no new code** (residual CI/UAT) |
| **IN_PROGRESS** | **PARTIAL** Class — bounded residual packet |
| **MISSING** | **NOT_STARTED** APPROVED_AGREED [DEV] |
| **DECISION_BLOCKED** | SOURCE_RECONCILIATION / SRC / TO_RATIFY — start gate = Founder/Product Architecture |

### E.3 — Segment: V1 dev critical path vs full-original [DEV]

| Segment | Definition | Packet ID prefix |
|---------|------------|------------------|
| **V1-CP** | Hint vertical (K.2), CX01 verification (K.3), QA-E2E/CI (K.15), platform DEV ADR closeout residuals blocking V1 | `PK-V1-*` |
| **FULL-DEV** | Post-V1 programme rows still **APPROVED_AGREED [DEV]** (ADM-OS, ERP-LIVE, AGT-MCP, etc.) | `PK-FD-*` |
| **CONDITIONAL** | Rows pending SRC / ratification | `PK-CND-*` |

### E.4 — Uncompleted **APPROVED_AGREED [DEV]** → packet map (**34 index rows** — exact)

**R1-F1 correction:** `TOS-LOOP`, `EIS-CUR`, and `EIS-ALIGN` are **`SOURCE_RECONCILIATION`** (RB01 §K.0 / RB02 §I) — **excluded** from this denominator; they map only to **`PK-CND-*`** in §F / §H.4. Do **not** treat `PK-V1-TOS-LOOP-RES` or `PK-FD-EIS-*-EXEC` as approved execution until Founder ratification.

| # | RB01 Req-ID | Class @ pin | RB03 packet | Segment |
|--:|-------------|-------------|-------------|---------|
| 1–8 | HINT-T1 … HINT-E2E | NOT_STARTED | PK-V1-HINT-* (§H.1) | V1-CP |
| 9–16 | CX01-I01R9 … CX01-I08 | PARTIAL / NS | PK-V1-CX-* (§H.2) | V1-CP |
| 17–27 | ADR-022, 023R1, 024, 026, 028, 033, 034, 035, 036, 046R1, ADR-AI-044 | PARTIAL | PK-V1-PLT-* (§H.3.2 — **one packet per ADR row**) | V1-CP |
| 28–29 | QA-E2E, QA-CI | PARTIAL | PK-V1-QA-* (§H.3.1) | V1-CP |
| 30 | AGT-GW | PARTIAL | PK-V1-AGT-GW (§H.3.3) | V1-CP |
| 31–32 | ADM-OS, ERP-LIVE | NOT_STARTED | PK-FD-ADM-OS, PK-FD-ERP-LIVE (§H.5) | FULL-DEV |
| 33–34 | AGT-MCP, AGT-SAFE | NOT_STARTED | PK-FD-AGT-MCP, PK-FD-AGT-SAFE (§H.5) | FULL-DEV |

**Segment check:** 8 hints + 8 CX01 + 11 platform ADRs + 2 QA + 1 AGT-GW + 2 Admin/ERP + 2 agent programme = **34**. `ADR-AI-044` and `AGT-GW` are **distinct index rows** — packets may overlap in gateway domain but **must not collapse** in the register.

**Misclassified (not in 34 — conditional only):** `TOS-LOOP` → `PK-CND-TOS-LOOP` (§F); `EIS-CUR` → `PK-CND-EIS-CUR`; `EIS-ALIGN` → `PK-CND-EIS-ALIGN`. Programme intent **preserved** under NO_CUT.

*Other rows with **Bind ≠ APPROVED_AGREED** (`VISION_TO_RATIFY`, `DISCOVERY_DRAFT`, rollups, forbidden) use §F / §H.6 / §H.8 — **not** in the 34.*

---

## F — Twelve `SOURCE_RECONCILIATION` carry-forward (RB02 §I — 0/12 promoted)

Each row retains **FDP=Y**. RB03 maps each to **`PK-CND-*`** with start gate **Founder/Product ratification** — **not** approved engineering execution.

| RB01 ID | NMAS | FDP category | RB03 packet | Start gate |
|---------|:----:|--------------|-------------|------------|
| TOS-LOOP | N | Product ratify | PK-CND-TOS-LOOP | SRC-03 + PA-LOOP-001 sign-off |
| TOS-A11Y | N | Product ratify | PK-CND-TOS-A11Y | ENG-A11Y-001 approved + FE CI |
| TOS-IND | **Y** | Product + forward ADR | PK-CND-TOS-IND | SRC-03 + institutional read-model ADR |
| STU-A11Y | **Y** | Product ratify | PK-CND-STU-A11Y | Student ENG-A11Y addendum |
| PRI-UX | N | Product ratify | PK-CND-PRI-UX | SRC-03 role-depth brief |
| PAR-UX | N | Product ratify | PK-CND-PAR-UX | SRC-03 multilingual/comms |
| EIS-CUR | **Y** | Forward ADR | PK-CND-EIS-CUR | Graph SoR ADR |
| EIS-ALIGN | **Y** | Forward ADR | PK-CND-EIS-ALIGN | After EIS-CUR ADR |
| EIS-ML | N | Product ratify | PK-CND-EIS-ML | SRC-03 medium list |
| ECO-SDK | **Y** | SRC-02 + Product | PK-CND-ECO-SDK | SRC-02 evidence |
| ECO-AN | **Y** | SRC-02 + Product | PK-CND-ECO-AN | SRC-02 Founder brief |
| QA-OBS | N | Product + [PROD] | PK-CND-QA-OBS-DEV / PK-PROD-OBS | Split DEV telemetry vs SRC-05 |

**Accounting (unchanged from RB02 §I.0):** ID_ADDRESSED **12/12** · RSF **9/12** · NMAS **6/12** · FDP **12/12** · Promoted without ratification **0**.

Per-row acceptance, size, and evidence: **RB02 §I.1** remains authoritative; §M.5 binds each row to a **DEC-ID** without promoting bind state.

---

## G — SRC-01…SRC-05 dispositions (RB02 §J)

| SRC | Topic | RB03 disposition | Blocks |
|-----|-------|------------------|--------|
| **SRC-01** | Post-Dec family checklists | Atomic candidates listed RB02 J.1 — **NEEDS_FOUNDER_RATIFICATION** before sizing post-V1 tranches | PK-FD-* calendar binding |
| **SRC-02** | External conversations | **STILL_SOURCE_REQUIRED** for ECO-* @ pin — evidence checklist RB02 J.2 | PK-CND-ECO-* |
| **SRC-03** | Indian-school fidelity | Draft corpus **SOURCE_FOUND** — thresholds **NEEDS_FOUNDER_RATIFICATION** (RB02 J.3) | PK-CND-TOS-*, STU-A11Y, PRI/PAR-UX, EIS-ML |
| **SRC-04** | Capacity / FTE | **UNKNOWN** — Founder checklist §M.1 | **All date ratification** |
| **SRC-05** | Production spend | **[PROD] charter only** — ADR-029…051 (RB01 K.5) | PK-PROD-* execution |

---

## H — Delivery packet register

### H.0 — Register conventions (RB03-06)

Each **approved** uncompleted **[DEV]** row maps to ≥1 packet. Fields below use compact tables; **Human owner = UNKNOWN** unless evidenced in repos (RB02 H.1).

| Column | Meaning |
|--------|---------|
| **PK-ID** | Stable packet identifier |
| **Req-IDs** | RB01 matrix IDs |
| **Bind / Class** | RB01 §K |
| **Owner DOMAIN** | Architecture / Backend / Frontend / Product / Cross |
| **Repos** | Target implementation repos |
| **Start gate** | Must pass before coding authorization |
| **Size** | S/M/L/XL + confidence (`RB01-aligned` / `hypothesis` / `UNKNOWN`) |
| **Auth** | `NOT AUTHORIZED FOR CODE` unless future Founder code authorization |

### H.1 — V1 critical path: ADR-063 hint vertical (atomic — no rollup double-count)

| PK-ID | Req-IDs | Class | Owner | Repos | Dependencies | Start gate | In scope | Out of scope | User outcome | E2E accept (+) | Adversarial (-) | Proof | Size |
|-------|---------|-------|-------|-------|--------------|------------|----------|--------------|--------------|----------------|-------------------|-------|------|
| PK-V1-HINT-T1 | HINT-T1 | NOT_STARTED | Backend | be | ADR-063 §5–7 | Founder code auth post-PK-HINT-A | `education.worksheet@2` registry; guarded append; §7.5 bypass closure | Student routes; publish to clients | Content owners register hint-bearing worksheet schema | Append with owner gates succeeds; `@1` unchanged | Generic append bypass; cross-tenant append | BE unit/integration; OpenAPI diff | M · RB01-aligned |
| PK-V1-HINT-T2 | HINT-T2 | NOT_STARTED | Backend | be | T1 | T1 merged | Semantic QA + `human_review_pass`; HARD BLOCK lint | Auto-publish | Reviewers attest hint-safe content | Review queue rejects leakage patterns | Answer text in hint field | BE tests + review fixtures | M · RB01-aligned |
| PK-V1-HINT-T1b | HINT-T1b | NOT_STARTED | Backend | be | T1 | T1 merged | Learning `@2` learner-safe projection on assignment GET | Raw hint on GET | Learners see assignment without answer leakage | Assignment GET strips forbidden fields | Hint body on assignment GET | BE contract tests | M · RB01-aligned |
| PK-V1-HINT-T1c | HINT-T1c | NOT_STARTED | Backend | be | T1 | T1 merged | Assessment `@2` convergence w/ ADR-055 | Score leakage | Assessment attempt flow unchanged safety | Attempt submit works | Hint/answer in assessment payload | BE tests | M · RB01-aligned |
| PK-V1-HINT-T0 | HINT-T0 | NOT_STARTED | Cross | be, fe | T1, T2 | T1+T2 BE gates | Teacher hint authoring API/UI contracts | In-attempt student use | Teachers author hints under governance | Save draft → review → publish path | Teacher sees learner attempt answers | FE component tests; BE API | L · hypothesis |
| PK-V1-HINT-B | HINT-B | NOT_STARTED | Backend | be | T1b, T2, S04 context | Published attested version | Attempt-scoped hint GET §8.2 FOR UPDATE | Unscoped listing | Learner requests hint within attempt policy | 404/403 when attempt closed | Cross-learner hint fetch | BE HTTP + PG integration | M · RB01-aligned |
| PK-V1-HINT-F | HINT-F | NOT_STARTED | Frontend | fe | B | B + contract pin | In-attempt hint UX | Parent/Principal surfaces | Learner optional hint in attempt UI | Happy path hint display | Hint in AT/exposed DOM to extensions | FE tests; SP02 scenarios | M · RB01-aligned |
| PK-V1-HINT-E2E | HINT-E2E | NOT_STARTED | Cross | be, fe, product | T0, B, F | All hint lanes | SP02 adversarial suite @ real stack | Mock-only proof | End-to-end hint vertical demonstrable | SP02A happy path | RB01 K.7 exclusion list | Product E2E spec; CI receipt | L · RB01-aligned |

**PK-HINT-A (recommendation only — NOT AUTHORIZED):** First coding candidate = **PK-V1-HINT-T1** scope only (Backend-only), per RB02 §H.3 — excludes B/F/T0/Student GET.

### H.2 — V1 critical path: AIEOS360 CX01 verification (no launcher rebuild)

| PK-ID | Req-IDs | Class | Owner | Repos | Dependencies | Start gate | In scope | Out of scope | User outcome | E2E accept (+) | Adversarial (-) | Proof | Size |
|-------|---------|-------|-------|-------|--------------|------------|----------|--------------|--------------|----------------|-------------------|-------|------|
| PK-V1-CX-I01R9 | CX01-I01R9 | PARTIAL | Frontend | fe | — | None for polish | Fresh rehearsal + optional CI script rerun | Rebuild launcher architecture | Operator can reset/start showcase | Scripts exit 0 @ pin | Hardcoded prod URLs | FE script logs; manual checklist | S · RB01-aligned |
| PK-V1-CX-I02 | CX01-I02 | PARTIAL | Frontend | fe | I01R9 | — | Role entry URL polish | New auth model | Each role reaches shell from launcher | URLs resolve in dev | Cross-tenant token in URL | FE e2e smoke | S · hypothesis |
| PK-V1-CX-I03 | CX01-I03 | PARTIAL | Frontend | fe | — | SRC-03 optional for copy | Student visual polish | New learning features | Showcase student path presentable | Rehearsal without engineering panel | PII in demo labels | Manual showcase | M · hypothesis |
| PK-V1-CX-I04 | CX01-I04 | PARTIAL | Frontend | fe | — | SRC-03 optional | Principal/Parent polish | Drill-down / scores | Role shells presentable | ADR-060/061 aggregates only | Forbidden drill-down affordances | Manual + unit tests | M · hypothesis |
| PK-V1-CX-I05 | CX01-I05 | PARTIAL | Frontend | fe | I02–I04 | — | Cross-role narrative continuity | Full product storyline | Continuity component matches cue sheet | Rehearsal doc steps pass | Broken handoff between roles | FE docs + rehearsal | M · RB01-aligned |
| PK-V1-CX-I06 | CX01-I06 | PARTIAL | Frontend | fe | — | — | Mode transparency panel truthfulness | Live prod AI keys | Operator sees real vs fake AI mode | configure-mode script + UI | Mislabeled Real-AI | Script + UI test | S · RB01-aligned |
| PK-V1-CX-I07 | CX01-I07 | PARTIAL | Cross | fe, be | I05, I06 | Integration env | Integrated rehearsal + product spec rerun | API mock regression | One-command integrated rehearsal | `test:e2e:aieos360-cx01-i07` green @ fresh run | Mocked backend in integrated path | CI receipt (BE+FE) | M · RB01-aligned |
| PK-V1-CX-I08 | CX01-I08 | NOT_STARTED | Cross | arch, product | #51, Product #3 | Draft PR review | Founder acceptance **pack** (docs/checklists) | New feature code | UAT-ready evidence bundle | Chief+Founder sign checklist | Treating doc pack as feature complete | Arch #51 + Product #3 merge **Founder auth** | S · RB01-aligned |

### H.3 — V1 cross-cutting quality & platform [DEV] residuals (RB03-06 expanded)

**Human owner:** **UNKNOWN** unless evidenced @ pin (all rows). **Auth:** `NOT AUTHORIZED FOR CODE`.

#### H.3.1 — Quality / CI packets (verification-heavy)

| PK-ID | Req | Owner | Repos | Deps / gate | In scope | Out / negatives | User outcome | E2E (+) | Adversarial (−) | Proof | Size |
|-------|-----|-------|-------|-------------|----------|-----------------|--------------|---------|-----------------|-------|------|
| PK-V1-QA-E2E | QA-E2E | Cross | fe, be | I07 rehearsal stable | Cross-role regression harness; fresh CI rerun | Net-new features | Stable showcase regression | Harness green @ fresh run | Cross-tenant fixture data | FE/BE CI receipt | **M** · verification |
| PK-V1-QA-CI | QA-CI | Platform | arch, be, fe | — | Document required checks per packet; Arch **no CI** honest | Claim Arch CI green | Maintainers know gate map | Checklist matches repo reality | N/A | Doc + manual audit | **S** · governance |

#### H.3.2 — Platform ADR partials (**one packet per index row** — no silent bundle closeout)

| PK-ID | Req | Owner | Repos | Deps / gate | In scope | Out / negatives | User outcome | E2E (+) | Adversarial (−) | Proof | Size |
|-------|-----|-------|-------|-------------|----------|-----------------|--------------|---------|-----------------|-------|------|
| PK-V1-PLT-022 | ADR-022 | Backend | be, infra | ADR frozen @ pin | Identity kernel dev gaps per ADR text | PROD identity | AuthZ consistent in dev | Tests @ pin + delta list | Privilege escalation | BE tests | **M** · partial |
| PK-V1-PLT-023R1 | ADR-023R1 | Backend | be | — | ContentVersion dev residuals | Bypass immutability | Publishers safe draft path | Version immutability tests | Cross-tenant version read | BE tests | **M** · partial |
| PK-V1-PLT-024 | ADR-024 | Backend | be | — | SoR boundary dev alignment | Competing SoR | Clear ownership in code | Contract tests | Roster SoR in AIEOS | BE tests | **M** · partial |
| PK-V1-PLT-026 | ADR-026 | Backend | be | — | Audit trail dev completeness | PROD log shipping | Operators trace actions | Audit emit tests | PII in audit blob | BE tests | **M** · partial |
| PK-V1-PLT-028 | ADR-028 | Backend | be, infra | — | Tenant isolation dev proof | Cross-tenant join | Tenants isolated in dev | Isolation tests | Cross-tenant query | BE/integration | **M** · partial |
| PK-V1-PLT-033 | ADR-033 | Backend | be | — | Asset model residual | Prod CDN policy | Assets referenced safely | Model tests | Unsigned asset fetch | BE tests | **M** · DESIGN residual |
| PK-V1-PLT-034 | ADR-034 | Backend | be | — | Asset security residual | Unsupported MIME exec | Safe asset handling | Security tests | Path traversal | BE tests | **M** · DESIGN residual |
| PK-V1-PLT-035 | ADR-035 | Backend | be | — | Processing pipeline residual | Unbounded transcode | Governed processing | Pipeline tests | DoS via upload | BE tests | **M** · DESIGN residual |
| PK-V1-PLT-036 | ADR-036 | Backend | be | — | Delivery residual | Public bucket leak | Signed delivery path | Delivery tests | Token reuse | BE tests | **M** · DESIGN residual |
| PK-V1-PLT-046R1 | ADR-046R1 | Backend | be | — | Outbox / dev event semantics | Prod broker | Reliable dev events | Outbox tests | Cross-tenant event | BE tests | **M** · partial |
| PK-V1-PLT-AI-044 | ADR-AI-044 | Architecture | arch, be | Forward ADR scope clarity | Agent/MCP **architecture** binding for dev gateway | MCP prod surface | Architects know tool boundary | ADR traceability | Unauthorized tools | Arch review + BE stub tests | **M** · **DECISION_BLOCKED** partial |

*Rolling “one L bundle closes five ADRs” is **forbidden** — each row needs demonstrable acceptance or explicit **DESIGN/DECISION_BLOCKED** (R1-F2).*

#### H.3.3 — Dev Model Gateway

| PK-ID | Req | Owner | Repos | Deps / gate | In scope | Out / negatives | User outcome | E2E (+) | Adversarial (−) | Proof | Size |
|-------|-----|-------|-------|-------------|----------|-----------------|--------------|---------|-----------------|-------|------|
| PK-V1-AGT-GW | AGT-GW | Backend | be | ADR-AI-044 clarity | Dev `StructuredModelGateway` paths @ pin | **Prod** routing (SRC-05) | Teachers get governed AI in dev | Fake/Groq paths work | Live prod keys in dev UI | BE tests | **M** · partial |

**H.3 planning rollup (band math only — §L.1):** treat PK-V1-PLT-022…028 as **one L**; PK-V1-PLT-033…036 as **one M**; PK-V1-PLT-046R1 + PK-V1-PLT-AI-044 as **one M**; PK-V1-AGT-GW as **one M**; QA-CI **S**; QA-E2E **M** → **1 S / 4 M / 1 L = 13 raw**. Per-ADR rows above remain binding for acceptance traceability (R1-F2).

### H.4 — Conditional programme rows (**SOURCE_RECONCILIATION** — not in 34)

| PK-ID | Req | Bind | Owner | Repos | Start gate | Summary | Size | Auth |
|-------|-----|------|-------|-------|------------|---------|------|------|
| PK-CND-TOS-LOOP-PLAN | TOS-LOOP | SOURCE_RECONCILIATION | Product/Arch | product, be, fe | `DEC-RB02-01` + PA-LOOP-001 + SRC-03 | Generic Intent→Improve replay **only after** ratification; Indian missions **not** in approved denominator | **M** | **NOT AUTHORIZED** |

**R1-F1/F3:** **Do not** include H.4 in approved V1 effort roll-ups (§L.1). Raw **0 S / 1 M = 2** if sized separately.

### H.5 — Full-original [DEV] programme (post-V1 — **4** index rows; EIS in §F only)

| PK-ID | Req | Owner | Repos | Deps / gate | In scope | Out / negatives | User outcome | E2E (+) | Adversarial (−) | Proof | Size |
|-------|-----|-------|-------|-------------|----------|-----------------|--------------|---------|-----------------|-------|------|
| PK-FD-ADM-OS | ADM-OS | Cross | product, be, fe | SRC-01 + ERP charter | Admin OS product surface beyond S04 four ports | Roster SoR (ADR-062) | School operators use Admin OS | Role workflows | ERP master violation | Product E2E (future) | **XL** · hypothesis |
| PK-FD-ERP-LIVE | ERP-LIVE | Cross | be, infra | SRC-01, SRC-05, forward ADR | External ERP/SIS **read/write adapter** | AIEOS competing enrollment SoR | Live institutional sync | Adapter contract tests | Cross-tenant ERP bleed | Integration + charter | **XL** · hypothesis |
| PK-FD-AGT-MCP | AGT-MCP | Backend | be | `DEC-RB02-10` + forward ADR | Governed MCP tool surface in dev | Prod MCP without SRC-05 | Extensible tools w/ authz | Tool registration tests | Tool privilege escalation | BE + Arch review | **XL** · blocked |
| PK-FD-AGT-SAFE | AGT-SAFE | Cross | be, product | SRC-01 | Eval/safety/provenance pipeline | Unchecked model deploy | Safe model lifecycle | Eval harness | PII in training logs | BE tests + policy | **L** · hypothesis |

*`EIS-CUR` / `EIS-ALIGN` execution packets **removed** — both remain `PK-CND-EIS-*` until Forward ADR (§F).*

### H.6 — Discovery draft reconciliation packets (not execution until merge + revalidation)

| PK-ID | Req-IDs | Class | Owner | Start gate | Summary | Size |
|-------|---------|-------|-------|------------|---------|------|
| PK-DSC-SP01 | SP01, DR01, EX01 | REQUIRES_PRODUCT_DECISION | Product/Arch | Founder merge auth per PR | Reconcile SP01R1 ↔ ADR-063 implementation; EX01 V1-EXPAND; DR01 gaps — **avoid duplicate** TOS DEV10 / S01–S04 / CX01 I01R9–I07 | L |

### H.7 — Packet counts & confidence

| Bucket | Index rows / packets | Evidence confidence |
|--------|---------------------:|---------------------|
| V1 hint atomic (H.1) | **8** | **High** DAG; **Medium** T0/F UX |
| V1 CX01 verification (H.2) | **8** | **High** baseline; **Medium** CI rerun |
| V1 platform/QA (H.3) | **14** packets → **11+2+1** index rows | **Medium** — per-ADR acceptance required |
| Full-original (H.5) | **4** | **Low** until SRC-01 / forward ADRs |
| Conditional SRC (F + H.4) | **12** + TOS-LOOP plan | **Blocked** — no approved code |
| Discovery (H.6) | 1 reconciliation | **Decision** only |
| Parked vision/forbidden (H.8) | 8 | **Non-executable** |

**Approved uncompleted [DEV] index rows:** **34** (§E.4). **V1-CP packets after gates:** **30** (H.1–H.3). **Full-original packets:** **4** (H.5). **No row omitted** under NO_CUT.

### H.8 — Vision, forbidden, and authority parking (R1-F7)

Non-executable — **NOT AUTHORIZED FOR CODE**. Programme families remain visible under NO_CUT.

| PK-ID | RB01 Req | Bind / authority | RB03 disposition |
|-------|----------|------------------|------------------|
| PK-CND-TOS-PLAN | TOS-PLAN | VISION_TO_RATIFY | Conditional planning only — forward ADR for Planner Agent |
| PK-CND-STU-FB | STU-FB | VISION_TO_RATIFY | Student feedback vision — Founder ratification required |
| PK-CND-STU-MAST | STU-MAST | VISION_TO_RATIFY | Mastery analytics vision — **no** unsupported mastery claims |
| PK-CND-AGT-ORCH | AGT-ORCH | VISION_TO_RATIFY | Agent orchestration vision — not MCP prod |
| PK-CND-ECO-XPLAT | ECO-XPLAT | VISION_TO_RATIFY | Cross-platform ecosystem — SRC-02 dependent |
| PK-FUT-PRI-DRILL | PRI-DRILL | FUTURE_CONDITIONAL_ADR | **Forbidden today** (ADR-060) — no Principal learner drill-down |
| PK-FUT-PAR-SCORE | PAR-SCORE | FUTURE_CONDITIONAL_ADR | **Forbidden today** (ADR-061) — no Parent evaluation scores |
| PK-FORBID-ERP-ROSTER | ERP-ROSTER | FORBIDDEN_CURRENT_AUTHORITY | **Not missing work** — track **ERP-LIVE** adapter only; **never** AIEOS rival roster SoR |

---

## I — ADR-063 dependency DAG (expanded)

Authority: `RB01-HINT-ARCH` **DONE_VERIFIED** (text only). Implementation packets: §H.1.

```mermaid
flowchart TD
  ARCH[ADR-063 @ main]
  T1[PK-V1-HINT-T1]
  T2[PK-V1-HINT-T2]
  T1b[PK-V1-HINT-T1b]
  T1c[PK-V1-HINT-T1c]
  T0[PK-V1-HINT-T0]
  B[PK-V1-HINT-B]
  F[PK-V1-HINT-F]
  E2E[PK-V1-HINT-E2E]

  ARCH --> T1
  T1 --> T2
  T1 --> T1b
  T1 --> T1c
  T2 --> T0
  T1 --> T0
  T1b --> B
  T2 --> B
  B --> F
  T1b --> E2E
  T1c --> E2E
  T0 --> E2E
  B --> E2E
  F --> E2E
```

| Edge | Parallel-safe? | Notes |
|------|----------------|-------|
| T1b ∥ T1c | **Yes** (after T1) | No cross-dependency |
| T0 co-design | **Partial** | UX/contracts early; shippable after T1+T2 |
| B | **Serial** | Needs attested publish + S04 coherence |
| Hint ∥ CX01 I07 | **Yes** | Different repos; integration E2E serializes |
| Hint ∥ PK-DSC-SP01 | **Conflict** | Same authority — reconcile SP01 before T0 merge |

**Schema ownership:** Content worksheet schema **@2** owned by Content domain; Learning projection **read-only** strip; Assessment convergence **fail-closed** on leakage.

---

## J — Draft Architecture / Product PR dependencies (RB03-09)

| Draft PR | Head @ gate | Duplication risk | RB03 rule |
|----------|-------------|------------------|-----------|
| Arch #57 SP01 | `5182f99d…` | Hint teacher UX / pedagogy | **Decision dependency** for PK-V1-HINT-T0 — not auto-merge |
| Arch #55 EX01 | `8b1d0769…` | V1 scope expansion | Reconcile to §H before new V1 packets |
| Arch #53 DR01 | `70986a01…` | Gap backlog | Feed PK-DSC-SP01 only |
| Arch #51 CX01 | `87725067…` | I08 acceptance | Required for PK-V1-CX-I08 |
| Product #3 | `90511df0…` | I08 product side | Pair with Arch #51 |

**Do not duplicate:** TOS-DEV10 chain, S01–S04 slices, CX01 I01R9–I07 implemented packages.

---

## K — Dependency map & critical path (derivation from §I DAG — R1-F5)

```mermaid
flowchart LR
  FD[Founder / PA decisions SRC-02/03]
  AD[Architecture ADR / packet review]
  BE[Backend contract + migrations]
  FE[Frontend surfaces]
  RS[Real-stack CI / Product E2E]
  DEV[Development functional acceptance]
  UAT[Founder human UAT / I08 pack]

  FD --> AD
  AD --> BE
  AD --> FE
  BE --> RS
  FE --> RS
  RS --> DEV
  DEV -.-> UAT
```

| Critical path lane | Packets (dependency-faithful) | Bottleneck |
|--------------------|------------------------------|------------|
| **CP-1 V1 hints (dev)** | **T1** unlocks **T2**, **T1b**, **T1c** (parallel); **T0** after **T1+T2**; **B** after **T1b+T2**; **F** after **B**; **E2E** after **T0**, **T1c**, **B**, **F** as applicable | Chief review + ContentVersion attestation |
| **CP-2 Showcase (dev)** | **I01R9→…→I07** integrated rehearsal | Integration env steward |
| **CP-2b Founder UAT (separate)** | **I08** + Arch #51 + Product #3 — **not** implied by I07 green or hint E2E | Founder + Chief checklist |
| **CP-3 Governance** | PK-DSC-SP01, SRC-03, §M.5 decisions | Founder calendar — blocks Experience Depth |
| **CP-4 Post-V1** | PK-FD-* (4 rows) | SRC-01 family ratification |

**Parallel-safe:** T1b ∥ T1c after T1; hint backend lanes ∥ CX01 FE polish until **I07** serializes integration. **Same-authority conflict:** SP01 hint UX vs PK-V1-HINT-T0 sequencing. **Founder human acceptance ≠ development readiness** (I08 / UAT g separate from RS).

---

## L — Engineering effort & capacity model (no dates)

### L.1 — Bottom-up size roll-up (illustrative — SRC-04 blocks ratification; R1-F3/F4)

Weights: S=1, M=2, L=4, XL=8. Buffer: `ceil(raw × 1.25)`.

| Segment | S | M | L | XL | Raw units | +25% buffer |
|---------|--:|--:|--:|---:|----------:|------------:|
| V1 hints (H.1) | 0 | 6 | 2 | 0 | **20** | 25 |
| V1 CX01 (H.2) | **4** | **4** | 0 | 0 | **12** | 15 |
| V1 QA/platform (H.3 — approved only) | **1** | **4** | **1** | 0 | **13** | 17 |
| **Approved V1 subtotal (H.1–H.3)** | **5** | **14** | **3** | 0 | **45** | **57** |
| Conditional TOS-LOOP plan (H.4) | 0 | 1 | 0 | 0 | **2** | 3 |
| *Mixed narrative error (prior P01)* | *4* | *15* | *4* | *0* | *50* | *59* |
| Full-original (H.5) | 0 | 0 | 1 | 3 | **28** | 35 |

**Do not** use the prior “4 S / 15 M / 4 L = 47” line — that sums to **50** raw, not 47 (R1-F3).

**Engineering-day sensitivity (conditional — not a schedule):** **57** buffered units ≈ **28.5** M-equivalents at dominant M=2 weighting. At **5–7 engineering-days per M-equivalent** (RB01 hypothesis band) → **~143–200 engineering-days** → **~29–40** five-day workweeks in a **single serial lane**, **before** Chief/Founder PR latency, Product Architecture review, or integration stewardship. **Do not** map this to RB01’s historical **25–35 workweek** illustration (that band assumed **50** buffered units and different packet mix). Review/integration latency **unmodeled** until SRC-04.

### L.2 — Capacity scenarios (conditional)

| Scenario | Assumption | Effect |
|----------|------------|--------|
| **Serial governed Cursor** | One implementation lane + serial Chief/Founder PR review | CP-1 then CP-2; FD packets queue after V1 |
| **Bounded two-lane** | Lane A: BE hints; Lane B: FE CX01 — no shared files | Reduces eligible parallel work only where DAG allows; **E2E still serial** |

**FTE inputs:** **UNKNOWN** (RB02 H.1). **Cursor merge frequency is NOT throughput evidence.**

---

## M — Founder input, date gate, code shortlist, decision backlog, STOP

### M.1 — Founder input sheet (SRC-04 — one page)

| # | Input needed | Used for |
|---|----------------|----------|
| 1 | Frontend / Backend / full-stack / QA **FTE** or fractions | L.2 scenarios |
| 2 | Named lanes vs serial Cursor-only | Parallelism claims |
| 3 | Educational / Product Architecture review capacity (ContentVersion, hints) | T2 attestation scheduling |
| 4 | Leave / blackout through tentative V1 band | Date model |
| 5 | Chief + Founder PR latency (days) | Effective throughput |
| 6 | Integration environment steward + refresh cadence | I07, HINT-E2E |
| 7 | SRC-02/03 acceptance evidence deposits | PK-CND-* promotion |
| 8 | **PA-001 / TLM-001** Approved vs Draft status | TOS-LOOP, packaging |

### M.2 — Date ratification gate (RB03-14)

| Label | Status |
|-------|--------|
| Nov/Dec 2026, Jan–May 2027 programme rows | **Historical baselines** (RB01 §H.1) |
| V1 Q1–Q2 2027, full-original H2 2027+ | **Tentative bands — NOT RATIFIED** |
| RB03 §L unit math | **Illustrative only** |
| **Ratification requires:** SRC-04 complete + atomic specs for remaining **12** SRC rows + Chief-reviewed packet order |

### M.3 — Shortlisted future work (**NOT AUTHORIZED FOR CODE** — R1-F8)

| Order | Packet | Kind | Prerequisites | Positive proof | Negative proof |
|------:|--------|------|---------------|----------------|----------------|
| 1 | **PK-HINT-A / PK-V1-HINT-T1** | **Net-new feature code** | ADR-063 frozen; OpenAPI pin | `@2` registry + append tests | §7.5 bypass denied |
| 2 | **PK-V1-CX-I07** | **Integration verification / rehearsal** (minimal net-new code) | Integration env available | Integrated e2e green @ fresh CI | No API mocks in integrated path |
| 3 | **PK-V1-QA-E2E** | **Regression harness / CI** (verification — not a feature packet) | I07 stable | Cross-role harness in CI | Cross-tenant data in tests |

Only **#1** is a first **feature-code** candidate. **#2–#3** are validation/rehearsal lanes that may reuse existing surfaces. **Founder code authorization** opens a **separate** workday per packet — this deposit does not authorize merge.

### M.4 — Acceptance gate distinctions (RB03-16 / 17)

| Gate | Meaning |
|------|---------|
| Development functional acceptance | CI + integration tests @ dev pins |
| Client showcase | CX01 rehearsal + mode truth |
| Founder human UAT | **Deferred** — I08 pack; not implied by dev green |
| Production deployment | **[PROD]** ADRs + SRC-05 only |

**[DEV] vs [PROD]:** PK-V1-* packets are dev CP; PK-PROD-* (observability, JWT, infra ADRs) require SRC-05 charter — **no privilege escalation**, **no** Parent scores / Principal drill-down.

### M.5 — Founder decision backlog (**12/12 RB02 + SRC + inputs** — R1-F6)

**Missing input = HOLD** — never assumed YES/NO.

| DEC-ID | RB02 row / topic | Exact question | Options (source-backed or UNKNOWN) | Consequence of delay | Authority | CP effect | Next gate |
|--------|------------------|----------------|--------------------------------------|----------------------|-----------|-----------|-----------|
| DEC-RB02-01 | TOS-LOOP | Ratify PA-LOOP-001 and bind Intent→Improve E2E acceptance? | Sign PA / defer Indian missions / HOLD | Teacher loop remains conditional | Founder + PA | Blocks Experience Depth tranche | PA-LOOP-001 Approved |
| DEC-RB02-02 | TOS-A11Y | Approve ENG-A11Y-001 as binding for Teacher surfaces? | Approve Draft / waive / HOLD | A11Y packets stay blocked | Product Architecture | FE CI expansion | ENG-A11Y-001 status |
| DEC-RB02-03 | TOS-IND | Authorize forward ADR for institutional read-model beyond ADR-062 four ports? | New ADR / ERP-LIVE only / HOLD | Indian calendar UX blocked | Founder + Arch | Admin/ERP CP | Forward ADR draft |
| DEC-RB02-04 | STU-A11Y | Add Student scope to ENG-A11Y-001? | Extend doc / new addendum / HOLD | Student a11y untested | Product Architecture | Student polish | PA addendum |
| DEC-RB02-05 | PRI-UX | Ratify SRC-03 Principal role-depth brief? | Approve brief / narrow scope / HOLD | Principal UX depth blocked | Founder + PA | CP-3 Experience | SRC-03 deposit |
| DEC-RB02-06 | PAR-UX | Ratify SRC-03 Parent multilingual/comms scope? | Approve brief / ADR-061 only / HOLD | Parent UX blocked | Founder + PA | CP-3 | SRC-03 + PAR-SCORE forbid |
| DEC-RB02-07 | EIS-CUR | Accept forward ADR for curriculum graph SoR? | Draft ADR / defer / HOLD | EIS programme blocked | Founder + Arch | Post-V1 EIS | Forward ADR |
| DEC-RB02-08 | EIS-ALIGN | Accept forward ADR for alignment engine after EIS-CUR? | Draft ADR / rules-first / HOLD | Alignment blocked | Founder + Arch | After DEC-RB02-07 | Forward ADR |
| DEC-RB02-09 | EIS-ML | Ratify P0 languages + ML policy for Indian schools? | SRC-03 list / human-only / HOLD | ML row stays conditional | Founder | Content quality | SRC-03 |
| DEC-RB02-10 | ECO-SDK | Accept SDK boundary ADR after SRC-02 evidence? | TLM-001 OQ path / new ADR / HOLD | Ecosystem SDK blocked | Founder | Post-V1 ECO | SRC-02 checklist |
| DEC-RB02-11 | ECO-AN | Deposit Founder analytics spec (SRC-02)? | Provide brief / defer / HOLD | Analytics row SOURCE_REQUIRED | Founder | Post-V1 ECO | SRC-02 item |
| DEC-RB02-12 | QA-OBS | Split DEV telemetry from [PROD] observability charter? | ENG-OBS Draft path / PROD-only / HOLD | Observability scope ambiguity | Founder + Eng | SRC-05 boundary | ENG-OBS-001 status |
| DEC-SRC-01 | SRC-01 | Ratify post-Dec family checklist for PK-FD-* tranches? | Approve list / amend / HOLD | Post-V1 calendar binding | Founder | CP-4 | SRC-01 workshop |
| DEC-SRC-02 | SRC-02 | Accept external conversation evidence for ECO-*? | Deposit minutes / HOLD | ECO rows blocked | Founder | ECO SDK/AN | SRC-02 checklist |
| DEC-SRC-03 | SRC-03 | Ratify Indian-school fidelity thresholds? | Approve thresholds / HOLD | TOS-IND, role UX, EIS-ML | Founder + PA | CP-3 | school-context ratification |
| DEC-SRC-04 | SRC-04 | Staffing / lane / throughput inputs? | Provide FTE table / HOLD | **All date ratification** | Founder | Capacity model | §M.1 complete |
| DEC-SRC-05 | SRC-05 | Authorize [PROD] spend charter separately? | Charter Y/N / HOLD | Prod observability/infra | Founder | [PROD] only | Spend charter |
| DEC-PA-001 | PA-001 | Is PA-001 packaging binding for programme? | Approved / Draft / UNKNOWN | Packaging ambiguity | Product Architecture | TOS/TLM | Status deposit |
| DEC-TLM-001 | TLM-001 | Close TLM-001 open questions affecting loop/SDK? | Resolve OQs / HOLD | LOOP + ECO ambiguity | Founder + PA | DEC-RB02-01/10 | OPEN_QUESTIONS review |
| DEC-SP01-01 | Arch #57 | Merge/reject SP01 before PK-V1-HINT-T0? | Merge / reject / HOLD | Hint UX conflict | Chief + Founder | CP-1 T0 | PR #57 review |
| DEC-EX01-01 | Arch #55 | Reconcile EX01 V1 expansion vs §H packets? | Merge / split / HOLD | Scope duplication | Chief + Founder | V1 scope | PR #55 review |
| DEC-DR01-01 | Arch #53 | Merge/reject DR01 gap backlog? | Merge / HOLD | Discovery backlog | Chief + Founder | PK-DSC-SP01 | PR #53 review |
| DEC-HINT-CODE | ADR-063 | Authorize PK-HINT-A / PK-V1-HINT-T1 code workday? | Y / N / HOLD | CP-1 start | Founder | CP-1 | Separate workday |
| DEC-I08-01 | CX01 I08 | Accept Founder UAT pack (Arch #51 + Product #3)? | Approve criteria / HOLD | Showcase sign-off | Founder | CP-2b UAT | **Not** dev CI green |

### M.6 — Coverage & QA (RB03-19 / 20)

| Metric | Value |
|--------|------:|
| RB01 matrix rows preserved | **100** |
| RB02 reconciliation IDs carried | **12/12** |
| SRC topics explicit | **5/5** |
| Uncompleted [DEV] index rows mapped (§E.4) | **34** |
| V1-CP packets (H.1–H.3) | **30** |
| Parked vision/forbidden (H.8) | **8** |
| **[PROD]** rows | Tracked in RB01 K.5 — **not** in V1 CP |
| Architecture CI | **NONE** — do not claim green |
| Product code authorized by RB03 | **0** |
| Exact dates ratified | **0** |

---

## N — Related documents (not modified)

[AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md](AIEOS-PROGRAM-RB01-FULL-SCOPE-REQUIREMENTS-TRACEABILITY-AND-REBASELINE.md) · [AIEOS-PROGRAM-RB02-REQUIREMENTS-RECONCILIATION-AND-CAPACITY-PREFLIGHT.md](AIEOS-PROGRAM-RB02-REQUIREMENTS-RECONCILIATION-AND-CAPACITY-PREFLIGHT.md) · [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) · [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md) · [Issue #66](https://github.com/eduvijna-ai/eduvijna-architecture/issues/66)

---

**End AIEOS-PROGRAM-RB03-P01R1 — Chief R1 corrections deposited; await re-review; PR #67 draft; no date ratified; no merge; no code authorized.**

**STOP LINE:** `RB03-P01R1 CORRECTION DEPOSITED / PR #67 DRAFT / MERGE NOT AUTHORIZED / NO DATES RATIFIED / NO PRODUCT CODE / CHIEF EXACT-HEAD RE-REVIEW PENDING`
