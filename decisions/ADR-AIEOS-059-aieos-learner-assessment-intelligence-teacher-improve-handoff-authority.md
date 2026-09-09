---
id: ADR-AIEOS-059
title: AIEOS Learner Assessment Intelligence & Teacher Improve Handoff Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: in-review
version: 1.0.0
created: 2026-09-09
last_updated: 2026-09-09
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-059 — AIEOS Learner Assessment Intelligence & Teacher Improve Handoff Authority

**Status:** Proposed / Freeze Candidate  
**Chief Architect architecture review:** PENDING  
**Founder / Product Architecture freeze:** NOT GRANTED  
**Date:** 2026-09-09  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md) · [ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md) · [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md) · [ADR-AIEOS-046](ADR-AIEOS-046-aieos-production-event-plane-identity-least-privilege-contract.md) · [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) · [ADR-044](ADR-044-ai-platform-behind-stable-services.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)

**Catalogue note:** Proposed / Freeze Candidate is **ARCHITECTURE AUTHORITY DEPOSIT ONLY**. This ADR proposes the **AIEOS Learner Assessment Intelligence & Teacher Improve Handoff Authority** for **AIEOS360-S01P2**. It is **not** Frozen, **not** Founder-approved, and **not** an implementation authorization. Architecture freeze, if later granted, still would not itself authorize Backend, Frontend, Product, migration, OpenAPI, NATS, Temporal, or production mutation. Implementation slices **AIEOS360-S01-I05-B1+** remain **blocked pending ADR-059 freeze** and then require separate Chief Architect authorization.

**ID family note:** `ADR-AIEOS-059` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 and from platform infrastructure ADR-AIEOS-048 / 048R1 / 048R2.

**Architecture programme:** **AIEOS 360 CLIENT SHOWCASE** / package **AIEOS360-S01**. AIEOS360-S01-I05A discovery = **ACCEPTED**. AIEOS360-S01-I04R1 = **CLOSED**. This ADR does **not** reopen Teacher OS domain authority, TeachingAssignment, ClassroomAssessment ownership, or Improve SoR design.

**Architecture choice (AIEOS360-S01-I05A):** **OPTION D — HYBRID** — Assessment-owned durable `LearnerAssessmentEvaluation` plus derived Teacher Assessment Intelligence projections.

Does **not** reopen or rewrite historical ADR bodies: ADR-AIEOS-023R1, ADR-AIEOS-024, ADR-AIEOS-025, ADR-AIEOS-028, ADR-AIEOS-031, ADR-AIEOS-053, ADR-AIEOS-054, ADR-AIEOS-055, ADR-AIEOS-056, ADR-AIEOS-058.

This deposit does **not** authorize implementation.

---

## Context

Teacher OS through TOS-CX01 and AIEOS360-S01 through I04R1 have a real cross-role path to raw learning evidence:

```text
Prepare → Review → Publish → TeachingAssignment
        → eligible Student
        → LearnerAttempt
        → immutable LearnerSubmission
        → class-level ClassroomAssessment (teacher judgment)
        → teacher-deliberate Improve (remediate_class TeachingWork)
```

ADR-AIEOS-058 froze Learning as the attempt/submission SoR and explicitly reserved grade / mastery / misconception / recommendation / personalization as later Assessment Intelligence / Learner Intelligence. ADR-AIEOS-055 froze ClassroomAssessment as **class-level teacher judgment** with no learner identity. ADR-AIEOS-056 froze Improve as a Teaching application capability that creates `TeachingWork(intent_type = remediate_class)` plus immutable `TeachingWorkRemediationOrigin` from a RECORDED ClassroomAssessment.

Governed evidence at this deposition:

