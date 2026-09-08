---
id: ADR-AIEOS-058
title: AIEOS Student Assignment Consumption & Learner Attempt Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: approved
version: 1.0.2
created: 2026-09-08
last_updated: 2026-09-08
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-058 — AIEOS Student Assignment Consumption & Learner Attempt Authority

**Status:** Frozen / Approved  
**Chief Architect architecture review:** ACCEPTED / PASS  
**Founder / Product Architecture freeze:** APPROVED — 2026-09-08  
**Date:** 2026-09-08  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md) · [ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md) · [ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md) · [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md) · [ADR-AIEOS-046](ADR-AIEOS-046-aieos-production-event-plane-identity-least-privilege-contract.md) · [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) · [ADR-044](ADR-044-ai-platform-behind-stable-services.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-057](ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md)

**Catalogue note:** Frozen / Approved is **ARCHITECTURE AUTHORITY ONLY**. This ADR freezes the **AIEOS Student Assignment Consumption & Learner Attempt Authority** for **AIEOS360-S01**. Founder / Product Architecture approval was granted **2026-09-08**. Architecture freeze ≠ Backend implementation authorization ≠ Frontend implementation authorization ≠ Product authorization ≠ migration authorization ≠ OpenAPI authorization ≠ NATS provisioning ≠ Temporal authorization ≠ deployment authorization ≠ production mutation authorization. This architecture freeze does **not** itself authorize implementation. Implementation slices **S01-I01+** remain **NOT AUTHORIZED**. **S01-I01** is the **NEXT CANDIDATE** and is **NOT YET AUTHORIZED**.

**ID family note:** `ADR-AIEOS-058` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 and from platform infrastructure ADR-AIEOS-048 / 048R1 / 048R2.

**Architecture programme:** **AIEOS 360 CLIENT SHOWCASE** / package **AIEOS360-S01**. TOS-CX01 closed Teacher OS Client Showcase Ready. This ADR does **not** reopen Teacher OS domain authority.

Does **not** reopen or rewrite: ADR-AIEOS-053 TeachingAssignment; ADR-AIEOS-054 TeachingExecution; ADR-AIEOS-055 ClassroomAssessment; ADR-AIEOS-027 Generic Content; ADR-AIEOS-046R1 production EVENT publisher scope; ADR-AIEOS-023R1 Principal kinds.

**AIEOS360-S01P1R1 (v1.0.1):** Chief Architect exact-head correction deposited while Proposed. S01 LearnerAttempt lifecycle is `IN_PROGRESS` → `SUBMITTED` only. `ABANDONED` / discard / reset = **DEFERRED FUTURE POLICY**. Current membership is evaluated at the command’s authoritative check; S01 does **not** claim atomic ERP↔AIEOS revocation ordering.

AIEOS360-S01P1 design deposit and AIEOS360-S01P1R1 lifecycle/membership correction were deposited as Proposed (v1.0.0 / v1.0.1) before freeze. Founder / Product Architecture approval was granted on **2026-09-08**. Exact approval: **Freeze ADR-AIEOS-058 — AIEOS Student Assignment Consumption & Learner Attempt Authority — Approved.** Chief Architect architecture review: **ACCEPTED / PASS**. This freeze does **not** authorize implementation.

Historical ADR-AIEOS-012 / 013 / 014 titles were not found in this repository and are **not** reconstructed here.

---

## Context

Teacher OS through TOS-CX01 has a real teacher vertical:

```text
Prepare → Review → Publish → TeachingAssignment → Teach → class-level Assess → Improve
```

ADR-AIEOS-053 froze TeachingAssignment as teacher-owned **class-scoped assignment intent** and deferred learner visibility, roster live-vs-snapshot, attempt, and submission to Future Student / Learning. ADR-AIEOS-055 froze ClassroomAssessment as **class-level** and reserved learner attempt/submission SoR for Student / Learning unless an explicit ADR-053 forward revision moves it.

Governed Backend/Frontend at this deposition have **no** LearnerAttempt, LearnerSubmission, student routes, roster tables, or Student OS shell. School Context today is a teacher ClassRef read façade only.

AIEOS360-S01 discovery (ACCEPTED) established the first real cross-role vertical:

```text
Teacher TeachingAssignment
        ↓
eligible Student
        ↓
Student sees assignment
        ↓
exact assigned ContentVersion (learner-safe projection)
        ↓
LearnerAttempt
        ↓
LearnerSubmission
        ↓
Learning Evidence boundary
```

