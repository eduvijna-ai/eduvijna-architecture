---
id: AIEOS-V1-SP01
title: Student Practice & Formative Instructional Feedback — Architecture Discovery
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: PROPOSED / DISCOVERY — CHIEF REVIEW PENDING
version: 1.0.0
created: 2026-11-02
last_updated: 2026-11-02
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# AIEOS-V1-SP01 — Student Practice & Formative Instructional Feedback Architecture Discovery

**Identity:** `AIEOS-V1-SP01` (PATH-STUDENT-PRACTICE)  
**Founder authorization:** 2026-11-02 — architecture discovery only for AIEOS V1-EXPAND; preserve ADR-AIEOS-058 / 059 / 061 authority; no implementation until architecture review and separate Founder scope/ADR authorization.  
**Mode:** **PROPOSED / DISCOVERY — CHIEF REVIEW PENDING** — not an ADR freeze, not Product authorization, not a code workday, not a merge authorization.  
**Governing workday:** [Architecture Issue #56](https://github.com/eduvijna-ai/eduvijna-architecture/issues/56)  
**Distinct from:** [EX01R1 PR #55](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) (OPEN / DRAFT / NOT MERGED — do not edit or merge).

**Terminal disposition (this package):** **AIEOS-V1-SP01 — DISCOVERY DRAFT PR OPEN / ARCHITECTURE REVIEW PENDING / DEC18 FEATURE NOT YET RATIFIED / IMPLEMENTATION NOT AUTHORIZED**

---

## Executive summary

At pinned governed sources, the Student OS already delivers a complete **assign → start attempt → save responses → submit → read-only submitted view** journey with learner-safe ContentVersion projection, explicit no-grade copy, and Parent/Principal/Teacher boundaries enforced in code and frozen ADRs. **Genuine new learner-visible practice or formative instructional feedback** (correctness, hints tied to answers, post-evaluation student feedback, retries, or scoring) **cannot be implemented without explicit forward ADR decisions**. Cosmetic copy duplicates (including EX01R1-withdrawn S02A) are **not** acceptable December P0 candidates.

**Discovery recommendation (not ratified):** If Founder selects a named December V1-EXPAND development item in this path, the **smallest defensible educational slice** is **Option SP01-B — teacher-authored learner-safe instructional hints** projected to Student **only during `IN_PROGRESS`**, sourced from governed Content preparation with a **positive allowlist extension** to ADR-AIEOS-027 learner projection — **not** from Assessment evaluation or Answer Key leakage. This remains **`ADR_FORWARD_REQUIRED` / BLOCKED FOR CODING** until a separate ADR package is frozen and Founder scope is ratified.

---

## SP01-01 — Exact source pins and open-PR preflight

**Preflight executed:** 2026-11-02 (UTC) immediately before first write. **Result: PASS** — no mismatch; authorization not expired.

### Remote `origin/main` identity

| Repository | Required SHA | Verified SHA | Method |
|------------|--------------|--------------|--------|
| `eduvijna-ai/eduvijna-architecture` | `491295c3cf0a151f31686a6a2e1a2176cd92c782` | **MATCH** | `git fetch origin main` in Architecture worktree |
| `eduvijna-ai/eduvijna-product` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | shallow clone + `git fetch origin main` |
| `eduvijna-ai/eduvijna-aieos-backend` | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | shallow clone + `git fetch origin main` |
| `eduvijna-ai/eduvijna-aieos-frontend` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** | shallow clone + `git fetch origin main` |
| `eduvijna-ai/eduvijna-aieos-infrastructure` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | shallow clone + `git fetch origin main` |

### Backend contract pins

| Pin | Required | Verified |
|-----|----------|----------|
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** (`sha256sum`) |
| Alembic head | `a360s010004` | **MATCH** (no migration lists `a360s010004` as `down_revision`) |

### Architecture worktree

| Check | Result |
|-------|--------|
| Branch base for this discovery | `491295c3cf0a151f31686a6a2e1a2176cd92c782` |
| Tracked worktree clean before write | **PASS** (`git status --porcelain` empty on `main`) |
| Architecture GitHub Actions | **NO CI CONFIGURED** (`.github/workflows/.gitkeep` only) |

### Open draft PR governance (unchanged / not merged)

| PR | Repo | State | Draft | Head OID | Notes |
|----|------|-------|-------|----------|-------|
| [#55 EX01R1](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) | Architecture | OPEN | yes | `8b1d07692e1698cf2be9d338f6d45a1707719146` | Base `491295c3…` — **not edited by SP01** |
| [#53 DR01](https://github.com/eduvijna-ai/eduvijna-architecture/pull/53) | Architecture | OPEN | yes | `70986a013ce776257f739eff6ab89727d6715df9` | Unchanged |
| [#51 I08](https://github.com/eduvijna-ai/eduvijna-architecture/pull/51) | Architecture | OPEN | yes | `87725067d3aa9f39dff05e634f71b05d8da85cd0` | Unchanged |
| [#3 I08-P](https://github.com/eduvijna-ai/eduvijna-product/pull/3) | Product | OPEN | yes | `90511df0358dcee1236adcde73659bfb2be95e37` | Unchanged |

**Fail-closed rule:** Any future drift of the above identities or unauthorized merge of #55 / #53 / #51 / Product #3 → **STOP — AIEOS-V1-SP01 AUTHORIZATION EXPIRED — GOVERNED SOURCE MOVED**.

---

## SP01-02 — December 18 development boundary (from EX01R1 / programme)

Recovered from [EX01R1 document on PR #55 head](https://github.com/eduvijna-ai/eduvijna-architecture/blob/8b1d07692e1698cf2be9d338f6d45a1707719146/AIEOS/AIEOS-V1-EX01-EXPANDED-DECEMBER-FEATURE-SCOPE-AND-CODE-PACKETS.md) and frozen roadmap references therein:

| Milestone | Meaning for SP01 |
|-----------|------------------|
| **Nov 20, 2026 (engineering showcase)** | Integrated cross-role rehearsal (CX01-I07 substrate); **not** the same as ratified V1-EXPAND product-development scope. Student submitted banner + showcase Teacher Assess handoff already support showcase narrative. |
| **2026-12-18** | **Development-ready** target for **Founder-ratified named** V1-EXPAND scope — integrated persona experiences under explicit scope — **not** UAT, **not** production, **not** automatic merge of 2027 depth. |
| **2027-01-29 Experience Depth** | UX polish items (e.g. W01 UX-03 dual chrome) explicitly **deferred** unless promoted. |
| **2027-01-29 → 2027-05-28** | Original AIEOS programme breadth (EIS depth, richer intelligence, etc.) **preserved** — must not be silently absorbed into December. |

**EX01R1 binding for Student practice:** Post-submit learner-safe “what happens next” **copy** = **`ALREADY_IMPLEMENTED`**. **Genuine** learner practice or response-level feedback = **`NEW_ADR_REQUIRED`** at Frontend pin. **S02A withdrawn** as P0; **S05** = optional operator UX only.

**SP01 does not ratify December scope.** Founder must separately accept a named learner-benefit slice after Chief review of this discovery.

---

## SP01-03 — Current Student UI (Frontend `569ef8be…`)

Evidence paths are relative to [eduvijna-aieos-frontend @ `569ef8be46617ab1412ddb3f5a0214c40bdb946b`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/tree/569ef8be46617ab1412ddb3f5a0214c40bdb946b).

### Routing and shell

| Surface | Path / file | Behavior |
|---------|-------------|----------|
| Student shell | `src/app/router.tsx` — `/student-os/*` under `StudentOsShell` | Role-isolated routes; Teacher routes remain separate (architecture test L103–109). |
| Home | `src/features/student-os/home/` | Lists assignments via `student_os_home` API. |
| Assignment list | `src/features/student-os/assignments/AssignmentsPage.tsx` | Cursor pagination via `next_cursor`; no fabricated offsets (architecture test L86–96). |
| Assignment detail | `src/features/student-os/assignments/AssignmentDetailPage.tsx` | Shows learner work preview, availability, **Start** / **Resume** attempt with idempotency (L35–80, start flow uses `startLearningAttempt`). |
| Attempt | `src/features/student-os/attempts/AttemptPage.tsx` | Core journey (below). |

### AttemptPage — actual behavior

| Concern | Location | Behavior |
|---------|----------|----------|
| Load attempt | L113–141 | `getLearningAttempt`; loads assignment unless SUBMITTED and assignment list miss (L129–134). |
| Read-only after submit | L147, L265–276 | `lifecycle_state === "SUBMITTED"` → no editors; **persistent Submitted banner** with explicit **no grade/score** copy (L271–275). |
| In progress | L278–281, L294–302 | `ResponseEditor` + Save / Submit with `If-Match` + `Idempotency-Key` (architecture test L86–100). |
| Submitted answers | L41–69, L304 | When no live questions, lists raw submitted values (no correctness). |
| Showcase handoff | L341–347 | External link to Teacher Assess intelligence for same assignment — **showcase only**, not student feedback. |
| Forbidden integrations | `student-os.architecture.test.ts` L74–84 | No Assessment intelligence, mastery, or Postgres in Student OS sources. |

### Tests anchoring behavior

| Test file | What it proves |
|-----------|----------------|
| `src/features/student-os/student-os.architecture.test.ts` | OpenAPI digest pin, required operation IDs, privacy forbiddens. |
| `e2e-student-product/student-os-assignment-attempt.product.spec.ts` | Product E2E including submitted reload read-only (comment W). |
| `e2e-aieos360-cx01-i07/integrated-showcase-rehearsal.product.spec.ts` | Submitted banner visible in integrated showcase. |

**Conclusion:** Student UI is **not** a thin placeholder; adding only copy or banner variants would **duplicate EX01R1 ALREADY_IMPLEMENTED** and must be rejected as December P0.

---

## SP01-04 — Backend Learning attempt / submission (Backend `637583f42…`)

### HTTP surface (Learning domain)

From `src/aieos/domains/learning/api/v1/routes.py` and architecture tests (`test_aieos360_s01_i03_architecture.py`):

| Operation | Path | Student actor |
|-----------|------|---------------|
| Home | `GET /api/v1/student-os/home` | Current roster-eligible assignments |
| List / get assignment | `GET /api/v1/student-os/assignments`, `…/{assignment_id}` | Learner-safe resource embedded |
| Start attempt | `POST /api/v1/learning/assignments/{assignment_id}/attempts` | Creates / returns `IN_PROGRESS` |
| Get attempt | `GET /api/v1/learning/attempts/{attempt_id}` | Owner learner only |
| Save responses | `PUT /api/v1/learning/attempts/{attempt_id}/responses` | **`IN_PROGRESS` only** |
| Submit | `POST /api/v1/learning/attempts/{attempt_id}/actions/submit` | **`IN_PROGRESS` → `SUBMITTED`** |

Frontend mirror: `src/services/api/studentLearningApi.ts` (pinned by architecture test).

### Mutability vs immutability

| Stage | Domain authority | Immutable after |
|-------|------------------|-----------------|
| Working responses | `AttemptResponseItems` on `LearnerAttempt` | **Submit** — aggregate transitions to `SUBMITTED` with `submission_id` |
| Raw evidence | `LearnerSubmission` | **Created at submit** — append-only evidence for Assessment |
| Attempt lifecycle | ADR-AIEOS-058 | **`IN_PROGRESS` → `SUBMITTED` only** — no retry/abandon in product policy |

Domain enforcement example: `LearnerAttempt` in `src/aieos/domains/learning/domain/attempt.py` — SUBMITTED requires `submitted_at` + `submission_id`; IN_PROGRESS forbids them (L119–128).

**No student API** exists to mutate post-submit state or start a second attempt for the same assignment without violating frozen ADR-058.

---

## SP01-05 — Assessment evaluation & Teacher Intelligence (separate boundary)

Assessment routes (`src/aieos/domains/assessment/api/v1/routes.py`) are **teacher-authorized** only — e.g.:

- `POST /api/v1/assessment/submissions/{submission_id}/actions/evaluate`
- `POST /api/v1/assessment/assignments/{assignment_id}/actions/ensure-evaluations`
- `GET /api/v1/assessment/assignments/{assignment_id}/intelligence`

**No** `/api/v1/student-os/…` or learner-facing evaluation GET exists.

### Restricted evaluation fields (teacher-only today)

`LearnerAssessmentEvaluationItemResponse` (`models.py` L58–66): `outcome`, `evaluation_method`, `objective_ids` — suitable for **Teacher Assess** and Improve handoff, **not** authorized for Student/Parent/Principal projection per ADR-AIEOS-059 / 061 / 060.

Teacher intelligence aggregates (`TeacherAssessmentIntelligenceResponse`) expose class distributions and per-learner evaluation joins — **explicitly forbidden** in Student OS static architecture guards.

**Binding invariant:** Submit ≠ Evaluate ≠ Feedback ≠ Mastery. Student must not receive evaluation DTOs by “reusing” teacher APIs or mapping evaluation outcomes into Student responses without forward ADR.

---

## SP01-06 — Content, learner projection, answer-leakage risk

### Learner-safe projection (positive allowlist)

`src/aieos/domains/learning/application/learner_projection.py`:

- Supports **Worksheet / Quiz / Homework** typed payloads only (L42–46).
- Builds `LearnerQuestion` with `id`, `prompt`, `question_type`, `options` only (L106–112).
- **Does not** pass through full payload; **does not** include `answer_key`, `teacher_notes`, or rubric fields.

### Teacher-only artifacts

Preparation pipeline (`domains/education/application/preparation_artifacts.py`, `domains/teaching/application/prepare.py`) maintains **AnswerKeyV1** and teacher notes as distinct artifacts. Quality baseline checks reference `answer_key_complete` — those artifacts are **not** in learner projection.

### Conceptual leakage tests (architecture)

| Risk | Current guard | If SP01 added unchecked feedback |
|------|---------------|----------------------------------|
| Multiple-choice key in options ordering | Options are visible to learner already — **content authoring** must not embed keyed answers in prompts | Automated “correct/incorrect” would expose key via Assessment |
| Short-answer exact match | No learner-side grading | String match feedback leaks teacher key |
| Hint text copied from AnswerKey | Not projected | Blind copy from AnswerKey → **critical leakage** |
| Post-submit “explainer” from evaluation | Not exposed | Mapping `outcome=CORRECT` → student UI → violates ADR-059 |

Any learner-visible instructional text must be **authoring-time**, **audited**, and **allowlisted** — not derived from `LearnerAssessmentEvaluation`.

---

## SP01-07 — Design options (2–4 learner-benefit candidates)

Each option is a **candidate**, not approved product.

### Option SP01-A — In-progress progress & self-review checklist (no correctness)

| Dimension | Detail |
|-----------|--------|
| **Student story** | While working, I see which questions still need an answer and can review my drafts before submitting — without being told if I am right. |
| **Missing today** | Partial — progress label exists; no structured per-question “unanswered” checklist or navigation affordances beyond scrolling. |
| **Best case** | Better completion rates and fewer accidental blank submits; stays within ADR-058 single submit. |
| **Worst case** | Perceived as cosmetic; EX01R1 may classify as polish not V1-EXPAND P0. |
| **New data/commands** | **None** if purely client-side over existing GET + save; optional server-side “completion summary” would be new read DTO. |
| **ADR** | **`NO_ADR_NEEDED`** only for pure UI over existing attempt + questions; **`ADR_FORWARD_REQUIRED`** if new Learning read models or semantics (e.g. “practice pass”). |

### Option SP01-B — Teacher-authored learner-safe hints (IN_PROGRESS only) — **discovery preference**

| Dimension | Detail |
|-----------|--------|
| **Student story** | My teacher attached optional hints to hard questions; I can open them while working, but I still submit once and I am not told my score. |
| **Missing today** | No hint fields in `LearnerResource` / projection; prompts only. |
| **Best case** | Genuine formative support without grading or second attempts; hints authored and reviewed at preparation time. |
| **Worst case** | Hints authored from AnswerKey copy → leakage; hints visible after submit → policy ambiguity. |
| **New data/commands** | **Yes — proposal:** optional `learner_hint` (or structured hint block) on question or assignment in ContentVersion payload, projected only in learner DTO; **no** new attempt state. |
| **ADR** | **`ADR_FORWARD_REQUIRED`** — extend ADR-AIEOS-027 allowlist + preparation QA; narrow ADR-058 clarification that hints do not alter lifecycle; Content schema + OpenAPI + projection tests. |

### Option SP01-C — Teacher-deliberate post-submit formative message (non-evaluative)

| Dimension | Detail |
|-----------|--------|
| **Student story** | After my teacher reviews the class, they release a short class or personal message about what to practice next — not an automatic grade. |
| **Missing today** | No Teaching or Learning artifact for student-readable teacher feedback tied to assignment/attempt. |
| **Best case** | Clear human feedback loop without exposing evaluation machinery. |
| **Worst case** | Becomes shadow grading if text correlates with evaluation outcomes; Parent visibility disputes under ADR-061. |
| **New data/commands** | **Yes — proposal:** new governed write (Teacher) + read (Student) with explicit non-score semantics and audit. |
| **ADR** | **`ADR_FORWARD_REQUIRED`** — new ADR or ADR-059/053 forward revisions; likely **medium/large** December slice. |

### Option SP01-D — Student-visible evaluation subset (correctness / objectives after submit)

| Dimension | Detail |
|-----------|--------|
| **Student story** | After submit (or after teacher evaluates), I see which questions were correct and what to study. |
| **Missing today** | **By design** — evaluation is Assessment-owned and teacher-intelligence-projected. |
| **Best case** | Strong feedback loop. |
| **Worst case** | Collapses Submit ≠ Evaluate boundary; Parent `EVALUATION_EXISTENCE=NO`; Principal aggregation re-identification; open-response policy leakage. |
| **New data/commands** | Student GET of evaluation or derived feedback — **major** new surface. |
| **ADR** | **`ADR_FORWARD_REQUIRED`** (ADR-059 + 061 + possibly 060) — **not recommended** as smallest December slice. |

---

## SP01-08 — Option comparison matrix

| Option | Classification | December coding without ADR? | Genuine new learner benefit? |
|--------|----------------|------------------------------|------------------------------|
| **SP01-A** | `NO_ADR_NEEDED` (UI-only) / `ADR_FORWARD_REQUIRED` (if server semantics) | UI-only: yes but **weak P0** | Marginal — risk duplicate of EX01 “already implemented” journey |
| **SP01-B** | **`ADR_FORWARD_REQUIRED`** | **NO — BLOCKED FOR CODING** | **Yes** — bounded formative hints |
| **SP01-C** | **`ADR_FORWARD_REQUIRED`** | **NO** | Yes — but larger governance surface |
| **SP01-D** | **`ADR_FORWARD_REQUIRED`** | **NO** | Yes — **conflicts** with frozen privacy posture |
| **Retry / practice attempt** | **`NOT_FEASIBLE`** without ADR-058 change | **NO** | Violates one-attempt policy |
| **Expose Teacher Intelligence to Student** | **`NOT_FEASIBLE`** | **NO** | Violates ADR-059 / Frontend guards |
| **Copy-only S02A revival** | **`NOT_FEASIBLE`** as P0 | N/A | EX01R1 **`ALREADY_IMPLEMENTED`** |
| **EIS / mastery personalization** | **`DEFER_2027`** | **NO** | Programme item beyond December |

**Honest December P0 statement:** There is **no** `SOURCE_VERIFIED_MISSING` + **`NO_ADR_NEEDED`** educational P0 for genuine practice/feedback at current pins. **Safe meaningful December feature requires ADR forward** (prefer **SP01-B**). **Do not fabricate** an artificial no-ADR P0.

---

## SP01-09 — Recommended December v1 thin slice (proposal only — not ratified)

**Working name (requires Founder ratification):** `V1-EXPAND-STUDENT-LEARNER-HINTS-V1`

| Element | Constraint |
|---------|------------|
| **Student OS** | On `AttemptPage` while `IN_PROGRESS`, optional collapsible hint per question when present in learner projection. |
| **Minimum positive experience** | Student can get teacher-approved scaffolding during work; submit flow unchanged; post-submit still read-only banner without score. |
| **Failure / empty** | No hints → UI identical to today; hint fetch errors → fail silent or generic “hint unavailable” without leaking answers. |
| **Reload** | Hints reloaded with assignment resource; no separate hint session state. |
| **Content types** | Worksheet / Quiz / Homework only (same as projection). |
| **Teacher control** | Hints authored in preparation / publish path; never auto-generated from evaluation in v1. |
| **Prohibited semantics** | No correctness, no score, no retry, no post-submit hint that reveals key, no Parent evaluation existence change. |
| **Frozen ADRs extended (not overwritten)** | ADR-AIEOS-027 (learner allowlist), ADR-AIEOS-058 (lifecycle unchanged), ADR-AIEOS-059 (no student evaluation), ADR-AIEOS-061 (no new parent fields without decision). |

**Optional additive (if Founder wants zero ADR):** ship **SP01-A** UI checklist only — Chief should treat as **polish**, not PATH-STUDENT-PRACTICE core outcome.

---

## SP01-10 — Ownership & data path (proposals only)

### Recommended path for SP01-B

```text
Teacher Prepare/Review/Publish (existing)
        ↓
ContentVersion payload (+ optional learner_hint fields, authoring-time QA)
        ↓
Learning learner_projection.project_learner_resource (extended allowlist)
        ↓
GET student-os/assignments/{id} / attempt context (existing APIs)
        ↓
Student AttemptPage (IN_PROGRESS display only)
```

| Concern | Owner |
|---------|--------|
| Hint text SoR | **ContentVersion** payload (authoritative artifact), not Learning or Assessment |
| Attempt / submit SoR | **Learning** (unchanged ADR-058) |
| Evaluation / correctness | **Assessment** — **not used** for hints in v1 |
| Teacher write path | **Teaching / Content** preparation commands (existing eligibility gates) |
| Idempotency | No new mutations on Learning for hint read |

**New API need (proposal):** Prefer **none** — extend existing assignment/attempt resource DTOs. If hints are large, optional `GET …/hints` with same authorization as assignment — **OpenAPI change gated separately**.

---

## SP01-11 — Visibility & authorization matrix

Legend: ✓ allowed · ✗ denied · ◐ derived allowlist only · — not applicable

| Capability | Student A (owner) | Student B | Wrong tenant | Revoked roster | Teacher (current class) | Teacher (lost class) | Parent (linked) | Principal |
|------------|-------------------|-----------|--------------|----------------|-------------------------|----------------------|-----------------|-----------|
| View assignment + learner work | ✓ | ✗ | ✗ | ✗ | ✓ (teacher routes) | ✗ | ◐ assignment facts only | — |
| IN_PROGRESS hints (SP01-B) | ✓ | ✗ | ✗ | ✗ | ✓ via prepare, not student API | ✗ | ✗ | ✗ |
| Save / submit attempt | ✓ own | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| Submitted answers (own) | ✓ read-only | ✗ | ✗ | ✗ | ✓ via review/intelligence | ✗ | ◐ status/submitted fact | ✗ drill-down |
| Evaluation items/outcomes | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ (`EVALUATION_EXISTENCE=NO`) | ✗ aggregate only |
| Answer key / teacher notes | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |
| Post-submit “feedback” (SP01-C) | ◐ if ADR defines | ✗ | ✗ | ✗ | ✓ author | ✗ | ◐ unless ADR forbids | ✗ |

**Fail-closed:** All checks use **current** tenant, **current** roster membership, and **current** teacher class authority — stale JWT or UI cache is not authority (ADR-058 / 059 / 062).

---

## SP01-12 — Adversarial architecture scenarios (14)

| ID | Scenario | Expected fail-closed behavior |
|----|----------|-------------------------------|
| **ADV-01** | Student B requests Student A `attempt_id` | 404/403 — owner binding |
| **ADV-02** | Second `POST …/attempts` while `IN_PROGRESS` exists | Reject or idempotent return — **no** second concurrent attempt (policy) |
| **ADV-03** | `PUT …/responses` after `SUBMITTED` | Reject — immutability |
| **ADV-04** | Submit with stale `If-Match` after save | Conflict — client reload |
| **ADV-05** | Submit with empty responses | Legal per ADR-059 unanswered evidence — UI should not promise “complete” scoring |
| **ADV-06** | Learner hints visible after submit (SP01-B bug) | Must hide — post-submit is evidence-only view |
| **ADV-07** | Hint text equals answer key entry | Authoring QA must block or flag — leakage |
| **ADV-08** | Student calls Teacher `…/intelligence` | 403 — role kernel |
| **ADV-09** | Parent polls for evaluation existence | Deny — ADR-061 |
| **ADV-10** | Principal attempts learner drill-down via feedback feature | Deny — ADR-060 aggregates only |
| **ADV-11** | Revoked roster member opens deep link to attempt | Deny on authoritative membership check |
| **ADV-12** | Stale assignment publication (student started old version) | Attempt bound to exact `content_version_id` at start — no silent upgrade |
| **ADV-13** | Evaluation not yet run — student expects feedback (SP01-D) | No student evaluation surface — banner unchanged |
| **ADV-14** | Provider/DB failure during save | Student sees retry-safe message; no partial submit |

---

## SP01-13 — ADR forward decision ledger (proposals — no ADR drafted here)

### Decision package D1 — Learner-safe instructional hints (for SP01-B)

| Question | Alternatives | Compatibility / tests |
|----------|--------------|------------------------|
| Where do hints live? | (a) ContentVersion payload field; (b) separate Content child artifact | (a) matches exact-version assignment binding; migration of published content |
| When visible? | (a) IN_PROGRESS only; (b) include post-submit | **Require (a)** for v1 to reduce leakage |
| Who authors? | Teacher preparation only vs AI-generated | AI hints require existing provider governance — **out of SP01 v1** |
| Leakage controls? | Positive allowlist + preparation lint vs manual review | Extend DEV04-style checks; block hint==key |
| Parent visibility? | Default **none** | Preserve ADR-061 allowlist |

**Likely touch:** ADR-AIEOS-027 forward revision; ADR-AIEOS-058 non-lifecycle extension note; preparation quality baseline docs.

### Decision package D2 — Post-submit teacher formative message (SP01-C)

| Question | Notes |
|----------|-------|
| New aggregate vs TeachingWork comment? | Must not collide with Improve remediation SoR (ADR-056) |
| Correlation with evaluation | Must not auto-publish from `LearnerAssessmentEvaluation` without teacher deliberate action |
| Parent visibility | Explicit deny by default |

**Likely touch:** New ADR or ADR-059/053 forward revision — **defer** if December scope tight.

### Decision package D3 — Student evaluation visibility (SP01-D)

**Recommendation:** **Do not pursue** for December thin slice — high privacy and ADR fan-out.

### No decision needed

**SP01-A** UI-only checklist — document in Product polish backlog if Founder accepts non-ADR December item.

---

## SP01-14 — Engineering critical-path proposal (separately gated — not authorized)

**Assumes:** Founder ratifies **SP01-B** + ADR D1 frozen + implementation workday authorized.

| Slice | Scope | Size | Depends on |
|-------|-------|------|------------|
| **B1 Content schema + QA** | Optional hint fields in worksheet/quiz/homework schemas; preparation lint | M | ADR D1 |
| **B2 Learning projection** | Extend `learner_projection.py` + models + tests | S | B1 |
| **B3 OpenAPI + consumer snapshot** | DTO fields on student assignment resource | S | B2 |
| **F1 Student Attempt UI** | Hint affordance IN_PROGRESS; architecture guard tests | S | B3 |
| **E2E** | Extend student product spec — hint visible, absent post-submit | S | F1 |

**Smallest demo:** One fixture assignment with two questions, one hint, student opens hint, submits, hint hidden after submit.

**Regression gates:** Existing S01 architecture tests; student-os.architecture forbiddens; parent/principal privacy tests unchanged.

**Risks to 2026-12-18:** ADR review latency; schema migration authorization; accidental coupling to Assessment evaluation; scope creep into SP01-D.

**2027 preserved:** Full learner intelligence, mastery, personalized recommendations, Parent evaluation policies, EIS depth — **not in December slice**.

---

## SP01-15 — Evidence deposit & gates

| Item | Status |
|------|--------|
| This document | **Deposited** as sole writable artifact on SP01 branch |
| Secret hygiene | Synthetic examples only; no credentials |
| Architecture CI | **NO CI CONFIGURED** — do not claim CI pass |
| Draft PR | Open **DRAFT / NOT MERGED** for Chief review |
| Implementation | **NOT AUTHORIZED** |
| December feature | **NOT YET RATIFIED** |
| ADR freeze | **NOT AUTHORIZED** |

---

## Approval / nonapproval matrix

| Gate | Who | Status |
|------|-----|--------|
| SP01 discovery complete | Cursor agent | **Complete pending PR** |
| Chief exact-head discovery review | Chief AI Enterprise Architect | **PENDING** |
| Founder named December learner-benefit | Founder | **NOT APPROVED** |
| ADR candidate drafting | Architecture office | **NOT AUTHORIZED** |
| Scenario validation / ADR freeze | Chief + Founder | **NOT AUTHORIZED** |
| Implementation slice | Engineering | **NOT AUTHORIZED** |
| Merge of SP01 PR | Governance | **NOT AUTHORIZED** |

---

## Completion report (Issue #56 §5 — items A–L)

### A — Exact source pins

All five repository `origin/main` SHAs, OpenAPI SHA-256, and Alembic head **`a360s010004`** verified **MATCH** (§ SP01-01).

### B — Open-PR state

#55 OPEN/DRAFT head `8b1d076…`; #53, #51, Product #3 OPEN/DRAFT — unchanged (§ SP01-01).

### C — Branch / base / head / parent

| Field | Value |
|-------|-------|
| Repository | `eduvijna-ai/eduvijna-architecture` |
| Branch | `cursor/sp01-student-practice-discovery-89ba` |
| Base | `491295c3cf0a151f31686a6a2e1a2176cd92c782` |
| Head | *(commit SHA recorded at PR open)* |
| Parent programme | PATH-STUDENT-PRACTICE / Issue #56; distinct from EX01R1 #55 |

### D — One-file diff

**Only** `AIEOS/AIEOS-V1-SP01-STUDENT-PRACTICE-FEEDBACK-ARCHITECTURE-DISCOVERY.md` added.

### E — Existing implementation proof

Student Attempt journey, submitted banner, Learning APIs, learner projection allowlist, Assessment teacher-only evaluation — § SP01-03–06 with repository path anchors.

### F — Alternatives & preferred benefit

Options SP01-A through SP01-D (§ SP01-07–08). **Preferred bounded candidate:** **SP01-B** learner-safe hints during `IN_PROGRESS`.

### G — ADR changes needed

**ADR_FORWARD_REQUIRED** for any genuine practice/feedback P0; decision packages D1–D3 (§ SP01-13). **No** no-ADR educational P0.

### H — Per-role privacy gates

Visibility matrix § SP01-11; Parent evaluation denial preserved.

### I — Adversarial scenarios

14 scenarios § SP01-12 (ADV-01–ADV-14).

### J — Feasibility / date / cut lines

December **development** target requires Founder ratification + ADR before coding; **BLOCKED FOR CODING** today; Nov 20 showcase and 2027 programme preserved (§ SP01-02, SP01-14).

### K — Checks / links

Architecture **NO CI CONFIGURED**; governed links to frozen ADRs at Architecture `491295c3…`; Backend/Frontend pins cited via GitHub blob URLs in body.

### L — Draft PR & unapproved work

Draft PR to be opened on branch `cursor/sp01-student-practice-discovery-89ba`. **Unapproved:** ADR drafting, Backend/Frontend implementation, OpenAPI merge, Founder UAT, scope ratification, merge.

---

**STOP — AIEOS-V1-SP01 — DISCOVERY DRAFT PR OPEN / ARCHITECTURE REVIEW PENDING / DEC18 FEATURE NOT YET RATIFIED / IMPLEMENTATION NOT AUTHORIZED**
