---
id: ADR-AIEOS-061
title: AIEOS Parent Intelligence & Learner Access Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: proposed
version: 1.0.0
created: 2026-09-17
last_updated: 2026-09-17
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-061 — AIEOS Parent Intelligence & Learner Access Authority

**Status:** Proposed  
**Chief Architect architecture review:** PENDING EXACT-HEAD REVIEW  
**Founder / Product Architecture freeze:** NOT GRANTED  
**IMPLEMENTATION NOT AUTHORIZED**

**Date:** 2026-09-17  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md) · [ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md) · [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md) · [ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md) · [ADR-AIEOS-046](ADR-AIEOS-046-aieos-production-event-plane-identity-least-privilege-contract.md) · [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) · [ADR-044](ADR-044-ai-platform-behind-stable-services.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) · [ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md)

**Catalogue note:** Proposed is **ARCHITECTURE PROPOSAL DEPOSIT ONLY**. This ADR deposits the **AIEOS Parent Intelligence & Learner Access Authority** for **AIEOS360-S03P3** Chief Architect review. It is **not Frozen**. It is **not Approved**. It is **not Implemented**. It is **not implementation-authorized**. Architecture proposal deposited ≠ Backend implementation authorization ≠ Frontend implementation authorization ≠ Product authorization ≠ Infrastructure authorization ≠ migration authorization ≠ OpenAPI authorization ≠ authorization-kernel code authorization ≠ School Context code authorization ≠ Parent API code authorization ≠ Parent UI authorization ≠ synthetic adapter implementation ≠ NATS authorization ≠ Temporal authorization ≠ Parent Agent authorization ≠ ERP/SIS integration authorization ≠ deployment authorization. **THIS ADR FREEZE/DEPOSIT DOES NOT AUTHORIZE IMPLEMENTATION.** Even after a later Freeze / Approved status, Backend implementation still requires separate Chief Architect authorization.

**ID family note:** `ADR-AIEOS-061` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 and from platform infrastructure ADR-AIEOS-048 / 048R1 / 048R2.

**Architecture programme:** **AIEOS 360 CLIENT SHOWCASE** / package **AIEOS360-S03**. Architecture proposal package: **AIEOS360-S03P3**. Lineage: **AIEOS360-S03P1** discovery = **ACCEPTED / PASS**; **AIEOS360-S03P2** architecture proposal = **DIRECTION ACCEPTED / CORRECTION REQUIRED**; **AIEOS360-S03P2R1** correction = **ACCEPTED / PASS**.

Does **not** reopen or rewrite historical ADR bodies: ADR-AIEOS-023R1, ADR-AIEOS-024, ADR-AIEOS-025, ADR-AIEOS-028, ADR-AIEOS-030, ADR-AIEOS-031, ADR-AIEOS-046, ADR-AIEOS-046R1, ADR-AIEOS-053, ADR-AIEOS-054, ADR-AIEOS-055, ADR-AIEOS-056, ADR-AIEOS-058, **ADR-AIEOS-059**, **ADR-AIEOS-060**.

This document deposits architecture for Chief Architect review. Implementation remains unauthorized. Do **not** start I01.

---

## Context

AIEOS360-S01 closed the Student assignment / attempt / submission path. [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) remains **Frozen / Approved**.

AIEOS360-S01-I05 closed Learner Assessment Intelligence / Teacher Improve handoff. [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) remains **Frozen / Approved**.

AIEOS360-S02 closed the Principal / School Intelligence development slice. [ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) remains **Frozen / Approved**.

AIEOS360-S03 is the next thin AIEOS360 experience: **Parent Intelligence**.

Binding product objective:

> PARENT CLARITY WITHOUT TEACHER OVERLOAD.

Shared vertical:

```text
Teacher → Publish / Assign → Student → Attempt / Submit
        → Learning Evidence → Assessment Intelligence
        → Teacher Improve → Principal / School Intelligence
        → PARENT INTELLIGENCE
```

