---
id: ADR-AIEOS-060
title: AIEOS Principal / School Intelligence Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: proposed
version: 1.0.0
created: 2026-09-16
last_updated: 2026-09-16
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-060 — AIEOS Principal / School Intelligence Authority

**Status:** Proposed / Freeze Candidate  
**NOT FROZEN**  
**NOT FOUNDER-APPROVED**  
**IMPLEMENTATION NOT AUTHORIZED**

**Date:** 2026-09-16  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md) · [ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md) · [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md) · [ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md) · [ADR-AIEOS-046](ADR-AIEOS-046-aieos-production-event-plane-identity-least-privilege-contract.md) · [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) · [ADR-044](ADR-044-ai-platform-behind-stable-services.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md)

**Catalogue note:** Proposed / Freeze Candidate is **ARCHITECTURE DEPOSIT ONLY**. This ADR proposes the **AIEOS Principal / School Intelligence Authority** for **AIEOS360-S02P1**. Founder / Product Architecture freeze is **not** granted. Chief Architect exact-head review is **pending**. This proposal does **not** authorize Backend implementation, Frontend implementation, Product change, migration, OpenAPI change, NATS change, Temporal change, Infrastructure change, deployment, or production mutation. **ADR-AIEOS-060 Proposed ≠ AIEOS360-S02 implementation authorization.**

**ID family note:** `ADR-AIEOS-060` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 and from platform infrastructure ADR-AIEOS-048 / 048R1 / 048R2.

**Architecture programme:** **AIEOS 360 CLIENT SHOWCASE** / package **AIEOS360-S02**. Architecture proposal package: **AIEOS360-S02P1**. Principal / School Intelligence Architecture Discovery = **ACCEPTED — PASS WITH BINDING ARCHITECTURE CORRECTION**.

This proposal does **not** reopen or rewrite historical ADR bodies: ADR-AIEOS-023R1, ADR-AIEOS-024, ADR-AIEOS-025, ADR-AIEOS-028, ADR-AIEOS-030, ADR-AIEOS-031, ADR-AIEOS-046R1, ADR-AIEOS-053, ADR-AIEOS-054, ADR-AIEOS-055, ADR-AIEOS-056, ADR-AIEOS-058, **ADR-AIEOS-059**.

This proposal does **not** authorize implementation.

---

## Context

Teacher OS through TOS-CX01 and AIEOS360-S01 through I05 now have a real cross-role path:

```text
Prepare → Review → Publish → TeachingAssignment
        → eligible Student
        → LearnerAttempt
        → immutable LearnerSubmission
        → LearnerAssessmentEvaluation (Assessment-owned)
        → Teacher Assessment Intelligence (derived, assignment-scoped)
        → class-level ClassroomAssessment (teacher judgment)
        → teacher-deliberate Improve (remediate_class TeachingWork)
```

AIEOS 360 CLIENT SHOWCASE next vertical is Principal / School Intelligence:

```text
Teacher → Student → Learning Evidence → Assessment Intelligence
        → Teacher Improve → PRINCIPAL / SCHOOL INTELLIGENCE
```

Desired product outcome:

> Principals see trustworthy school teaching/learning health without creating new teacher workload, false mastery claims, learner-PII leakage, or a teacher-surveillance/ranking system.

Governed evidence at this deposition (read-only; not modified by this ADR):

