# AIEOS-V1-SP02A — Learner Hints Scenario Validation

**Status:** **PROPOSED / SCENARIO VALIDATION — CHIEF REVIEW PENDING**  
**Workday:** AIEOS-V1-SP02 ([Issue #58](https://github.com/eduvijna-ai/eduvijna-architecture/issues/58))  
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

---

## Summary

| Classification | Count |
|----------------|------:|
| PASS_CANDIDATE | 26 |
| CONFLICT | 0 |
| OPEN | 2 |
| DEFER | 2 |
| **Total scenarios** | **30** |

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
| SP02-S18 | Hint text equals `answer` field (exact string) | **PASS_CANDIDATE** | ADR-063 §5 QA | Publish QA **fail-closed** (proposal); if slipped through, governance failure — not ADR conflict |
| SP02-S19 | Hint paraphrases answer (semantic duplicate) | **OPEN** | SP01R1 semantic leakage table | Human review required; automated lint **may miss** — **OPEN** acceptance thresholds (O63-03) |
| SP02-S20 | MCQ hint eliminates three distractors by name | **PASS_CANDIDATE** | ADR-063 §5 forbidden content | Review/QA should reject; server still only returns hint text — no grade |
| SP02-S21 | Student replays captured hint GET response after submit | **PASS_CANDIDATE** | ADR-063 §4 retroactive secrecy | Client may retain stale body; **server** denies new reads; architecture does not promise erasure |
| SP02-S22 | Concurrent hint GET and submit POST | **PASS_CANDIDATE** | ADR-063 §8 TOCTOU | At most one succeeds; post-submit hint GET **deny** |
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
| SP02-S33 | Duplicate idempotent hint GET same question | **PASS_CANDIDATE** | ADR-063 §8 | Same allowlisted body; no mutation |
| SP02-S34 | LearnerAssessmentEvaluation exists; student requests hint | **PASS_CANDIDATE** | ADR-059 evaluation ≠ feedback | Hint path independent; evaluation DTOs **unmodified** |
| SP02-S35 | Attempt uses `LearnerResource` projection — verify `answer`/`explanation` still excluded | **PASS_CANDIDATE** | Backend learner projection; ADR-058 §22 | Assignment/attempt resource **must not** add answer/explanation/hints |

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
| Near-duplicate / paraphrase | S18–S19 | QA gate / OPEN policy |
| Teacher lost class | S29 | 403 |
| Denied content schema (quiz hint) | S31 | DEFER / 404 or feature off |
| P2 AI unapproved | S30 | not available |
| Parent / Principal | S25–S27 | 403 |
| Response replay after submit | S21 | new GET denied |

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

## OPEN items affecting scenario disposition

| ID | Scenario | Decision needed at freeze |
|----|----------|---------------------------|
| O63-03 | S19 paraphrase QA | Minimum automated + human acceptance |
| O63-02 | Teacher authoring adversarial (not expanded above) | Capability naming and denial semantics |

---

## Implementation authorization boundary

Passing this scenario validation **does not** authorize code, OpenAPI edits, schema registration, UI, merge of ADR-063, or December delivery. **Chief review** of exact PR head → **Founder freeze** → **separate engineering workday**.

**Related STOP line:** `AIEOS-V1-SP02 — ADR CANDIDATE + SCENARIO VALIDATION DRAFT PR OPEN / CHIEF REVIEW PENDING / ADR NOT FROZEN / CODE NOT AUTHORIZED / DECEMBER DEVELOPMENT TARGET AT RISK`.