This ADR freezes that authority. It does **not** authorize implementation.

---

## Decision

### 1. Separation invariants (binding)

Preserve ADR-AIEOS-053 / 054 / 055 and extend the attempt/submit boundary:

```text
Generated   ≠  Approved
Approved    ≠  Published
Published   ≠  Assigned
Assigned    ≠  Attempted
Attempted   ≠  Submitted
Submitted   ≠  Graded
Graded      ≠  Assessed
Assessed    ≠  Mastered
```

Also preserve:

```text
Assigned  ≠  Externally Delivered
```

**ADR-AIEOS-053 TeachingAssignment authority is not reopened.** TeachingAssignment remains assignment-intent SoR. This ADR does not add learner roster snapshots, `max_attempts`, or learner identity fields to TeachingAssignment.

### 2. Authority table

| Concern | Authority |
|---------|-----------|
| Teacher-owned classroom assignment intent | **TeachingAssignment** — AIEOS Teaching ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| Artifact / immutable version payload | **Content / ContentVersion** — AIEOS Content ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)) |
| Class identity / learner enrollment / Class membership master | **ERP / SIS / Admin School Context** |
| Current learner membership for access | **AIEOS School Context learner-membership read façade** — **not** the ERP master |
| Authenticated actor | **AIEOS Principal** (`HUMAN`) ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md)) |
| Attempt working state | **LearnerAttempt** + **AttemptResponseItems** — AIEOS Learning (this ADR) |
| Raw immutable learning evidence | **LearnerSubmission** — AIEOS Learning (this ADR) |
| Class-level teacher assessment | **ClassroomAssessment** — AIEOS Assessment ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)) |
| Grade / mastery / misconception / recommendation / personalization | **Future** Assessment Intelligence / Learner Intelligence — **not S01** |
| Optional LMS delivery | **Future** external connector ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |

Learner attempt/submission **MUST NOT** be moved into ClassroomAssessment. Any later move into Assessment requires an explicit governed forward revision of ADR-AIEOS-053 **and** this ADR.

### 3. Learner identity

The authenticated student is an **ACTIVE HUMAN** AIEOS Principal.

Do **NOT** create `PrincipalKind.STUDENT`.  
Do **NOT** invent a second authentication identity.

**LearnerAttempt business ownership field:** `learner_principal_id`.

Direct S01:

```text
principal_id = effective_actor_id = learner_principal_id
```

No teacher-as-student impersonation.  
No delegation in S01.

A future learner/student profile may reference PrincipalId. It is **not** an S01 SoR.

An optional opaque `school_learner_ref` may be carried as **correlation metadata** if School Context supplies it. It **MUST NOT** become a competing authentication identity.

### 4. Roster semantics

**S01 roster model:** live current membership for **current access** + immutable historical **submission** retention.

TeachingAssignment continues to bind only `class_ref`. **No** learner roster snapshot is added to TeachingAssignment. S01 does **not** claim a historical roster SoR.

Student **current** assignment eligibility:

```text
current ERP/SIS membership façade
  ∩
TeachingAssignment eligibility
```

| Case | Rule |
|------|------|
| Current member + ACTIVE + available | Current access |
| Joins after assignment creation | Eligible while the assignment remains ACTIVE / startable |
| Leaves before starting | Cannot start once removal is observed at the command membership check |
| Leaves while `IN_PROGRESS` | If removal is observed at save/submit membership check → fail closed; existing attempt may remain `IN_PROGRESS`; no auto-delete / auto-submit / auto-abandon. An already-authorized command that received a positive membership decision before revocation becomes observable may complete. Subsequent current-access commands fail closed once removal is observed |
| Leaves after `SUBMITTED` | Submitted evidence remains immutable |
| Removed learner | Not present in the **current** assignment list once removal is observed |
| Own already-submitted evidence | May remain readable subject to ACTIVE Principal / tenant authority |
| Membership façade unavailable | **FAIL CLOSED** for current assignment activity |

The façade is replaceable. It is **not** the ERP master. Production ERP/SIS remains later. NON_PRODUCTION synthetic membership is an implementation substrate after freeze — **not** authorized by this deposit.

