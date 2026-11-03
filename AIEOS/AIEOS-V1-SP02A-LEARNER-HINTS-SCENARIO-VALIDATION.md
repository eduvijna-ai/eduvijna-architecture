# AIEOS-V1-SP02A — Learner Hints Scenario Validation

**Status:** **PROPOSED / SCENARIO VALIDATION — CHIEF REVIEW PENDING**  
**Workday:** AIEOS-V1-SP02-FR01R1 — contract corrections on FR01 head `1501668…`.  
**Candidate ADR:** [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) (**PROPOSED / NOT FROZEN**)  
**Feature name:** `V1-EXPAND-STUDENT-LEARNER-HINTS-V1`  
**Disclosure pattern under test:** **R1** — `GET /api/v1/learning/attempts/{attempt_id}/learner-hints` (architecture proposal only; **not implemented**)

**Exact pins (read-only evidence base):**

| Surface | SHA / head |
|---------|------------|
| Architecture `origin/main` | `491295c3cf0a151f31686a6a2e1a2176cd92c782` |
| Backend `origin/main` | `637583f42b7c475ef83f6f99bca7e65e665a253d` |
| Frontend `origin/main` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` |
| OpenAPI SHA-256 | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` |
| SP01R1 document | PR #57 head `5182f99d028f32bcd55570c5d44f5c1f64ad5277` |

**Classification legend:**

| Status | Meaning |
|--------|---------|
| **PASS_CANDIDATE** | ADR-AIEOS-063 proposal, if frozen and implemented as specified, handles the case without frozen ADR conflict |
| **CONFLICT** | Would violate a frozen ADR unless Founder revises frozen authority |
| **OPEN** | Requires freeze-time decision before implementation |
| **DEFER** | Out of December worksheet-first proposal scope |

**Method:** Static architecture validation against frozen ADRs and pinned repository facts. **No code executed.** Adversarial cases name direct HTTP intent for future E2E.

**Important:** **PASS_CANDIDATE** means the PROPOSED ADR **would** handle the case if frozen and implemented as specified — **not** a executed runtime PASS. **OPEN** scenarios require Founder freeze decisions before implementation.

---

## Summary

**Derivation rule:** Counts are the exact tally of the **Classification** column in rows **SP02-S01 through SP02-S64** below.

| Classification | Count |
|----------------|------:|
| PASS_CANDIDATE | 62 |
| CONFLICT | 0 |
| OPEN | 0 |
| DEFER | 2 |
| **Total scenarios** | **64** |

---

## Scenario matrix