Governed evidence at this deposition (read-only; not modified by this ADR):

| Surface | Pin |
|---------|-----|
| Architecture `origin/main` base | `4475cb60e69b2acbc5f97ed5a67e418979533ba7` |
| Backend `origin/main` | `e2bfce86afece6772eaf7c2f1eb18e2dd2240f1b` |
| Frontend `origin/main` | `1b4263d0668f66d84cc261c79a2e81883375219e` |
| Product `origin/main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Alembic head | `a360s010004` |
| Authoritative OpenAPI SHA-256 | `BE60CC2A4612F77AB333088D264B9501B9AB842995AEC1539DA89EA0E8462B47` |

**AIEOS360-S03P1 discovery found:**

- no authoritative current adult→learner access authority
- no Parent OS implementation
- no parent capability
- no Parent Intelligence SoR
- no production guardian ERP/SIS adapter
- no safe basis to authorize Parent reads without new current authority

**AIEOS360-S03P2 + S03P2R1** established the corrected proposed architecture deposited here.

---

## Decision

### 1. Separation invariants (binding)

Preserve ADR-AIEOS-053 / 054 / 055 / 056 / 058 / 059 / 060:

```text
Published                         ≠  Assigned
Assigned                          ≠  Attempted
Attempted                         ≠  Submitted
Submitted                         ≠  Evaluated
Evaluated                         ≠  Mastered
Assigned                          ≠  Taught
Taught                            ≠  Assessed
Assessed                          ≠  Mastered
Assessment signal                 ≠  Improve acceptance
LearnerAssessmentEvaluation       ≠  ClassroomAssessment
Derived Teacher Intelligence      ≠  teacher class-level judgment
Deterministic item outcome        ≠  mastery / competency attainment
Submission-scoped objective evidence ≠ learner-model truth
School Intelligence projection    ≠  a new business SoR
Parent Intelligence projection    ≠  a new business SoR
Authorization                     ≠  Presentation
Adult actor lifecycle             ≠  Learner data-subject status
AUTHORITATIVE FACT                ≠  GENERATED EXPLANATION
```

Do **not** move family / guardian / custody / household master into AIEOS.  
Do **not** put evaluation or mastery fields into Parent Intelligence.  
Do **not** reuse Teacher Assessment Intelligence or Principal School Intelligence as Parent sources or DTOs.

### 2. What Parent Intelligence is

**Selected:** Parent Intelligence is a **DERIVED_ON_REQUEST**, privacy-safe, learner-scoped **read projection**.

It is **NOT**:

- family SoR
- guardian SoR
- custody SoR
- household SoR
- Parent Intelligence business SoR
- Student Intelligence duplicate
- Teacher Assessment Intelligence projection reuse
- Principal School Intelligence projection reuse

Architecture:

```text
TrustedRequestIdentity
  ↓
Current Tenant Authority
  ↓
ACTIVE HUMAN adult Principal
  ↓
parent.intelligence.read
  ↓
Parent Learner Access Current Authority
  ↓
authorized learner Principal IDs
  ↓
current learner membership / source composition
  ↓
positive-allowlist Parent Intelligence read projection
  ↓