A learner no longer observed as a current member receives **no new current-access command authorization**. S01 does **not** claim instantaneous cross-system revocation.

Membership checks are **external / current-authority façade checks** during command execution. They do **not** participate in the same database transaction as ERP/SIS. No distributed 2PC / XA with ERP.

Current learner membership is evaluated at the authoritative membership check used for the command.

If membership is denied or unavailable at that check, the command fails closed.

A membership change that occurs after a successful external authority check is not atomically ordered with the local AIEOS transaction in S01.

AIEOS does not claim atomic ERP↔AIEOS revocation ordering without a future versioned/fenced membership contract.

Such membership change governs subsequent current-access commands.

S01 does **not** invent ERP locks, leases, distributed transactions, historical membership SoR, or an event-synchronization requirement.

### 5. Exact ContentVersion

The student consumes:

```text
TeachingAssignment.content_id
+
TeachingAssignment.content_version_id
```

**exactly.**

Later changes to `Content.published_version_id` **DO NOT** change an existing assignment. Existing assignments never silently float to a newer publication.

Copied onto LearnerAttempt at start and onto LearnerSubmission at submit. Immutable on those records.

### 6. Learner-safe content projection

Student routes **MUST** return a **canonical learner-facing projection** for the specific known content type and schema version.

Normal student routes must **NEVER** return raw Generic Content payload.

This is a **positive allowlist**, not “raw payload minus answer/explanation.”

**Only explicitly learner-allowlisted fields may cross Student APIs.**

Current learner-facing content kinds:

- `worksheet`
- `quiz`
- `homework`

Teacher-only kinds (fail closed on Student routes):

- `lesson_plan`
- `answer_key`
- `teacher_notes`

The projection must omit **all** non-learner fields, including as applicable:

- `answer`
- `explanation`
- `teacher_summary`
- `teacher_notes`
- answer-key linkage
- other teacher-only metadata

This ADR does **not** freeze every eventual DTO property. It freezes the allowlist invariant.

Unknown content type / schema version without a governed learner mapper → **FAIL CLOSED**. **NO raw fallback.**

Generic Content SoR is **not** redesigned.

### 7. LearnerAttempt

**Owning domain:** Learning  
**Conceptual schema:** `learning`  
**Aggregate:** LearnerAttempt

Candidate minimum fields:

| Field | Semantics |
|-------|-----------|
| `attempt_id` | Aggregate identity (UUIDv7) |
| `tenant_id` | Tenant scope |
| `learner_principal_id` | Represented HUMAN student Principal |
| `teaching_assignment_id` | ResourceRef / opaque ID to TeachingAssignment |
| `content_id` | Exact assigned Content identity (copied at start) |
| `content_version_id` | Exact assigned ContentVersion (copied at start) |
| `class_ref` | Copied at start (audit; not live roster SoR) |
| `attempt_number` | Forward-compatible sequence; S01 normally `1` |
| `lifecycle_state` | `IN_PROGRESS` \| `SUBMITTED` |
| `started_at` | Server-controlled |
| `last_saved_at` | Server-controlled |
| `submitted_at` | Set on submit |
| `submission_id` | Exact LearnerSubmission after submit |
| `aggregate_revision` | Optimistic concurrency |
| `created_at` / `updated_at` | Audit timestamps |

Optional audit metadata may include `assignment_revision_at_start`.

**Explicitly excluded:**

- score, grade, mastery
- misconception, recommendation
- AI output
- ClassroomAssessment identity as business authority

Cross-domain identifiers use ResourceRef / opaque ID boundaries. **No** default cross-domain PostgreSQL FKs ([ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md)).

### 8. Attempt lifecycle

S01 minimum:

```text
IN_PROGRESS → SUBMITTED
```

`SUBMITTED` is **terminal**.  
No reopen of the same submitted attempt.

`ABANDONED` / discard / reset semantics = **DEFERRED FUTURE POLICY**.

S01 has no governed actor or command for abandonment and freezes one-attempt business policy.

Do **not** invent:

- abandon endpoint
- teacher abandon
- system auto-abandon
- new attempt after abandon
- retry policy

Late is **not** a lifecycle state.  
Do **not** add `GRADED` or `MASTERED` to LearnerAttempt.  
Do **not** add `ABANDONED` to the S01 `lifecycle_state` field.

Assignment `CLOSED` or `CANCELLED`, membership loss, or other current-authority loss:

- existing `IN_PROGRESS` attempt **may remain** `IN_PROGRESS`
- save = **denied**
- submit = **denied**
- no auto-delete
- no auto-submit
- no auto-abandon

### 9. Attempt cardinality

Persistence **MUST** remain future-capable of multiple attempts.

Therefore: **NO** permanent uniqueness constraint on `learner + assignment` alone.

At most **one `IN_PROGRESS`** attempt may exist for:

```text
tenant_id + learner_principal_id + teaching_assignment_id
```

**S01 business policy is ONE ATTEMPT ONLY.**

After a learner has a `SUBMITTED` attempt for an assignment, starting another attempt in S01 → **NOT AUTHORIZED / FAIL CLOSED** until a future explicit attempt/retry policy is frozen.

Do **not** add `max_attempts` to TeachingAssignment.

`attempt_number` exists for forward compatibility. Current S01 value is normally `1`.

Multiple permitted attempts as a user capability: **DEFERRED / FUTURE POLICY**.

### 10. Response working state

Conceptual table: `learning.attempt_response_items`

Mutable while the attempt is `IN_PROGRESS`.

Logical identity:

```text
attempt_id + question_id
```

Existing governed educational questions already provide stable question IDs.

Responses must be typed/bounded for supported kinds:

- multiple choice
- short answer
- true/false

Partial save is permitted.

Do **not** use one uncontrolled attempt mega-JSON.  
Generic Content is not modified.

### 11. LearnerSubmission

**LearnerSubmission is a distinct immutable Learning-domain record.**  
It is the authoritative **raw learning-evidence snapshot**.

Candidate fields:

| Field | Semantics |
|-------|-----------|
| `submission_id` | Identity (UUIDv7) |
| `tenant_id` | Tenant |
| `attempt_id` | Source attempt |
| `learner_principal_id` | Same HUMAN Principal |
| `teaching_assignment_id` | Opaque assignment ID |
| `content_id` / `content_version_id` | Exact assigned version |
| `class_ref` | Copied |
| response snapshot | Frozen working responses |
| `submitted_at` | Server-controlled |
| `assignment_revision_at_submit` | TeachingAssignment revision observed |
| `due_at_at_submit` | Immutable due snapshot (nullable) |
| `created_at` | Audit |

No grade fields. No mastery fields.

On successful submit: the attempt becomes `SUBMITTED` and references the exact `submission_id`.

Resubmission is **NOT** available in S01.

### 12. Late semantics

Do **not** store an unexplained `late = true/false` that would drift if `TeachingAssignment.due_at` later changes.

Freeze `due_at_at_submit` as an immutable snapshot.

If persisted, `was_late_at_submit` means **exactly**:

```text
due_at_at_submit != null
AND submitted_at > due_at_at_submit
```

Later TeachingAssignment due-date edits **do not** rewrite historical submission evidence.

If `due_at` has passed while the assignment remains `ACTIVE`, S01 still allows submission; lateness is determined against the due snapshot at submit.

### 13. Learning Evidence boundary

```text
LearnerSubmission = raw immutable learning evidence
```

Later derived authority (NOT S01):

- score / grade
- mastery
- misconception
- recommendation
- personalization
- assessment intelligence

Submit **MUST NOT** automatically mutate:

- ClassroomAssessment
- Teacher Improve
- Mastery
- Teacher Memory

### 14. ClassroomAssessment

[ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) remains binding.

ClassroomAssessment remains teacher-owned and class-level.

Do **not**:

- add `learner_id`
- add `submission_id`
- convert it into learner-level result SoR

Future learner Assessment Intelligence may consume LearnerSubmission through a later explicit architecture decision.

### 15. Student assignment eligibility

For current Student **list / open / start / save / submit**, require as applicable:

- trusted tenant
- ACTIVE HUMAN Principal
- active tenant authority
- Principal = learner owner of the attempt
- assignment exists in tenant
- current learner membership in `assignment.class_ref`
- `ACTIVE` assignment for mutations
- `available_from <= now` for current work / start
- learner-facing content kind
- exact assigned ContentVersion

UUID knowledge is **never** authority.

| Assignment state | Student mutation |
|------------------|------------------|
| `CLOSED` | no start / save / submit |
| `CANCELLED` | no start / save / submit |
| `ACTIVE` and `due_at` passed | submission remains allowed in S01; lateness vs due snapshot |