| Surface | Pin |
|---------|-----|
| Architecture `origin/main` base | `cd9cd87d6101990e52e9c8267322aaa6633fced3` |
| Backend `origin/main` | `3d25bb2d7ae3a6a95affdf075a75f20db48a6959` |
| Frontend `origin/main` | `2fe17e349bfcf772377bebd0718e1094936adaae` |
| Product `origin/main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Alembic head | `a360s010004` |
| Authoritative OpenAPI SHA-256 | `7B51CE21725651B8D556B9DD6D264473DF0A2E7CAF30D722E1CC776C651FAFBB` |

**AIEOS360-S01-I05 = COMPLETE / CLOSED** against ADR-AIEOS-059 Frozen / Approved (historical ADR-059 body unchanged). Sequence B1 → B2 → B3 → F1 → E2E is complete in current Backend/Frontend source. Teacher Assessment Intelligence exists as an assignment-scoped derived projection that exposes `learner_principal_id`. ADR-AIEOS-059 §23 forbids exposing learner Assessment Intelligence to Principal or Parent in that ADR.

Current source has **no** Principal OS product, **no** school-scope capability, and **no** school-wide intelligence API. Existing School Context ports answer a **teacher's currently assignable classes** or a **learner's own current memberships**. They do not answer principal school/campus/class scope and cannot enumerate a school roster.

Product Phase 4 mentions “coverage vs mastery narratives.” Frozen architecture states Evaluated ≠ Mastered and submission-scoped objective evidence ≠ learner-model truth. This ADR binds the near-term Principal vocabulary to evidence-flow, not mastery.

Chief Architect discovery disposition: **ACCEPTED — PASS WITH BINDING ARCHITECTURE CORRECTION.** The correction: “school grain” alone is not sufficient privacy protection, because an authorized school/campus/grade scope may itself contain a tiny population. Initial Principal OS therefore defers all learner-sensitive assessment-outcome aggregation. No numeric cohort threshold is invented.

---

## Decision

### 1. Separation invariants (binding)

Preserve ADR-AIEOS-053 / 054 / 055 / 056 / 058 / 059:

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
```

Do **not** move school/class/roster master into AIEOS.  
Do **not** put evaluation or mastery fields into TeachingAssignment, TeachingExecution, or LearnerSubmission.  
Do **not** reuse Teacher Assessment Intelligence DTOs as the Principal representation.

### 2. What School Intelligence is

**Selected:** School Intelligence is a **CROSS-DOMAIN APPLICATION / READ PROJECTION**.

It composes governed read facts from existing authoritative domains. It is **NOT** a new business SoR.

| Concern | Authority remains |
|---------|-------------------|
| Teacher-owned classroom assignment intent | **TeachingAssignment** — Teaching ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| Classroom execution / completed teaching evidence | **TeachingExecution** — Teaching ([ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md)) |
| Improve / remediation work | **TeachingWork** + immutable **TeachingWorkRemediationOrigin** — Teaching ([ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md)) |
| Attempt working state | **LearnerAttempt** — Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Raw immutable learning evidence | **LearnerSubmission** — Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Class-level HUMAN teacher judgment | **ClassroomAssessment** — Assessment ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)) |
| Durable evaluation of one submission | **LearnerAssessmentEvaluation** — Assessment ([ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md)) |
| Artifact / immutable version payload | **Content / ContentVersion** — Content |
| School / campus / class / roster / institutional structure / current school scope | **ERP / SIS / Admin School Context** |
| Current teacher ClassRef assignability | **SchoolContextClassReader / SchoolContextClassAuthority** — Teaching (unchanged; **not** Principal authority) |
| Current learner membership check | **School Context learner-membership façade** — Learning (unchanged; **not** roster enumeration) |
| Principal Intelligence display | **Derived cross-domain read projection** — **this ADR**; not a competing SoR |
| Long-term mastery / misconception / personalization | **Future Learner Intelligence** — **out of this ADR** |

School Intelligence **MUST NOT** duplicate or take ownership of those facts.

`education` remains educational payload/schema ownership. It does **not** own School Intelligence.

### 3. Architecture options evaluated

| Option | Summary | Verdict |
|--------|---------|---------|
| **A** | Pure derived read-time projection over existing SoRs | **Selected for initial architecture** |
| **B** | Derived materialized/read-model snapshots with explicit provenance and rebuild semantics, not a business SoR | **Deferred evolution** — may be separately authorized later if rebuildable, provenance-retaining, explicitly not a competing SoR, and freshness/watermark semantics are frozen |
| **C** | New durable School Intelligence aggregate / business SoR | **Rejected** — competing truth for Teaching / Learning / Assessment / Content / ERP |
| **D** | Event-driven materialized school read model | **Rejected for first architecture** — ADR-AIEOS-046R1 does not authorize Assessment or School Intelligence production PUB; Learning NATS remains HOLD; Temporal is not required for a read |

