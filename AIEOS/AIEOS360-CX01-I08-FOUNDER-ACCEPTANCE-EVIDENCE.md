---
id: AIEOS360-CX01-I08
title: AIEOS360 Client Showcase — Founder Acceptance Evidence Dossier
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: acceptance-pending
version: 1.0.0
created: 2026-11-02
last_updated: 2026-11-02
programme: AIEOS360-CX01 — Client Showcase (target 2026-11-20 development readiness)
workday: I08 — Founder Client Showcase acceptance + architecture closeout (CX01-C01)
governance_authorization: Founder 2026-11-02 — “Go ahead I08 implementation, tasklist.”
linked_issues:
  - https://github.com/eduvijna-ai/eduvijna-architecture/issues/50
  - https://github.com/eduvijna-ai/eduvijna-product/issues/2
linked_product_record: product-architecture/aieos360/AIEOS360-CX01-I08-CLIENT-SHOWCASE-ACCEPTANCE.md
acceptance_contract: AIEOS360-CX01-W01 §1.3
---

# AIEOS360-CX01-I08 — Founder Acceptance Evidence Dossier

**Identity:** `AIEOS360-CX01-I08`  
**Mode:** Architecture acceptance records only — **does not authorize application code, merges, or production.**  
**Terminal dossier status:** **ACCEPTANCE EVIDENCE READY — FOUNDER SIGN-OFF PENDING**  
**Explicit non-claims:** **AIEOS 360 CLIENT SHOWCASE READY** is **not** declared here. **PRODUCTION READY = NO.**

---

## I08-01 — Governed intake and exact source identity

**Gate repeated:** 2026-11-02 (Cursor Cloud Agent, before branch creation)

