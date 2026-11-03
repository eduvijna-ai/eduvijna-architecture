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
**Freeze readiness:** **NOT FREEZE-READY** — **FREEZE-BLOCKING OPEN:** **O63-02** (teacher authoring authorization gate) and **O63-03** (semantic QA minimum process) must be resolved at Founder freeze; see §12.  
**Implementation:** **NOT AUTHORIZED**  
**Date:** 2026-11-03  
**Revision:** SP02R1 corrective deposit (Chief exact-head review 2026-11-03)  

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

#### 3.1 `education.worksheet@2` compatibility / convergence matrix (pinned facts + proposal)

At Backend pin `637583f42b7c475ef83f6f99bca7e65e665a253d`, **`education.worksheet@2` is not registered and is not consumable** on the existing AIEOS360 worksheet vertical without additional engineering. Hint fields alone are insufficient; **Learning** and **Assessment** adapters must converge with Content registration before December development can claim end-to-end safety.

| Stage / consumer | Pinned `@1` behavior | Pinned `@2` behavior | **Proposed** post-implementation requirement |
|------------------|---------------------|----------------------|-----------------------------------------------|
| **Content schema registry** | `education.worksheet@1` registered; strict `extra=forbid` on V1 models (`src/aieos/domains/education/schema.py`, `worksheet_v1.py`) | **Not registered** — v2 payload cannot be validated/stored as typed v2 without registry work | Register `education.worksheet@2` with optional `learner_hint`; retain **GCI-G03** reader for `@1` immutable history |
| **Teacher authoring / review / publish** | Prepare → review → approve → publish for `@1` worksheets | No hint editor; no `@2` commands | T0/T1: structured hint fields on **new version** only; same ReviewDecision / publish separation ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)) |
| **Learning learner-safe projection** | `_SUPPORTED` map includes `@1`; builds hint-free `LearnerResource` (`learner_projection.py`) | **`ContentNotLearnerConsumable`** for unknown schema — Student cannot open assignment/attempt for v2-only version | Extend projection with **`@2` mapper**: same learner-safe surface as v1 (prompt/options/type only); **still no hints** on assignment/attempt GET |
| **Learning response validation** | Typed save against `@1` question shapes | Would reject unsupported schema | `@2` response validation **must** accept same learner answer shapes as v1 for shared question types |
| **Assessment exact-version evaluation** | Evaluator supports `@1` worksheet (`exact_content.py`) | **`EvaluationContentUnsupported`** — post-submit Teacher Assessment Intelligence / Improve path **breaks** for v2-only assignments | Register **`@2` evaluation adapter**: private access to `answer` / `explanation` per [ADR-AIEOS-059](ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md); **never** expose those fields on Student hint GET |
| **Gated hint read** | N/A (no hints) | N/A at pin | Reads `learner_hint` only via **separate** attempt-scoped GET (§R1), not via learner projection |
| **Already-assigned `@1` version** | Unchanged | N/A | No retrofit; hints only on **new** published `@2` version + **new/future** assignment pin |

**Negative architectural tests (future E2E — not executed under SP02R1):** unsupported schema rejection; `@1` backward compatibility after `@2` registration; `@2` Student consumption without hint leakage on assignment GET; `@2` submit → evaluate → Teacher Improve; old pinned `@1` assignment after `@2` publish elsewhere; Assessment private fields absent from Student hint responses.

**December 18 development:** **AT RISK** — T1 must explicitly include **Content registry + Learning projection + Assessment exact-content** convergence, not hint GET alone.

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

**FREEZE-BLOCKING OPEN — O63-03:** Founder must freeze a **testable minimum quality process** before implementation. Until then this ADR is **not freeze-ready**.

**Mandatory human process (proposal — must be frozen verbatim or replaced at freeze):**

1. **Author attestation:** named HUMAN teacher author confirms hint is optional scaffolding, not assessment feedback.
2. **Reviewer attestation:** independent HUMAN reviewer approves exact version only after structured review of **every** non-empty hint (not Review Queue free-text — GCI-G06).
3. **Fail-closed publish gate:** publish command **rejects** when mandatory checklist incomplete or automated **blocking** flags unresolved.

