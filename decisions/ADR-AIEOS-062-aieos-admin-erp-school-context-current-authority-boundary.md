---
id: ADR-AIEOS-062
title: AIEOS Admin / ERP School Context Current-Authority Boundary
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: proposed
version: 1.0.0
created: 2026-09-17
last_updated: 2026-09-17
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-062 — AIEOS Admin / ERP School Context Current-Authority Boundary

**Status:** Proposed  
**Founder / Product Architecture freeze:** NOT GRANTED  
**IMPLEMENTATION NOT AUTHORIZED**

**Date:** 2026-09-17  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md) · [ADR-AIEOS-046R1](ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) · [ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) · [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)

**Catalogue note:** Proposed is **ARCHITECTURE DESIGN DEPOSIT ONLY**. This ADR proposes the **AIEOS Admin / ERP School Context Current-Authority Boundary** for **AIEOS360-S04P2**. It is **not** Frozen / Approved. Proposed ≠ Frozen ≠ Approved ≠ implementation authorization ≠ Backend authorization ≠ Frontend authorization ≠ Product authorization ≠ Infrastructure authorization ≠ migration authorization ≠ OpenAPI authorization ≠ School Context code authorization ≠ Admin OS authorization ≠ production ERP/SIS integration authorization ≠ NATS authorization ≠ Temporal authorization ≠ deployment authorization. **ADR-AIEOS-062 Proposed ≠ AIEOS360-S04 implementation authorization.** Do **not** start S04-I01.

**ID family note:** `ADR-AIEOS-062` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 and from platform infrastructure ADR-AIEOS-048 / 048R1 / 048R2.

**Architecture programme:** **AIEOS 360 CLIENT SHOWCASE** / package **AIEOS360-S04**. Architecture proposal package: **AIEOS360-S04P2**. Lineage: **AIEOS360-S04P1** discovery = **ACCEPTED / PASS**.

Does **not** reopen or rewrite historical ADR bodies: ADR-AIEOS-023R1, ADR-AIEOS-030, ADR-AIEOS-031, ADR-AIEOS-053, ADR-AIEOS-054, ADR-AIEOS-055, ADR-AIEOS-056, ADR-AIEOS-058, ADR-AIEOS-059, ADR-AIEOS-060, ADR-AIEOS-061.

---

## Context

AIEOS360-S03 closed Parent Intelligence as a development slice. [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) remains **Frozen / Approved**. **AIEOS360-S03 = DEVELOPMENT SLICE COMPLETE / CLOSED.** **Development Slice Complete = YES. Production Ready = NO.**

The shared AIEOS360 vertical is:

```text
Teacher → Publish / Assign → Student → Attempt / Save / Submit
        → Learning Evidence → Assessment Intelligence
        → Teacher Improve → Principal / School Intelligence
        → Parent Intelligence → Admin / ERP Context
```

Teacher, Student, Principal, and Parent journeys already exist as thin real development slices. Each already consumes **external School Context current authority** through a distinct domain-facing port. None of those ports is the ERP/SIS master.

**AIEOS360-S04P1 discovery found:**

- Frozen ADRs already assign class / roster / enrollment / school scope / adult→learner access mastery to **Admin / ERP / SIS School Context**.
- AIEOS already owns Tenant / Principal / Membership / Capability and the Teaching / Learning / Assessment / Content business SoRs.
- Four distinct School Context ports already exist. Production composes Unconfigured / omitted readers and **fails closed**.
- NON_PRODUCTION development adapters exist, but they are **four disconnected synthetic maps**, not one school.
- No production ERP/SIS adapter exists.
- No AIEOS School / Class / Roster / Enrollment / Family table claims those masters.
- No Admin OS, Admin UI, `PrincipalKind.ADMIN`, or `admin.*` capability exists.
- The missing AIEOS360 client value is **coherence and observability of externally sourced current facts**, not a new AIEOS school database.

Governed evidence at this deposition (read-only; not modified by this ADR):

| Surface | Pin |
|---------|-----|
| Architecture `origin/main` base | `2e44b2d3d51e262393526e42e443f5648f0a94d1` |
| Backend `origin/main` | `138f37bfa7a44c33b206c6b78118154bbb9bc8eb` |
| Frontend `origin/main` | `20a06f048510a2519e0487d12ea7c16f59e7fd7c` |
| Product `origin/main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Alembic head | `a360s010004` |
| Authoritative OpenAPI SHA-256 | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` |

**AIEOS360-S03 remains DEVELOPMENT SLICE COMPLETE / CLOSED.** This deposit does not reopen S03.