| ID | Scenario | Class | Source / evidence | Expected outcome (R1 + ADR-063 proposal) |
|----|----------|-------|-------------------|------------------------------------------|
| SP02-S01 | Eligible student starts worksheet assignment; attempt `IN_PROGRESS`; version contains optional `learner_hint` on Q3 | **PASS_CANDIDATE** | ADR-058 §7–8; ADR-063 §4 | Gated hint GET returns Q3 hint text; assignment GET still has **no** hint fields |
| SP02-S02 | Same as S01 but question has **no** hint field | **PASS_CANDIDATE** | ADR-063 §3 schema optional | Hint list empty or omits question; Student experience unchanged from today |
| SP02-S03 | Student has **NOT_STARTED** assignment (no attempt) | **PASS_CANDIDATE** | SP01R1 R1-F1; ADR-063 §4 | `GET assignment` — no hints; hint endpoint not callable without attempt id → **deny** |
| SP02-S04 | Direct HTTP hint GET with valid attempt id but lifecycle **SUBMITTED** | **PASS_CANDIDATE** | ADR-058 §8 terminal; SP01R1 §post-submit | **403/409 deny**; no hint body; submitted answers readable via existing attempt routes only |
| SP02-S05 | Student opens assignment detail after submit (UI) | **PASS_CANDIDATE** | ADR-063 §6 matrix | UI must not show new hints; server must not emit hints on assignment GET |
| SP02-S06 | Student B guesses Student A `attempt_id` UUID | **PASS_CANDIDATE** | ADR-058 §22 ownership | **Deny** — not owner; non-enumerating response |
| SP02-S07 | Student same tenant, wrong assignment attempt id (tampered path) | **PASS_CANDIDATE** | ADR-058 §22 | **Deny** |
| SP02-S08 | Cross-tenant JWT on foreign attempt | **PASS_CANDIDATE** | ADR-027 tenancy; ADR-058 | **Deny** |
| SP02-S09 | Suspended HUMAN Principal | **PASS_CANDIDATE** | ADR-058 §22 | All current access **deny** including hints |
| SP02-S10 | Membership revoked while attempt **IN_PROGRESS** (observed at read) | **PASS_CANDIDATE** | ADR-058 §4 roster; SP01R1 R1-F2 | Hint GET **deny**; save/submit **deny**; attempt may remain IN_PROGRESS |
| SP02-S11 | Membership revoked after **SUBMITTED**; student reads own submission | **PASS_CANDIDATE** | ADR-058 §4 historical read | Submission read **may allow**; hint GET **deny** — hints not historic backdoor |
| SP02-S12 | Assignment **CLOSED** while IN_PROGRESS | **PASS_CANDIDATE** | ADR-058 §8 | Hint GET **deny** (aligned with save/submit) |
| SP02-S13 | Assignment **CANCELLED** while IN_PROGRESS | **PASS_CANDIDATE** | ADR-058 §8 | Hint GET **deny** |
| SP02-S14 | TeachingAssignment pins ContentVersion **V1**; teacher publishes hint-bearing **V2** | **PASS_CANDIDATE** | ADR-053 exact pin; ADR-027 immutable | Student attempt bound to **V1** — hint GET uses V1 payload only; **no** V2 hints appear mid-attempt |
| SP02-S15 | New assignment created after V2 publish pins V2 | **PASS_CANDIDATE** | ADR-053 | New attempts copy V2; hints available per gates |
| SP02-S16 | Teacher tries to mutate committed version JSON in place | **PASS_CANDIDATE** | ADR-027 GCI-G01/G05; Backend immutability | **Rejected** — must create new ContentVersion |
| SP02-S17 | Teacher stores hint text in Review Queue free-text comment only | **PASS_CANDIDATE** | ADR-027 GCI-G06; SP01R1 R1-F3 | **Not learner accessible**; not acceptable hint carrier |
| SP02-S18 | Hint text equals `answer` field (exact string) | **PASS_CANDIDATE** | ADR-063 §5.2 | **HARD BLOCK** before review; publish impossible |
| SP02-S19 | Hint paraphrases answer (semantic duplicate) | **PASS_CANDIDATE** | ADR-063 §5.2–§5.3 | **FLAG** + attestation `human_review_pass` required; lint alone insufficient |
| SP02-S20 | MCQ hint eliminates three distractors by name | **PASS_CANDIDATE** | ADR-063 §5 forbidden content | Review/QA should reject; server still only returns hint text — no grade |
| SP02-S21 | Student replays captured hint GET response after submit | **PASS_CANDIDATE** | ADR-063 §4 retroactive secrecy | Client may retain stale body; **server** denies new reads; architecture does not promise erasure |
| SP02-S22 | Concurrent hint GET and submit POST (same attempt) | **PASS_CANDIDATE** | ADR-063 §8.2; `submit_attempt.py` lock order | Serialize on assignment→attempt **`FOR UPDATE`**; submit-first ⇒ hint **deny** at step 7; no bogus “one HTTP winner” rule |
| SP02-S23 | School Context membership provider timeout/error | **PASS_CANDIDATE** | ADR-062 fail-closed | Hint GET **deny** without membership affirmation |
| SP02-S24 | ContentVersion read failure mid-request | **PASS_CANDIDATE** | ADR-063 §6 | **Deny** — no partial hint leak from error payload |
| SP02-S25 | Parent authenticated GET on student attempt hint route | **PASS_CANDIDATE** | ADR-061 Parent allowlist | **Deny** — no Parent hint extension |
| SP02-S26 | Parent infers hint existence from child UI side channel | **PASS_CANDIDATE** | ADR-061 EVALUATION_EXISTENCE=NO | Product must avoid Parent-visible hint indicators; architecture does not add Parent reads |
| SP02-S27 | Principal attempts learner hint drill-down | **PASS_CANDIDATE** | ADR-060 aggregate anti-PII | **Deny** |
| SP02-S28 | Teacher (current class) calls student hint GET with student attempt id | **PASS_CANDIDATE** | ADR-058 no impersonation | **Deny** on Student/Learning student routes |
| SP02-S29 | Teacher lost class membership calls hint GET | **PASS_CANDIDATE** | ADR-058 teacher routes separate | **Deny** |
| SP02-S30 | P2 AI-suggested hint without teacher approval workflow | **DEFER** | Founder scope P2 deferred | Must not ship in V1-EXPAND P1; **DEFER** |
| SP02-S31 | Quiz content type hint request | **DEFER** | ADR-063 December worksheet-only | **DEFER** until separate approval |
| SP02-S32 | R2 design: hint embedded in assignment GET with server strip | **PASS_CANDIDATE** (as **negative design**) | SP01R1 R1-F1 | Documented as **rejected** primary pattern; if implemented, regression risk → fail future review |
| SP02-S33 | Two sequential hint GETs; authority unchanged between requests | **PASS_CANDIDATE** | ADR-063 §8.2 | Each GET repeats full gate + lock path; identical body only while still authorized |
| SP02-S34 | LearnerAssessmentEvaluation exists; student requests hint | **PASS_CANDIDATE** | ADR-059 evaluation ≠ feedback | Hint path independent; evaluation DTOs **unmodified** |
| SP02-S35 | Attempt uses `LearnerResource` projection — verify `answer`/`explanation` still excluded | **PASS_CANDIDATE** | Backend learner projection; ADR-058 §22 | Assignment/attempt resource **must not** add answer/explanation/hints |
| SP02-S36 | Teacher **without** tenant grant for `content.version.create` attempts hint-version append | **PASS_CANDIDATE** | ADR-063 §7.1–§7.2; kernel | **Deny** at capability check — no new grant in FR01 |
| SP02-S37 | Teacher cross-tenant hint authoring command on foreign Content | **PASS_CANDIDATE** | ADR-027 tenancy; §7 concealment | **Deny**; non-enumerating failure |
| SP02-S38 | Teacher **owner** but `authoring_class_ref` fails `require_assignable_class_ref` (lost/stale class) | **PASS_CANDIDATE** | ADR-062; §7.2 step 6 | **Deny** append |
| SP02-S39 | Assignment pins `education.worksheet@2` before Learning `@2` learner projection ships (pin fact) | **PASS_CANDIDATE** | Backend `learner_projection.py` `_SUPPORTED` | Today → **ContentNotLearnerConsumable**; T1b **required** before Student consumption |
| SP02-S40 | Student submits `@2` worksheet before Assessment `@2` exact evaluator ships (pin fact) | **PASS_CANDIDATE** | Backend `exact_content.py` | Today → **EvaluationContentUnsupported**; T1c **required** for evaluate → Improve |
| SP02-S41 | Existing assignments remain on `worksheet@1` after `@2` registered | **PASS_CANDIDATE** | GCI-G03; ADR-063 §3.1 | `@1` reader retained; behavior unchanged |
| SP02-S42 | `@2` assignment GET / attempt resource for Student | **PASS_CANDIDATE** | ADR-063 §3.1 proposed mapper | Prompt/options/type only; **no** hints on normal learner DTO |
| SP02-S43 | Post-submit Assessment evaluates `@2` with private `answer`/`explanation` | **PASS_CANDIDATE** | ADR-059; ADR-063 §3.1 | Evaluator uses authoring fields; Student hint GET still minimal allowlist |
| SP02-S44 | Hint GET returns 200, then submit succeeds; client issues **new** hint GET | **PASS_CANDIDATE** | ADR-063 §8.2 | Second GET **deny** at B8; first 200 **not** retroactively recalled |
| SP02-S45 | Membership revoked after first hint GET; second hint GET | **PASS_CANDIDATE** | ADR-058 §4 TOCTOU | Second GET **deny** at A4 |
| SP02-S46 | Teacher has `content.version.create` but is **not** `owner_principal_id` | **PASS_CANDIDATE** | ADR-063 §7.2 step 4 | **Deny** (no steward delegation frozen) |
| SP02-S47 | Teacher owner + grant + valid `authoring_class_ref`; mechanical QA clear | **PASS_CANDIDATE** | ADR-063 §7 | Append **allowed**; review/submit follows |
| SP02-S48 | Author attempts `content.review.decide` APPROVE on own hint-bearing version | **PASS_CANDIDATE** | ADR-063 §7.3; §5.3 | **Deny** — author ≠ reviewer when hints present |
| SP02-S49 | Reviewer APPROVE without `WorksheetLearnerHintVersionAttestationV1` | **PASS_CANDIDATE** | ADR-063 §5.3 | **Deny** fail-closed |
| SP02-S50 | `content.publish` while attestation `payload_digest` ≠ current version payload | **PASS_CANDIDATE** | ADR-063 §5.3 | **Deny** |
| SP02-S51 | Submit transaction holds attempt lock; concurrent hint GET waits then sees `SUBMITTED` | **PASS_CANDIDATE** | ADR-063 §8.2 | Hint **deny** at B8 |
| SP02-S52 | Hint transaction completes 200 while still `IN_PROGRESS`; submit later; new hint GET | **PASS_CANDIDATE** | ADR-063 §8.2 | New GET **deny**; prior 200 may remain on client |
| SP02-S53 | Assignment **CANCELLED** during hint GET locked transaction | **PASS_CANDIDATE** | ADR-063 §8.2 B3/B8 | **Deny** |
| SP02-S54 | Author loses `content.version.create` after append; **separate** publisher with `content.publish` publishes hint version | **PASS_CANDIDATE** | ADR-063 §7.3; Backend `publish.py` | **Allow** publish (publisher-centric; author create not re-required) |
| SP02-S55 | Suspended/inactive HUMAN author at guarded append | **PASS_CANDIDATE** | §7.2 step 1 | Append **deny** |
| SP02-S56 | MCQ hint contains option string (mechanical hard block) | **PASS_CANDIDATE** | ADR-063 §5.2 | Block before review |
| SP02-S57 | Full `@2` vertical: assign → attempt → hint GET → submit → evaluate → Improve (architecture) | **PASS_CANDIDATE** | ADR-063 §3.1 T1a–T1c | Requires all adapters; pin today **incomplete** — **not runtime PASS** |
| SP02-S58 | Direct generic `POST …/contents/{id}/versions` with hint-bearing `@2` payload | **PASS_CANDIDATE** | ADR-063 §7.5 | **Reject** — only guarded append may create hints |
| SP02-S59 | Hint-bearing version exists without attestation (legacy path); reviewer APPROVE | **PASS_CANDIDATE** | ADR-063 §5.3 defense in depth | **Deny** APPROVE |
| SP02-S60 | Hint-bearing APPROVED version; publisher lacks `content.publish` | **PASS_CANDIDATE** | ADR-063 §7.3 | Publish **deny** |
| SP02-S61 | Hint GET with only `attempt_id`; assignment/class from **stored** attempt preview | **PASS_CANDIDATE** | ADR-063 §8.2 Phase A | No client-supplied assignment/class authority |
| SP02-S62 | Author equals publisher on hint-bearing version publish attempt | **PASS_CANDIDATE** | ADR-063 §7.3 | **Deny** |
| SP02-S63 | Reviewer loses `content.review.decide` before APPROVE retry | **PASS_CANDIDATE** | §7.3 revocation matrix | **Deny** |
| SP02-S64 | Suspended/inactive HUMAN **publisher** at publish | **PASS_CANDIDATE** | §7.3 | Publish **deny** |