Parent OS
```

Time baseline: **CURRENT_FACTS_AS_OF_REQUEST**.

No Parent Intelligence persistence.  
No Parent UoW mutation.  
No ensure-evaluations side effect.  
GET is side-effect free.  
No durable access snapshot.  
Revalidate every GET.  
Historical relationship creates no current access right.

Compose only after the authorized learner set has been resolved.

### 3. Identity

`PrincipalKind` remains exactly:

```text
HUMAN
WORKLOAD
```

Do **NOT** create:

- `PrincipalKind.PARENT`
- `PrincipalKind.GUARDIAN`
- `PrincipalKind.STUDENT`
- `PrincipalKind.LEARNER`

Adult product “parent” = **ACTIVE HUMAN Principal**.  
Child product “learner” = canonical **HUMAN Principal** used as the learner data subject.

Adult remains:

```text
principal_id = effective_actor_id
```

No impersonation of child.  
No delegation to child for S03 baseline.

JWT proves `principal_id` only ([ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md)).  
JWT / header / frontend learner ID never proves entitlement.

### 4. Exact capability

**Proposed capability:** `parent.intelligence.read`

Require **BOTH**:

1. exact capability **ALLOW** ([ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md); default DENY)
2. Parent Learner Access Current Authority

Capability alone does **not** grant access to all learners.  
Tenant membership alone does **not** grant child access.  
School membership alone does **not** grant child access.  
`school.intelligence.read` does **not** grant child access.  
`assessment.assignment.intelligence.read` does **not** grant Parent access.

Unknown / ungranted capability = **DENY**.

### 5. Parent Learner Access Current Authority

Define:

```text
SchoolContextParentLearnerAccessReader
```

Conceptual operation:

```text
list_current_authorized_learners(
  tenant_id,
  adult_principal_id
) → tuple[AuthorizedLearnerAccess, ...]
```

Where:

```text
AuthorizedLearnerAccess:
  learner_principal_id: UUID
