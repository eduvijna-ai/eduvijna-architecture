---
id: AIEOS-V1-SP01
title: Student Practice & Formative Instructional Feedback — Architecture Discovery
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: PROPOSED / DISCOVERY — SP01R1 CORRECTED / CHIEF RE-REVIEW PENDING
version: 1.1.0
created: 2026-11-02
last_updated: 2026-11-02
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# AIEOS-V1-SP01 — Student Practice & Formative Instructional Feedback Architecture Discovery

**Identity:** `AIEOS-V1-SP01` (PATH-STUDENT-PRACTICE)  
**Founder authorization:** 2026-11-02 — architecture discovery only for AIEOS V1-EXPAND; preserve ADR-AIEOS-058 / 059 / 061 authority; no implementation until architecture review and separate Founder scope/ADR authorization.  
**Mode:** **PROPOSED / DISCOVERY — SP01R1 CORRECTED / CHIEF RE-REVIEW PENDING** — not an ADR freeze, not Product authorization, not a code workday, not a merge authorization.  
**Lineage:** SP01 initial deposit + **SP01R1** Chief exact-head corrections (R1-F1 / R1-F2 / R1-F3) — additive commit only atop PR [#57](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) head `4d346235f2ca7f38792fe59f318b41bd1e9421cc`.  
**Governing workday:** [Architecture Issue #56](https://github.com/eduvijna-ai/eduvijna-architecture/issues/56)  
**Distinct from:** [EX01R1 PR #55](https://github.com/eduvijna-ai/eduvijna-architecture/pull/55) (OPEN / DRAFT / NOT MERGED — do not edit or merge).

**Terminal disposition (this package):** **AIEOS-V1-SP01 — DISCOVERY DRAFT PR OPEN / ARCHITECTURE REVIEW PENDING / DEC18 FEATURE NOT YET RATIFIED / IMPLEMENTATION NOT AUTHORIZED**

---

## Executive summary

At pinned governed sources, the Student OS already delivers a complete **assign → start attempt → save responses → submit → read-only submitted view** journey with learner-safe ContentVersion projection, explicit no-grade copy, and Parent/Principal/Teacher boundaries enforced in code and frozen ADRs. **Genuine new learner-visible practice or formative instructional feedback** (correctness, hints tied to answers, post-evaluation student feedback, retries, or scoring) **cannot be implemented without explicit forward ADR decisions**. Cosmetic copy duplicates (including EX01R1-withdrawn S02A) are **not** acceptable December P0 candidates.

**Discovery recommendation (not ratified):** If Founder selects a named December V1-EXPAND development item in this path, the **smallest defensible educational slice** remains **Option SP01-B — learner-safe instructional hints** visible **only while the owned `LearnerAttempt` is `IN_PROGRESS`**, with **mandatory server-side hint disclosure gating** (not UI-only hiding). Hints must be authored through a **governed ContentVersion path** (new immutable version + review/approve/publish) — **not** from Assessment evaluation, Answer Key, or Review Queue comments. **SP01R1:** The existing assignment GET DTO is **not** safe for hints without a new read contract (§ SP01-10). Teacher hint **authoring UI/API is not implemented** at pinned Frontend (§ SP01-06 / SP01-B). This remains **`ADR_FORWARD_REQUIRED` / BLOCKED FOR CODING** until ADR + Founder scope + implementation authorization.

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

### SP01R1 preflight (2026-11-02, before corrective commit)

| Check | Result |
|-------|--------|
| PR [#57](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) | OPEN / DRAFT / NOT MERGED |
| Authorized parent head | `4d346235f2ca7f38792fe59f318b41bd1e9421cc` — **MATCH** local branch |
| Base | `491295c3cf0a151f31686a6a2e1a2176cd92c782` — **MATCH** |
| Five-repo pins + OpenAPI + Alembic | **MATCH** (re-fetched) |
| Writable scope | **Only** this Markdown file |

**SP01R1 authorization:** One additive commit; no amend/rebase/force-push.

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

### Assignment GET returns learner resource without attempt-state gating (SP01R1 / R1-F1 evidence)

At Backend pin, `GetCurrentAssignmentService.get` ([`current_assignments.py` L188–214](https://github.com/eduvijna-ai/eduvijna-aieos-backend/blob/637583f42b7c475ef83f6f99bca7e65e665a253d/src/aieos/domains/learning/application/current_assignments.py#L188-L214)) **unconditionally** loads and returns `learner_resource` together with `attempt_summary` for assignments that remain on the student’s current list — including **`NOT_STARTED`**, **`IN_PROGRESS`**, and **`SUBMITTED`** attempt summaries.

HTTP mapping ([`routes.py` L88–130, L228–242](https://github.com/eduvijna-ai/eduvijna-aieos-backend/blob/637583f42b7c475ef83f6f99bca7e65e665a253d/src/aieos/domains/learning/api/v1/routes.py#L88-L130)) exposes that resource on `GET /api/v1/student-os/assignments/{assignment_id}` via `_resource_response` with **no** attempt-lifecycle filter.

Frontend consumes the same DTO **before** Start ([`AssignmentDetailPage.tsx` L172–175](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/student-os/assignments/AssignmentDetailPage.tsx#L172-L175)) and after submit on [`AttemptPage.tsx` L285–292](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/student-os/attempts/AttemptPage.tsx#L285-L292) when assignment is still loaded.

**SP01R1 binding:** Adding `learner_hint` to the ContentVersion-derived `LearnerResource` on this DTO **does not** achieve IN_PROGRESS-only disclosure without an explicit **server-side** read contract (§ SP01-10). **UI hiding is not security.**

### SUBMITTED attempt read vs membership (SP01R1 / R1-F2 evidence)

[`get_attempt.py` L56–78](https://github.com/eduvijna-ai/eduvijna-aieos-backend/blob/637583f42b7c475ef83f6f99bca7e65e665a253d/src/aieos/domains/learning/application/get_attempt.py#L56-L78): current class membership / assignment eligibility is enforced for **`IN_PROGRESS`** access paths; **own `SUBMITTED`** attempt read remains available to the owning ACTIVE HUMAN Principal under tenant authority **without** re-checking current class membership — consistent with [ADR-AIEOS-058 §4 / §22](https://github.com/eduvijna-ai/eduvijna-architecture/blob/491295c3cf0a151f31686a6a2e1a2176cd92c782/decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) (*own already-submitted evidence may remain readable after class-membership loss*).

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

### Teacher hint authoring — not implemented at pin (SP01R1 / R1-F3 evidence)

| Surface | Pin evidence | Implication |
|---------|--------------|-------------|
| [`ReviewDetailPage.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/teacher-os/review/ReviewDetailPage.tsx) | Approve / Request Changes / Reject | **No** per-question hint editor |
| [`WorkPage.tsx`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/features/teacher-os/work/WorkPage.tsx) | TeachingWork preparation / goal context | **Not** typed question/hint authoring |
| [`contentApi.ts`](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/src/services/api/contentApi.ts) | GET version / publish | **No** teacher hint-append UI |
| Backend [`content/api/v1/routes.py` L291–328](https://github.com/eduvijna-ai/eduvijna-aieos-backend/blob/637583f42b7c475ef83f6f99bca7e65e665a253d/src/aieos/domains/content/api/v1/routes.py#L291-L328) | ContentVersion append endpoint exists | **Does not prove** governed Teacher OS journey |

**Prohibited covert paths:** Review Queue free-text comments, TeachingWork notes, or Content append without review/approve/publish are **not** acceptable hint carriers.

### ContentVersion immutability (ADR-AIEOS-027)

Committed ContentVersion payloads are **immutable**. Adding hints to content that already has a published version requires a **new** `content_version_id`, full **review → approve → publish** before the hint-bearing version may bind to **future** assignments. An assignment already pinned to version **V** never silently gains hints authored on **V+1**. ADR must decide: optional field on existing schema vs new registered schema version — **not** in-place mutation of committed versions.

### Semantic leakage beyond `hint == answer` (SP01R1)

| Failure mode | Why string equality lint is insufficient |
|--------------|------------------------------------------|
| Paraphrased answer in hint | Same semantic content, different string |
| Multiple-choice elimination | Hint narrows options without stating key |
| Cross-artifact bleed | Hint copied from teacher notes / answer-key rationale |
| Age / difficulty mismatch | Hint inappropriate for learner context |

**Required controls (proposal):** strict learner-safe **positive allowlist** projection; preparation-time **human review** gate; semantic QA rules with **fail-closed** publish block; no automated promotion from AnswerKey or evaluation artifacts in v1.

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

### Option SP01-B — Learner-safe instructional hints (`IN_PROGRESS` only, server-gated) — **discovery preference**

| Dimension | Detail |
|-----------|--------|
| **Student story** | While my attempt is in progress, I can open teacher-approved optional hints on hard questions; I still submit once and never see a grade on this screen. |
| **Missing today** | No hint fields in learner projection; **no server-side IN_PROGRESS-only hint read contract**; **no Teacher OS hint authoring/editor journey** (only generic prepare/review/publish — § SP01-06). |
| **Provenance choices (ADR)** | **(P1) Teacher-authored** — requires new editor/command + capability gate. **(P2) AI-suggested, teacher-approved** — different provider/review gates; **not** assumed in December v1 unless Founder selects. |
| **Best case** | Formative scaffolding without grading; hints bound to exact ContentVersion at attempt start. |
| **Worst case** | Hint leakage; hints on assignment GET before start or after submit via DTO; retroactive “un-disclosure” promised but impossible once seen. |
| **New data/commands** | **Yes — architecture proposals only:** optional hint payload on **new** ContentVersion(s); **state-filtered hint read** (§ SP01-10); **not** naive extension of assignment GET `LearnerResource`. |
| **ADR** | **`ADR_FORWARD_REQUIRED`** — ADR-027 allowlist + immutability/versioning; ADR-058 lifecycle unchanged; server disclosure contract; Teacher authoring ownership; OpenAPI authorization later. |

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
| **Scope cut (honest December)** | **Worksheet content type first** at pin; Quiz/Homework hint schemas **deferred** unless ADR explicitly expands — avoids silent three-schema commitment. |
| **Student OS** | Hint affordance on `AttemptPage` **only when server returns gated hints** for owned `IN_PROGRESS` attempt. |
| **Server contract (binding for any implementation)** | Hints **must not** rely on React-only hiding. Choose one documented pattern (§ SP01-10). |
| **Minimum positive experience** | Optional collapsible per-question hints during work; submit unchanged; post-submit banner still no score. |
| **Post-submit / NOT_STARTED** | **No new gated hint delivery** on `GET assignment` or `GET attempt` when attempt absent, `NOT_STARTED`, or `SUBMITTED`. |
| **Retroactive secrecy** | If a hint was disclosed during `IN_PROGRESS`, it **cannot** be made unknown afterward; policy is **no further server delivery** after submit, not erasure. |
| **Failure / empty** | No hints in version → identical to today; errors → generic unavailable, no answer leakage. |
| **Teacher control** | **P1 teacher-authored path:** missing editor/command must be built (§ SP01-14); hints only on **new approved/published** ContentVersion; never from evaluation. |
| **Prohibited semantics** | No correctness/score/retry; no Review-comment hints; no in-place ContentVersion mutation. |
| **Frozen ADRs extended (not overwritten)** | ADR-027, ADR-058 (incl. submitted evidence after roster loss), ADR-059, ADR-061. |

**Optional additive (if Founder wants zero ADR):** **SP01-A** UI checklist only — polish, not core PATH-STUDENT-PRACTICE outcome.

---

## SP01-10 — Ownership, data path & **server-side hint read contract** (proposals only)

### Why the current assignment DTO is insufficient (R1-F1)

Today’s `GET /api/v1/student-os/assignments/{id}` embeds a full `LearnerResource` for all attempt summary states. **Any hint field placed in that resource would leak to NOT_STARTED and SUBMITTED** unless the server strips or withholds hints by rule. **Do not assume** the existing DTO is safe.

### Recommended disclosure architecture — **Option SP01-B-R1 (preferred): attempt-scoped gated read**

**Architecture proposal only** — OpenAPI / implementation authorization separate.

```text
GET /api/v1/learning/attempts/{attempt_id}/learner-hints   (proposal)
```

**Authoritative checks (fail closed):**

| Check | On failure |
|-------|------------|
| ACTIVE HUMAN Principal; correct tenant | 403 / 404 |
| Caller is exact attempt owner | 403 / 404 |
| `LearnerAttempt.lifecycle_state == IN_PROGRESS` | 409 or 403 — **no hints** |
| Current membership + assignment authority for **current-access** practice | 403 when denied (same family as save/submit membership checks) |
| Attempt bound to exact assigned `content_version_id` | 409 on stale client |

**Response:** positive-allowlist hint DTO only (question id + hint text); **never** answer key, outcomes, or evaluation fields.

**Behaviors:**

| Situation | Server behavior |
|-----------|-----------------|
| No attempt started (`NOT_STARTED`) | Endpoint not callable without attempt id; assignment GET **must not** include gated hints |
| `SUBMITTED` | **Reject** gated hint read; attempt GET returns submitted responses only (existing) |
| Revoked membership + `IN_PROGRESS` | Deny hint read (and save/submit) — current-access fail closed |
| Revoked membership + own `SUBMITTED` | Deny **hints**; **allow** own submitted answer history per ADR-058 |
| Direct HTTP / stale ETag | No hint body without passing all gates |

### Alternative — **Option SP01-B-R2: state-filtered assignment resource**

Split or filter `learner_resource` on assignment GET based on **owned attempt state**:

- **`NOT_STARTED` / `SUBMITTED`:** return prompts-only resource (hints omitted server-side).
- **`IN_PROGRESS`:** include hints only for questions in the **exact** bound ContentVersion.

Still requires Learning-layer orchestration change in `GetCurrentAssignmentService` / routes — **not** a Frontend-only filter.

### End-to-end data path (after contract selected)

```text
Teacher hint editor/command (NOT IMPLEMENTED — new) + review/approve/publish
        ↓
NEW ContentVersion payload (immutable) with allowlisted hint fields
        ↓
LearnerAttempt start binds exact content_version_id
        ↓
IN_PROGRESS only: gated hint read (SP01-B-R1 or SP01-B-R2)
        ↓
Student AttemptPage (display only; not authorization)
```

| Concern | Owner |
|---------|--------|
| Hint text SoR | **ContentVersion** (new versions only) |
| Hint **disclosure** authority | **Learning** orchestration + auth kernel |
| Attempt / submit SoR | **Learning** (ADR-058 unchanged) |
| Evaluation | **Assessment** — not used for hints |

**OpenAPI:** New operation or filtered DTO = **proposal**; requires separate contract authorization.

---

## SP01-11 — Visibility & authorization matrix

Legend: ✓ allowed · ✗ denied · ◐ derived allowlist · ⊘ own historical evidence (membership not required) · — n/a

**SP01R1:** Distinguish **(A) current-access practice** (assignment visibility, start/save/submit, **IN_PROGRESS hints**) vs **(B) own submitted answer evidence** (ADR-058 §4 / §22).

| Capability | Student A (owner) | Student B | Wrong tenant | Revoked roster | Teacher (current class) | Teacher (lost class) | Parent | Principal |
|------------|-------------------|-----------|--------------|----------------|-------------------------|----------------------|--------|-----------|
| View current assignment + learner work (prompts) | ✓ (A) | ✗ | ✗ | ✗ (A) | ✓ teacher routes | ✗ | ◐ facts | — |
| **Gated hints (SP01-B)** | ✓ **only `IN_PROGRESS` + (A)** | ✗ | ✗ | ✗ **(A)** | ✓ author via Content, not student GET | ✗ | ✗ | ✗ |
| Start / save / submit | ✓ (A) | ✗ | ✗ | ✗ (A) | ✗ | ✗ | ✗ | ✗ |
| **Submitted answers (own)** | ✓ read-only | ✗ | ✗ | **⊘ (B)** — ADR-058 | ✓ teacher intelligence | ✗ | ◐ status/fact | ✗ |
| Evaluation outcomes | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ (`EVALUATION_EXISTENCE=NO`) | ✗ aggregate |
| Answer key / teacher notes | ✗ | ✗ | ✗ | ✗ | ✓ | ✗ | ✗ | ✗ |

**Fail-closed:** **(A)** requires current tenant, ACTIVE HUMAN Principal, and **current** membership/assignment authority where applicable. **(B)** submitted evidence read follows ADR-058 — **not** the same gate as hints. Stale JWT/UI cache is never authority.

---

## SP01-12 — Adversarial architecture scenarios (22)

| ID | Scenario | Expected fail-closed behavior |
|----|----------|-------------------------------|
| **ADV-01** | Student B requests Student A `attempt_id` | 404/403 — owner binding |
| **ADV-02** | Second `POST …/attempts` while `IN_PROGRESS` exists | Reject or idempotent return — **no** second concurrent attempt (policy) |
| **ADV-03** | `PUT …/responses` after `SUBMITTED` | Reject — immutability |
| **ADV-04** | Submit with stale `If-Match` after save | Conflict — client reload |
| **ADV-05** | Submit with empty responses | Legal per ADR-059 unanswered evidence — UI must not promise scoring |
| **ADV-06** | **Direct HTTP:** gated hints when `SUBMITTED` | **Server rejects** — no hint body; UI hide irrelevant |
| **ADV-07** | **Direct HTTP:** gated hints on assignment GET `NOT_STARTED` | **No hint fields** in response (filtered DTO or no hint endpoint) |
| **ADV-08** | Hint text equals or paraphrases answer key | Publish blocked by semantic QA — fail closed |
| **ADV-09** | Student calls Teacher `…/intelligence` | 403 — role kernel |
| **ADV-10** | Parent polls for evaluation existence | Deny — ADR-061 |
| **ADV-11** | **Revoked roster:** deep link `IN_PROGRESS` hint/save/submit | **Deny (A)** — current-access |
| **ADV-12** | **Revoked roster:** deep link **own** `SUBMITTED` attempt GET | **Allow (B)** — submitted answers readable; **no hints** |
| **ADV-13** | Stale assignment — attempt pinned to older `content_version_id` while newer hint version published | Student sees hints **only** if bound version contains them; no silent upgrade |
| **ADV-14** | Wrong learner / wrong tenant / expired auth on hint read | 403/404 — no leakage |
| **ADV-15** | Evaluation not yet run — student expects scored feedback (SP01-D) | No student evaluation surface |
| **ADV-16** | Provider/DB failure during save | Retry-safe error; no partial submit |
| **ADV-17** | Teacher stores hints in Review Queue comment | **Must not** project to learner — unauthorized channel |
| **ADV-18** | Content append tries to mutate committed version in place | Reject — new version + review cycle required |
| **ADV-19** | Client removes hint UI after submit but replays cached hint JSON | Server **still** must not serve gated hints post-submit |
| **ADV-20** | MCQ hint eliminates all but one option | Semantic QA fail closed at publish |
| **ADV-21** | AI-suggested hint without teacher approval (P2 path) | Out of v1 scope — deny unless ADR + provider gate |
| **ADV-22** | Principal attempts learner drill-down via hint telemetry | Deny — ADR-060 aggregates only |

**Regression emphasis (SP01R1):** Negative HTTP probes for ADV-06, ADV-07, ADV-11, ADV-12 must be **server-side** contract tests in any future implementation slice — not E2E UI-only.

---

## SP01-13 — ADR forward decision ledger (proposals — no ADR drafted here)

### Decision package D1 — Learner-safe instructional hints (for SP01-B)

| Question | Alternatives | Compatibility / tests |
|----------|--------------|------------------------|
| Where do hints live? | (a) New-field on **new** ContentVersion; (b) separate artifact | (a) preferred for exact-version binding; **no in-place mutation** |
| When visible? | Server gated **`IN_PROGRESS` only** | SP01-B-R1 or SP01-B-R2; negative HTTP ADV-06/07 |
| Server contract | Attempt-scoped GET vs filtered assignment resource | Document in ADR; OpenAPI later |
| Who authors? | **P1 teacher-authored** vs **P2 AI-suggested + teacher approved** | P1 requires **new editor/command** (missing today); P2 adds provider ADR |
| Schema evolution | Optional field on WorksheetV1 vs new schema version | ADR decision — reader compatibility |
| Leakage controls | Positive allowlist + human review + semantic QA | Beyond `hint == answer`; ADV-08/20 |
| Parent visibility? | Default **none** | ADR-061 |
| December scope cut | Worksheet-first | Quiz/Homework later — 2027 breadth preserved |

**Likely touch:** ADR-AIEOS-027 forward revision; ADR-AIEOS-058 **disclosure vs submitted-evidence** clarification (not lifecycle change); Learning read orchestration; Teacher OS authoring slice.

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

**Assumes:** Founder ratifies **SP01-B (worksheet-first)** + ADR D1 frozen + implementation workday authorized.

| Slice | Scope | Size | Depends on |
|-------|-------|------|------------|
| **T0 Teacher hint authoring** | New Teacher OS editor/command + capability gate; **not** Review comments | **L** | ADR D1 |
| **T1 Content schema + immutability** | Hint fields on **new** Worksheet ContentVersion only; review→approve→publish path | **M** | T0, ADR D1 |
| **T2 Semantic QA / fail-closed lint** | Paraphrase/MCQ-elimination rules; human review checkpoint | **M** | T1 |
| **B2 Learning gated read** | SP01-B-R1 (preferred) or SP01-B-R2; membership/attempt state orchestration | **M** | T1, ADR D1 |
| **B3 OpenAPI + snapshot** | New operation or filtered DTO — **authorized separately** | **S** | B2 |
| **F1 Student Attempt UI** | Consumes gated read only; architecture forbiddens | **S** | B3 |
| **E2E + negative HTTP** | ADV-06/07/11/12 server probes + product happy path | **M** | F1 |

**Smallest demo:** Teacher authors hints on **new** worksheet version → assign → student starts → **server returns hints only IN_PROGRESS** → submit → direct HTTP confirms **no** post-submit hint delivery; revoked-roster case matches ADR-058 (B).

**December feasibility (honest):** **At risk** — T0+T1+T2 dominate calendar; worksheet-only cut reduces but does not remove authoring gap. ADR latency remains gating.

**2027 preserved:** Quiz/Homework hints, AI-suggested hints (P2), richer formative feedback (SP01-C/D), EIS depth — **not** silently moved into December.

**Risks:** Treating assignment GET as sufficient (R1-F1 recurrence); ADR-058 submitted-read regression; covert Review-comment hints; in-place ContentVersion mutation.

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
| Chief exact-head discovery review | Chief AI Enterprise Architect | **SP01R1 corrections deposited — RE-REVIEW PENDING** |
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
| Head | `4d346235f2ca7f38792fe59f318b41bd1e9421cc` (SP01) → SP01R1 commit on push |
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

**22** scenarios § SP01-12 (ADV-01–ADV-22), including SP01R1 direct-HTTP hint negatives and ADR-058 revoked-roster submitted-read split.

### J — Feasibility / date / cut lines

December **development** target requires Founder ratification + ADR before coding; **BLOCKED FOR CODING**; worksheet-first cut; authoring slice **L** — Dec18 **at risk** (§ SP01-14); Nov 20 showcase and 2027 programme preserved.

### K — Checks / links

Architecture **NO CI CONFIGURED**; five-repo pins re-verified at SP01R1; Backend/Frontend evidence links in § SP01-04 / SP01-06.

### L — Draft PR & unapproved work

PR [#57](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) on `cursor/sp01-student-practice-discovery-89ba` — **Unapproved:** merge, ADR, implementation, Founder scope ratification.

---

## SP01R1 — Chief correction report (2026-11-02)

**Disposition:** SOURCE PASS / DESIGN REVIEW PASS WITH SP01R1 REQUIRED — **MERGE NOT AUTHORIZED**

| Finding | Correction applied |
|---------|-------------------|
| **R1-F1** Server hint visibility | Documented assignment GET unconditional resource; chose **SP01-B-R1** (attempt-scoped gated read, preferred) and **SP01-B-R2** (filtered assignment resource); **removed** “no new API” assumption; ADV-06/07/19; § SP01-09–10 |
| **R1-F2** Submitted evidence after roster loss | Matrix § SP01-11 distinguishes **(A) current-access** vs **(B) own submitted evidence**; ADV-11/12; aligned with ADR-058 §4/§22 and `get_attempt.py` |
| **R1-F3** Authoring / versioning truth | § SP01-06 authoring gap table; immutability + new version path; P1 vs P2 provenance; semantic QA beyond string match; worksheet-first December cut; § SP01-14 T0–T2 dependency graph |

**Commit lineage (authorized):**

| Field | Value |
|-------|-------|
| Parent commit | `4d346235f2ca7f38792fe59f318b41bd1e9421cc` |
| SP01R1 head | *(recorded at push)* |
| Changed files | **Only** `AIEOS/AIEOS-V1-SP01-STUDENT-PRACTICE-FEEDBACK-ARCHITECTURE-DISCOVERY.md` |
| Architecture CI | **NO CI CONFIGURED** |

**STOP — SP01R1 COMPLETE — PR #57 UPDATED — CHIEF RE-REVIEW PENDING — DEC18 NOT RATIFIED — IMPLEMENTATION NOT AUTHORIZED**

---

**STOP — AIEOS-V1-SP01 — DISCOVERY DRAFT PR OPEN / SP01R1 CORRECTED / CHIEF RE-REVIEW PENDING / DEC18 FEATURE NOT YET RATIFIED / IMPLEMENTATION NOT AUTHORIZED**