**Selected initial persistence:** **PURE DERIVED READ-TIME PROJECTION.**

No School Intelligence business table.

A future materialized read model **MAY** be separately authorized only if:

- rebuildable from authoritative SoRs,
- provenance retained,
- explicitly not a competing SoR,
- freshness/watermark semantics are frozen.

### 4. School Scope Current Authority

Freeze as proposed architecture a **DISTINCT** **School Scope Current Authority**.

Do **NOT** overload:

- `SchoolContextClassReader`
- `SchoolContextClassAuthority`
- learner-membership reader
- JWT claims
- client headers

JWT / request identity still proves `principal_id` only ([ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md)). School authority, role, class scope, capabilities, and permissions **MUST NOT** be trusted from client headers or JWT claims as substitute authority.

Required semantics:

1. Trusted request identity establishes `principal_id` only.
2. Current tenant membership is server-side.
3. Exact capability is server-side ([ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md); default DENY).
4. Effective actor must be current ACTIVE **HUMAN**.
5. **WORKLOAD** must not silently become a Principal OS user.
6. Current school / campus / grade / class scope comes from School Context / ERP.
7. Scope enumeration must be authoritative.
8. Authority unavailable = fail closed.
9. Authority loss = access loss.
10. Historical role occupancy ≠ perpetual access.
11. Aggregation may only read facts whose ClassRefs intersect current authorized scope.

**Proposed exact capability:** `school.intelligence.read`

Unknown / ungranted capability = **DENY**.

Do not place role, school, campus, ClassRef list, or entitlement into trusted client claims as authority.

Tenant RLS remains tenant isolation. It is **not** school/campus/class isolation. Application composition **must** filter to current authorized ClassRefs **before** aggregation.

### 5. Principal HUMAN requirement

Principal OS commands and reads require **all** of:

```text
same tenant
  +
current ACTIVE HUMAN principal
  +
exact capability school.intelligence.read ALLOW
  +
current School Scope Current Authority
```

Direct Principal OS baseline: `effective_actor_id` = `principal_id`.

`teacher_principal_id` / `learner_principal_id` field names are identity correlation IDs. They are **not** Principal OS product authority.

No `PrincipalKind.PRINCIPAL` is introduced. Principal OS users remain `HUMAN` principals with current school-scope authority and the exact capability.

### 6. Learner-PII baseline

Initial Principal Intelligence contains **ZERO learner identities**.

**FORBID:**

- `learner_principal_id`
- learner names
- learner lists
- raw `response_snapshot`
- answer text
- Teacher Assessment Intelligence `learners[]`
- raw answer keys
- learner drill-down

No Principal API may reuse the Teacher Assessment Intelligence representation.

Raw learner responses **MUST NOT** become Principal-visible. Historical source facts do not introduce learner identity merely because they are historical.

### 7. Teacher anti-surveillance baseline

Principal OS **MUST NOT** become:

- teacher leaderboard
- teacher performance score
- automated teacher evaluation
- teacher ranking
- best/worst teacher display
- disciplinary recommendation system

Initial projection **MUST NOT** expose:

- `PRIVATE_EXECUTION_NOTE`
- ClassroomAssessment note text
- teacher private Memory
- free-text teaching observations
- teacher comparison rankings

Primary grain:

```text
school summary
  +
authorized class activity / evidence-flow cards
```

Do **not** make `teacher_principal_id` a presentation grain.

Class display labels may residual-identify a teacher in a small school. That residual risk is acknowledged. It does **not** authorize ranking, scoring, or comparison UX.

ClassroomAssessment result-level **comparison class-by-class is deferred in v1** because a class commonly identifies its teacher and creates surveillance/ranking pressure.

### 8. Small-cohort / disclosure baseline