---

## Decision

### 1. Primary ownership (binding)

**Admin / ERP / SIS School Context remains the authoritative BUSINESS MASTER** for current school-context facts such as:

- Class identity
- learner enrollment / Class membership
- teacher↔Class authority
- Principal↔school / Class scope
- adult↔learner current access
- external family / guardian / custody relationships where applicable

**AIEOS MUST NOT become a competing master for those concerns.**

AIEOS continues to own its existing business SoRs:

| Concern | Authority remains |
|---------|-------------------|
| Tenant / Principal / Membership / Capability | AIEOS Security ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md)) |
| Content / ContentVersion | AIEOS Content |
| TeachingAssignment | AIEOS Teaching ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| TeachingExecution | AIEOS Teaching ([ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md)) |
| LearnerAttempt / AttemptResponseItems / LearnerSubmission | AIEOS Learning ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| LearnerAssessmentEvaluation | AIEOS Assessment ([ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md)) |
| ClassroomAssessment | AIEOS Assessment ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)) |
| TeachingWork / RemediationOrigin | AIEOS Teaching ([ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md)) |
| School Intelligence display | Derived read projection ([ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md)); not a school master |
| Parent Intelligence display | Derived read projection ([ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)); not a family master |

External School Context facts **authorize or scope** those AIEOS operations. They do **not** absorb their ownership.

AIEOS may store opaque `class_ref` values and AIEOS `PrincipalId` references on its own aggregates. That is correlation, not Class / roster / enrollment mastery.

### 2. What AIEOS360-S04 “Admin / ERP Context” is

**Selected definition:**

> AIEOS360-S04 “Admin / ERP Context” is **the external current-authority boundary completing the AIEOS360 vertical**.

It is **NOT**:

- a full ERP
- a full SIS
- an Admin OS
- a school-management database
- an AIEOS school master
- a roster SoR
- a family / custody SoR
- an identity provider
- a production ERP connector

**Architecture objective:**

one coherent school-context fact universe  
projected through the existing domain-specific School Context authority ports  
so that the existing Teacher, Student, Principal, and Parent journeys all observe the same school context.

### 3. Separation invariants (binding)

Preserve ADR-AIEOS-053 / 054 / 055 / 056 / 058 / 059 / 060 / 061:

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
School Intelligence projection    ≠  a new business SoR
Parent Intelligence projection    ≠  a new business SoR
School Context current-authority façade ≠ ERP / SIS / Admin master
Frontend observation              ≠  business authority
Cached / stale UI state           ≠  business authority
Provider implementation           ≠  domain contract
NON_PRODUCTION current-fact fixture ≠ Admin domain command
Authorization                     ≠  Presentation
```

Do **not** move Class / roster / enrollment / family / custody master into AIEOS.  
Do **not** collapse the four School Context ports into one application contract.  
Do **not** treat JWT / IdP / frontend role labels as school authority.

### 4. Four distinct ports (binding)

The following contracts remain **separate domain-facing ports**. This ADR does **not** create a giant `SchoolContextService` application contract.

| Port | Owning domain | Question answered | Existing authority |
|------|---------------|-------------------|--------------------|
| **A. Teaching School Context Class authority** | Teaching | Which ClassRefs may this teacher currently assign / teach / assess? | `SchoolContextClassReader` / `SchoolContextClassAuthority` ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md); Assessment bootstrap reuse per [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)) |
| **B. Learning learner-membership authority** | Learning | Is this learner currently a member of this ClassRef? | `SchoolContextLearnerMembershipReader` / `SchoolContextLearnerMembershipAuthority` ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| **C. Principal School Scope authority** | School Intelligence | Which ClassRefs are currently in this HUMAN Principal's authorized school scope? | `SchoolContextPrincipalScopeReader` / `CurrentPrincipalSchoolScopeService` ([ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md)) |
| **D. Parent Learner Access authority** | Parent Intelligence | Which learner Principals may this adult currently access? | `SchoolContextParentLearnerAccessReader` / `CurrentParentLearnerAccessService` ([ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)) |

Do **not** overload:

- teacher assignability as learner membership
- learner membership as Principal scope
- Principal scope as Parent access
- JWT claims / client headers / frontend cache as any of the above

**Provider implementation consolidation ≠ contract consolidation.**

A single provider implementation **MAY** implement or project the four interfaces from one coherent source of facts. The four questions remain four contracts.

ClassroomAssessment continues to consume Teaching ClassRef current authority as its Bootstrap assessable-class gate ([ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)). This ADR does **not** freeze a fifth “currently assessable class” port. A later dedicated Assessment class-authority remains possible without changing this ownership model.

### 5. Coherent NON_PRODUCTION School Context current-fact provider

The intended S04 development / showcase realization is:

**ONE COHERENT NON_PRODUCTION SCHOOL CONTEXT CURRENT-FACT PROVIDER**

Characteristics:

- NON_PRODUCTION only
- deterministic
- explicit tenant boundary
- one coherent school / class / learner / teacher / adult fact universe
- implements / projects the existing four reader contracts
- replaceable
- no production runtime import
- no network dependency required for the showcase
- no durable School / Class / Roster / Enrollment / Family tables
- **not** an ERP / SIS master
- **not** a production adapter

Do **not** call this provider itself “the ERP”.

It is a **development surrogate** for the external-authority contract.

Production remains:

```text
unconfigured / omitted / fail closed
```

until a separate production ERP / SIS provider is explicitly designed and authorized.

Unavailable / unconfigured **MUST NOT** become empty implicit ALLOW.

### 6. Coherent showcase fact model

Minimum conceptual current-fact relationships for the showcase:

```text
Tenant
  HUMAN Teacher Principal
  HUMAN Learner Principal(s)
  HUMAN Principal / school-leader Principal
  HUMAN Adult / Parent Principal
  ClassRef (opaque)
  Teacher Principal  → currently assignable ClassRef(s)
  Learner Principal  → current ClassRef membership
  Principal Principal → currently authorized ClassRef scope
  Adult Principal    → currently authorized Learner Principal(s)