```

The authority answers **ONLY**:

> Which learner Principals may this current HUMAN Principal access now in this tenant?

It does **not** encode or expose:

- parent
- guardian
- caregiver
- custody
- household
- family-law category

AIEOS consumes current access truth from **ERP / SIS / Admin School Context**.  
AIEOS does **not** master those relationships.

Do **NOT** overload:

- `SchoolContextClassReader`
- `SchoolContextClassAuthority`
- learner-membership reader
- Principal School Scope Current Authority
- JWT claims
- client headers

### 6. Authorization ≠ presentation

This distinction is binding.

Parent Learner Access Current Authority returns **`learner_principal_id` only**.

It must **NOT** require:

- `presentation_label`
- `display_name`
- `legal_name`
- email
- surname
- username

Missing presentation metadata must **NOT**:

- revoke access
- produce contract-invalid
- produce unavailable
- turn valid access into HTTP 503

Learner display / presentation is a separate optional future School Context projection.

S03 v1 production contract does **not** require learner display names.

`presentation_label` is **not** required in the v1 production contract.

NON_PRODUCTION may later add synthetic presentation labels through **separate composition**, never through the access authority.

### 7. Learner Principal integrity

Every `learner_principal_id` returned by the trusted access provider **must** be validated.

Contract-invalid / fail closed if a returned subject is:

- malformed UUID
- unknown AIEOS Principal
- `PrincipalKind` **WORKLOAD**
- `PrincipalKind` **NULL**
- duplicate ID
- tenant-incompatible subject

**One invalid access-set member invalidates the request.**  
Do **not** silently drop bad IDs.

For a client-guessed selector that is **not** already in a successfully validated authorized set:

- **DO NOT** probe the guessed Principal
- return the concealment response

### 8. Actor lifecycle vs learner data subject

**ADULT ACTOR** must be **ACTIVE HUMAN** to obtain business authority.

**LEARNER DATA SUBJECT** is not the actor in Parent Intelligence.

Child `SUSPENDED` or `DISABLED` status does **NOT** by itself revoke adult Parent Intelligence access.

Current access is governed by:

- current adult→learner access authority
- tenant compatibility
- current learner membership / current school context

If ERP / SIS intends to revoke adult access, the access authority must **stop returning** that learner.

Do **not** interpret `DISABLED` / `SUSPENDED` as custody, transfer, or family-access semantics.

Student OS actor rules remain unchanged.

### 9. Success / failure semantics

Successful current access result with **zero learners**:

```text
SUCCESS
home → HTTP 200
children = []
```

This is **NOT** authority unavailable.

Authority:

- unconfigured
- unavailable
- timeout
- unexpected failure
- malformed contract
- invalid learner subject set

→ **FAIL CLOSED**  
→ HTTP **503** at Parent API boundary

No durable access snapshot.  
Revalidate every GET.  
Historical relationship creates no current access right.

### 10. HTTP concealment

Deterministic Parent API boundary semantics:

| Condition | HTTP |
|-----------|------|
| **A.** Caller cannot access requested tenant / adult security or capability authorization fails | **403** |
| **B.** Caller has valid tenant context, but requested `learner_principal_id` is not in the current authorized set | **404 conceal** |
| **C.** Access authority / source unavailable or contract-invalid | **503** |
| **D.** Successful zero authorized learners | **200** `children = []` |
| **E.** Authorized learner | **200** |

Use **exactly the same concealment class** for:

- guessed same-class learner
- guessed cross-class learner
- unauthorized sibling
- learner in another school
- learner in another tenant
- revoked learner
- formerly authorized learner
- unknown / invented UUID

Do **not** reveal which condition occurred.  
Do **not** probe guessed learner kind / status / tenant before concealment.

### 11. Source of truth

| Concern | Authority remains |
|---------|-------------------|
| Current adult→learner **ACCESS** | External **ERP / SIS / Admin School Context** |
| AIEOS access surface | Consume-only current-authority façade |
| TeachingAssignment | Teaching ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| LearnerAttempt / LearnerSubmission | Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Content / ContentVersion | Content |
| Assessment facts / ClassroomAssessment / LearnerAssessmentEvaluation | Assessment ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md)) |
| Identity | Security / Authorization kernel ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md)) |
| School / roster / learner access | External School Context / ERP / SIS authority |
| Parent Intelligence display | Derived cross-domain read projection — **this ADR**; not a competing SoR |

Do **not** create a Parent business table.

`education` remains educational payload/schema ownership. It does **not** own Parent Intelligence.

### 12. Derived projection inputs

Candidate existing inputs **after** authorized learner set resolution:

- current authorized learner Principal IDs
- current learner Class membership
- current ACTIVE / available TeachingAssignments
- that learner's LearnerAttempt / LearnerSubmission only
- parent-safe Content `title` / `content_type` extract

Never invoke Teacher Assessment Intelligence or Principal School Intelligence as Parent sources.

Projection mode: **DERIVED_ON_REQUEST**.  
Facts: **CURRENT_FACTS_AS_OF_REQUEST**.

### 13. Initial allowed vocabulary

Freeze initial baseline to:

```text
ASSIGNED / AVAILABLE
NOT_STARTED
IN_PROGRESS
SUBMITTED
```

Meaning:

| Status | Meaning |
|--------|---------|
| `NOT_STARTED` | current assignment exists; no learner attempt |
| `IN_PROGRESS` | learner attempt exists and is in progress |
| `SUBMITTED` | learner attempt submitted and LearnerSubmission exists |

Preserve:

```text
Published ≠ Assigned
Assigned ≠ Attempted
Attempted ≠ Submitted
Submitted ≠ Evaluated
Evaluated ≠ Mastered
Assessed ≠ Mastered
item correctness ≠ mastery
submission evidence ≠ learner-model truth
```

### 14. Evaluation

```text
EVALUATION_EXISTENCE = NO
```

for S03 v1.

Do **not** expose through Parent v1:

- evaluated
- graded
- score
- correct / incorrect items
- objective evidence
- mastery
- competency attainment

A later architecture revision may add appropriate learner-authorized assessment information.

**ADR-AIEOS-059 is not reopened by S03 baseline.**

### 15. Minimal external Parent contract

Proposed **conceptual** Parent external DTO:

```text
ParentIntelligenceReadModel
  generated_at
  projection_mode
  time_window
  children

ParentChildCard
  learner_principal_id
  assignments

ParentAssignmentStatus
  assignment_id
  title
  content_type
  available_from
  due_at
  attempt_status
  submitted_at