---

## Required negative HTTP tests (future E2E backlog)

These map to mandatory adversarial coverage from Issue #58 / SP01R1:

| Test | Scenario IDs | Expected HTTP |
|------|--------------|---------------|
| NOT_STARTED assignment GET carries no hints | S03 | 200 assignment without hint fields |
| SUBMITTED hint GET | S04 | 403/409, no body |
| Ownership / tenant | S06–S08 | 403/404 |
| Roster loss IN_PROGRESS | S10 | 403 |
| Roster loss SUBMITTED + submission read | S11 | submission 200; hint 403 |
| Old assigned version vs newer published | S14–S15 | hints from pinned version only |
| Review comment channel | S17 | no learner route exposes comments as hints |
| Parent / Principal | S25–S27 | 403 |
| P2 AI / Quiz hint | S30–S31 | DEFER |
| Response replay / cache | S21, S44 | new GET denied |
| Teacher lost class hint GET | S29 | 403 |
| worksheet@2 Learning | S39, S42 | T1b |
| worksheet@2 Assessment | S40, S43 | T1c |
| v1 backward compat | S41 | unchanged |
| Near-duplicate / paraphrase | S19, S56 | FLAG + attestation / hard block |
| Teacher without capability grant | S36 | deny |
| Teacher non-owner | S46 | deny |
| Teacher lost class authoring | S38 | deny |
| Author self-approve | S48 | deny |
| Missing attestation | S49–S50 | deny |
| Submit/hint lock race | S22, S51–S52 | §8.2 |
| Assignment cancel during hint lock | S53 | deny |
| Revoked publisher grant | S60, S64 | deny |
| Author create revoked; separate publisher | S54 | allow publish |
| Generic append hint bypass | S58 | reject |
| Attestation/digest on APPROVE | S49, S59, S50 | deny |
| Trusted preview hint GET | S61 | Phase A stored fields |
| Author=publisher hint version | S62 | deny |
| Full @2 vertical | S57 | T1a–T1c |