```

All must describe **one coherent school story**. The same ClassRef that a teacher may assign is the ClassRef a member learner may attempt, that a Principal may include in school scope, and whose learner a currently authorized adult may see.

Do **NOT** introduce as AIEOS aggregates:

- School
- Campus
- AcademicYear
- Class
- Enrollment
- Roster
- Family

unless a future ADR separately changes ownership.

`class_ref` remains opaque School Context identity.

### 7. Current-fact mutation semantics

For S04 demonstration / testing, the NON_PRODUCTION provider **MAY** support controlled mutation of its current facts so revocation / re-scope behavior can be demonstrated.

Examples:

- add / remove learner membership
- add / remove teacher ClassRef authority
- change Principal ClassRef scope
- grant / revoke adult→learner access

**Binding distinction:**

```text
THIS IS TEST / DEVELOPMENT PROVIDER CONTROL.
```

It is **NOT**:

- an AIEOS school business command
- Admin domain ownership
- an ERP mutation API
- a SIS write API
- a production admin capability
- a new business SoR

Prefer direct fixture / provider control through test / development composition.

Do **NOT** require a public HTTP Admin API.  
Do **NOT** introduce a production endpoint merely to drive E2E.

Any later user-facing Admin control surface requires **separate** product / architecture authorization.

### 8. Admin identity

Preserve:

```text
PrincipalKind = HUMAN | WORKLOAD
```

Do **NOT** add `PrincipalKind.ADMIN`.

A product-facing administrator, if ever introduced, is an **ACTIVE HUMAN** AIEOS Principal subject to:

- ACTIVE Principal
- ACTIVE Tenant
- ACTIVE Membership
- exact capability
- domain-specific current authority where required

External ERP role, IdP group, “admin” claim, tenant claim, or scope **MUST NOT** automatically become AIEOS business authority ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md) · [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md)).

No new `admin.*` capability is required merely to consume School Context current-authority facts. Existing domain capabilities (`school.intelligence.read`, `parent.intelligence.read`, Teaching / Assessment / Content catalogs) remain sufficient for the consuming journeys.

### 9. External identifier correlation

AIEOS `PrincipalId` remains the AIEOS identity.

External ERP / SIS person IDs **MUST NOT** become competing authentication identities.

Opaque external correlation metadata **MAY** exist where justified.

Example: `school_learner_ref`

Rules:

- optional
- opaque
- tenant-scoped
- correlation only
- not authentication proof
- not authorization proof
- not a replacement `PrincipalId`

Duplicate ClassRef, duplicate learner Principal, blank required identity, cross-tenant data, or malformed correlation **MUST fail closed**. Do not silently drop invalid members from an otherwise successful set where the owning port already requires fail-closed contract validation ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)).

### 10. Freshness / revocation (current authority)

Preserve **CURRENT** authority semantics.

Do **NOT** claim instantaneous cross-system revocation.  
Do **NOT** invent distributed 2PC / XA.  
Do **NOT** claim atomic ERP↔AIEOS revocation ordering.

| Event | Subsequent current-authority behavior |
|-------|----------------------------------------|
| New learner membership | Visible on subsequent current membership observation |
| Learner removed | Subsequent membership-gated current access fails closed; already-submitted immutable evidence remains |
| Teacher removed from ClassRef | Subsequent ClassRef authority check denies governed Teacher / Assessment ClassRef operations |
| Principal scope removed | Subsequent Principal Intelligence request uses the reduced ClassRef set |
| Adult→learner access revoked | Subsequent Parent request no longer authorizes that learner; selected unauthorized learner remains concealed according to [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) |
| Tenant suspended | AIEOS security authority fails closed independently of School Context |
| Provider unavailable / unconfigured / malformed | Unavailable / fail closed; **MUST NOT** become empty implicit ALLOW |

Frontend GET observation, cached class lists, and JWT claims remain **not** durable authorization.

### 11. Privacy / data minimization

Keep existing narrow contracts. Baseline data remains approximately:

| Port | Minimum fields |
|------|----------------|
| Teacher Class authority | `class_ref`, `display_label` |
| Learner membership | `class_ref`, optional `school_learner_ref` |
| Principal scope | `class_ref`, `display_label` |
| Parent access | `learner_principal_id` |

Do **NOT** widen S04 into:

- SIS demographics
- attendance
- fees / finance
- HR / payroll
- custody categories
- addresses
- medical data
- learner assessment outcomes
- mastery
- staff records

Cross-tenant malformed provider data **MUST fail closed**.

### 12. Integration direction

Architectural direction:

```text
AIEOS domain
  → application School Context port
  → replaceable School Context provider
  → external Admin / ERP / SIS current authority