**Testable minimum checklist items (proposal):**

| Check | Automated flag (non-blocking alone) | Human judgment required |
|-------|-------------------------------------|-------------------------|
| Exact string match hint ↔ `answer` | **Block publish** | Confirm paraphrase / synonym variants |
| Hint contains full `explanation` copy | **Block publish** | Partial overlap / concept leak |
| MCQ distractor elimination by name | Flag | Reviewer reject |
| PII / profanity patterns | Flag or block | Context review |
| Reading level / age mismatch vs class | Flag only | Reviewer reject |

**Do not claim** deterministic lint proves semantic safety. Automated rules **block only obvious mechanical violations**; paraphrase, pedagogy, and age-appropriateness remain **human** at freeze and runtime governance.

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

**FREEZE-BLOCKING OPEN — O63-02:** Exact **capability / role gate is not pre-approved** in this deposit. Founder must freeze authorization checks before implementation. This ADR **does not grant** a new capability name or kernel permission.

**Candidate authorization checks (proposal — require Founder freeze selection):**

| Check | Intent |
|-------|--------|
| ACTIVE HUMAN `effective_actor` is teacher author | Same Principal model as other Teacher OS mutations ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md)) |
| Tenant match on Content aggregate | Client tenant id not authority ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)) |
| **Current** teacher–class authority for the worksheet’s teaching context | School Context façade — not ERP master ([ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)) |
| Content stewardship / edit intent on target Content aggregate | Exact capability string **OPEN** — must align with existing Teacher OS content commands without inventing silent grants |
| Failed authoring concealment | Cross-tenant, wrong tenant, non-member, lost class, missing stewardship → **deny** with same non-enumerating posture as other Teacher content commands |

**Minimal conceptual path (proposal):**

1. Teacher passing **frozen** O63-02 checks opens worksheet Content in **authoring** mode.
2. Command creates **new ContentVersion** with hint fields on selected questions.
3. **Submit for review** → Review Queue **structured** hint panel (not comment thread).
4. **APPROVE** exact version → **publish** → eligible for **future** assignment pins.

**Prohibited:** ReviewDecision comments, TeachingWork notes, Assessment Improve payloads, P2 provider AI.

**Audit (proposal):** version created / submitted / approved / published with actor; hints only via new version commands.

### 8. Concurrency, idempotency, TOCTOU (proposal)

Hint GET is **read-only** but **not authorization-free**. It does **not** inherit ADR-058 §16 submit mutation locks automatically; the candidate must define an explicit **attempt-scoped read contract** aligned with [ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §4 and §16 limitations.

#### 8.1 Minimal read authorization / linearization contract (proposal)

**Scope:** Single `LearnerAttempt` row in Learning SoR (same aggregate as submit).

**Mechanism (proposal — implementable without 2PC):**

1. Load attempt by id under tenant RLS.
2. Acquire **attempt-scoped DB concurrency** shared with submit transition — e.g. read attempt row **`FOR UPDATE`** (submit already requires exclusive transition) or **`FOR SHARE`** plus **re-read `lifecycle_state` immediately before serializing the HTTP 200 body**.
3. Re-run **all** gated checks on that fresh row: owner, membership, assignment ACTIVE/not cancelled, `lifecycle_state == IN_PROGRESS`, version pin match.
4. Only if still `IN_PROGRESS`, load hint text from ContentVersion and emit allowlisted DTO.

**Guarantees (proposal — do not over-promise):**

| Statement | Held? |
|-----------|-------|
| Every **new** hint GET **after** attempt is `SUBMITTED` **must fail closed** (no hint body) | **Yes — required** |
| Every **new** hint GET **after** membership/assignment denial observed **must fail closed** | **Yes — required** |
| Parallel hint GET + submit: if submit **commits first**, hint GET in progress **must not** emit 200 (re-read sees `SUBMITTED` → deny) | **Yes — required** (depends on §8.1 locking / final re-read) |
| Hint GET that **already returned 200** while `IN_PROGRESS`, then submit commits | **May stand** — no retroactive HTTP recall; **subsequent** GETs **deny** (same retroactive-secrecy posture as §4) |
| Absolute global ordering of two HTTP responses without DB coordination | **Not promised** |
| ERP membership revocation instantaneous with AIEOS | **Not promised** ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §4, §16) |