---

## Frozen ADR conflict register

| Frozen ADR | Conflict found? | Notes |
|------------|-----------------|-------|
| ADR-AIEOS-027 | **No** | New version + review + publish required |
| ADR-AIEOS-053 | **No** | Exact version pin preserved |
| ADR-AIEOS-055 | **No** | No assessment hint coupling |
| ADR-AIEOS-056 | **No** | Improve unchanged |
| ADR-AIEOS-058 | **No** | IN_PROGRESS + membership gating aligned |
| ADR-AIEOS-059 | **No** | No student evaluation feedback |
| ADR-AIEOS-060 | **No** | No Principal hint drill-down |
| ADR-AIEOS-061 | **No** | No Parent reads |
| ADR-AIEOS-062 | **No** | Current membership façade reused |

**Blocker conflicts:** **None** identified for PROPOSED ADR candidacy.

---

## Freeze-candidate policy cross-reference (FR01-11)

| Issue | ADR section | Scenario coverage |
|-------|-------------|-------------------|
| O63-02 authoring | §7, §7.5 | S36–S38, S46–S48, S54, S58 |
| O63-03 QA / attestation | §5.3 | S18–S19, S49–S50, S56, S59 |
| Concurrency §8.2 | §8.2 | S22, S33, S44–S45, S51–S53, S61 |
| Review/publish revocation | §7.3 | S48, S54, S60, S62–S64 |
| worksheet@2 convergence | §3.1 | S39–S43, S57 |

**Founder ratification required** before ADR freeze. **NOT FROZEN** in this deposit.

---

## Implementation authorization boundary

Passing this scenario validation **does not** authorize code, OpenAPI edits, schema registration, UI, merge of ADR-063, or December delivery. **Chief review** of exact PR head → **Founder freeze** → **separate engineering workday**.

**Related STOP line:** `AIEOS-V1-SP02-FR01R1 — FREEZE-CANDIDATE CONTRACT CORRECTION DEPOSITED / CHIEF EXACT-HEAD REVIEW PENDING / PR #59 DRAFT NOT MERGED / ADR-AIEOS-063 NOT FROZEN / PRODUCT CODE NOT AUTHORIZED`.