| Surface | Pin |
|---------|-----|
| Architecture `origin/main` | `5a7efb2c71570c602c0e52c243dd472ab9a66b5e` |
| Backend `origin/main` | `921d35eb08890a4e1d86cf95daf9d38cdfc4a13c` |
| Frontend `origin/main` | `65b59a0bd30d254fce92c322c0a7f437a90b08af` |
| Product `origin/main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Alembic head | `a360s010002` |
| Authoritative OpenAPI SHA-256 | `4691D6BADA2157D436435BB5CCDD6797EA670D1A87543D42CA39A478F940F330` |

AIEOS360-S01-I01 through I04R1 are **CLOSED**. Durable `LearnerAttempt` / `LearnerSubmission` exist. Teacher Assessment Intelligence, durable learner evaluation, and the evidence-informed Improve handoff do **not** yet have architecture authority.

**Repurposing forbidden:**

| Existing aggregate | Must NOT become learner-evaluation truth |
|--------------------|------------------------------------------|
| **LearnerSubmission** | Submitted ≠ Evaluated; raw responses ≠ grades |
| **LearnerAttempt** | Attempt lifecycle ≠ evaluation |
| **ClassroomAssessment** | Class-level teacher judgment ≠ per-learner evaluation |
| **TeachingAssignment** | Assignment intent ≠ assessed / evaluated |
| **TeachingWork / TeachingWorkRemediationOrigin** | Improve acceptance ≠ evaluation |
| **Content / ContentVersion** | Artifact payload ≠ evaluation event |

AIEOS360-S01-I05A established that the smallest safe next architecture is Assessment-owned durable evaluation of one immutable submission against the exact assigned ContentVersion, with Teacher Assessment Intelligence as a **derived** projection and Improve remaining the existing ADR-AIEOS-056 command path.

---

## Decision

### 1. Separation invariants (binding)

Preserve ADR-AIEOS-053 / 054 / 055 / 056 / 058:

```text
Generated   ≠  Approved
Approved    ≠  Published
Published   ≠  Assigned
Assigned    ≠  Attempted
Attempted   ≠  Submitted
Submitted   ≠  Evaluated
Evaluated   ≠  Mastered
Assigned    ≠  Taught
Taught      ≠  Assessed
Assessed    ≠  Mastered
Assigned    ≠  Externally Delivered
```

**New / restated invariants introduced by this ADR:**

```text
Assessed                         ≠  Mastered
Assessment signal                ≠  Improve acceptance
Improve suggested                ≠  Improve accepted
Improve accepted                 ≠  Content generated
LearnerAssessmentEvaluation      ≠  ClassroomAssessment
Derived Teacher Intelligence     ≠  teacher class-level judgment
Deterministic item outcome       ≠  mastery / competency attainment
Submission-scoped objective evidence ≠ learner-model truth
```

Do **not** move grading or evaluation fields into `LearnerSubmission`.  
Do **not** retrofit learner identities into `ClassroomAssessment`.  
Do **not** introduce a separate Improve SoR.

### 2. Authority table

| Concern | Authority |
|---------|-----------|
| Teacher-owned classroom assignment intent | **TeachingAssignment** — Teaching ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| Artifact / immutable version payload | **Content / ContentVersion** — Content |
| Attempt working state | **LearnerAttempt** + **AttemptResponseItems** — Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Raw immutable learning evidence | **LearnerSubmission** — Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Durable evaluation of one submission against exact ContentVersion | **LearnerAssessmentEvaluation** — Assessment (**this ADR**) |
| Teacher Assessment Intelligence display | **Derived Assessment projection** — Assessment (**this ADR**); not a competing SoR |
| Class-level teacher assessment judgment | **ClassroomAssessment** — Assessment ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)) |
| Improve / remediation capability | **Teaching application** — `POST /api/v1/teaching/works/from-classroom-assessment` ([ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md)) |
| Class / roster master | **ERP / SIS / Admin School Context** |
| Current ClassRef / teacher-target authority | **AIEOS School Context current-authority port** (fail closed) |
| Current learner membership for student access | **AIEOS School Context learner-membership façade** ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Long-term mastery / misconception / personalization | **Future Learner Intelligence** — **out of this ADR** |

Learning remains the authoritative SoR for `LearnerAttempt`, `AttemptResponseItem`, and `LearnerSubmission`.

### 3. Architecture options evaluated

| Option | Summary | Verdict |
|--------|---------|---------|
| **A** | Assessment immutable learner evaluation only, with no teacher projection | **Rejected as insufficient for the AIEOS360 path** — durable evaluation is necessary but teachers cannot act on evidence without an assignment-scoped derived intelligence surface |
| **B** | Put evaluation / grading fields into Learning / `LearnerSubmission` | **Rejected** — submission truth ≠ evaluation truth; would couple raw evidence to policy-versioned grading and force Learning writes on Assessment policy change |
| **C** | Compute-only transient evaluation with no durable record | **Rejected** — durable education evidence requires replay, audit, provenance, and evaluation-policy-version traceability |
| **D** | Assessment durable `LearnerAssessmentEvaluation` + derived Teacher Assessment Intelligence projections | **Selected** |

**Selected: OPTION D.**

OPTION D is the smallest safe architecture for the AIEOS360 path because:

1. It preserves Learning as immutable raw evidence (ADR-AIEOS-058).
2. It places policy-versioned evaluation where Assessment already owns class-level judgment (ADR-AIEOS-055) without collapsing those two facts.
3. It gives teachers a real evidence surface without inventing a third Improve SoR (ADR-AIEOS-056 unchanged).
4. It keeps derived intelligence as a projection, so display copy does not become a new source of truth.

### 4. LearnerAssessmentEvaluation aggregate

**Name:** `LearnerAssessmentEvaluation`  
**Domain:** Assessment  
**Proposed PostgreSQL schema:** `assessment` (same Assessment schema family as ClassroomAssessment; distinct aggregate)

**Purpose:** Durable evaluation of **one** immutable `LearnerSubmission` against the **exact** `ContentVersion` that the submission / attempt is bound to.

**It does NOT own:**

- attempt lifecycle
- responses
- submission lifecycle
- assignment
- content
- mastery
- misconception truth
- personalization
- Improve acceptance
- TeachingWork
- ClassroomAssessment

#### 4.1 Minimum provenance

| Field | Semantics |
|-------|-----------|
| `evaluation_id` | Aggregate identity (UUIDv7) |
| `tenant_id` | Tenant scope |
| `learner_principal_id` | Copied from the evaluated submission; correlation, not a new identity SoR |
| `submission_id` | Exact immutable LearnerSubmission |
| `attempt_id` | Exact LearnerAttempt bound to that submission |
| `teaching_assignment_id` | Exact TeachingAssignment bound to that attempt/submission |
| `content_id` | Exact Content identity copied from the submission / assignment binding |
| `content_version_id` | Exact immutable ContentVersion; **never** a later published pointer |
| `class_ref` | Opaque School Context class identifier copied from the submission / assignment |
| `evaluation_policy_id` | Durable evaluation-policy business identity |
| `evaluation_policy_version` | Integer policy version; bugfix / rule change requires a new version |
| `evaluated_at` | Server-controlled timestamp at insert |
| `created_at` | Audit timestamp; equals `evaluated_at` for this immutable record |

**No `aggregate_revision`.** The record is immutable. Optimistic concurrency is not required on an append-only fact whose business identity is unique.

Do **not** add `aggregate_revision` merely because ClassroomAssessment uses one.

#### 4.2 Per-question evaluation (minimum)

Each evaluation contains an ordered, submission-complete per-question result set. Minimum fields:

| Field | Semantics |
|-------|-----------|
| `question_id` | Exact ContentVersion question identity |
| `response_kind` | `MULTIPLE_CHOICE` \| `TRUE_FALSE` \| `SHORT_ANSWER` from the submission |
| `outcome` | Canonical item outcome (see §8–10) |
| `evaluation_method` | How the outcome was produced (see §8–10) |
| `objective_ids` | Copied from the **exact ContentVersion question**, never from the frontend |

Frontend-supplied correctness, scores, objective mappings, or explanations are **ignored**. They are not inputs. Item outcomes and objective_ids are derived only from:

```text
immutable LearnerSubmission
  +