Teacher ownership of the assignment is **not** a student authorization grant.

### 16. Concurrency

Use `aggregate_revision` + `ETag` / `If-Match` for mutable attempts.

`Idempotency-Key` for command identity.

Submit must be race-safe against assignment close, assignment cancel, attempt save, and duplicate submit.

For **internal AIEOS state**, deterministic authority ordering:

```text
TeachingAssignment authority
  then
LearnerAttempt authority
  then
LearnerSubmission creation
```

The implementation must serialize Assignment lifecycle authority and Attempt transition sufficiently that:

- cancel/close wins first → submission fails
- submit wins authoritative eligibility first and commits → immutable submission exists

Exactly one authoritative **internal AIEOS** outcome.

ERP/SIS membership does **not** participate in that internal serialization. Membership is evaluated at the authoritative membership check used for the command. Denied or unavailable at that check → fail closed. A membership change after a successful external authority check is not atomically ordered with the local AIEOS transaction in S01. No distributed 2PC / XA. No atomic ERP↔AIEOS revocation ordering without a future versioned/fenced membership contract. Such a change governs subsequent current-access commands.

### 17. Idempotency

Platform command identity ([ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md)):

| Case | Result |
|------|--------|
| Same `Idempotency-Key` + same canonical request | Replay same result |
| Same key + materially different request | Fail closed |
| Different key | Distinct command where lifecycle permits |

Conceptual operations:

- `learning_attempt_start.v1`
- `learning_attempt_save_responses.v1`
- `learning_attempt_submit.v1`

Business uniqueness is not idempotency.

### 18. Events

Candidate business facts (transactional outbox; facts, not commands):

- `io.eduvijna.aieos.learning.attempt.started.v1`
- `io.eduvijna.aieos.learning.attempt.submitted.v1`

[ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) production EVENT publisher PUB currently authorizes only:

```text
io.eduvijna.aieos.content.>
io.eduvijna.aieos.teaching.>
```

It does **not** authorize `io.eduvijna.aieos.learning.>`.

Therefore:

- Learning outbox persistence may be implemented in development **after** implementation authorization
- Production NATS publication of Learning events remains **HOLD**
- A later narrow event-plane forward revision is required before production Learning-event publication

This ADR **does not** modify ADR-AIEOS-046R1.

### 19. Temporal

**Temporal is NOT REQUIRED for S01.**

Start / save / submit are ordinary authoritative domain commands. Future durable learner workflows may revisit Temporal.

### 20. AI / Model Gateway

LearnerAttempt and submit have **NO** AI provider dependency.

No Groq call during authoritative submit.  
No OpenAI call.  
No Model Gateway requirement.

Later Assessment Intelligence may interpret already-created evidence through AIEOS Model Gateway. **Submission authority ≠ AI output.**

### 21. MCP / Agents

No Student Agent in S01.  
No MCP implementation in S01.

```text
LearnerAttempt     ≠  MCP state
LearnerSubmission  ≠  Agent state
Learning Evidence  ≠  LLM state
```

Frontend talks only to AIEOS application APIs ([ADR-044](ADR-044-ai-platform-behind-stable-services.md)).

### 22. Security

Fail-closed ownership:

- A learner can access only **own** attempt/submission
- One tenant cannot access another
- One learner cannot access another learner’s attempt by UUID
- A teacher cannot impersonate a learner through Student routes
- Suspended / inactive Principal: no current access / mutation
- Current class membership: required for current assignment activity, evaluated at the command’s authoritative membership check
- Already-submitted own evidence: may remain readable after class membership loss, subject to ACTIVE Principal / tenant authority
- Membership revocation is not claimed as instantaneous or atomically ordered with the local AIEOS transaction
- Support / delegation: **not S01**

### 23. Minimum Student experience

Thin experience boundary only (not full Student OS):

```text
/student-os/home
/student-os/assignments/{assignment_id}
/student-os/attempts/{attempt_id}
```

```text
Student sees current assignments
  → opens learner-safe resource
  → starts / resumes
  → answers
  → saves
  → submits
  → sees submitted confirmation
```

Out of S01:

- Student Mission intelligence
- AI Tutor
- student Library
- mastery dashboard
- Parent OS
- Principal OS
- full personalization

### 24. API candidate