```

Recommended production protocol category:

**synchronous current-authority query through a provider adapter**

This ADR remains **vendor-neutral**. It does **not** select a specific ERP / SIS vendor.

Do **NOT** directly read vendor database tables from AIEOS.  
NATS is **NOT** required.  
Temporal is **NOT** required.  
Batch / import is **NOT** the S04 baseline.  
A durable synchronized replica is **NOT** the S04 baseline.  
Production event publication is **NOT** authorized.

### 13. Admin UI

Admin UI is **NOT REQUIRED** for the S04 architecture baseline.

The authority chain can be demonstrated through effects on the existing:

- Teacher OS
- Student OS
- Principal OS
- Parent OS

A decorative Admin page that does not participate in authority is explicitly **insufficient**.

Any future Admin UI requires a separately governed product decision.

### 14. Options evaluated

| Option | Summary | Verdict |
|--------|---------|---------|
| **A** | External Master + AIEOS Current-Authority Adapter | **PROPOSED DIRECTION** |
| **B** | AIEOS durable Admin School Context master | **REJECTED** — conflicts with existing frozen ownership and creates competing School / Class / Roster / Enrollment SoRs |
| **C** | Governed synchronized replica | **DEFERRED** — introduces freshness, provenance, reconciliation, revocation-lag, and second-master risks unnecessary for the thin AIEOS360 showcase |
| **D** | Coherent NON_PRODUCTION provider | **Implementation specialization of Option A**, not a different ownership model |

Option A is the inherited frozen ownership model. This ADR freezes the S04 **boundary**, not a new school SoR.

### 15. Proposed later S04 acceptance scenario

Later implementation, **if separately authorized after freeze**, should prove:

```text
one coherent NON_PRODUCTION School Context current-fact provider
  → Teacher has current ClassRef authority
  → Teacher publishes / assigns to that ClassRef
  → Student has current membership
  → Student starts / saves / submits
  → existing Learning Evidence / Assessment / Improve path remains intact
  → Principal scope contains the SAME ClassRef and sees authorized derived School Intelligence
  → Parent current access points to the SAME learner and sees Parent Intelligence