exact ContentVersion
  +
named evaluation policy / version
```

#### 4.3 Lineage validation (fail closed)

Before insert, the Assessment application **must** validate:

- submission exists in the same tenant and is the immutable submitted evidence
- `attempt_id`, `teaching_assignment_id`, `content_id`, `content_version_id`, `class_ref`, and `learner_principal_id` match the submission
- the assignment's immutable `content_id` / `content_version_id` still equal those copied onto the submission
- the ContentVersion exists and is the exact bound version — **not** `Content.published_version_id` if that pointer has moved

Mismatch → **FAIL CLOSED**. Do **not** evaluate against a newer ContentVersion.

### 5. Evaluation policy versioning

Freeze a durable evaluation-policy concept.

**Business identity of one evaluation fact:**

```text
tenant_id
  + submission_id
  + evaluation_policy_id
  + evaluation_policy_version
```

The same exact business identity **must** be replay-safe: a repeated ensure / evaluate returns the same durable result.

**First baseline policy:**

| Field | Value |
|-------|-------|
| `evaluation_policy_id` | `aieos.learner_assessment.deterministic` |
| First `evaluation_policy_version` | `1` |

Version 1 encodes: MULTIPLE_CHOICE exact-option deterministic grading; TRUE_FALSE strict `true`/`false` content-answer normalization; SHORT_ANSWER `OPEN_RESPONSE_UNEVALUATED`; submission-scoped objective rollup with incompleteness → `INSUFFICIENT_EVIDENCE`.

A policy bugfix or changed evaluation rule **MUST** require a new `evaluation_policy_version`. No silent rewriting of previously issued evaluation facts.

#### 5.1 Correction / re-evaluation model — append-only superseding authority

**Selected:** **A — immutable records; a later evaluation under a new policy version supersedes the previous one for current-projection purposes.**

**Rejected:** B — lifecycle-controlled VOID/SUPERSEDE on the same row. That would invent mutable evaluation state and `aggregate_revision` without an invariant gain.

Rules:

1. Each `LearnerAssessmentEvaluation` row is **immutable after insert**. No update API. No last-write-wins overwrite.
2. Re-evaluation under a **new** policy version inserts a **new** row with the new `(evaluation_policy_id, evaluation_policy_version)`.
3. Historical rows remain historical evidence and audit-readable under Assessment authorization.
4. Teacher Assessment Intelligence **current** evaluation for a submission is the row matching the **currently authorized** `(evaluation_policy_id, evaluation_policy_version)`.
5. An obsolete-policy row is **not** current derived truth. If no current-policy row exists, per-learner evaluation state is `NOT_EVALUATED_UNDER_CURRENT_POLICY`.
6. Request under an **obsolete** policy:
   - exact business identity already exists → **replay** the existing immutable row
   - exact business identity does **not** exist → **FAIL CLOSED** (do not mint new evaluations under a retired policy in this baseline)
7. Request under the **currently authorized** policy:
   - exact identity exists → replay
   - exact identity missing → evaluate and insert

There is no VOID of a learner evaluation in this baseline. If a submission itself were later governed as invalid, that remains a Learning concern; Assessment does not rewrite Learning.

### 6. Item outcome and evaluation-method vocabulary

Canonical item `outcome`:

| Code | Meaning |
|------|---------|
| `CORRECT` | Deterministic match of a legal submitted value against the exact ContentVersion answer under the named policy |
| `INCORRECT` | Deterministic mismatch of a legal submitted value against the exact ContentVersion answer |
| `OPEN_RESPONSE_UNEVALUATED` | Submitted open response; no authoritative deterministic grade in this baseline |
| `UNEVALUATED_POLICY_REJECT` | Fail-closed evaluation-policy / data-contract failure; **not** a normal incorrect answer |

Canonical `evaluation_method`:

| Code | Meaning |
|------|---------|
| `DETERMINISTIC_CONTENT_ANSWER` | MC or TF compared to exact ContentVersion answer under the named policy |
| `OPEN_RESPONSE_BASELINE` | SHORT_ANSWER first baseline; no rubric |
| `POLICY_REJECT` | Contract / policy failure; fail closed |

`INCORRECT` and `UNEVALUATED_POLICY_REJECT` **must remain distinct**. An invalid option, kind mismatch, or illegal content answer is not “the learner got it wrong.”

### 7. MULTIPLE_CHOICE policy (v1 deterministic)

MULTIPLE_CHOICE is deterministic in v1.

Evaluate the LearnerSubmission **string choice** against the exact ContentVersion `question.answer`.

**Require, else `UNEVALUATED_POLICY_REJECT` / `POLICY_REJECT`:**

- the question exists on the exact ContentVersion
- question kind is multiple-choice and matches submission `response_kind`
- submitted value is a legal option (`question.options`)
- content `answer` is a legal option

If all of the above hold: exact string equality of submitted choice to `question.answer` → `CORRECT` or `INCORRECT` with `DETERMINISTIC_CONTENT_ANSWER`.

Do **not** evaluate against a newer ContentVersion.

### 8. TRUE_FALSE policy (v1 deterministic through strict normalization)

Learning authority already stores TRUE_FALSE as a **strict boolean** response. Content currently stores `answer` as a **string**. This ADR does **not** widen the Education payload schema.

**v1 normalization applies only to the ContentVersion string answer:**

```text
trim
  +