Conceptual contract only. Final HTTP contracts require implementation-slice OpenAPI review. Conventions: RFC 9457, stable `operationId`, ETag / If-Match, Idempotency-Key, AIEOS-only frontend boundary.

Student OS read façade:

| Method | Path |
|--------|------|
| GET | `/api/v1/student-os/home` |
| GET | `/api/v1/student-os/assignments` |
| GET | `/api/v1/student-os/assignments/{assignment_id}` |

Learning SoR:

| Method | Path |
|--------|------|
| POST | `/api/v1/learning/assignments/{assignment_id}/attempts` |
| GET | `/api/v1/learning/attempts/{attempt_id}` |
| PUT | `/api/v1/learning/attempts/{attempt_id}/responses` |
| POST | `/api/v1/learning/attempts/{attempt_id}/actions/submit` |

Possible teacher read (summary only):

| Method | Path |
|--------|------|
| GET | `/api/v1/teaching/assignments/{assignment_id}/submissions` |

This deposit does **not** authorize OpenAPI change.

### 25. Persistence / Resource boundary (conceptual)

No migration in this architecture deposition.

Conceptual objects:

- `learning.attempts`
- `learning.attempt_response_items`
- `learning.submissions`

RLS posture consistent with other tenant-owned AIEOS schemas.

Cross-domain identifiers (TeachingAssignment, Content, ContentVersion) are ResourceRef / opaque ID boundaries. Do **not** add cross-domain PostgreSQL FKs by default.

S01 does **not** create: roster table, student-profile table, mastery table, grading table.

---

## Scenarios

| ID | Scenario | Disposition |
|----|----------|-------------|
| S01-01 | Existing class learner receives active assignment | Candidate **PASS** |
| S01-02 | Non-member guesses assignment ID | Candidate **PASS** — fail closed |
| S01-03 | Student joins class after assignment was created | Candidate **PASS** — eligible while ACTIVE/startable |
| S01-04 | Student leaves class before opening assignment | Candidate **PASS** — cannot start |
| S01-05 | Student leaves class after submitting | Candidate **PASS** — evidence retained; not on current list |
| S01-06 | `available_from` is in the future | Candidate **PASS** — not current work |
| S01-07 | `due_at` passed, assignment remains ACTIVE | Candidate **PASS** — submit allowed; lateness vs snapshot |
| S01-08 | Assignment CLOSED before attempt starts | Candidate **PASS** — no start |
| S01-09 | Assignment CANCELLED while attempt is IN_PROGRESS | Candidate **PASS** — save/submit fail closed; attempt may remain IN_PROGRESS; no auto-abandon |
| S01-10 | Teacher publishes a newer ContentVersion after assignment creation | Candidate **PASS** — assignment unchanged |
| S01-11 | Student opens existing assignment after newer version exists | Candidate **PASS** — assigned version |
| S01-12 | Two browser tabs update same attempt | Candidate **PASS** — If-Match |
| S01-13 | Duplicate start-attempt request | Candidate **PASS** — idempotency / one IN_PROGRESS |
| S01-14 | Duplicate submit request | Candidate **PASS** — replay |
| S01-15 | Save races with submit | Candidate **PASS** |
| S01-16 | Multiple permitted attempts | **DEFERRED / NOT AUTHORIZED IN S01** |
| S01-17 | Student tries to access another learner's attempt | Candidate **PASS** — fail closed |
| S01-18 | Suspended student Principal | Candidate **PASS** — fail closed |
| S01-19 | Worksheet with answer-key relationship | Candidate **PASS** — projection only |
| S01-20 | Student attempts to retrieve teacher-only Answer Key | Candidate **PASS** — fail closed |
| S01-21 | Submission creates learning evidence but no grade/mastery | Candidate **PASS** |
| S01-22 | Teacher sees submission existence without mutating ClassroomAssessment | Candidate **PASS** |
| S01-23 | Future ERP outage during membership resolution | Candidate **PASS** — fail closed |
| S01-24 | Retry after ambiguous HTTP outcome | Candidate **PASS** — Idempotency-Key |
| S01-25 | Tenant isolation attack | Candidate **PASS** — fail closed |
| S01-26 | Learner leaves class after attempt started but before submit | Candidate **PASS** — no new current-access authorization once removal is observed at the command membership check; save/submit fail closed when observed; already-authorized command may complete if positive membership was decided before revocation becomes observable; no automatic deletion of attempt; no automatic submission; no auto-abandon; subsequent commands fail closed once removal is observed |
| S01-27 | Teacher changes `due_at` after learner submitted | Candidate **PASS** — `due_at_at_submit` and lateness fact do not change |
| S01-28 | Submit races assignment cancel/close | Candidate **PASS** — internal AIEOS authority serialization; exactly one authoritative internal outcome |
| S01-29 | Future Content schema adds a teacher-only field | Candidate **PASS** — student projection does not expose it unless explicitly allowlisted |
| S01-30 | ERP/SIS membership revocation races with LearnerAttempt submit | Candidate **PASS** with bounded semantics — Case A: revocation observed by the authoritative membership check → submit fails closed. Case B: membership positively authorized by the command check and revocation occurs/becomes observable afterward → already-authorized local command may commit. No atomic ERP↔AIEOS ordering claim. Subsequent current-access commands fail closed. No distributed 2PC |