| Authority | Expected `origin/main` | Actual | Result |
|-----------|------------------------|--------|--------|
| Architecture `eduvijna-architecture` | `491295c3cf0a151f31686a6a2e1a2176cd92c782` | **MATCH** | PASS |
| Product `eduvijna-product` | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | PASS |
| Backend `eduvijna-aieos-backend` | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | PASS |
| Frontend `eduvijna-aieos-frontend` | `569ef8be46617ab1412ddb3f5a0214c40bdb946b` | **MATCH** | PASS |
| Infrastructure `eduvijna-aieos-infrastructure` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | PASS |
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json` on Backend pin) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **Not re-hashed in I08 scope** (read-only pin unchanged at Backend `637583f42…`; same pin as W01/S04 closeout) | PASS (pin continuity) |
| Alembic head | `a360s010004` | **Not re-verified in I08 scope** (read-only pin unchanged) | PASS (pin continuity) |

**Architecture / Product writable worktrees:** clean tracked tree at gate time.  
**I07 engineering close:** [Frontend Issue #46](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/issues/46) **CLOSED**; [Frontend PR #47](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/47) **MERGED** at Frontend pin above; [post-merge verification comment](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/47#issuecomment-6572411930).  
**Merge parents (Frontend #47):** parent1 `e7ff20b84ce8edabf1c849e8c19a7340cbaebcfa`; parent2 `0994002b48b3135dc175269534eb8ce6353eb855`; merged **2026-11-02T08:05:08Z**.  
**Delivery circuit breaker:** [AIEOS-GOV-CI01](https://github.com/eduvijna-ai/eduvijna-architecture/issues/49) — observed; no second consecutive failed push in I08 (records-only).  
**Historic W01 Issue #47:** remains **OPEN** by history — not closed by I08.

**Gate result:** **PASS — I08 AUTHORIZATION VALID**

---

## I08-02 — W01 §1.3 six-criterion acceptance matrix

Governing contract: [AIEOS360-CX01-W01 §1.3](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)

| # | W01 criterion | Classification | Evidence summary |
|---|---------------|----------------|------------------|
| 1 | Deterministic rehearsal — reset/reseed canonical scenario on shared local/non-production data | **ENGINEERING_PROVEN** | I07 integrated proof on shared PostgreSQL 18 with **FakeStructuredModelGateway** deterministic kit; mandatory Backend Fake PreparationKit proof **PASS**; reset/start/status/stop scripts documented in Frontend [presenter preflight](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md). **FOUNDER_DEMONSTRATED:** not recorded. |
| 2 | Role entry points — Teacher, Student, Principal, Parent on **same** coherent school story | **ENGINEERING_PROVEN** | I07 same-run 10/10 phases; coherent `DevelopmentCoherentSchoolContextProvider` (ADR-AIEOS-062); four OS shells + showcase launcher from I01–I06 at Frontend pin. **FOUNDER_DEMONSTRATED:** not recorded. |
| 3 | Human walkthrough **without** engineering-only DEV session wiring **during** the visible story | **PENDING_FOUNDER** | Preflight requires **pre-connected memory-only** role tabs before audience ([I07 preflight](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md)). CI does not substitute for Founder in-room walkthrough. No Founder attestation captured. |
| 4 | Showcase presentation — Student / Principal / Parent at client-demo bar | **ENGINEERING_PROVEN** (functional + I02–I05 uplift merged) · **PENDING_FOUNDER** (presentation acceptance) | I07 UX phases I02–I05 merged in PR #47; automated guards PASS. TOS-CX01 bar applies fully to Teacher only (historic Founder acceptance **2026-09-07**). Cross-role polish is **implemented in engineering sense**; **client-demo confidence** awaits Founder observation. |
| 5 | Mode clarity — deterministic vs real-AI explicit and safe | **ENGINEERING_PROVEN** | I06 mode governance merged; Provider Aggregator read-only; default rehearsal path **DETERMINISTIC (Fake)** per I07 proof. **REAL_AI** whole-vertical live provider generation **PENDING** (see gaps). TOS-CX01 Teacher-only Groq Real-AI (**2026-09-07**) is **historic separate** proof — not whole-AIEOS360 cross-role live generation. |
| 6 | Evidence — integrated real-stack proof retained; **no** production readiness claim | **ENGINEERING_PROVEN** | Post-merge CI [41410487754](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/41410487754) **SUCCESS** 9/9; I07 **10/10 PASS**; CodeQL [41410487287](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/41410487287) **SUCCESS** 3/3. This dossier and closeout repeat **Production Ready = NO**. |

**Legend:** `ENGINEERING_PROVEN` | `FOUNDER_DEMONSTRATED` | `PENDING_FOUNDER` | `GAP` | `DEFERRED_NOT_REQUIRED`

---

## I08-03 — Canonical school narrative (`AIEOS360-CX-SCENARIO-01`)

Frozen scenario — **no new domain semantics** in I08.

| Step | Role | Beat | Authority |
|------|------|------|-----------|
| 1 | Teacher (HUMAN) | Prepare six-artifact kit → Review → Approve → Publish | TOS-CX01 / ADR-AIEOS-052 |
| 2 | Teacher | Assign published content to Grade5A `class-5a` | ADR-AIEOS-053 |
| 3 | Teacher | (Optional) Teach + class Assess | ADR-AIEOS-054/055 — **optional**, not fabricated in I07 mandatory path |
| 4 | Student A | Start → Save → Submit | ADR-AIEOS-058 |
| 5 | System | Current-policy `LearnerAssessmentEvaluation` | ADR-AIEOS-059 |
| 6 | Teacher | Assessment Intelligence → deliberate Improve | ADR-AIEOS-059 → ADR-AIEOS-056 |
| 7 | Principal | Refresh School Intelligence aggregates | ADR-AIEOS-060 — DERIVED_ON_REQUEST |
| 8 | Parent | Home → authorized child lifecycle read | ADR-AIEOS-061 — `EVALUATION_EXISTENCE = NO` |
| 9 | Coherence | Same ClassRef / learner facts across roles | ADR-AIEOS-062 |
| — | Student B / wrong-tenant | Denied / concealed | Privacy-adversarial guards in I07 proof |

---

## I08-04 — Acceptance evidence provenance register

**Same-run proven (I07 integrated proof — Frontend merge `569ef8be…`, CI run 41410487754):**

| Phase | Scope | Provenance |
|-------|-------|------------|
| Mandatory Fake PreparationKit | Backend proof job in Frontend CI | Same run 41410487754 |
| I07-01 … I07-10 | Integrated cross-role product spec phases | Same run; 10/10 PASS |
| Privacy / adversarial | Student B, wrong-tenant, Parent evaluation absence | Asserted in I07 harness (same run) |
| I01R9 reset×2 + lifecycle | Environment reset discipline | I07 coverage per Frontend docs |
| I06 mode truth | DETERMINISTIC default in integrated proof | Same run |

**Historic separate proven (do not merge into same-run claim):**

| Evidence | Pin / note |
|----------|------------|
| S04-I03 integrated cross-role E2E | Frontend `80125be6…` era — superseded for showcase by I07 at `569ef8be…` |
| S01-I05 Improve handoff E2E | Separate proof map per W01 §3.3 |
| TOS-CX01 Founder Real-AI Teacher path | **2026-09-07** — Teacher-only |
| [I07 coverage matrix](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-COVERAGE-MATRIX.md) | Historic `pending green CI` text at commit time — read with post-merge green logs **41410487754**; matrix **not silently rewritten** |

**Human-only / not yet proven:**

| Item | Status |
|------|--------|
| Founder in-person presenter walkthrough | **NOT RUN / NOT RECORDED** |
| Client audience observation | **NOT RECORDED** |
| Whole-AIEOS360 REAL_AI live provider generation | **PENDING** |

**Policy:** No raw DB identities, bearer tokens, fixture learner IDs, or credential screenshots in this dossier.

---

## I08-05 — Reproducible safe Founder operator preflight

**References (read-only, Frontend pin):**

- [AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-PRESENTER-PREFLIGHT.md)
- [AIEOS360-CX01-I07-FOUNDER-CUE-SHEET.md](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-FOUNDER-CUE-SHEET.md)

**Confirmed requirements (documentation — not attestation that Founder executed):**

| Requirement | Status |
|-------------|--------|
| Local **NON_PRODUCTION** disposable PostgreSQL 18 only | Documented |
| Owned reset / start / status / stop; 8 healthy managed processes | Documented |
| Four role tabs **explicitly session-connected in memory** before live audience | Documented |
| No tokens visible in client-facing UI during walkthrough | Documented |
| Safe recovery and teardown | Documented |
| **No SSO**; no automatic impersonation | Accepted limitation |

---

## I08-06 — Demo mode selection (recorded for Founder rehearsal)

| Mode | Description | I08 record |
|------|-------------|------------|
| **Mode A (default)** | New **Fake** deterministic kit matching I07 integrated proof | **Recommended default** for Founder rehearsal; matches CI 41410487754 proof class |
| **Mode B** | Seeded approved-but-unpublished synthetic worksheet to narrate preconditions | Allowed alternative; **do not mix ContentVersion IDs** across modes in one story |

**Truth labels:**

- I07 automated proof = **DETERMINISTIC Fake** — **REAL_AI LIVE GENERATION PENDING** for full cross-role paid provider path.
- Provider Aggregator remains runtime observability truth — not a substitute for generated-content proof class.

**No real paid provider call under I08** without new explicit safety/provider authorization.

---

## I08-07 — Founder manual rehearsal checklist (observer)

**Outcome key:** `PASS` | `PARTIAL` | `FAIL` | `NOT RUN` — **Cursor does not enter PASS on Founder's behalf.**

| Beat | Role | Expected entry / observable | Outcome | Evidence note |
|------|------|----------------------------|---------|---------------|
| 1 | Teacher | Prepare → Review → Publish; readable kit | **NOT RUN** | |
| 2 | Teacher | Assign Grade5A | **NOT RUN** | |
| 3 | Student A | Start / Save / Submit | **NOT RUN** | |
| 4 | Teacher | Assessment Intelligence → Improve | **NOT RUN** | |
| 5 | Principal | School Intelligence refresh; aggregates only | **NOT RUN** | |
| 6 | Parent | Child lifecycle read; no evaluation detail | **NOT RUN** | |
| 7 | Negative | Student B denied; wrong-tenant denied | **NOT RUN** | |
| 8 | Continuity | Scenario map / handoffs; no live DEV paste | **NOT RUN** | |
| 9 | Presentation | Client-device readability; role transitions | **NOT RUN** | |

**Cue sheet:** [Founder cue sheet](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/569ef8be46617ab1412ddb3f5a0214c40bdb946b/docs/AIEOS360-CX01-I07-FOUNDER-CUE-SHEET.md)

---

## I08-08 — Actual human pass / blocker capture

**FOUNDER ACCEPTANCE PENDING**

| Topic | Recorded Founder statement |
|-------|------------------------------|
| Role navigation confidence | *None supplied* |
| Presentation bar (Student / Principal / Parent) | *None supplied* |
| Complete single-school story correctness | *None supplied* |
| No DEV session paste during visible walk | *None supplied* |
| Client-demo readiness | *None supplied* |

No invented screenshots, quotes, attendance, or client testimony.

---

## I08-09 — Privacy and authority review

| Check | Engineering proof | UI/API semantics (no learner-private disclosure) |
|-------|-------------------|--------------------------------------------------|
| Parent sees assigned child lifecycle only | I07 same-run | `EVALUATION_EXISTENCE = NO` per ADR-AIEOS-061 |
| Principal sees aggregate DERIVED_ON_REQUEST | I07 same-run | No learner score / mastery / ranking in v1 |
| Student B denied | I07 adversarial phase | Generic concealment |
| Wrong-tenant denied | I07 adversarial phase | Fail closed |
| Admin / ERP facts | External current authority | ADR-AIEOS-062; no Admin OS |

---

## I08-10 — Presentation and continuity acceptance

| Area | Engineering (I02–I05 + I03 shell) | Founder observation |
|------|-----------------------------------|---------------------|
| Teacher entry | Merged | **PENDING** |
| Student / Principal / Parent entry | Merged | **PENDING** |
| Cross-role scenario map / handoffs | Merged (I03) | **PENDING** |
| Responsive client-device bar | Implemented per I07 scope | **PENDING** |

Material UX blockers discovered in Founder walkthrough → propose **new governed work package**; not undocumented I08 code change.

---

## I08-11 — Explainable AI / educational semantics and caveats

**Lifecycle (binding):**

`Generated ≠ Approved ≠ Published ≠ Assigned ≠ Started ≠ Submitted ≠ Evaluated ≠ Mastered`

**Teaching loop:**

`Taught ≠ Assessed ≠ Mastered` — optional Teach/Assess not required for showcase spine.

**Assessment semantics:**

- Human / class `MIXED` classroom assessment is **not** learner mastery outcome.
- AI Assistant v1 = **READ / REASON / SUGGEST** only (ADR-AIEOS-057).
- Bounded DEV04 preparation orchestration ≠ general agent platform; **Planner Agent** and broad **Agents/MCP** deferred (**2027-04-23**).

---

## I08-12 — Gap, exception and risk register

| ID | Gap / limitation | Class | Owner / decision |
|----|------------------|-------|------------------|
| G-01 | Founder human walkthrough not recorded | **BLOCKER_FOR_SHOWCASE** (for unconditional READY) | Founder — separate acceptance message |
| G-02 | DEV session pre-connect (memory-only tabs) | **ACCEPTED_LIMITATION** | NON_PRODUCTION composition |
| G-03 | No SSO / production Principal or Parent auth | **ACCEPTED_LIMITATION** | Deferred production |
| G-04 | Mode B synthetic worksheet narrative | **ACCEPTED_LIMITATION** if Mode B chosen | Founder mode choice |
| G-05 | Whole-AIEOS360 REAL_AI cross-role live generation | **DEFERRED_ORIGINAL_SCOPE** / **PENDING** | Separate authorization |
| G-06 | Production ERP/SIS, Admin OS, Agents/MCP, EIS complete | **DEFERRED_ORIGINAL_SCOPE** | Locked 2027 programme |
| G-07 | CI PASS ≠ in-room rehearsal | **ACCEPTED_LIMITATION** | Governance |

No new ADR opened in I08.

---

## I08-13 — Readiness verdict matrix (separate declarations)

| Verdict | Status |
|---------|--------|
| **I07 ENGINEERING COMPLETE** | **YES** — Issue #46 closed; PR #47 merged; CI 41410487754 |
| **I08 ACCEPTANCE EVIDENCE READY** | **YES** — this dossier + Product record + draft PRs |
| **AIEOS 360 CLIENT SHOWCASE READY** | **NO** — requires explicit Founder acceptance per W01 §1.3 |
| **AIEOS v1 DEV READY** | Separate programme — target **2026-12-18**; not auto-started |
| **PRODUCTION READY** | **NO** |

---

## I08-14 — Dossier status

| Field | Value |
|-------|-------|
| Document status | **`acceptance-pending`** |
| Founder signature block | **PENDING** — see §I08-18 |
| Architecture closeout | [AIEOS360-CX01-C01-CLIENT-SHOWCASE-CLOSEOUT.md](AIEOS360-CX01-C01-CLIENT-SHOWCASE-CLOSEOUT.md) — **PROPOSED / PENDING FOUNDER ACCEPTANCE** |

---

## I08-15 — CX01-C01 closeout pointer

Conditional programme closeout drafted separately; **does not** alter W01 historical baseline truth or Frozen ADR bodies.

---

## I08-16 — Architecture & Product record sync

| Repo | Branch (Cursor) | Base | Purpose |
|------|-----------------|------|---------|
| Architecture | `cursor/aieos360-cx01-i08-founder-acceptance-architecture-closeout-f7d1` | `491295c3…` | This dossier, C01 closeout, current-state/roadmap/journey/changelog |
| Product | `cursor/aieos360-cx01-i08-product-acceptance-record-f7d1` | `b4b3048f…` | Product acceptance record + index link |

Cross-links in PR descriptions; **no cross-repo merge** before independent review.

---

## I08-17 — Validation checklist (pre-merge review)

| Check | Result |
|-------|--------|
| Markdown internal links | To be verified in CI/review |
| W01 six criteria addressed | **YES** — §I08-02 |
| No secrets / synthetic PII | **YES** — policy in §I08-04 |
| No Frozen ADR body edits | **YES** |
| No Backend/Frontend/Infra/OpenAPI/Alembic mutation | **YES** — records only |
| Status alignment Architecture ↔ Product | **YES** — both **acceptance-pending** |
| AIEOS-GOV-CI01 | Observed for I08 pushes |

---

## I08-18 — Founder showcase acceptance gate

**STOP.** After draft PR submission:

1. Founder completes real presenter walkthrough (or supplies sanitized observation record).
2. Founder approves limitations, demo mode, and open gaps in an **explicit separate message**.
3. Only then authorize exact-head Architecture/Product PR merges, post-merge verification, and I08 issue closure.

**Without step 1–2:** [Architecture Issue #50](https://github.com/eduvijna-ai/eduvijna-architecture/issues/50) and [Product Issue #2](https://github.com/eduvijna-ai/eduvijna-product/issues/2) remain **OPEN**. **Do not** declare **AIEOS 360 CLIENT SHOWCASE READY**.

### Founder acceptance placeholder

| Field | Value |
|-------|-------|
| Founder name | _Pending_ |
| Date (UTC) | _Pending_ |
| Mode A / B | _Pending_ |
| W01 criteria disposition | _Pending_ |
| Authorized programme declaration | _Pending_ |

---

## Related

- [AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md](AIEOS360-CX01-W01-CLIENT-SHOWCASE-GAP-BASELINE.md)
- [AIEOS360-CX01-C01-CLIENT-SHOWCASE-CLOSEOUT.md](AIEOS360-CX01-C01-CLIENT-SHOWCASE-CLOSEOUT.md)
- [AIEOS-CURRENT-STATE.md](AIEOS-CURRENT-STATE.md)
- [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md)