case-fold / lower
```

Only the normalized values `"true"` and `"false"` are accepted. Map those to bool and compare with the submitted boolean.

Everything else, including `yes` / `no`, `1` / `0`, `T` / `F`, truthy/falsy, and localized values → **FAIL CLOSED** / `UNEVALUATED_POLICY_REJECT`.

Examples:

| Content answer | After trim + lower | Result |
|----------------|--------------------|--------|
| `"TRUE "` | `"true"` | Legal; map to `true`; compare |
| `"False"` | `"false"` | Legal; map to `false`; compare |
| `"yes"` | `"yes"` | `UNEVALUATED_POLICY_REJECT` |
| `"1"` | `"1"` | `UNEVALUATED_POLICY_REJECT` |

Do **not** silently accept additional aliases unless a future content-contract revision explicitly authorizes them.

Also require: question exists; kind matches; submitted value is the Learning boolean. Kind / existence failure → `UNEVALUATED_POLICY_REJECT`.

### 9. SHORT_ANSWER policy (v1 not deterministically graded)

SHORT_ANSWER **MUST NOT** receive authoritative `CORRECT` / `INCORRECT` deterministic grading in the first ADR-059 baseline.

Current content contains `answer` and `explanation` but no governed rubric, alternate valid answers, numeric equivalence, semantic equivalence, or partial-credit model.

**Canonical first vocabulary:** `OPEN_RESPONSE_UNEVALUATED` with `evaluation_method = OPEN_RESPONSE_BASELINE`.

**Why this code, not `REQUIRES_TEACHER_REVIEW`:** this ADR creates evaluation authority, not a teacher-review work-item SoR or review queue. `REQUIRES_TEACHER_REVIEW` would imply a workflow that is not being designed here. `OPEN_RESPONSE_UNEVALUATED` states the evaluation fact: the item was received and remains unevaluated.

Do **not** invent a rubric.  
Do **not** use naive normalized string equality as educational grade authority, even when the submitted text happens to equal `question.answer`.  
AI-assisted open-response evaluation remains **FUTURE** / separately authorized (§20).

### 10. Submission-scoped objective evidence

The exact ContentVersion question already carries `objective_ids`. ADR-059 may freeze **submission-scoped** objective evidence only.

It is **explicitly not**:

- mastery
- competency attainment
- learner-model truth
- misconception truth
- long-term strength / weakness

#### 10.1 Canonical vocabulary

| Code | Meaning |
|------|---------|
| `DEMONSTRATED_ON_SUBMITTED_ITEMS` | Every submitted item linked to this objective was authoritatively evaluable and `CORRECT` |
| `MIXED_ON_SUBMITTED_ITEMS` | All relevant submitted items were authoritatively evaluable; at least one `CORRECT` and at least one `INCORRECT` |
| `NOT_YET_DEMONSTRATED_ON_SUBMITTED_ITEMS` | All relevant submitted items were authoritatively evaluable and all were `INCORRECT` |
| `INSUFFICIENT_EVIDENCE` | At least one relevant submitted item could not be evaluated authoritatively |

Roll up only objectives that appear on at least one submitted item for that evaluation. Do not invent class-wide objective mastery.

#### 10.2 Completeness rule (binding)

Do **not** claim `DEMONSTRATED_ON_SUBMITTED_ITEMS` merely because all **deterministically evaluated** items were correct if another relevant submitted item for that same objective is unevaluated.

For v1, if **any** relevant submitted objective-linked item cannot be evaluated authoritatively (`OPEN_RESPONSE_UNEVALUATED` or `UNEVALUATED_POLICY_REJECT`), the rollup **must** be `INSUFFICIENT_EVIDENCE`.

Authoritatively evaluable means item `outcome` is `CORRECT` or `INCORRECT`.

Examples:

| Submitted items for one objective | Rollup |
|-----------------------------------|--------|
| MC `CORRECT` + SA unevaluated | `INSUFFICIENT_EVIDENCE` — **not** demonstrated |
| MC `CORRECT` + TF `CORRECT` and no unevaluated relevant items | `DEMONSTRATED_ON_SUBMITTED_ITEMS` |
| one `CORRECT` + one `INCORRECT`, all evaluable | `MIXED_ON_SUBMITTED_ITEMS` |
| all evaluable and all `INCORRECT` | `NOT_YET_DEMONSTRATED_ON_SUBMITTED_ITEMS` |

### 11. Raw / derived / suggested / decision separation

Teacher Assessment Intelligence **must** classify displayed data.

**RAW FACT** (Learning / Teaching / Identity; not invented by Assessment):

- submission exists
- submission timestamp
- learner identity (`learner_principal_id`)
- question response (subject to authorization)
- assignment binding / exact ContentVersion identity

**DERIVED DETERMINISTIC FACT** (Assessment evaluation + projection):

- MC correctness
- TF correctness
- frequently missed deterministic question
- submission-scoped objective evidence
- submitted learner count
- evaluated learner count (current policy)
- per-learner evaluation state

**AI SUGGESTION:** **none** in the initial ADR-059 implementation baseline.

**TEACHER DECISION:**

- ClassroomAssessment judgment (RECORD / CORRECT / VOID)
- Improve choice
- remediation goal
- future open-response review

Do **not** persist display copy as a new SoR unless required by an invariant. v1 Teacher Assessment Intelligence is an Assessment-owned **derived-on-read projection**. A later materialized read model may be added without becoming a competing SoR, provided it remains rebuildable from `LearnerSubmission` + `LearnerAssessmentEvaluation` + assignment / content / authority facts.

### 12. Teacher Assessment Intelligence projection

Define an **assignment-scoped** Teacher Assessment Intelligence projection.

Minimum useful v1:

| Signal | Source |
|--------|--------|
| submitted learner count | count of `LearnerSubmission` for the assignment |
| evaluated learner count | count of those submissions with a current-policy `LearnerAssessmentEvaluation` |
| per-learner evaluation state | `NOT_EVALUATED` / `EVALUATED_UNDER_CURRENT_POLICY` / `NOT_EVALUATED_UNDER_CURRENT_POLICY` plus current-policy outcomes when present |
| question-level `CORRECT` / `INCORRECT` / unevaluated distribution | current-policy item outcomes only |
| frequently missed deterministic questions | items with `INCORRECT` among deterministically evaluated responses; exclude unevaluated items from the miss numerator |
| objective-evidence rollup | §10, current-policy evaluations only |

Do **not** claim a class score, mastery rate, or “the class understood X.”

#### 12.1 Not-submitted count

Do **not** claim a not-submitted count unless a governed School Context / ERP roster authority can supply the **denominator** as an authoritative learner roster for the relevant class.

The current trusted learner-membership port is a **check-time façade** (ADR-AIEOS-058). It is **not** evidenced as an authoritative class-roster enumeration for teachers.

**First implementation: omit “not submitted” count.**

Never derive class roster size or missing-learner count from guesses, stale frontend state, or assignment UI data.

### 13. Teacher authorization

Teacher access to learner evidence requires **all** of:

```text
same tenant
  +