```

Then prove at least these current-authority changes:

1. remove learner membership → subsequent Student current-access command denied
2. remove teacher ClassRef authority → subsequent governed Teacher ClassRef operation denied
3. remove Principal ClassRef scope → subsequent Principal read excludes that ClassRef
4. revoke adult→learner access → subsequent Parent access denied / concealed

No `/api` Playwright mocks for the final real-stack proof.

Existing immutable historical evidence must remain intact according to owning-domain rules.

This scenario is **design guidance**. It is **not** implementation authorization.

### 16. Expected implementation slicing — NOT AUTHORIZED

Candidate later slices, **NOT AUTHORIZED** by this deposit:

| Slice | Intent |
|-------|--------|
| **S04-I01** | Coherent NON_PRODUCTION School Context current-fact provider behind the four existing ports |
| **S04-I02** | Development composition convergence so Teacher / Student / Principal / Parent use the same provider fact universe |
| **S04-I03** | Real-stack AIEOS360 authority-change E2E proving positive access + membership / scope / access revocations across existing product surfaces |

Do **not** automatically create an Admin frontend slice.  
Do **not** create production ERP integration in S04.

These remain expected candidates only until this ADR is Frozen / Approved **and** explicit implementation authorization is issued.

### 17. Explicitly deferred

- production ERP / SIS provider
- ERP vendor selection
- full ERP
- full SIS
- Admin OS
- school / class / roster / enrollment AIEOS SoRs
- finance / fees
- HR / payroll
- admissions
- timetable
- transport
- messaging
- family / custody management
- identity provisioning
- tenant administration
- cross-tenant super-admin
- `PrincipalKind.ADMIN`
- production Admin mutation API
- durable School Context replica
- NATS School Context sync
- Temporal School Context workflow
- production event publication
- distributed transactions / 2PC
- Parent evaluation / mastery exposure
- Principal learner-sensitive analytics

### 18. Precedence

This ADR **preserves** and does **not** reopen:

- [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md)
- [ADR-AIEOS-030](ADR-AIEOS-030-production-jwt-bearer.md)
- [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md)
- [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)
- [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md)
- [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)
- [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md)
- [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)
- [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md)
- [ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md)
- [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)

If a later package requires changing semantic ownership in any of those ADRs, that package must use an explicit governed forward revision. This ADR does not silently revise them.

---

## Consequences

### Positive

- Completes the AIEOS360 vertical architecture without inventing an Admin OS or school SoR.
- Makes Teacher / Student / Principal / Parent observe one school-context universe.
- Preserves replaceable current-authority adapters and production fail-closed defaults.
- Keeps AIEOS business SoRs in AIEOS.

### Negative / constraints

- Production school-context authority remains blocked until a real ERP / SIS provider exists.
- Development adapters today are not a coherent school; later S04 implementation must converge them.
- No instantaneous cross-system revocation is claimed.
- No Admin UI is provided by this baseline.

### Explicitly not authorized

- Backend / Frontend / Product / Infrastructure change
- Migration / OpenAPI
- School Context code / coherent provider implementation
- Admin OS / Admin UI
- production ERP / SIS adapter
- AIEOS360-S04 implementation slices I01–I03
- AIEOS school / class / roster / enrollment / family tables
- `PrincipalKind.ADMIN`
- new `admin.*` capability
- NATS / Temporal School Context
- production event publication
- distributed 2PC / XA
- production deployment

---

## Consistency validation (deposit-time)

| Check | Result |
|-------|--------|
| External Admin / ERP / SIS remains school-context business master | **PASS** |
| AIEOS business SoRs remain AIEOS-owned | **PASS** |
| Four existing School Context ports preserved distinctly | **PASS** |
| Provider consolidation ≠ contract consolidation | **PASS** |
| Coherent NON_PRODUCTION provider is Option A specialization, not Option B | **PASS** |
| Production remains unconfigured / fail closed | **PASS** |
| Provider current-fact mutation ≠ AIEOS school command | **PASS** |
| Admin UI not required | **PASS** |
| `PrincipalKind.ADMIN` not created | **PASS** |
| No new `admin.*` capability | **PASS** |
| No AIEOS School / Class / Roster / Enrollment / Family SoR | **PASS** |
| Option B rejected; Option C deferred | **PASS** |
| Current-authority freshness; no 2PC; no instantaneous revocation claim | **PASS** |
| PrincipalId remains identity; ERP person ID is not authentication | **PASS** |
| Privacy contracts not widened | **PASS** |
| NATS / Temporal not required | **PASS** |
| Prior frozen ADRs not reopened | **PASS** |
| S04 implementation not authorized | **PASS** |
| ADR status Proposed; not Frozen / Approved | **PASS** |

---

## Implementation authorization

This architecture deposit does **not** itself authorize implementation.

**ADR-AIEOS-062 Proposed ≠ AIEOS360-S04 implementation authorization.**

Implementation remains **NOT AUTHORIZED** until:

1. Chief Architect exact-head review of this Proposed deposit
2. Founder / Product Architecture freeze of ADR-AIEOS-062
3. freeze-commit exact-head review
4. Architecture PR merge authorization and post-merge verification
5. a **separate** Chief Architect implementation authorization

Do **not** start S04-I01.