---

## Implementation sequence — planning only

This architecture freeze does **not** itself authorize implementation. **S01-I01** = **NEXT CANDIDATE, NOT YET AUTHORIZED**.

| Slice | Purpose |
|-------|---------|
| **S01-I01** | Learner-membership façade + NON_PRODUCTION student HUMAN Principal / membership substrate |
| **S01-I02** | Learning domain persistence: Attempt + ResponseItems + Submission + RLS |
| **S01-I03** | Student-os read façade + Learning command APIs + learner-safe positive projection |
| **S01-I04** | Student OS shell / assignment / attempt / submit UX |
| **S01-I05** | Product E2E: Teacher Assign → Student sees → opens exact learner-safe version → attempts → submits → durable LearnerSubmission exists → ClassroomAssessment unchanged |

No implementation begins from this freeze.

---

## Consequences

### Positive

- First AIEOS 360 Student Intelligence vertical can be frozen without reopening TeachingAssignment or class-level Assessment.
- Learner identity stays on ADR-AIEOS-023R1 HUMAN Principals.
- Exact assigned ContentVersion and positive learner projection close the answer-key leakage path without redesigning Generic Content.
- Immutable LearnerSubmission is raw evidence; later intelligence remains additive.

### Negative / constraints

- Live membership means late joiners can become eligible while the assignment remains startable.
- S01 does not claim atomic ERP↔AIEOS membership revocation ordering; subsequent current-access commands fail closed once removal is observed.
- S01 one-attempt policy is stricter than the persistence model; retry requires a later freeze.
- Production Learning events cannot publish under current ADR-AIEOS-046R1 publisher ACL.
- Real ERP/SIS membership is not in-repo; S01 depends on a façade + NON_PRODUCTION substrate after implementation authorization.

### Explicitly not authorized

- Backend / Frontend / Product / Infrastructure change
- Migration / OpenAPI
- S01-I01+ implementation
- PrincipalKind.STUDENT
- Roster snapshot on TeachingAssignment
- Moving attempt/submission into ClassroomAssessment
- Temporal, Groq/OpenAI/Model Gateway on submit, Student Agent, MCP
- Production NATS Learning publication
- Production deployment
- abandon endpoint; teacher abandon; system auto-abandon; new attempt after abandon; S01 retry policy
- ERP locks / leases / 2PC / XA; historical membership SoR; event-synchronization requirement for S01 membership revocation

---

## Consistency validation (deposit-time)

| Check | Result |
|-------|--------|
| TeachingAssignment not reopened | **PASS** — class_ref only; no roster snapshot; no max_attempts |
| ClassroomAssessment remains class-level | **PASS** — no learner_id / submission_id |
| Principal kinds unchanged | **PASS** — HUMAN only; no STUDENT kind |
| Assigned ≠ Attempted ≠ Submitted ≠ Graded | **PASS** |
| Learner-safe projection is allowlist, not subtractive | **PASS** |
| ADR-AIEOS-046R1 not modified | **PASS** — production Learning PUB HOLD recorded |
| Implementation not authorized | **PASS** |
| S01 lifecycle is IN_PROGRESS → SUBMITTED only | **PASS** — ABANDONED deferred |
| No atomic ERP↔AIEOS membership ordering claimed | **PASS** — check-time façade; subsequent commands fail closed |

No exception invented where a conflict would exist.