effective HUMAN teacher semantics
  +
current server-side authority for the relevant class / assignment
```

Frontend class ownership is **not** authorization.

**Historical learner membership:** a learner who submitted while legitimately eligible may later leave the class. That learner’s historical immutable submission / evaluation remains historical evidence. A **currently authorized** teacher may read that historical submitted evidence without requiring that the learner still be enrolled today.

**Historical assignment ownership ≠ perpetual learner-PII access.** A teacher who no longer has **current** authority over the relevant class **MUST NOT** retain learner-level evidence access merely because that teacher originally created the assignment.

Current teacher authority unavailable, stale, or cross-tenant → **FAIL CLOSED**.

If a future institutional records policy requires former-teacher historical access, govern that separately. This ADR does not grant it.

### 14. Learner authorization

Do **not** broaden Student OS in this ADR merely for grading.

**Learner evaluation self-read:** **out of initial scope**. A future additive Student Assessment view may be designed later.

This architecture decision must **not** expose to Student OS:

- answer keys
- teacher-only explanations
- other learners’ evidence
- class aggregates

ADR-AIEOS-058 learner-safe content projection and own-submission readability remain unchanged. Evaluation facts, answer keys, and class intelligence are not added to Student routes here.

### 15. ClassroomAssessment relationship

ClassroomAssessment remains class-level teacher judgment under ADR-AIEOS-055.

```text
LearnerAssessmentEvaluation  ≠  ClassroomAssessment
```

Do **not** add `learner_id` / `student_id` to ClassroomAssessment.  
Do **not** make ClassroomAssessment own submissions.  
Do **not** automatically RECORD or CORRECT ClassroomAssessment from evaluated learner submissions.

Teacher Assessment Intelligence may present derived learner / class patterns as **advisory evidence** that informs a HUMAN teacher judgment. The teacher explicitly RECORDS or CORRECTS ClassroomAssessment when appropriate.

That preserves:

```text
derived evidence  ≠  teacher class-level assessment judgment
```

ClassroomAssessment may already exist before any learner evaluation. Later evaluations do not mutate it. A later CORRECT of ClassroomAssessment does not rewrite evaluations.

### 16. Improve handoff (ADR-AIEOS-056 unchanged)

ADR-AIEOS-056 remains unchanged for initial implementation.

**Required path:**

```text
Teacher Assessment Intelligence
  → teacher reviews real evidence
  → teacher may RECORD / CORRECT ClassroomAssessment
  → teacher chooses Improve
  → teacher confirms / edits remediation goal
  → existing POST /api/v1/teaching/works/from-classroom-assessment
  → TeachingWork(intent_type = remediate_class)
  → immutable TeachingWorkRemediationOrigin
