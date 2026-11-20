---
id: AIEOS-V1-SP01-RC01
title: SP01 Discovery → ADR-063 → Merged Hint Slices → T0 Teacher Authoring Reconciliation
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: PROPOSED / RECONCILIATION — NOT NORMATIVE — NOT MERGE AUTHORIZED
version: 1.0.0
created: 2026-11-20
last_updated: 2026-11-20
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# PK-DSC-SP01-RC01 — SP01 → ADR-063 → T0 Teacher Authoring Reconciliation

**Workday:** [Architecture Issue #68](https://github.com/eduvijna-ai/eduvijna-architecture/issues/68)  
**Mode:** Architecture discovery / reconciliation **only** — one non-normative evidence document. **No** Backend, Frontend, Product, Infrastructure, ADR, draft-PR, schema, API, grant, CI, or production changes in RC01. **No** T0 implementation authorization.

**Authoritative frozen architecture (read-only @ pins below):**

- [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) — approved on Architecture `main`
- [AIEOS-PROGRAM-RB03](../AIEOS/AIEOS-PROGRAM-RB03-BOTTOM-UP-DELIVERY-PACKETS-AND-CAPACITY-REBASELINE.md) — §§H.1, H.6, I, J
- [AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md](./AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md)

**Historical discovery (read-only, not merged):** [PR #57](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) head `5182f99d028f32bcd55570c5d44f5c1f64ad5277` — `AIEOS/AIEOS-V1-SP01-STUDENT-PRACTICE-FEEDBACK-ARCHITECTURE-DISCOVERY.md`

**Merged implementation evidence (read-only @ Backend/Frontend pins below):**

| Packet | PR | Merge target |
|--------|-----|--------------|
| T1 worksheet@2 + guarded append | Backend [#64](https://github.com/eduvijna-ai/eduvijna-aieos-backend/pull/64) | `main` |
| T2 semantic QA + attestation | Backend [#66](https://github.com/eduvijna-ai/eduvijna-aieos-backend/pull/66) | `main` |
| T1b Learning @2 learner-safe projection | Backend [#68](https://github.com/eduvijna-ai/eduvijna-aieos-backend/pull/68) | `main` |
| T1c Assessment @2 evaluation | Backend [#70](https://github.com/eduvijna-ai/eduvijna-aieos-backend/pull/70) | `main` |
| B attempt-scoped learner-hints GET | Backend [#72](https://github.com/eduvijna-ai/eduvijna-aieos-backend/pull/72) | `e8c7154e7207ac1b39cef244b5084ae5cc1ae07b` |
| F Student in-attempt learner-hint UX | Frontend [#49](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/49) | `e8847871d61f2b894f53a51c97a99a0054198932` |

**Terminal (RC01 deliverable):** `PK-DSC-SP01-RC01 — ARCHITECTURE DRAFT PR OPEN / T0 PRE-CODE RECONCILIATION DELIVERED / NOT MERGED / CHIEF EXACT-HEAD REVIEW REQUIRED`

---

## A — Source-gate receipt (2026-11-20)

### A.1 Five live remote `main` identities

| Repository | Required SHA @ issue gate | Agent-verified `origin/main` | Result |
|------------|---------------------------|------------------------------|--------|
| `eduvijna-ai/eduvijna-architecture` | `de6f104e9a57ab65b8fdfd4364d8beedce3db3d5` | **MATCH** (`git fetch origin main`) | Writable — RC01 branch only |
| `eduvijna-ai/eduvijna-aieos-backend` | `e8c7154e7207ac1b39cef244b5084ae5cc1ae07b` | **MATCH** (GitHub API `get_branch`) | Read only |
| `eduvijna-ai/eduvijna-aieos-frontend` | `e8847871d61f2b894f53a51c97a99a0054198932` | **MATCH** | Read only |
| `eduvijna-ai/eduvijna-product` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | Read only |
| `eduvijna-ai/eduvijna-aieos-infrastructure` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **Not verified by agent** — GitHub App cannot access repo; Chief independently witnessed SHA at issue creation | Cite Chief pin only |

### A.2 Open draft PR gate (unchanged — no mutation)

| PR | Repo | State | Draft | Head SHA | Base SHA | Agent vs required head |
|----|------|-------|-------|----------|----------|------------------------|
| [#57 SP01](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) | Architecture | OPEN | yes | `5182f99d028f32bcd55570c5d44f5c1f64ad5277` | `491295c3cf0a151f31686a6a2e1a2176cd92c782` | **MATCH** |
| [#55 EX01](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) | Architecture | OPEN | yes | `8b1d07692e1698cf2be9d338f6d45a1707719146` | `491295c3…` | **MATCH** |
| [#53 DR01](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53) | Architecture | OPEN | yes | `70986a013ce776257f739eff6ab89727d6715df9` | `491295c3…` | **MATCH** |
| [#51 CX01-I08](https://github.com/eduvijna-ai/eduvijna-architecture/pull/51) | Architecture | OPEN | yes | `87725067d3aa9f39dff05e634f71b05d8da85cd0` | `491295c3…` | **MATCH** |
| [#3 CX01-I08-P](https://github.com/eduvijna-ai/eduvijna-product/pull/3) | Product | OPEN | yes | `90511df0358dcee1236adcde73659bfb2be95e37` | `b4b3048…` | **MATCH** |

**Overlap check:** No open Architecture branch or PR named RC01 / SP01-ADR063 reconciliation existed before this write.

### A.3 Backend OpenAPI pin (@ `e8c7154e…`)

| Artifact | Path | SHA-256 (raw file bytes) | Required @ issue #68 | Result |
|----------|------|--------------------------|----------------------|--------|
| OpenAPI contract | `contracts/openapi/aieos-v1.json` | `43F877E122389A7347DDB00D25F37D8BE8BD907F43FF6960E5DC6E794B1A0071` | Same | **MATCH** |

**Note:** ADR-063 body still cites pre-hint OpenAPI `4042FB27…` at its 2026-11-03 pin table; current Backend `main` contract digest is **post T1–B merges** — do not conflate historical ADR pin prose with live contract.

**Alembic head @ Backend pin (agent read):** `a360s010005` (`a360s010005_worksheet_learner_hint_attestations.py` ← `a360s010004`).

### A.4 RC01 git identities (filled after push)

| Field | Value |
|-------|-------|
| Repository | `eduvijna-ai/eduvijna-architecture` |
| Branch | `cursor/sp01-adr063-t0-reconciliation-90bb` |
| Base | `de6f104e9a57ab65b8fdfd4364d8beedce3db3d5` |
| Initial deposit commit | `860807af08d9b1d3c45f307d2b0740777f206092` (sole parent `de6f104e9a57ab65b8fdfd4364d8beedce3db3d5`); **PR #69 current HEAD is authoritative in GitHub, not self-pinned inside this document**. |
| Changed files | **Only** `AIEOS/AIEOS-V1-SP01-ADR063-T0-AUTHORING-RECONCILIATION.md` |

### A.5 Architecture CI

| Check | Result |
|-------|--------|
| `.github/workflows/*` | **NO CI CONFIGURED** (`.github/workflows/.gitkeep` only) |
| RC01 CI claim | **None** — review is source/diff/links/schema/terminology/ADR fidelity only |

---

## B — Historical vs current authority ledger

Classification key: **SUPERSEDED_BY_ADR063** · **STILL_VALID_DISCOVERY** · **HISTORICAL_SOURCE_PIN** · **REQUIRES_RECONCILIATION**

| # | SP01R1 claim (PR #57 @ `5182f99d…`) | ADR-063 / RB03 current authority | Merged code @ BE/FE pins | Classification |
|---|-------------------------------------|----------------------------------|--------------------------|----------------|
| B1 | Assignment GET embeds `learner_resource` without attempt-state hint gating — UI hide unsafe | R1 attempt-scoped gated GET frozen; assignment GET must stay hint-free | T1b projection strips hints; B/F use `GET …/learner-hints` only | **STILL_VALID_DISCOVERY** (problem statement); **SUPERSEDED_BY_ADR063** (remedy = R1) |
| B2 | Own SUBMITTED evidence may remain readable after roster loss; hints must not | ADR-058 §4/§22 + ADR-063 §6 matrix | B denies post-submit; get_attempt behavior unchanged | **STILL_VALID_DISCOVERY** |
| B3 | Teacher hint authoring UI/API **not implemented** | §7 guarded command + `content.version.create`; no silent grant | Domain `AppendWorksheetLearnerHintsContentVersionService` exists; **no OpenAPI HTTP route**; Teacher FE has **zero** `learner_hint` references | **REQUIRES_RECONCILIATION** → **T0 gap remains** |
| B4 | Preferred **SP01-B-R1** `GET …/attempts/{id}/learner-hints` | Frozen O63-07 list GET | OpenAPI + `routes.py`; PR #72 merged | **SUPERSEDED_BY_ADR063** — **implemented (B)** — **do not reimplement** |
| B5 | Reject **SP01-B-R2** primary (state-filtered assignment DTO) | R2 rejected for primary | Not implemented as primary path | **SUPERSEDED_BY_ADR063** |
| B6 | Hints via **new immutable ContentVersion** + review → approve → publish | §3, §7, GCI-G02/G05 | T1/T2: worksheet@2, attestation table, review/publish gates | **SUPERSEDED_BY_ADR063** — **partially implemented (T1/T2)** — **not Teacher E2E** |
| B7 | Worksheet-first December cut; Quiz/Homework deferred | Founder scope boundary §1 | Only worksheet paths in merged code | **SUPERSEDED_BY_ADR063** |
| B8 | Critical path **T0 → T1 → T2 → B → F** (SP01-14) | RB03 §I DAG: **T1 → T2 ∥ T1b/T1c → T0 (after T1+T2) → B (after T1b+T2) → F → E2E** | **T1/T2/T1b/T1c/B/F merged**; **T0 not** | **REQUIRES_RECONCILIATION** — SP01 sequence is **obsolete DAG** |
| B9 | `ADR_FORWARD_REQUIRED` / discovery not ADR | ADR-063 on `main` (approved) | N/A | **SUPERSEDED_BY_ADR063** |
| B10 | P1 teacher-authored only; P2 AI deferred | O63-05 **DEFERRED** | No P2 code | **STILL_VALID_DISCOVERY** |
| B11 | 22 adversarial scenarios ADV-01–22 | SP02A scenario doc + ADR-063 matrices | B/F tests cover subset; full SP02A E2E **not claimed** | **STILL_VALID_DISCOVERY** (test catalog); **REQUIRES_RECONCILIATION** (execution status) |
| B12 | Five-repo pins @ `491295c3…` / BE `637583f42…` | Issue #68 pins @ `de6f104…` / `e8c715…` / `e884787…` | Evidence links must use **current** SHAs | **HISTORICAL_SOURCE_PIN** in PR #57 body — **not** execution authority |

**Ledger rule:** PR #57 remains valid **as dated discovery**; it is **not** normative policy and must not override ADR-063 or RB03 §I.

---

## C — T0 readiness matrix

**Interpretation:** Student F proving hints in tests **does not** imply Teacher T0 is built. T0 = governed **write** path + Teacher UI + review attestation UX + publish handoff.

| Layer | T1 | T2 | T1b | T1c | B | F | **T0 (teacher authoring)** |
|-------|----|----|-----|-----|---|---|----------------------------|
| Status @ pins | Merged | Merged | Merged | Merged | Merged | Merged | **NOT DELIVERED** |
| BE domain services | `worksheet_v2`, `worksheet_hint_append`, generic append §7.5 guard | QA + `RecordWorksheetLearnerHintAttestationService`, publish attestation gate | `learner_projection` @2 | Assessment `@2` evaluator | `get_learner_hints.py` §8.2 locks | — | `AppendWorksheetLearnerHintsContentVersionService` **internal only** |
| BE HTTP / OpenAPI | Generic content routes; guarded append **not** in OpenAPI | Attestation record **not** exposed as standalone public API in OpenAPI grep | Assignment GET safe | Assessment paths | `learning_attempt_learner_hints_get` | — | **Missing** teacher-facing guarded append + attestation UX APIs |
| FE | — | — | — | — | Student `QuestionLearnerHint`, `getLearningAttemptLearnerHints` | AttemptPage integration | **No** Teacher OS hint editor / class_ref capture / attestation panel |
| Kernel grants | `content.version.create` exists; **no silent tenant grant** | Same | — | — | — | — | Tenant grant provisioning **out of RC01** — still required for real schools |
| E2E teacher → student hint | — | — | — | — | Student slice tested | FE component tests | **No** cross-role authoring E2E |

### C.1 Evidence anchors (Backend `e8c7154e…`)

| Concern | Path |
|---------|------|
| Guarded append command | `src/aieos/domains/content/application/worksheet_hint_append.py` |
| Generic append bypass guard | `HttpAppendContentVersionService` / content routes (T1) |
| Attestation + review gate | `worksheet_hint_attestation_record.py`, `worksheet_hint_attestation_gate.py` |
| Learner hint GET | `src/aieos/domains/learning/application/get_learner_hints.py`, `api/v1/routes.py` |
| Governed hint extraction (publish+approve) | `src/aieos/platform/runtime/worksheet_learner_hints.py` |

### C.2 Evidence anchors (Frontend `e8847871d…`)

| Concern | Path |
|---------|------|
| Student hint UX | `src/features/student-os/attempts/QuestionLearnerHint.tsx`, `AttemptPage.tsx` |
| Student API | `src/services/api/studentLearningApi.ts` |
| Teacher OS | `PreparePage.tsx`, `ReviewDetailPage.tsx` — **no learner-hint fields** (agent `rg` @ pin) |

### C.3 RB03 register lag (**REQUIRES_RECONCILIATION**)

RB03 §H.1 still lists T1–F as `NOT_STARTED` at Architecture `de6f104…` merge time. **Code reality** @ Backend/Frontend pins contradicts register rows. **RC01 does not edit RB03** — Chief may reconcile register in a separate governed Architecture merge.

---

## D — Frozen T0 minimum policy (ADR-063 §7 summary)

Normative source: ADR-063 §§5–7. RC01 restates **T0-only** controls for implementation packet design — **not new policy**.

| Control | Frozen rule |
|---------|-------------|
| Actor | ACTIVE HUMAN Teacher; execution tenant = Content aggregate tenant |
| Capability | Existing **`content.version.create`** + domain gates — **no new capability**; **no silent tenant grant** |
| Ownership | Content **`owner_principal_id` only** — non-owner deny |
| Class authority | Explicit **`authoring_class_ref`** → `SchoolContextClassAuthority.require_assignable_class_ref` |
| Versioning | **New immutable** `education.worksheet` **schema_version == 2** with validated `learner_hint` strings |
| Generic append bypass | **Reject key-present `learner_hint`** on `@2` for generic `POST …/versions` |
| Guarded path only | Only `AppendWorksheetLearnerHintsContentVersion` (conceptual) may append valid hints |
| Review | `content.review.decide` — reviewer **≠ author** when hints present; §5.3 attestation + digest **same transaction** |
| Publish | `content.publish` — publisher **≠ author and ≠ reviewer** when hints present |
| Prohibited SoR | No Review Queue notes / TeachingWork notes / evaluation as hint source |

---

## E — Contract design packet readiness (DESIGN ONLY)

**Status:** Proposed names — **not implemented / not approved API** unless separately authorized.

### E.1 Backend delta (PK-V1-HINT-T0-B-I01 — proposal)

| Item | Today @ `e8c7154e…` | T0 delta |
|------|---------------------|----------|
| Guarded append HTTP | Domain service only | Expose governed command (e.g. `POST /api/v1/contents/{content_id}/worksheet-learner-hint-versions` or Content sub-resource) wiring `AppendWorksheetLearnerHintsContentVersionService` |
| DTO | Internal pydantic models | OpenAPI request: payload + **`authoring_class_ref`** + idempotency |
| Attestation record API | `RecordWorksheetLearnerHintAttestationService` internal | Reviewer-facing record endpoint or embed in review flow per existing Teacher patterns — **must not** use Review Queue free text |
| Reuse | `content.review.submit`, `content.review.decide`, `content.publish` | **Reuse** where ADR-063 §7.3 already correct |

### E.2 Frontend delta (PK-V1-HINT-T0-F-I01 — proposal)

| Item | Today @ `e8847871d…` | T0 delta |
|------|----------------------|----------|
| Worksheet editor | Prepare/review flows without per-question hints | Per-question optional `learner_hint` editor on **new version** path only |
| Class context | Existing class pickers elsewhere | Capture **`authoring_class_ref`** on hint-bearing append |
| Reviewer UX | Review approve/reject | Structured attestation view: mechanical QA flags + `human_review_pass` per question (ADR-063 §5.3) |
| Publish | Existing publish | Unchanged semantics; enforce publisher ≠ author/reviewer when hints present |

### E.3 Explicit non-goals for T0 packets

- No duplicate B `learner-hints` GET or F AttemptPage affordance
- No Parent/Principal surfaces
- No kernel grant seeding in Architecture-only work
- No Quiz/Homework schema

---

## F — Test matrix (design partition — RC01 does not claim execution)

| Area | Happy path | Representative negatives |
|------|------------|-------------------------|
| **T0-B HTTP** | Owner + grant + valid class_ref → guarded append creates @2 version | Owner mismatch; missing grant; invalid ClassRef; wrong tenant; generic append with `learner_hint` key (all shapes) |
| **T0 review** | Independent reviewer + attestation digest match → APPROVE | Reviewer = author; missing attestation; digest mismatch |
| **T0 publish** | Separate publisher with `content.publish` | Publisher = author/reviewer; publish without APPROVE |
| **B (existing)** | IN_PROGRESS owner GET hints | SUBMITTED deny; wrong attempt; membership revoked |
| **F (existing)** | UI shows hints when API returns | No hint DOM when API denies |
| **Leakage** | — | Assignment GET / attempt resource without hint bodies; answer/explanation/teacher-note absent from hint DTO |
| **SP02A** | Cross-reference scenario IDs | Map ADV-* / SP02A cases to BE HTTP / FE component / cross-repo E2E tiers |

**Merged slice tests (exist @ pins — RC01 does not re-run):** e.g. Backend `tests/domains/learning/test_aieos_v1_hint_b.py`; Frontend `attempt.learner-hint.test.tsx`, `learnerHintPolicy.test.ts`.

---

## G — Reconciliation disposition (draft PRs — no RC01 mutation)

| Artifact | Recommendation | Rationale |
|----------|----------------|-----------|
| **Arch PR #57 SP01** | **Close unmerged / archive as historical discovery** after Chief accepts RC01; optional future merge **only** as dated PROPOSED appendix with banner — **not** as live execution DAG | Superseded by ADR-063 + merged T1–B/F; obsolete T0-first ordering; base `491295c3…` far behind `main` |
| **Arch PR #55 EX01** | **Remain OPEN/DRAFT** — separate Founder scope decision | Unrelated to hint T0 except programme context |
| **Arch PR #53 DR01** | **Remain OPEN/DRAFT** — feeds PK-DSC-SP01 gap themes only | Historical pins stale |
| **Arch PR #51 + Product #3 I08** | **Remain OPEN/DRAFT** — Founder acceptance separate | No RC01 overlap |
| **This RC01 PR** | **OPEN DRAFT — NOT MERGED** this workday | Chief exact-head review required |

**DEC-SP01-01 (RB03 §M.5):** Recommend **archive #57** rather than merge-as-normative; execute only with separate Founder + Chief authorization — **not** standing delegation.

---

## H — Delivery next-step (bounded packets — NOT AUTHORIZED in RC01)

Sequence per reconciled RB03 §I (post T1/T2/T1b/T1c/B/F):

```text
PK-V1-HINT-T0-B-I01  →  PK-V1-HINT-T0-F-I01  →  PK-V1-HINT-E2E-I01 (real stack, after T0+B+F)
```

| Packet | Scope | Depends on |
|--------|-------|------------|
| **PK-V1-HINT-T0-B-I01** | Teacher guarded append HTTP + attestation/review wiring per §E.1 | T1+T2 merged (**satisfied**); RC01 reconciliation merged (**governance**) |
| **PK-V1-HINT-T0-F-I01** | Teacher editor + reviewer attestation UI per §E.2 | T0-B contract pin |
| **PK-V1-HINT-E2E-I01** | SP02A adversarial suite on real stack | T0 + existing B + F |

Each packet: separate issue, file whitelist, tests, single-review merge gate — **no** RC01 code launch.

---

## I — Remaining decisions / STOP

| ID | Topic | Owner | Status |
|----|-------|-------|--------|
| I1 | Merge vs archive PR #57 | Chief + Founder | **OPEN** — RC01 recommends archive |
| I2 | RB03 §H.1 row status vs merged code | Chief Architecture | **OPEN** — register update separate PR |
| I3 | Exact HTTP shape for guarded append | Chief + Backend | **OPEN** — §E.1 proposals |
| I4 | Tenant `content.version.create` grants for pilot schools | Founder / Admin | **OPEN** — not Architecture-only |
| I5 | PK-V1-HINT-E2E timing vs Dec 18 target | Founder programme | **OPEN** — preserve **NO_CUT**; Dec 18 = development target **AT RISK** per ADR-063 |
| I6 | Nov 20 showcase / human UAT / production | Founder gates | **Unchanged** — RC01 creates no readiness claims |

**Settled (do not reopen as discovery):** R1 hint GET, worksheet@2, §5.3 attestation, §7.5 generic bypass, author ≠ reviewer ≠ publisher, IN_PROGRESS-only disclosure — all **frozen in ADR-063**.

---

## Governance self-check (RC01)

| Check | Result |
|-------|--------|
| Single new file only | **PASS** (this document) |
| Base = exact Architecture `main` @ gate | **PASS** |
| No draft PR edits | **PASS** |
| No implementation code | **PASS** |
| No Architecture CI false claim | **PASS** |
| SP01 not rewritten — classified against evidence | **PASS** |
| B/F not duplicated in T0 scope | **PASS** |

---

**STOP — PK-DSC-SP01-RC01 — CHIEF EXACT-HEAD REVIEW REQUIRED — NOT MERGED — NO T0 IMPLEMENTATION**