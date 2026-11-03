---
id: ADR-AIEOS-063
title: AIEOS Learner-Safe Instructional Hints Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: proposed
version: 1.0.0
created: 2026-11-03
last_updated: 2026-11-03
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-063 — AIEOS Learner-Safe Instructional Hints Authority

**Status:** **PROPOSED / CHIEF REVIEW PENDING / FOUNDER FREEZE REQUIRED**  
**Implementation:** **NOT AUTHORIZED**  
**Date:** 2026-11-03  

**Founder product-direction authorization (2026-11-03):** `V1-EXPAND-STUDENT-LEARNER-HINTS-V1` is the **approved proposed worksheet-first December 18, 2026 development-ready scope** for this feature family. That authorization permits **this architecture deposit and scenario validation only**. It is **not** ADR freeze, **not** Backend/Frontend/Product implementation authorization, **not** OpenAPI authorization, **not** a production or UAT guarantee, and **not** permission to merge [PR #57 SP01R1](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57).

**Workday:** **AIEOS-V1-SP02** — ADR candidate + scenario validation ([Issue #58](https://github.com/eduvijna-ai/eduvijna-architecture/issues/58)).  
**Lineage:** [SP01 Issue #56](https://github.com/eduvijna-ai/eduvijna-architecture/issues/56); [SP01R1 PR #57](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57) head `5182f99d028f32bcd55570c5d44f5c1f64ad5277` (read-only; **not merged**); Chief SP01R1 acceptance ([PR #57 comment](https://github.com/eduvijna-ai/eduvijna-architecture/pull/57#issuecomment-6603867945)).

**Related:** [ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md) · [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) · [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) · [ADR-AIEOS-060](ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) · [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) · [ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)

**Catalogue note:** **PROPOSED** is architecture candidate status only. No frozen ADR is modified by this deposit. **Frozen / Approved ≠ implemented.** December 18, 2026 is a **development readiness target**, not Founder UAT or deployment. **December 18 remains AT RISK** until ADR freeze, teacher authoring journey, schema/review path, semantic QA, gated read API, Student UI, and negative HTTP tests are separately authorized and delivered.

**Exact governed pins (SP02 preflight — 2026-11-03):**

| Surface | Pin |
|---------|-----|
| Architecture `origin/main` | `491295c3cf0a151f31686a6a2e1a2176cd92c782` |
| Product `origin/main` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Backend `origin/main` | `637583f42b7c475ef83f6f99bca7e65e665a253d` |
| Frontend `origin/main` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Authoritative OpenAPI SHA-256 | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` |
| Alembic head | `a360s010004` |

Does **not** reopen or rewrite frozen bodies: ADR-AIEOS-027, 053, 055, 056, 058, 059, 060, 061, 062.

---

## Context

AIEOS360-S01 through S03 closed Student attempt/submission, Assessment Intelligence, Principal School Intelligence, and Parent Intelligence as **architecture** authorities. At the pinned Backend/Frontend, Student OS already supports **assign → start attempt → save → submit → read-only submitted view** with a **learner-safe ContentVersion projection** that **excludes** answer keys, explanations, teacher notes, and evaluation fields from the student-facing resource.

Founder authorized a **named V1-EXPAND** direction: **`V1-EXPAND-STUDENT-LEARNER-HINTS-V1`** — optional **teacher-authored, human-reviewed, learner-safe instructional hints** on **worksheet** content, visible to the owning student **only while** their `LearnerAttempt` is **`IN_PROGRESS`**, without introducing grades, retries, or Parent/Assessment/Principal extensions.

SP01R1 discovery established binding gaps:

1. **R1-F1:** `GET /api/v1/student-os/assignments/{assignment_id}` returns a full learner resource for **all** attempt-summary states. Embedding hints in that DTO would leak hints to **NOT_STARTED** and **SUBMITTED** unless the server applies state-specific stripping — which is fragile and couples assignment browsing to attempt lifecycle.
2. **R1-F2:** After roster revocation, **current-access** commands fail closed, but **own SUBMITTED** response history may remain readable under [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md). Hints must **not** become a post-revocation or post-submit backdoor.
3. **R1-F3:** Teacher per-question hint **authoring UI/API is not implemented** at pinned Frontend. Hints must enter only through a **new immutable ContentVersion** with explicit **review → approve → publish**, not Review Queue free-text, TeachingWork notes, or Assessment/Answer Key channels.

Pinned Backend `WorksheetV1` (`education.worksheet@1`, `src/aieos/domains/education/worksheet_v1.py`) uses **`extra=forbid`** on all models. Each question already carries **`answer`** and **`explanation`** fields that are **teacher/authoring truth** and are **not** part of the learner-safe projection today. Learner hints are a **distinct instructional surface** that must not collapse into those fields.

---

## Problem

Students working worksheet assignments lack **optional formative scaffolding** that teachers can deliberately author and quality-gate, while the platform must preserve:

- immutable exact-version assignment binding ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md), [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md));
- **Approved ≠ Published** and **Assigned ≠ Attempted** separation ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md));
- **Submitted ≠ Evaluated** and **evaluation ≠ learner feedback** ([ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md));
- Parent **`EVALUATION_EXISTENCE = NO`** and no new Parent reads ([ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md));
- one-attempt **`IN_PROGRESS` → `SUBMITTED`** policy with **no retry** ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §8–9).

Any hint design that relies on UI hiding, unconditional assignment GET payloads, Review comments, or in-place ContentVersion mutation **fails** SP01R1 and frozen ADR boundaries.

---

## Alternatives considered

### R1 — Attempt-scoped gated hint GET (**recommended candidate**)

**Proposal:** Introduce a **separate read contract** (conceptual):

```http
GET /api/v1/learning/attempts/{attempt_id}/learner-hints
GET /api/v1/learning/attempts/{attempt_id}/learner-hints/{question_id}
```

Hints are returned **only** when **all** authoritative checks pass at request time:

- ACTIVE HUMAN `effective_actor` = `learner_principal_id` = attempt owner;
- tenant match;
- **current** class membership for the attempt’s `class_ref` ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §4, [ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md));
- TeachingAssignment **ACTIVE** and startable/eligible for ongoing work;
- attempt `lifecycle_state == IN_PROGRESS`;
- attempt-bound `content_version_id` matches TeachingAssignment pin;
- hint text loaded from **that exact ContentVersion** payload only.

**Deny:** `403` / `404` (policy-selected consistent non-enumerating posture) when any gate fails. **No hint body** on provider/read errors — fail closed.

**Pros:** Positive allowlist; assignment GET unchanged; aligns with Learning SoR ownership of attempts; explicit audit surface; SP01R1 R1-F1 satisfied.  
**Cons:** Extra round-trip; requires new OpenAPI + Student UI wiring (not authorized here).

### R2 — State-filtered assignment / attempt DTO

**Proposal:** Keep hints in ContentVersion-derived structures but **server-strip** hints unless `IN_PROGRESS` on embedded attempt summary.

**Pros:** Fewer HTTP calls.  
**Cons:** Easy to regress when DTO fields are reused; couples Content payload parsing to Student OS read façade; higher risk of NOT_STARTED/SUBMITTED leakage via cache, partial projections, or future fields; weaker separation from `LearnerResource` learner-safe rules in [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §22.

**Disposition:** **R1 recommended** for freeze candidacy. R2 remains documented as **rejected for primary design** due to leakage and maintenance risk (SP01R1 R1-F1).

---

## Decision proposal

**If frozen**, AIEOS adopts **R1** as the authoritative learner hint **disclosure** pattern for **`V1-EXPAND-STUDENT-LEARNER-HINTS-V1`**, with the content, authoring, and lifecycle rules below. Until freeze, this section is **proposal only**.

### 1. Feature boundary (December development target)

| In scope (proposal) | Out of scope (proposal) |
|---------------------|-------------------------|
| **Worksheet** (`education.worksheet@1` / `WorksheetV1`) only | Quiz / Homework hint schemas unless separately approved |
| **P1** teacher-authored per-question hints, voluntary | **P2** AI-suggested hints requiring teacher approval — **DEFERRED** |
| Hints on **new** immutable ContentVersion after review/approve/publish | In-place mutation of committed versions |
| Server-gated read during **own** `IN_PROGRESS` attempt | Correctness, score, grade, mastery, misconception, personalization |
| Optional collapsible Student UI affordance when server returns hints | Parent hint reads; Principal learner drill-down |
| Audit of hint **read disclosure** (conceptual) | Changing Assessment or Parent DTOs |

### 2. Authority / SoR table (proposal)

| Concern | Authority |
|---------|-----------|
| Hint **text storage** (canonical) | **ContentVersion** typed payload — Generic Content ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)) |
| Hint **eligibility for assignment** | **Published** ContentVersion pin on **TeachingAssignment** ([ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)) |
| Hint **disclosure to student** | **Learning** domain gated read — bound to **LearnerAttempt** ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md)) |
| Teacher **authoring** of hint-bearing versions | **Teacher OS + Content commands** — **NOT IMPLEMENTED** at pin; requires new capability (§7) |
| Human **review / approve** | **ReviewDecision** on exact version ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md) §Review; GCI-G05, GCI-G06) |
| **Publication** | Explicit publish command; Approved ≠ Published |
| Answer key / explanation / evaluation | **Not** learner hints; remain excluded from learner projection |
| Assessment intelligence | [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) — **no** student-facing evaluation or hint coupling |
| Parent reads | [ADR-AIEOS-061](ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) — **no** extension |

**New invariant (proposal):**

```text
Authored Instructional Hint  ≠  Answer Key
Authored Instructional Hint  ≠  Question Explanation (authoring field)
Authored Instructional Hint  ≠  Assessment Evaluation / Feedback
Hint Disclosure              ≠  Grade / Mastery / Retry
Published Hint Version       ≠  Retroactive change to already-assigned ContentVersion
IN_PROGRESS Gated Read       ≠  Historic Hint Read after SUBMITTED
```

### 3. Content schema evolution (WorksheetV1)

**Pinned fact:** `WorksheetV1` / `WorksheetQuestionV1` use `model_config = ConfigDict(extra="forbid")` (Backend pin).

**Proposal (preferred):** Register **`education.worksheet@2`** (or equivalent registered schema id) as a **forward** schema that adds an **optional** per-question field, conceptually:

```json
"learner_hint": { "text": "..." }
```

- **Absent** `learner_hint` on a question ⇒ behavior identical to today (no hint for that question).
- **Existing** immutable `education.worksheet@1` versions **remain readable** via GCI-G03 retained reader; no retrofit.
- Adding hints to content that already shipped as v1 ⇒ **new ContentVersion** on the same Content aggregate (GCI-G02), new schema registration, full review cycle, explicit publish.
- **Rejected:** Silent extra fields on v1 (forbidden by `extra=forbid` anyway) or post-commit JSON mutation.

**Reader / projection rules (proposal):**

- **Learner-safe assignment/attempt resource projection** continues to **exclude** `answer`, `explanation`, `teacher_notes`, `teacher_summary`, and any hint fields.
- **Gated hint endpoint** reads hint text **only** from the attempt-bound `content_version_id` and returns a **minimal DTO**: `{ question_id, hint_text }` (+ optional display metadata without pedagogical leakage).

### 4. Lifecycle and current policy

```text
Teacher authors hint-bearing worksheet version (P1)
  → submit for review
  → ReviewDecision APPROVE (exact version)
  → explicit publish
  → future TeachingAssignment pins new ContentVersion
  → Student starts attempt (copies content_version_id)
  → IN_PROGRESS: gated hint GET permitted
  → SUBMITTED: no NEW gated hint delivery
```

**Assignment already pinned to version V:** never gains hints from version V+N. Teachers must create a **new assignment** (or future reassignment policy — **not proposed here**) to use hint-bearing versions.

**Retroactive secrecy:** If a hint was disclosed during `IN_PROGRESS`, architecture **does not** promise erasure from client memory or audit logs. Policy is **stop further server delivery** after terminal states, not “un-see.”

**NOT_STARTED:** No attempt id ⇒ no hint endpoint; assignment GET **must not** include hint bodies.

**Membership loss while IN_PROGRESS:** hint read **denied** (same posture as save/submit fail-closed per ADR-058 §4).

**Membership loss after SUBMITTED:** own submitted answers may remain readable; **hints denied**.

### 5. Semantic QA and leakage controls (proposal)

Hints are **instructional scaffolding**, not stealth answer keys.

**Required governance (human-in-the-loop):**

- Teacher (or authorized author) enters hint text in **dedicated** authoring surface tied to **ContentVersion creation**, not Review free-text ([GCI-G06](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)).
- Reviewer confirms hints are **optional** and **learner-safe** before APPROVE.
- **Fail-closed** publish gate if mandatory QA checklist incomplete (implementation detail deferred).

**Automated assists (proposal, non-exhaustive):** block exact string equality with `answer`; flag MCQ options appearing verbatim in hint; length bounds; profanity/PII patterns — **supplement** human review, **not** replace it. **Do not claim** deterministic lint eliminates paraphrase, synonym, or age-inappropriate leakage.

**Explicitly forbidden hint content:** direct answer text, “option B is wrong,” copied `explanation`, teacher_notes bleed, evaluation outcomes, links to answer key artifacts.

### 6. Authorization / visibility matrix (proposal)

| Actor / state | Assignment GET (no hints in resource) | Gated hint GET |
|---------------|--------------------------------------|----------------|
| Owner student, NOT_STARTED | Allowed (existing); **no hints** | **Deny** — no IN_PROGRESS attempt |
| Owner student, IN_PROGRESS, all current gates pass | Allowed | **Allow** (question-level or list) |
| Owner student, IN_PROGRESS, membership revoked | Assignment/save/submit fail closed | **Deny** |
| Owner student, SUBMITTED | Submitted view; **no hints** | **Deny** |
| Owner student, SUBMITTED, membership lost | Own submission read may remain (ADR-058) | **Deny** |
| Student B, same class | Own resources only | **Deny** on A’s attempt id |
| Wrong tenant / forged attempt id | Fail closed | **Deny** / non-enumerating 404 |
| Suspended / inactive Principal | No current access | **Deny** |
| Teacher current class | Teacher routes unchanged; **not** student hint proxy | **Deny** on student attempt (no impersonation) |
| Teacher lost class | N/A | **Deny** |
| Parent | No new reads (ADR-061) | **Deny** |
| Principal | Aggregate intelligence only (ADR-060) | **Deny** learner hint drill-down |
| Backend School Context error | Fail closed on membership-dependent routes | **Deny** — no hint body |
| Content read error | Learner resource degradation per existing rules | **Deny** — no partial hint leak |

### 7. P1 teacher authoring (NOT IMPLEMENTED — proposal)

**Pinned gap (R1-F3):** Frontend `ReviewDetailPage`, `WorkPage`, `contentApi` — **no** per-question hint editor at `569ef8be46617ab1412ddb3f5a0214c40bdb946b`.

**Minimal conceptual path (proposal):**

1. Teacher with **current class + tenant + content stewardship capability** (exact capability name = **OPEN** — see §12) opens worksheet Content in **authoring** mode.
2. Command creates **new ContentVersion** (or draft version) with hint fields populated on selected questions.
3. **Submit for review** → Review Queue shows hint text in **structured** reviewer panel (not comment thread).
4. **APPROVE** exact version → teacher **publish** → version eligible for **future** assignment pins.

**Prohibited:** storing hints in ReviewDecision comments, TeachingWork remediation notes, Assessment Improve payloads, or provider AI calls for P2.

**Audit (proposal):** version created / submitted / approved / published with actor; hint field mutation only via new version commands.

### 8. Concurrency, idempotency, TOCTOU (proposal)

**Checks are evaluated at authoritative read time**, not cached in client trust stores.

| Race | Proposal |
|------|----------|
| Hint GET then submit completes | Submit wins; subsequent hint GET **deny** |
| Submit in flight, hint GET parallel | At most one succeeds; loser **deny** on lifecycle |
| Membership revoked between UI render and hint GET | **Deny** when revocation observed |
| Assignment CLOSED/CANCELLED | hint GET **deny** (aligned with save/submit) |
| Duplicate hint GET | Idempotent same body; no side-effect |
| Stale ETag on attempt | Attempt GET uses existing concurrency; hint GET revalidates lifecycle + membership |

**Limitation (explicit):** ADR-058 already states membership revocation is **not** instantaneous ERP↔AIEOS ordering. A request that **already passed** gates may complete; subsequent requests **fail closed**. No fictional distributed lock / 2PC / lease.

**Browser caching:** `Cache-Control: private, no-store` on hint responses (proposal); hints **must not** rely on localStorage/service worker persistence for authorization.

### 9. Conceptual OpenAPI / DTO (proposal — NOT AUTHORIZED)

**Ingress:** Student JWT; `effective_actor` = learner; Learning domain.

**Allowlisted response (example shape):**

```json
{
  "attempt_id": "...",
  "content_version_id": "...",
  "hints": [
    { "question_id": "q1", "hint_text": "Think about the common denominator." }
  ]
}
```

**Errors:** RFC 9457 problem+json; stable `operationId`; no answer/explanation fields in error payloads.

**Telemetry / audit (proposal):** log hint read events with `attempt_id`, `question_id`, actor, tenant, outcome — **not** full hint text in aggregate Principal dashboards.

### 10. Frozen authority consistency (summary)

| Frozen ADR | Relevant binding | Hint proposal alignment |
|------------|------------------|-------------------------|
| **027** | Immutable ContentVersion; review; publish; GCI-G03/G05/G06 | Hints only via **new** version + review + publish |
| **053** | Assignment pins exact published ContentVersion | Hints follow pin; no float-forward |
| **055** | Assessment ≠ learner feedback | Hints not from evaluation |
| **058** | IN_PROGRESS only for current work; one attempt; membership for current access | Gated read only IN_PROGRESS + current membership |
| **059** | Evaluation teacher-only; not student score | No coupling |
| **061** | Parent allowlist; EVALUATION_EXISTENCE=NO | No Parent hint API |
| **062** | Current membership façade | Membership revalidated on hint GET |

**Conflicts requiring Founder freeze clarification:** None identified that **block** candidacy; several **OPEN** implementation choices remain (§12).

---

## Consequences

- **Positive:** Formative scaffolding without grading; preserves exact-version discipline; closes SP01R1 leakage class if implemented as specified.
- **Negative:** Additional engineering packets (authoring UI, schema v2, QA, API, E2E negatives); December target **AT RISK**.
- **Neutral:** Existing assignments and versions unchanged; Quiz/Homework deferred.

---

## Engineering critical path (architecture-only — NOT AUTHORIZED)

| Phase | Packet | Gate |
|-------|--------|------|
| **T0** | Teacher hint authoring UI + capability + audit | Human can create hint-bearing **draft version** |
| **T1** | Register worksheet@2 + Content review/publish path | Approved published version with hints |
| **T2** | Semantic QA checklist + fail-closed publish | No exact-answer hints ship |
| **B** | Learning hint GET + OpenAPI + negative tests | SUBMITTED/NOT_STARTED/membership denied |
| **F** | Student AttemptPage affordance | UI only when server returns hints |
| **E2E** | Adversarial HTTP suite | SP02A scenarios PASS |

**Programme preservation (proposal acknowledgment):** Nov 20, 2026 showcase (integrated non-production stack); Dec 18, 2026 **development** client target for this feature; Jan 29, 2027 experience depth; full AIEOS programme through May 28, 2027 — **unchanged commitments**, not replaced by hints scope.

---

## Open issues (explicit)

| ID | Topic | Status |
|----|-------|--------|
| O63-01 | Optional field on worksheet@2 vs parallel schema registry naming | **PROPOSED** — worksheet@2 preferred |
| O63-02 | Exact Teacher capability / role gate for hint authoring | **OPEN** |
| O63-03 | Minimum semantic QA acceptance thresholds | **OPEN** |
| O63-04 | Hint revision policy (edit after publish ⇒ new version only — assumed; confirm at freeze) | **PROPOSED** |
| O63-05 | P2 AI-suggested hints | **DEFERRED** |
| O63-06 | Quiz/Homework hints | **DEFERRED** |
| O63-07 | Per-question vs all-hints list GET shape | **OPEN** (either allowed if same gates) |

---

## Implementation status

| Item | Status at pin |
|------|----------------|
| ADR-AIEOS-063 freeze | **NOT FROZEN — PROPOSED** |
| Hint fields in Worksheet schema | **NOT PRESENT** (`worksheet@1` only) |
| Gated hint HTTP route | **NOT IN OpenAPI** (`4042FB27…C1D0`) |
| Teacher hint authoring UI | **NOT IMPLEMENTED** |
| Student hint UI | **NOT IMPLEMENTED** |

**STOP LINE:** Chief review of this PROPOSED ADR → Founder freeze decision → **separate** implementation workday authorization required before any product code.

---

## Scenario validation reference

Detailed ≥24-case analysis: [AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md](../AIEOS/AIEOS-V1-SP02A-LEARNER-HINTS-SCENARIO-VALIDATION.md).