```

No automatic creation of TeachingWork, Content, Publication, Assignment, intervention, or mastery.

Do **not** create a direct `LearnerAssessmentEvaluation` → TeachingWork origin in the ADR-059 baseline. That would require a separately governed forward extension of ADR-AIEOS-056.

A UI deep-link **may** carry advisory display / suggestion state. It **must not** bypass the existing governed ClassroomAssessment-origin requirement. Duplicate Improve clicks remain governed by ADR-AIEOS-056 Idempotency-Key replay.

Automatic Improve is **prohibited**.

### 17. Evaluation trigger

Do **not** permit a side-effecting GET.

Specifically reject:

```text
GET intelligence  →  silently create LearnerAssessmentEvaluation
```

Reads must remain reads.

| Option | Summary | Verdict |
|--------|---------|---------|
| **A** | Explicit idempotent Assessment EVALUATE / ENSURE command | **Selected** for first baseline |
| **B** | Durable local transactional-outbox consumer after Learning submission | **Deferred companion** — Learning NATS PUB remains HOLD; may later drive A without changing evaluation ownership |
| **C** | Post-submit second application transaction inside Learning submit | **Rejected** — grading must not live in the Learning SUBMIT transaction |
| **D** | Temporal workflow | **Rejected** — ordinary domain command; Temporal is not required |

Initial implementation **MUST NOT** depend on production NATS because Learning NATS PUB remains HOLD under ADR-AIEOS-046R1.

**Preferred first implementation:** explicit idempotent Assessment evaluation command and assignment-scoped **batch ensure** command, with business-key replay protection.

It may later be driven automatically by a governed Assessment-owned outbox consumer without changing evaluation ownership.

No Temporal merely for this workflow.

Conceptual operations (not OpenAPI authorization):

- `assessment_learner_evaluation_ensure.v1`
- `assessment_assignment_evaluations_ensure.v1`

Platform `Idempotency-Key` remains the command-identity replay rule ([ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md)). Business uniqueness is the evaluation business key in §5. Both apply.

### 18. Transaction / unit of work

Assessment application owns the evaluation transaction.

Conceptually:

```text
BEGIN Assessment UoW
  read immutable LearnerSubmission through governed Learning read port
  read exact ContentVersion through governed Content read port
  validate lineage
  evaluate under exact evaluation policy
  insert LearnerAssessmentEvaluation
  record Security Audit
  optionally create Assessment-owned transactional outbox intent if later chosen
COMMIT
```

Never:

- write Learning tables
- change `LearnerSubmission`
- change `LearnerAttempt`
- change `ClassroomAssessment`
- create `TeachingWork`
- update mastery

Application service owns the UoW boundary. Repositories do not independently commit ([ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md)).

If Learning submission already committed and a later Assessment ensure fails: Learning evidence remains; evaluation is absent; retry of ensure is the recovery path. That is not a distributed transaction with Learning.

### 19. Idempotency / concurrency

**Business uniqueness:**

```text
tenant_id
  + submission_id
  + evaluation_policy_id
  + evaluation_policy_version