```

`presentation_label` is **NOT** required in the v1 production contract.

Internal-only composition fields must **not** appear merely because the server possesses them.

Internal-only baseline includes:

- `class_ref`
- `content_id`
- `content_version_id`
- `assignment_lifecycle`
- `attempt_id`
- `submission_id`
- `evaluation_id`
- `teacher_principal_id`
- membership tuples
- raw School Context values
- internal sources arrays

Exact OpenAPI path / `operationId` is **not** implemented by this deposit. Conceptual Parent API boundary is a read-only GET home plus optional learner selector, with the HTTP concealment semantics in §10.

### 16. Strictly forbidden Parent disclosure

Do **not** expose:

- other learner identities
- learner / class rosters
- class counts / distributions
- small-cohort metrics
- raw attempt responses
- submission snapshots
- item correctness
- answer keys
- `teacher_notes`
- `teacher_summary`
- `PRIVATE_EXECUTION_NOTE`
- ClassroomAssessment `class_result_note`
- ClassroomAssessment `class_result_level`
- Teacher Memory
- Improve goal / body
- RemediationOrigin internal snapshots
- teacher principal identifiers
- Principal School Intelligence metrics
- Teacher Assessment Intelligence `learners[]`
- system / model prompts
- internal AI provenance
- mastery %
- competency claims
- learner level
- diagnosis
- risk score
- predicted performance
- ranking
- “behind peers”
- learner-model strength / weakness claims

### 17. Resource bounds

Architecture requires:

- bounded resource consumption
- deterministic ordering
- no silent truncation
- explicit pagination or bounded-query behavior where required
- safe failure when an implementation protection bound is exceeded

Do **NOT** freeze arbitrary `20 children` / `20 assignments` or any other numeric development bound as domain truth.

Exact limits belong to implementation / configuration.

### 18. NON_PRODUCTION showcase rule

This ADR authorizes the architectural **RULE** for a later **NON_PRODUCTION** synthetic Parent Learner Access adapter.

It is **NOT** implemented by this ADR deposit.

Requirements when later implemented:

- same `SchoolContextParentLearnerAccessReader` port
- explicit NON_PRODUCTION selection
- never silently selected in production
- production unconfigured reader fails closed
- synthetic access does not imply ERP integration
- synthetic presentation label, if any, stays separate from authority
- support multi-child / multi-adult / revocation / cross-tenant / malformed-contract tests

### 19. Teacher workload

Binding product objective: **PARENT CLARITY WITHOUT TEACHER OVERLOAD.**

Initial Parent Intelligence derives status from existing governed facts.

It must **NOT** require:

- teacher-written Parent summaries
- new ClassroomAssessment notes
- new Teacher Memory
- per-assignment teacher messages
- teacher approval just to expose assignment lifecycle truth

### 20. Communication / actions

S03 baseline is **READ ONLY**.

Out of scope:

- parent messaging
- teacher messaging
- notifications
- PTM workflows
- acknowledgements
- intervention requests
- action plans
- teacher-approved narrative digests
- Parent mutations

Communication remains a future governed capability / domain.

### 21. AI / Agent

Parent Agent: **DEFERRED**.

No LLM required for baseline.

Freeze invariant:

```text
AUTHORITATIVE FACT  ≠  GENERATED EXPLANATION
```

Any future Parent narrative must:

- remain bounded by authorized facts
- preserve provenance
- not invent learner conclusions
- not become learner SoR truth

No frontend-to-model contract ([ADR-044](ADR-044-ai-platform-behind-stable-services.md)).

### 22. Events / Temporal

Initial Parent Intelligence requires:

```text
NATS: NO
Temporal: NO
```

Do not add event / workflow machinery merely for symmetry.

Current production EVENT publisher PUB remains:

```text
io.eduvijna.aieos.content.>
io.eduvijna.aieos.teaching.>
```

No Parent Intelligence production event authorization.  
No Assessment production event authorization by this ADR.  
ADR-AIEOS-046R1 is not broadened.

### 23. Privacy

Classify Parent Intelligence as:

```text
DIRECT MINOR-DATA DISCLOSURE
```

Required posture:

- server-side authorization
- current learner-access authority
- positive allowlist DTO
- fail closed
- conceal unauthorized learner selectors
- no Teacher / Principal DTO reuse

### 24. Historical access

Current authority governs all reads.

Historical relationship occupancy alone creates **no** continuing right.

If current adult→learner access disappears, subsequent GET must not return that learner.

Do not infer historical ERP enrollment / custody that the current School Context contract cannot prove.

### 25. Ownership (binding)

| Concern | Choice |
|---------|--------|
| Ownership | Cross-domain application / read projection; no new business domain SoR |
| Persistence | Pure derived on-request projection |
| Authorization | Distinct Parent Learner Access Current Authority + `parent.intelligence.read` + ACTIVE HUMAN adult |
| Access result | `learner_principal_id` only; presentation is separate |
| Evaluation | `EVALUATION_EXISTENCE = NO` |
| Events / Temporal / Parent Agent | None in the first baseline |

A dedicated Parent **business** aggregate is **rejected**.  
Family / custody / household mastering is **rejected**.  
Reuse of Teacher or Principal Intelligence DTOs is **rejected**.

---

## Scenarios

| ID | Scenario | Expected behaviour |
|----|----------|--------------------|
| A61-01 | ACTIVE HUMAN with `parent.intelligence.read` and current authorized learners | Derived-on-request snapshot; `generated_at`; children cards for authorized learners only |
| A61-02 | Successful current access with zero learners | HTTP **200**; `children = []`; not unavailable |
| A61-03 | WORKLOAD principal calls Parent OS | FAIL CLOSED / **403** |
| A61-04 | Capability missing / unknown / revoked | DENY / **403** |
| A61-05 | Tenant membership without child access | No child cards; guessed selector **404 conceal** |
| A61-06 | School membership / `school.intelligence.read` without Parent access | No Parent access |
| A61-07 | `assessment.assignment.intelligence.read` without Parent access | No Parent access |
| A61-08 | JWT / header / frontend learner ID asserted | Ignored; not entitlement |
| A61-09 | Access authority unconfigured / unavailable / timeout | FAIL CLOSED / **503** |
| A61-10 | Provider returns malformed UUID / unknown Principal / WORKLOAD / NULL / duplicate / tenant-incompatible ID | Contract-invalid; **503**; do not silently drop |
| A61-11 | Client guesses unauthorized / unknown / revoked / other-tenant learner | **404 conceal**; do not probe guessed Principal |
| A61-12 | Child Principal is SUSPENDED / DISABLED | Does **not** by itself revoke adult access; authority set governs |
| A61-13 | Historical relationship without current access | No current right |
| A61-14 | Missing presentation / display name | Access remains valid; not 503; not contract-invalid |
| A61-15 | GET would ensure evaluations | Forbidden; GET remains a read; `EVALUATION_EXISTENCE = NO` |
| A61-16 | Request for score / mastery / item correctness | Omit / reject; not Parent v1 vocabulary |
| A61-17 | Reuse Teacher `learners[]` or Principal School Intelligence as Parent payload | Forbidden |
| A61-18 | Production NATS / Temporal / Parent Agent proposed solely for this read | Not required; not authorized |
| A61-19 | Production unconfigured access reader | FAIL CLOSED; never silent NON_PRODUCTION adapter |
| A61-20 | Teacher asked to write a Parent summary as a prerequisite | Forbidden; no teacher overload |
| A61-21 | Parent mutation / messaging / acknowledgement | Out of S03 baseline |
| A61-22 | Numeric 20/20 bound treated as domain truth | Forbidden; limits are implementation/configuration |
| A61-23 | Duplicate GET | Same derived snapshot semantics; no mutation; no Idempotency-Key |
| A61-24 | Cross-tenant Parent request | FAIL CLOSED / **403** |

Every listed **authorization / unavailable / privacy / contract-invalid** failure is **fail closed**. Truthful empty `children = []` is allowed only after successful current authority.

---

## Implementation sequence — planning only

**THIS ADR FREEZE/DEPOSIT DOES NOT AUTHORIZE IMPLEMENTATION.**

Even after later Freeze / Approved status: Backend implementation requires separate Chief Architect authorization.

Do **not** execute any slice now.

Expected later slicing only:

| Slice | Purpose | Status |
|-------|---------|--------|
| **I01** | Parent Learner Access Current Authority + authorization substrate | **NOT AUTHORIZED** |
| **I02** | Derived Parent Intelligence API | **NOT AUTHORIZED** |
| **I03** | Parent OS read-only frontend | **NOT AUTHORIZED** |
| **I04** | real-stack AIEOS360 Parent E2E | **NOT AUTHORIZED** |

---

## Consequences

### Positive

- A real Parent step can extend the AIEOS360 vertical.
- No teacher manual-update prerequisite.
- No family / custody SoR introduced.
- Current access remains externally authoritative.
- Privacy surface remains deliberately small.
- Production can later replace a NON_PRODUCTION adapter behind the same port.

### Negative / constraints

- Production Parent access remains blocked until a real School Context / ERP / SIS provider exists.
- No learner presentation name in the baseline production contract.
- No assessment / evaluation disclosure.
- No attendance.
- No fees.
- No timetable.
- No communication.
- No Parent Agent.
- No historical Parent transcript.

### Explicitly not authorized

- Backend / Frontend / Product / Infrastructure change
- Migration / OpenAPI
- Authorization-kernel code
- School Context code
- Parent API code
- Parent UI
- Synthetic adapter implementation
- NATS / Temporal
- Parent Agent
- ERP / SIS integration
- AIEOS360-S03 implementation slices I01–I04
- New Parent business SoR / table
- `PrincipalKind.PARENT` / `GUARDIAN` / `STUDENT` / `LEARNER`
- Reuse of Teacher Assessment Intelligence or Principal School Intelligence
- Evaluation / mastery / score disclosure
- Production deployment

---

## Consistency validation (deposit-time)

| Check | Result |
|-------|--------|
| Parent Intelligence is a derived-on-request projection, not a business SoR | **PASS** |
| Existing Teaching / Learning / Assessment / Content / ERP authority preserved | **PASS** |
| Distinct Parent Learner Access Current Authority; other School Context ports not overloaded | **PASS** |
| JWT / client headers / frontend learner ID are not entitlement | **PASS** |
| `PrincipalKind` remains HUMAN / WORKLOAD only | **PASS** |
| Capability `parent.intelligence.read` plus current access set required | **PASS** |
| Authorization ≠ presentation; access result is `learner_principal_id` only | **PASS** |
| Invalid provider subject set fail-closed; no silent drop | **PASS** |
| Adult ACTIVE HUMAN vs learner data-subject status distinguished | **PASS** |
| Empty authorized set is 200 `children []`; authority failure is 503 | **PASS** |
| Unauthorized learner selector is 404 conceal | **PASS** |
| `EVALUATION_EXISTENCE = NO`; ADR-AIEOS-059 not reopened | **PASS** |
| Allowed vocabulary ASSIGNED/AVAILABLE, NOT_STARTED, IN_PROGRESS, SUBMITTED | **PASS** |
| No Teacher / Principal DTO reuse | **PASS** |
| No NATS / Temporal / Parent Agent in baseline | **PASS** |
| NON_PRODUCTION adapter is a rule only, not implemented here | **PASS** |
| Implementation not authorized; I01–I04 not started | **PASS** |
| ADR status Proposed; not Frozen; not Approved | **PASS** |