No governed minimum-cohort / suppression policy exists.

**Do not invent `N >= k`.**

“School grain” alone is **not** sufficient privacy protection, because an authorized school / campus / grade scope may itself contain a tiny population.

Therefore the **INITIAL** ADR-060 baseline **MUST DEFER** all learner-sensitive assessment-outcome aggregation that could re-identify a learner.

**Deferred from initial Principal OS:**

- objective evidence outcome distributions
- `INSUFFICIENT_EVIDENCE` learner-evaluation counts as an academic outcome
- frequently missed question intelligence
- per-question correctness distributions
- MC/TF correctness distributions
- learner assessment outcome heatmaps
- class-vs-class learner outcome comparisons
- class-level objective evidence
- any learner-derived mastery-like rollup
- class-by-class ClassroomAssessment result comparison

A future separately governed disclosure / suppression decision may add such aggregates. That future decision is **not** this ADR and is **not** authorized here.

### 9. Allowed first Principal Intelligence

The first truthful Principal OS surface **MAY** include:

**A.** Authoritative in-scope class count — **ONLY** if School Scope Current Authority enumerates it.

**B.** Classes with AIEOS assignment activity — **count**, not an unsupported percentage.

**C.** TeachingAssignment count — with explicit lifecycle / time-window semantics.

**D.** LearnerSubmission count for authorized in-scope assignments. **No learner IDs.**

**E.** Current-policy `LearnerAssessmentEvaluation` count for in-scope submitted evidence. **No evaluation item / outcome disclosure.**

**F.** Evaluation coverage among submitted (see §10). Labelled **“among submitted”**, never submission rate or learner coverage.

**G.** Submitted-but-not-current-policy-evaluated count.

**H.** Count of classes / assignments with a **RECORDED** ClassroomAssessment — without note text and without class-result ranking / comparison.

**I.** **COMPLETED** TeachingExecution count — without observation / private-note bodies.

**J.** Improve / remediation activity count using durable `TeachingWorkRemediationOrigin` class provenance.

For remediation class attribution use:

```text
TeachingWorkRemediationOrigin.source_class_ref
```

Do **NOT** infer class identity from TeachingWork free-text `class_label` / `subject` / `topic`.

Every displayed metric must have an exact definition, numerator, denominator (or explicit count-not-rate), time window, included / excluded population, source SoR, freshness semantics, and authority boundary.

### 10. Denominator law

Every rate requires an authoritative denominator. No inferred denominators. No “0%” when the denominator is unknown.

**Allowed:**

```text
evaluation_coverage_among_submitted =
  count(current-policy evaluations for authorized submitted evidence)
  /
  count(authorized LearnerSubmissions)
```

This **MUST** be labelled “among submitted”.

**Do NOT define** until authoritative roster enumeration exists:

```text
submission_rate = submitted / eligible roster
```

**Do NOT expose** until authoritative eligible learner enumeration exists:

```text
not-submitted learner count
```

Class coverage **percentage** may exist only if School Scope Current Authority authoritatively enumerates in-scope classes. Otherwise expose **counts**.

### 11. Mastery / Learner Intelligence boundary

**Binding:**

```text
Evaluated                         ≠  Mastered
Assessed                          ≠  Mastered
Deterministic item outcome        ≠  mastery
Submission-scoped objective evidence ≠ learner-model truth
Assessment signal                 ≠  Improve acceptance
```

Principal OS **MUST NOT** display:

- mastery %
- competency attained
- school mastery
- student ability score
- predicted exam outcome
- school performance score

Product roadmap “coverage vs mastery narratives” is **future vision language**. It is **not** current Principal OS authority.

Initial Principal OS uses:

- teaching activity
- assignment activity
- submission evidence
- evaluation coverage among submitted
- recorded class-assessment activity
- completed teaching evidence
- Improve / remediation activity
- evidence-flow completeness

Opening durable Learner Intelligence / mastery architecture is **NOT** required for AIEOS360-S02 v1.