**Rejected prior wording:** “At most one succeeds; loser deny” without locking — **withdrawn** (SP02R1-F2).

**Duplicate GET / replay:** Each request is a **fresh authorization**. Identical body permitted **only** while all gates still pass. **Cached or replayed** prior 200 responses are **not** fresh authorization. Client replay after submit/revocation **must** fail on server re-check.

**Membership TOCTOU:** Same as ADR-058 — command that passed membership check before external revocation may complete; **subsequent** hint GETs fail closed once revocation is observed.

| Race | Proposal |
|------|----------|
| Submit commits, then new hint GET | **Deny** |
| Hint GET re-read sees `SUBMITTED` before response | **Deny** |
| Hint GET returned 200, then submit | **No server erasure**; next GET **deny** |
| Membership revoked between two hint GETs | First may succeed if still current; second **deny** |
| Assignment CLOSED/CANCELLED | **Deny** |
| Stale browser cache of hint response | `Cache-Control: private, no-store`; cache **not** authority |

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
| **T0** | Teacher hint authoring UI + **O63-02 frozen** capability checks + audit | Authorized human can create hint-bearing **draft version** |
| **T1a** | Register `worksheet@2` + Content review/publish | Approved published `@2` with hints |
| **T1b** | Learning `@2` learner-safe projection + response validation | Student can open/submit `@2` worksheet **without** hints on assignment GET |
| **T1c** | Assessment `@2` exact-content evaluation adapter | Post-submit evaluate → Teacher Improve path works for `@2` |
| **T2** | **O63-03 frozen** semantic QA + fail-closed publish | No mechanical answer/explanation leaks ship |
| **B** | Learning hint GET + §8.1 concurrency + OpenAPI + race/membership negative tests | SUBMITTED/NOT_STARTED/revocation/replay denied |
| **F** | Student AttemptPage affordance | UI only when server returns hints |
| **E2E** | SP02A adversarial + schema convergence suite | Architectural tests implemented — runtime PASS separate |

**December 18 development:** **AT RISK** — T1b/T1c are **not optional**; hint GET alone is insufficient.

**Programme preservation (proposal acknowledgment):** Nov 20, 2026 showcase (integrated non-production stack); Dec 18, 2026 **development** client target for this feature; Jan 29, 2027 experience depth; full AIEOS programme through May 28, 2027 — **unchanged commitments**, not replaced by hints scope.

---

## Open issues (explicit)

| ID | Topic | Status |
|----|-------|--------|
| O63-01 | Optional field on worksheet@2 vs parallel schema registry naming | **PROPOSED** — worksheet@2 preferred |
| O63-02 | Exact Teacher capability / role gate for hint authoring | **FREEZE-BLOCKING OPEN** — candidate checks in §7; **no silent grant** |
| O63-03 | Minimum semantic QA acceptance thresholds | **FREEZE-BLOCKING OPEN** — candidate process in §5 |
| O63-04 | Hint revision policy (edit after publish ⇒ new version only — assumed; confirm at freeze) | **PROPOSED** |
| O63-05 | P2 AI-suggested hints | **DEFERRED** |
| O63-06 | Quiz/Homework hints | **DEFERRED** |
| O63-07 | Per-question vs all-hints list GET shape | **OPEN** (either allowed if same gates) |

**Founder freeze must explicitly close O63-02 and O63-03** (or replace with alternate frozen text). Until then: **do not treat ADR-AIEOS-063 as freeze-ready.**

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