```

| Case | Result |
|------|--------|
| Same evaluation request / same business identity | Same durable result (replay) |
| Concurrent identical evaluation | One durable business outcome (unique constraint; winner inserts; loser reads existing) |
| Different policy version | New explicit evaluation row |
| Same `Idempotency-Key` + same canonical request | Replay same HTTP/command outcome |
| Same key + materially different request | FAIL CLOSED |
| Obsolete policy, row exists | Replay existing row; does not become current projection |
| Obsolete policy, row does not exist | FAIL CLOSED |
| No last-write-wins overwrite | Binding |

### 20. Event / outbox

Learning currently emits submission identity facts only. Learning remains unchanged. Production Learning NATS publishing remains HOLD.

If ADR-059 proposes Assessment events, they must be Assessment-owned. Domain code must **not** directly publish NATS ([ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md)).

Current production EVENT publisher PUB ([ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md)) authorizes only:

```text
io.eduvijna.aieos.content.>
io.eduvijna.aieos.teaching.>
```

It does **not** authorize `io.eduvijna.aieos.assessment.>`. This ADR **does not** modify ADR-AIEOS-046R1 and does **not** freeze production Assessment EVENT PUB.

Existing naming pattern is `io.eduvijna.aieos.{domain}.{aggregate}.{past_tense_verb}.v1` (for example `io.eduvijna.aieos.teaching.assignment.created.v1`). The logical candidate `learner_assessment_evaluated.v1` therefore maps to the subject candidate:

```text
io.eduvijna.aieos.assessment.learner_evaluation.recorded.v1
```

That name is a **candidate only**. It is not production-frozen. Events must not leak raw learner response payloads unless separately governed.

**First client-showcase implementation:** no broker dependency. Optional Assessment-owned transactional outbox may persist the candidate fact for later publication after a future event-plane revision. Duplicate outbox delivery must be idempotent at consumers. No consumer is required in this baseline.

### 21. AI boundary

ADR-059 first implementation authority is **deterministic only**.

No AI is required for MULTIPLE_CHOICE or TRUE_FALSE.  
SHORT_ANSWER remains `OPEN_RESPONSE_UNEVALUATED`.

Future AI-assisted evaluation MAY be described only as future extension and **must** require:

- provider-neutral `StructuredModelGateway`
- typed structured result
- evaluation policy / version
- exact input provenance
- bounded prompt / input schema
- fail-closed behavior
- teacher review
- audit
- clear non-mastery semantics

LLM output **MUST NOT** automatically become mastery, misconception truth, grade authority without governed policy, Improve acceptance, TeachingWork, or learner intervention.

Do **not** create an Assessment Insight Agent implementation in this ADR.

### 22. Mastery / Learner Intelligence boundary

**Explicitly out of scope:**

- long-term mastery
- competency mastery
- misconception truth
- durable strength / weakness
- personalized recommendation
- next-best activity
- Student Agent
- learner memory / model

These require separate governed Learner Intelligence architecture.

ADR-059 produces trustworthy **submission-scoped** assessment evidence. It does **not** create the learner model.

### 23. Future Principal / Parent boundary

Do **not** expose learner Assessment Intelligence to Principal or Parent in this ADR.

Design durable evaluation provenance (`tenant_id`, learner principal, submission, assignment, exact ContentVersion, policy id/version) so later governed projections can consume it safely.

No future persona automatically receives raw learner responses.  
No Principal / Parent permissions are created now.

### 24. Client-showcase path

Thin **real** vertical:

```text
Teacher Assign
  → Student Attempt
  → Student Submit
  → Assessment Evaluate / Ensure
  → durable LearnerAssessmentEvaluation
  → Teacher Assessment Intelligence
  → real question / objective signal
  → teacher judgment
  → ClassroomAssessment where appropriate
  → teacher chooses Improve
  → teacher confirms remediation goal
  → existing remediate_class TeachingWork