### 12. Initial read model

Initial query is:

```text
read-only
derived-on-request
side-effect free
deterministic
```

GET **MUST NOT**:

- evaluate submissions
- ensure evaluations
- record ClassroomAssessment
- create Improve work
- generate Content
- publish Content
- create TeachingAssignment
- start / complete TeachingExecution
- emit a notification
- emit an event
- start Temporal
- write a School Intelligence snapshot

Missing facts = truthful zero / empty evidence **only when** authority and source read succeeded.

Authority unavailable = fail closed / unavailable.

Source-domain failure **MUST NOT** be represented as zero activity.

Include `generated_at` and sufficient source / provenance / freshness metadata to explain the snapshot.

Optional time windows apply to source event times (`assigned_at`, `submitted_at`, `evaluated_at`, `recorded_at`, `completed_at`). Default = current facts at request time. “What the principal saw last Tuesday” as a reconstructed dashboard is Option B later, not this baseline.

Current-policy evaluations only for current evaluation-count / coverage signals. Obsolete-policy rows remain historical Assessment evidence and do not become current Principal projection.

Pagination and deterministic ordering (authorized `class_ref`, then stable id) are required if the in-scope class list can exceed a bounded page. First showcase may use a bounded list, but ordering remains deterministic.

### 13. API architecture (contract intent only)

Proposed initial persona surface:

```text
GET /api/v1/principal-os/school-intelligence
```

This is architecture contract intent only. **No OpenAPI edit is authorized by this proposal.**

It **MUST**:

- require exact current Principal / School authority
- require HUMAN actor
- use `school.intelligence.read`
- be side-effect free
- return no learner identities
- not reuse Assessment Teacher Intelligence DTOs
- not expose raw note / response bodies

RFC 9457 error semantics remain the platform standard ([ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md)).

No Idempotency-Key on GET.

### 14. Frontend architecture (design only)

Principal OS is a distinct persona experience.

Proposed first journey:

```text
/principal-os
  → School Health / Intelligence
    → school summary
    → authorized class activity / evidence-flow cards
```

No Teacher OS role-switch shortcut as authority.  
No Student OS reuse as authority.  
No learner list.  
No teacher leaderboard.  
No outcome heatmap in v1.

Principal frontend remains behind the normal AIEOS API boundary ([ADR-044](ADR-044-ai-platform-behind-stable-services.md)).

This proposal does **not** authorize Frontend implementation.

### 15. AI / narrative baseline

Initial Principal Intelligence: **DETERMINISTIC STRUCTURED FACTS ONLY.**

No AI-generated Principal narrative in the first implementation baseline.  
No Assessment Insight Agent.  
No autonomous recommendations.  
No generated disciplinary / adoption judgments.

Later template or model narrative requires separate authorization.

If later added:

- deterministic governed facts remain authority
- AI text is interpretation only
- no learner PII prompt leakage
- no teacher ranking
- no mutation from generated text

### 16. Events / Temporal

No NATS dependency for initial Principal Intelligence.

Do **NOT** broaden [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) publisher scope.

Current production EVENT publisher PUB remains:

```text
io.eduvijna.aieos.content.>
io.eduvijna.aieos.teaching.>
```

No Assessment production event authorization.  
No School Intelligence production event authorization.  
No Temporal workflow.

School Intelligence read composition is not workflow truth.

### 17. Historical access

Current authority governs all reads.

A currently authorized Principal may read permitted historical **aggregate** facts for ClassRefs **currently** within the actor's authorized scope.

Historical role occupancy alone creates no continuing right.

If current school / class authority disappears, fail closed.

Do not infer historical ERP enrollment / authority that the current School Context contract cannot prove.

No learner identity is introduced merely because the source fact is historical.

VOIDED ClassroomAssessments remain history, not current recorded-assessment counts.  
Obsolete-policy evaluations remain Assessment history, not current Principal coverage.

### 18. Future boundaries

Explicitly **out of** the initial ADR-060 implementation baseline:

- Learner Intelligence / mastery
- Parent Intelligence
- Parent learner detail
- Admin / ERP mutation
- attendance writes
- gradebook writes
- timetable writes
- school configuration writes
- notifications
- production event expansion
- Temporal
- cross-school benchmarking
- teacher performance evaluation
- learner prediction
- AI school narrative
- small-cohort learner-outcome aggregation

Preserve future direction **without merging authorization models**:

```text
Principal / School Intelligence
  → Parent Intelligence
  → Admin / ERP Context
```

Parent Intelligence will require learner-authorized projections, not Principal aggregates.  
Admin / ERP remains institutional master for school / class / roster. Principal reads School Context; it does not write ERP.

### 19. Ownership recommendation (binding for this proposal)

| Concern | Choice |
|---------|--------|
| Ownership | Cross-domain application / read projection; no new business domain SoR |
| Persistence | Pure derived read-time projection |
| Authorization | Distinct School Scope Current Authority + `school.intelligence.read` + HUMAN |
| PII | Zero learner identities |
| Teacher grain | Class activity cards; no teacher ranking |
| Events / Temporal / AI | None in the first baseline |

Assessment-owned school projection is **rejected** as the long-term owner because school health also requires TeachingAssignment, TeachingExecution, Improve origin, and School Context. Education-domain ownership is **rejected**. A dedicated School Intelligence **business** aggregate is **rejected**. A dedicated **read-model** bounded context remains a later Option B evolution, not this baseline.

---

## Scenarios

| ID | Scenario | Expected behaviour |
|----|----------|--------------------|
| A60-01 | HUMAN principal with current school-scope and `school.intelligence.read` | Derived-on-read snapshot; `generated_at`; no learner identities |
| A60-02 | WORKLOAD principal calls Principal OS | FAIL CLOSED |
| A60-03 | Capability missing / unknown / revoked | DENY |
| A60-04 | School Scope Current Authority unavailable | FAIL CLOSED / unavailable — not empty-success zeros |
| A60-05 | Principal loses class/school authority | Subsequent GET FAIL CLOSED for that scope |
| A60-06 | Historical role occupancy without current scope | No access |
| A60-07 | JWT / header asserts school-admin / class list | Ignored; not authority |
| A60-08 | Client requests Teacher Assessment Intelligence DTO as Principal payload | Forbidden; distinct representation |
| A60-09 | GET would be convenient to ensure evaluations | Forbidden; GET remains a read |
| A60-10 | Source Assessment read fails | Must not display “0 evaluations” as no activity |
| A60-11 | No TeachingAssignments in authorized scope | Truthful zero **after** successful source read |
| A60-12 | School Scope cannot enumerate classes | No class-coverage **percentage**; counts only |
| A60-13 | No roster enumeration | No submission rate; no not-submitted count |
| A60-14 | Request for mastery % / school performance score | Reject / omit; not Principal vocabulary |
| A60-15 | Request for teacher ranking | Reject |
| A60-16 | Request for learner list / drill-down | Reject |
| A60-17 | Request for objective / question outcome heatmap | Deferred; not v1 |
| A60-18 | Class-by-class ClassroomAssessment result comparison | Deferred in v1 |
| A60-19 | Improve count uses TeachingWork.class_label | Forbidden; use `TeachingWorkRemediationOrigin.source_class_ref` |
| A60-20 | PRIVATE_EXECUTION_NOTE or assessment note requested | Forbidden |
| A60-21 | Cross-tenant Principal request | FAIL CLOSED |
| A60-22 | Tiny authorized scope (one class, one submission) | Still no learner-sensitive outcome aggregates; counts/evidence-flow only |
| A60-23 | Duplicate GET | Same derived snapshot semantics; no mutation; no Idempotency-Key |
| A60-24 | Production NATS / Temporal proposed solely for this read | Not required; not authorized by this ADR |

Every listed **authorization / unavailable / privacy** failure is **fail closed**. Truthful zeros are allowed only after successful current authority and successful source-domain reads.

