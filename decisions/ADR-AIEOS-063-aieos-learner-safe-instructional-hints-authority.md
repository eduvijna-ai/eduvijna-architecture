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
**Freeze readiness:** **FREEZE-CANDIDATE POLICIES SELECTED — FOUNDER RATIFICATION REQUIRED** (O63-02 §7, O63-03 §5, concurrency §8.2). **NOT FROZEN / NOT IMPLEMENTED.** This workday **does not grant** kernel capabilities or merge PR #59.  
**Workday lineage:** SP02 → SP02R1 (`e82cd5b…`) → **SP02-FR01** ([Issue #60](https://github.com/eduvijna-ai/eduvijna-architecture/issues/60)).  
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

## Source evidence (FR01-02 — pinned Backend `637583f42…`, read-only)

| Fact | Evidence (Backend pin) | Architecture use |
|------|------------------------|------------------|
| Content aggregate owner | `owner_principal_id` on Content (`domains/content/domain/content.py`) | O63-02 owner gate |
| Code-governed capabilities | `content.version.create`, `content.review.submit`, `content.review.decide`, `content.publish` in `domains/content/application/ports.py`; kernel adapters in `platform/security/authorization/content_adapters.py` | Existing vocabulary; **existence ≠ teacher hint grant** |
| Generic append service | `HttpAppendContentVersionService` (`domains/content/application/http_append.py`) enforces tenant/head/schema/idempotency | **Does not** prove current-class or hint-specific gates |
| Current ClassRef (Teaching) | `SchoolContextClassAuthority.require_assignable_class_ref` (`domains/teaching/application/school_context.py`) | Bind **explicit** `class_ref` on hint append command |
| Non-authoritative label | `TeachingWork.class_label` contextual text (`domains/teaching/domain/work.py`) | **Must not** substitute for ClassRef |
| Submit lock order | `SubmitAttemptService`: `get_assignment_for_update` **then** `attempts.get_for_update` (`domains/learning/application/submit_attempt.py` L146–150) | Hint read §8.2 aligns |
| Attempt read today | `GetAttemptService.get` — no declared row lock | Hint read requires **new** locked path |
| Worksheet `@1` only consumers | `education/schema.py`, `learner_projection.py`, `assessment/.../exact_content.py` | §3.1 T1a–T1c |

**Derived design** in §5–§8 is **not implemented** at pin. **Future implementation** requires separate engineering authorization and kernel tenant grants where applicable.

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

### 5. Semantic QA and leakage controls — O63-03 **FREEZE-CANDIDATE** (FOUNDER RATIFICATION REQUIRED)

**Status:** Selected minimum policy for Founder freeze vote. **NOT FROZEN. NOT IMPLEMENTED.**

Hints are **instructional scaffolding**, not stealth answer keys. Applies to **each optional** per-question `learner_hint` on `education.worksheet@2`.

#### 5.1 Per-question hint payload minimum (schema)

| Rule | Requirement |
|------|-------------|
| Presence | Field **absent** ⇒ no hint (identical to today). **Empty string forbidden** — treat as authoring validation error. |
| Type | Single plain-text `hint_text` string only (no markdown/HTML, no embedded objects). |
| Length | **1–500** Unicode scalars after trim (implementation MAY normalize whitespace once). |
| Prohibited tokens | No HTTP(S) URLs, no `mailto:`, no score/grade/mastery/evaluation vocabulary, no answer-key artifact references. |
| Isolation | Must not duplicate `teacher_notes`, `explanation`, or `answer` fields. |

#### 5.2 Mechanical checks (per non-empty hint, against same question’s prompt/options/answer/explanation)

| Check | Result |
|-------|--------|
| `hint_text` equals `answer` (case-insensitive trim) | **HARD BLOCK** — cannot submit for review |
| `hint_text` equals full `explanation` | **HARD BLOCK** |
| `hint_text` contains any MCQ `option` string verbatim (multiple_choice) | **HARD BLOCK** |
| `hint_text` contains URL / email pattern | **HARD BLOCK** |
| Token overlap with `answer` or `explanation` above configured similarity flag threshold | **FLAG** — requires human attestation (§5.3) |
| Profanity / obvious PII pattern | **FLAG** or **BLOCK** (implementation choice; default **FLAG** + human) |
| Reading-level heuristic vs declared worksheet difficulty | **FLAG** only |

**Do not claim** deterministic lint proves semantic safety. **Paraphrase, pedagogy, distractor implication, and age fit** require **HUMAN** review.

#### 5.3 Version-scoped attestation record (selected model)

**Selected:** immutable typed append **`WorksheetLearnerHintVersionAttestationV1`** bound to **exact** `content_version_id` (Content-domain governed record or structured ReviewDecision attachment — implementation detail). **Architecture requirements:**

| Field / rule | Requirement |
|--------------|-------------|
| `content_version_id` | Exact version under review |
| `author_principal_id` | HUMAN who created hint-bearing version |
| `reviewer_principal_id` | HUMAN who attests safety |
| **Author ≠ reviewer** | **Required** when **any** `learner_hint` is non-empty |
| `per_question_outcomes[]` | For each non-empty hint: `question_id`, mechanical `hard_block_clear`, `human_review_pass` |
| `attested_at` | Server timestamp |
| Immutability | New ContentVersion ⇒ **new** attestation cycle |

**Fail-closed gates:**

- `content.review.decide` **APPROVE** **rejected** if attestation missing, stale vs payload digest, or any `human_review_pass=false`.
- `content.publish` **rejected** if version not **APPROVED** or attestation incomplete.
- Any change to hint text ⇒ **new ContentVersion** + new attestation (GCI-G05).

**Prohibited carriers:** Review Queue free-text comments, TeachingWork notes, Answer Key, Assessment artifacts (GCI-G06).

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

#### 6.1 Teacher hint authoring fail-closed matrix (O63-02 freeze-candidate)

| Actor / condition | Append hint-bearing version |
|-------------------|----------------------------|
| ACTIVE HUMAN owner + `content.version.create` grant + valid `authoring_class_ref` | **Allow** (mechanical QA permitting) |
| Missing `content.version.create` grant | **Deny** |
| Non-owner (no steward delegation frozen) | **Deny** |
| Cross-tenant / wrong tenant | **Deny** (conceal) |
| Stale / revoked / non-assignable `authoring_class_ref` | **Deny** |
| Suspended / inactive Principal | **Deny** |
| Author = reviewer on hint version APPROVE | **Deny** |
| APPROVE/Publish without §5.3 attestation | **Deny** |

### 7. P1 teacher authoring — O63-02 **FREEZE-CANDIDATE** (FOUNDER RATIFICATION REQUIRED)

**Status:** **ONE selected policy** (below). **NOT FROZEN. NOT IMPLEMENTED.** This workday **does not** register kernel grants, mutate AuthorizationKernel catalogs, or authorize Backend routes.

**Pinned gap:** Frontend hint editor **NOT IMPLEMENTED** (`569ef8be…`).

#### 7.1 Selected policy — reuse `content.version.create` + mandatory domain gates (not a new capability)

**Rejected for minimum governance:** a new purpose-scoped kernel capability (e.g. `content.worksheet_hint.author`) as the **primary** gate — adds catalog surface without reducing risk if domain checks are skipped.

**Selected freeze-candidate:** Continue to require existing kernel capability **`content.version.create`** (`CONTENT_VERSION_CREATE` in `ports.py`) **plus** a **new domain command/port** (conceptual: `AppendWorksheetLearnerHintsContentVersion`) that enforces **all** checks below **before** append. Kernel grant of `content.version.create` remains a **separate future tenant-admin action** — **not performed in SP02-FR01**.

**No silent grant:** Teachers without tenant grant for `content.version.create` **fail closed** at kernel check. Non-owner principals **fail closed** even with capability unless a **future** steward-delegation ADR exists (none frozen here — **owner-only**).

#### 7.2 Authoritative check order (fail-closed, conceal on deny)

1. **ACTIVE HUMAN** principal (`CurrentPrincipalClassificationAuthority`).
2. **Execution tenant** = Content aggregate tenant (RLS + trusted context; client tenant not authority).
3. **`AuthorizationKernel.decide_capability`** → `content.version.create` (**exact grant required**).
4. Load Content; **`owner_principal_id == effective_actor_id`** (non-owner deny).
5. Command carries explicit **`authoring_class_ref`** (opaque string) — **not** `TeachingWork.class_label`.
6. **`SchoolContextClassAuthority.require_assignable_class_ref(tenant, teacher_principal_id, authoring_class_ref)`** — current teacher–class authority ([ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)).
7. Payload = **new immutable** `education.worksheet@2` version with optional hints; schema/ mechanical QA §5.2 **hard blocks** before review submit.
8. **Idempotent append** + audit (actor, class_ref, content_id, version_id).

**ClassRef binding:** `authoring_class_ref` is **provenance metadata** on the version command/recording only; ERP/SIS remains master; Content is **not** a roster SoR.

#### 7.3 Review / publish separation (existing capabilities)

| Step | Capability (existing code vocabulary) | Actor rule |
|------|--------------------------------------|------------|
| Submit for review | `content.review.submit` | Author (owner) |
| Safety attestation + decide | `content.review.decide` | **Reviewer ≠ author** when any hint present (§5.3) |
| Publish | `content.publish` | Publisher (may equal author **only** when **zero** hints; otherwise **recommend** separate publisher with decide capability) |

Hints **never** stored in Review free-text, TeachingWork notes, or Answer Key.

#### 7.4 Minimal Teacher path (unchanged flow, gated)

Author with §7.2 checks → new version → review submit → structured hint panel + attestation → independent reviewer APPROVE → publish → **future** assignment pin.

**Audit:** append / review / publish / attestation events with principal + class_ref + version id.

### 8. Concurrency, idempotency, TOCTOU — **FREEZE-CANDIDATE** (§8.2)

Hint GET is read-only but requires **explicit Learning-domain authorization linearization** consistent with submit ([ADR-AIEOS-058](ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) §16; Backend `submit_attempt.py`).

#### 8.1 Non-goals (explicit)

- No ERP↔AIEOS 2PC; membership evaluated **outside** DB transaction per command.
- No guarantee of **HTTP response arrival ordering** between clients.
- No retroactive recall of a **completed** 200 hint response body.
- No “exactly one of hint GET or submit wins HTTP race” without reference to lock timing.

#### 8.2 Selected hint-read contract (implementable)

**Service (conceptual):** `GetLearnerHintsService` in Learning, **single DB transaction** per request:

| Step | Action |
|------|--------|
| 1 | External **School Context learner membership** check (same port family as submit) — if deny/unavailable → **fail closed**, no hint body |
| 2 | **`get_assignment_for_update(teaching_assignment_id)`** — same lock order as submit (**assignment first**) |
| 3 | Validate assignment consumable (ACTIVE, not cancelled/closed) |
| 4 | **`attempts.get_for_update(attempt_id)`** — **row exclusive lock**, same mode as submit |
| 5 | Owner tenant, `lifecycle_state == IN_PROGRESS`, attempt matches assignment, exact `content_version_id` pin |
| 6 | Load hint allowlist from ContentVersion payload (Content read **inside** transaction **after** attempt lock) |
| 7 | **Authorization linearization point:** **re-read** `lifecycle_state` on **still-locked** attempt row; if not `IN_PROGRESS` → **deny** (no body) |
| 8 | Emit allowlisted DTO; commit (release locks) |

**Interaction with submit:** Submit uses **identical** assignment-then-attempt **`FOR UPDATE`** order. Concurrent hint GET and submit **serialize** on attempt row; whichever transaction commits second observes terminal state and **must deny** hint emission at step 7.

**In-flight completed 200:** If step 8 committed while `IN_PROGRESS`, response **may** reach client **after** submit started but **only** if submit had not yet acquired attempt lock; if submit commits first, hint path **denies** at step 7. **Do not** promise global ordering of packets on the wire.

**Every new GET** repeats steps 1–7. **Cached/replayed** responses are not authorization.

**Membership TOCTOU:** Same as ADR-058 — prior authorized command may complete; **subsequent** hint GETs fail once revocation observed at step 1.

| Race | Expected |
|------|----------|
| Submit commits, then new hint GET | **Deny** at step 7 |
| Assignment cancel/close during locked read | **Deny** at step 3/7 |
| Two GETs; submit between them | First **may** 200; second **deny** |
| Revocation between GETs | Second **deny** at step 1 |
| Client replay after submit | **Deny** on server re-check |

**Caching:** `Cache-Control: private, no-store` on hint responses.

### 9. Conceptual OpenAPI / DTO (proposal — NOT AUTHORIZED)

**Dec18 endpoint shape (O63-07 selected):** **`GET /api/v1/learning/attempts/{attempt_id}/learner-hints`** returning all allowlisted hints for the attempt (optional future per-question sub-path — **deferred**).

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
| **T0** | Teacher hint UI + **O63-02** domain command on `content.version.create` | Owner + class_ref + kernel grant enforced |
| **T1a** | Register `worksheet@2` + attestation storage + review/publish gates | §5.3 attestation required |
| **T1b** | Learning `@2` learner-safe projection + response validation | Student open/submit `@2` |
| **T1c** | Assessment `@2` exact-content evaluation adapter | Evaluate → Improve |
| **T2** | **O63-03** mechanical blocks + attestation UX | Fail-closed approve/publish |
| **B** | `GetLearnerHintsService` §8.2 + list GET + race negatives | Lock order matches submit |
| **F** | Student AttemptPage affordance | UI only when server returns hints |
| **E2E** | SP02A adversarial + schema convergence suite | Architectural tests implemented — runtime PASS separate |

**December 18 development:** **AT RISK** — T1b/T1c are **not optional**; hint GET alone is insufficient.

**Programme preservation (proposal acknowledgment):** Nov 20, 2026 showcase (integrated non-production stack); Dec 18, 2026 **development** client target for this feature; Jan 29, 2027 experience depth; full AIEOS programme through May 28, 2027 — **unchanged commitments**, not replaced by hints scope.

---

## Open issues (explicit)

| ID | Topic | Status |
|----|-------|--------|
| O63-01 | Optional field on worksheet@2 vs parallel schema registry naming | **PROPOSED** — worksheet@2 preferred |
| O63-02 | Teacher hint authoring authorization | **FREEZE-CANDIDATE SELECTED** — §7.1–§7.2; **FOUNDER RATIFICATION REQUIRED**; **no grant in this workday** |
| O63-03 | Semantic QA + attestation minimum | **FREEZE-CANDIDATE SELECTED** — §5; **FOUNDER RATIFICATION REQUIRED** |
| O63-07 | Hint GET shape | **SELECTED** — list GET for Dec18 (§9) |
| O63-04 | Hint revision after publish | **PROPOSED** — new version only |
| O63-05 | P2 AI-suggested hints | **DEFERRED** |
| O63-06 | Quiz/Homework hints | **DEFERRED** |

**Founder ratification** must explicitly adopt §5, §7, and §8.2 (or substitute equivalent frozen text). **Until Founder freeze commit, ADR-AIEOS-063 remains PROPOSED only.**

---

## Founder freeze decision sheet (FR01-14)

**If Founder approves ADR-AIEOS-063 freeze**, they would be ratifying at minimum:

| # | Policy | Implication |
|---|--------|-------------|
| 1 | **O63-02:** `content.version.create` + owner + explicit `authoring_class_ref` + `require_assignable_class_ref` | No new capability name; kernel **tenant grants** still required separately before production |
| 2 | **Non-owner authors** | **Denied** unless future steward delegation ADR |
| 3 | **Author ≠ reviewer** when any hint present | Independent `content.review.decide` |
| 4 | **O63-03:** §5 mechanical blocks + `WorksheetLearnerHintVersionAttestationV1` | Fail-closed approve/publish |
| 5 | **Hint read §8.2** | Assignment→attempt **`FOR UPDATE`**; linearization at locked re-read |
| 6 | **worksheet@2 + T1b/T1c** | Full Student→Assessment path mandatory |
| 7 | **R1 list hint GET** | No hints on assignment DTO |

**Still unauthorized after ADR freeze:** Backend/Frontend implementation, OpenAPI change, kernel grants, UI, provider AI (P2), PR #59 merge, deployment, UAT.

**Residual implementation details (not architecture authority):** attestation storage table vs ReviewDecision attachment; exact similarity flag thresholds; publisher=author when zero hints.

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