```

No fake intelligence.  
No hard-coded grades.  
No mastery claim.  
No mock result represented as production evidence.

### 25. API candidates (conceptual only)

Final HTTP contracts require implementation-slice OpenAPI review. This deposit does **not** authorize OpenAPI change.

Conventions: RFC 9457, stable `operationId`, Idempotency-Key on commands, AIEOS-only frontend boundary ([ADR-044](ADR-044-ai-platform-behind-stable-services.md)).

| Method | Path | Effect |
|--------|------|--------|
| POST | `/api/v1/assessment/submissions/{submission_id}/actions/evaluate` | Idempotent ensure of current-policy evaluation |
| POST | `/api/v1/assessment/assignments/{assignment_id}/actions/ensure-evaluations` | Batch ensure for submitted learners |
| GET | `/api/v1/assessment/assignments/{assignment_id}/intelligence` | Read-only Teacher Assessment Intelligence projection |

GET **must not** insert evaluations.

### 26. Persistence / resource boundary (conceptual)

No migration in this architecture deposition.

Conceptual objects:

- `assessment.learner_evaluations`
- `assessment.learner_evaluation_items` (or equivalent JSONB owned exclusively by the evaluation aggregate)

RLS posture consistent with other tenant-owned AIEOS schemas.

Cross-domain identifiers (Learning submission/attempt, TeachingAssignment, Content, ContentVersion) are ResourceRef / opaque ID boundaries. Do **not** add cross-domain PostgreSQL FKs by default.

This ADR does **not** create: mastery table, Improve aggregate, roster table, student-profile table, or ClassroomAssessment learner columns.

Security audit per [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md). Conceptual audit action candidate: `assessment.learner_evaluation.ensure`. Final capability string freeze is deferred to implementation authorization. Security audit is not the evaluation business SoR.

---

## Scenarios

| ID | Scenario | Expected behaviour |
|----|----------|--------------------|
| A59-01 | Same submission evaluated twice, same policy version | Replay-safe; one durable row; same result |
| A59-02 | Same submission evaluated concurrently, same policy version | One durable business outcome; unique constraint; no last-write-wins |
| A59-03 | Same submission re-evaluated after policy version changes | New immutable row under the new version; prior row retained; current projection uses currently authorized version only |
| A59-04 | Content published pointer moves after assignment | Evaluation still uses the exact assigned / submitted ContentVersion; fail closed if lineage disagrees |
| A59-05 | ContentVersion answer differs in a newer version | Newer version is irrelevant; do not grade against it |
| A59-06 | Learner leaves class after legitimate submission | Historical submission / evaluation remain historical evidence; currently authorized teacher may read them |
| A59-07 | Teacher loses class authority after assignment | FAIL CLOSED for learner-level evidence; historical assignment ownership is not perpetual PII access |
| A59-08 | Cross-tenant teacher requests learner evidence | FAIL CLOSED |
| A59-09 | MC response references an invalid option | `UNEVALUATED_POLICY_REJECT` — not `INCORRECT` |
| A59-10 | TF content answer is `"yes"` | `UNEVALUATED_POLICY_REJECT` |
| A59-11 | TF content answer is `"TRUE "` (whitespace / case) | Legal after trim + lower; map to `true`; compare to submitted bool |
| A59-12 | SA exact text happens to equal `question.answer` | Still `OPEN_RESPONSE_UNEVALUATED`; not `CORRECT` |
| A59-13 | Objective has MC `CORRECT` + SA unevaluated | `INSUFFICIENT_EVIDENCE` — not demonstrated |
| A59-14 | Objective has correct + incorrect deterministic questions, all evaluable | `MIXED_ON_SUBMITTED_ITEMS` |
| A59-15 | ClassroomAssessment already exists before learner evaluations | Unchanged; evaluations do not auto-RECORD or mutate it |
| A59-16 | ClassroomAssessment is CORRECTED after learner evaluation | ClassroomAssessment revision changes; evaluations unchanged |
| A59-17 | Improve requested without ClassroomAssessment | Existing ADR-AIEOS-056 fail-closed / eligibility rules; no new LearnerEvaluation→Work origin |
| A59-18 | Duplicate Improve UI click | ADR-AIEOS-056 Idempotency-Key replay; no second Work from the click |
| A59-19 | Evaluation persistence fails after Learning submission already committed | Submission remains; evaluation absent; retry ensure; no Learning rewrite; no distributed 2PC |
| A59-20 | Assessment event / outbox delivery duplicated | Idempotent at consumer; first implementation has no required broker consumer |
| A59-21 | No authoritative roster available for not-submitted count | **Omit** the count; do not guess |
| A59-22 | Frontend supplies fake correctness | Ignored; server derives from submission + exact ContentVersion + policy |
| A59-23 | Learner tries to read answer key / evaluation answer key | FAIL CLOSED; learner evaluation self-read out of initial scope |
| A59-24 | Teacher tries to read evidence after losing class authority | FAIL CLOSED |
| A59-25 | Current ClassRef authority service unavailable | FAIL CLOSED |

Every listed failure is **fail closed** except replay of an already-committed identical business identity, which is **replay-safe**, and omit-not-submitted, which is **omit rather than fail-open with a fabricated denominator**.

---

## Implementation sequence — planning only

This deposit does **not** authorize implementation. Next implementation remains **blocked pending ADR-059 freeze**. After freeze, slices still require separate Chief Architect authorization. Do **not** bundle backend, frontend, architecture freeze, and E2E into one giant implementation PR.

| Slice | Purpose |
|-------|---------|
| **AIEOS360-S01-I05-B1** | Assessment persistence + deterministic evaluator |
| **AIEOS360-S01-I05-B2** | Assessment application / API + exact authority composition |
| **AIEOS360-S01-I05-B3** | Teacher Assessment Intelligence read projection / API |
| **AIEOS360-S01-I05-F1** | Teacher Assessment Intelligence frontend experience + Improve handoff |
| **AIEOS360-S01-I05-E2E** | Real Student submit → evaluate → Teacher intelligence → Improve journey |

AIEOS360-S01-I04R1 remains **CLOSED**. I05 is not started by this ADR.

---

## Consequences

### Positive

- AIEOS 360 can show teachers real question / objective signal without claiming mastery.
- Learning remains the raw-evidence SoR; Assessment owns policy-versioned evaluation.
- ClassroomAssessment and Improve stay human-deliberate.
- Replay, audit, and policy-version traceability are possible because evaluation is durable and append-only.

### Negative / constraints

- SHORT_ANSWER remains unevaluated until a later governed rubric or AI-review policy exists.
- Not-submitted counts are omitted until roster enumeration authority exists.
- Production Assessment events cannot publish under current ADR-AIEOS-046R1 publisher ACL.
- Teachers who lose current class authority lose learner-evidence access even if they created the assignment.

### Explicitly not authorized

- Backend / Frontend / Product / Infrastructure change
- Migration / OpenAPI
- NATS provisioning / production Assessment or Learning EVENT PUB
- Temporal
- AIEOS360-S01-I05-B1+ implementation
- Moving grades into `LearnerSubmission`
- Learner columns on `ClassroomAssessment`
- Separate Improve SoR
- Automatic TeachingWork / Content / Publication / Assignment / intervention / mastery
- Direct `LearnerAssessmentEvaluation` → TeachingWork origin
- Side-effecting GET
- AI grading / Assessment Insight Agent
- Learner evaluation self-read / Student answer keys
- Principal / Parent Assessment Intelligence
- Education payload schema widening for TRUE_FALSE answers
- Production deployment

---

## Consistency validation (deposit-time)

| Check | Result |
|-------|--------|
| Learning ownership of Attempt / Submission preserved | **PASS** |
| Assessment owns `LearnerAssessmentEvaluation` | **PASS** |
| ClassroomAssessment remains class-level | **PASS** — no learner_id |
| ADR-AIEOS-056 Improve path unchanged | **PASS** — no automatic Improve |
| Assigned ≠ Attempted ≠ Submitted ≠ Evaluated ≠ Mastered | **PASS** |
| Assessed ≠ Mastered; signal ≠ Improve acceptance | **PASS** |
| Historical ADRs 053–058 bodies not edited | **PASS** |
| ADR-AIEOS-046R1 not modified | **PASS** — Assessment PUB not frozen |
| Implementation not authorized | **PASS** |
| Status is Proposed / Freeze Candidate | **PASS** — not Frozen / not Founder-approved |

No exception invented where a conflict would exist.