---

## Implementation sequence — planning only

This architecture proposal does **not** itself authorize implementation. **ADR-AIEOS-060 Proposed ≠ AIEOS360-S02 implementation authorization.** After any future freeze, implementation remains **NOT AUTHORIZED** until a separate Chief Architect implementation authorization. Do **not** assign permanent implementation slice IDs in this proposal. Do **not** bundle architecture freeze and Principal OS coding into one PR.

Descriptive sequence (not authorized):

| Step | Purpose | Status |
|------|---------|--------|
| Architecture freeze of this ADR | Founder / Product Architecture freeze after exact-head review | **NOT FROZEN** |
| School Scope Current Authority substrate | Distinct fail-closed port; NON_PRODUCTION adapter is not ERP master | **NOT AUTHORIZED** |
| Backend derived-on-read query + GET | Cross-domain projection; no new business SoR; no learner identities | **NOT AUTHORIZED** |
| Principal OS frontend read journey | Distinct `/principal-os` shell; class evidence-flow cards | **NOT AUTHORIZED** |
| Real cross-role E2E | Teacher assign → Student submit → evaluate → Improve → Principal aggregates on the same facts | **NOT AUTHORIZED** |
| Architecture / programme closeout | Orientation sync after separately authorized implementation | **NOT AUTHORIZED** |

---

## Consequences

### Positive

- AIEOS 360 can show principals real teaching / assessment **evidence-flow** without claiming mastery or opening Learner Intelligence.
- Existing SoRs remain authoritative; School Intelligence cannot silently become a competing master.
- Principal access is current server-side school-scope authority, not JWT role theatre.
- Learner PII and teacher-surveillance ranking are excluded from the first surface by architecture, not by UI hiding.

### Negative / constraints

- First Principal OS cannot show syllabus-coverage %, mastery, not-submitted rates, class-result comparisons, or objective heatmaps.
- School Context / ERP must supply a distinct school-scope port before class-coverage **percentages** can exist.
- Query cost of derived-on-read is accepted for first showcase; materialized snapshots require a later ADR.
- Production Assessment / School Intelligence events remain unauthorized.

### Explicitly not authorized

- Backend / Frontend / Product / Infrastructure change
- Migration / OpenAPI
- NATS provisioning / production Assessment or School Intelligence EVENT PUB
- Temporal
- AIEOS360-S02 implementation
- New School Intelligence business SoR / table
- Overloading teacher ClassRef or learner-membership ports as Principal authority
- Reuse of Teacher Assessment Intelligence `learners[]`
- Learner identities / drill-down
- Teacher ranking / performance score
- Invented numeric small-cohort threshold
- Mastery / Learner Intelligence
- Parent Intelligence
- Admin / ERP mutation
- Production deployment

---

## Consistency validation (proposal-time)

| Check | Result |
|-------|--------|
| School Intelligence is a derived projection, not a business SoR | **PASS** |
| Existing Teaching / Learning / Assessment / Content / ERP authority preserved | **PASS** |
| Distinct School Scope Current Authority; teacher ClassRef port not overloaded | **PASS** |
| JWT / client headers are not school authority | **PASS** |
| HUMAN required; WORKLOAD fail closed | **PASS** |
| Zero learner identity in initial Principal projection | **PASS** |
| Teacher ranking / surveillance prohibited | **PASS** |
| Small-cohort: no invented N; learner-sensitive outcomes deferred | **PASS** |
| Denominator law: among-submitted coverage allowed; roster rates forbidden | **PASS** |
| Mastery vocabulary rejected for Principal OS v1 | **PASS** |
| GET side-effect free | **PASS** |
| ADR-AIEOS-046R1 not broadened | **PASS** |
| ADR-AIEOS-059 body not rewritten | **PASS** |
| Implementation not authorized | **PASS** |
| Status is Proposed / Freeze Candidate | **PASS** — **NOT FROZEN**; **NOT FOUNDER-APPROVED** |

No exception invented where a conflict would exist.
