---
id: ADR-AIEOS-064
title: AIEOS Exact-Version Reviewer & Private Content Read Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: approved
version: 1.0.0
created: 2026-11-24
last_updated: 2026-11-24
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-064 — AIEOS Exact-Version Reviewer & Private Content Read Authority

**Status:** **Frozen / Approved — Founder authorization 2026-11-24**  
**Implementation:** **NOT AUTHORIZED** (governed implementation packets G1–G5 are **separately scoped**)  
**Repository status:** Record deposited on **Draft Architecture PR #71** (`ea-ci03-d1-exact-reviewer-read-candidate`); **merge to `origin/main` pending** — freeze approval is **not** a merge instruction.

**Founder freeze provenance (verbatim instruction, 2026-11-24):**  
> Freeze AIEOS Exact-Version Reviewer & Private Content Read Authority — Approved. Proceed with governed implementation.  
Source: [Architecture PR #71 — Founder freeze comment](https://github.com/eduvijna-ai/eduvijna-architecture/pull/71#issuecomment-7125596146)

**Reviewed proposal SHA (normative source of policy, historical document preserved unchanged):** `096efdc9b2ab5db19d864e62dbe7e8d8458823dd` — `AIEOS/AIEOS-V1-HINT-CI03-D1-REVIEWER-READ-AUTHORITY-PROPOSAL.md` (CI03-D1-R3).  
**Chief architect review:** [CI03-D1-R3 PASS / proposal workday closed](https://github.com/eduvijna-ai/eduvijna-architecture/pull/71#issuecomment-7125481711).  
**G1-D0 source disposition:** [Backend Issue #75 — Chief G1-D0](https://github.com/eduvijna-ai/eduvijna-aieos-backend/issues/75#issuecomment-7125572871).

**Workday:** **CI03-FZ01** — canonical freeze record ([Architecture Issue #70](https://github.com/eduvijna-ai/eduvijna-architecture/issues/70)).

**Related (bodies unchanged):** [ADR-AIEOS-063](ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) · [ADR-048](ADR-048-review-queue-owns-approval.md) · [ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) · [ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md) · [ADR-AIEOS-031](ADR-AIEOS-031-aieos-production-authorization-kernel.md)

**Exact governed pins (CI03 evidence — read-only):**

| Surface | SHA / identifier |
|---------|------------------|
| Architecture `origin/main` (pre-merge base) | `3c0a66aa0a06835e12bb6eeb0da64b7fe147999f` |
| Backend `origin/main` | `5bbc09bc895407b71a61f9ba86a7209ff9c10ffa` |
| Frontend `origin/main` | `e3a6b4a307edf359a00e027fd50f872751934f5b` |
| Frontend Draft PR #53 head (held) | `cd4f8e3134fac3574249d787cd9cb8eb73af88f6` |
| OpenAPI SHA-256 | `0061BCF6065FAFA184F196829A87AF98ADEDFCE6B633D45704141A5B48045D22` |
| Alembic head | `a360s010005` |

**Catalogue note:** **Frozen / Approved = ARCHITECTURE AUTHORITY ONLY.** Does **not** claim Hint PG18 E2E complete, runtime PASS, production readiness, kernel grants, blanket migrations, Infrastructure mutation, or Frontend PR #53 merge. SP02A remains **65 NOT_TESTED + 2 DEFERRED** (S30/S31). No actual HTTP disclosure or production incident is claimed.

---

## Context

ADR-AIEOS-063 requires a **distinct HUMAN reviewer** for hint-bearing `education.worksheet@2` with digest-bound attestation before APPROVE. At Backend pin `5bbc09bc…`, Teacher OS **`teacher_os_review_queue_get`** is **owner-scoped** (`owner_principal_id == caller`), so an independent reviewer receives **404** on cross-owner review detail (PG18 Phase C evidence). `KernelReviewAuthorization` treats `content_id` / `version_id` as **context only** — tenant-wide `content.review.decide` is **not** per-resource read authority. Generic `content_version_get` loads by tenant without caller-scoped worksheet confidentiality (G1-D0 source finding — risk classified, **not** confirmed exploit).

This ADR freezes **cross-owner exact-version reviewer read** (Option A) and **private worksheet read hardening prerequisites** without modifying ADR-AIEOS-063, ADR-048, or ADR-AIEOS-062 bodies.

---

## Decision (frozen architecture authority)

### O64-01 — Dedicated assigned-reviews read (Option A)

Preserve existing owner-only:

- `teacher_os_review_queue_list`
- `teacher_os_review_queue_get`

Add a **separate, non-enumerating** exact-version read for assigned reviewers (indicative):

```http
GET /api/v1/teacher-os/assigned-reviews/{content_id}/versions/{version_id}
```

**Initial scope:** hint-bearing `education.worksheet` `schema_version == 2`, stewardship `IN_REVIEW`, current version only. Owner queue SQL **unchanged** (ADR-048 governs judgment semantics; owner-only detail is **existing implementation**, not new ADR mandate).

### O64-02 — Capability and assignment (no blanket decide)

For this slice, **`content.review.decide` ALLOW** plus **exact active assignment** is the **sole** capability baseline for **both** assigned-reviews **read** and review **commands**. **No separate read capability.** Assignment is **always** required in addition to kernel capability.

### O64-03 — Issuer, reviewer, and actor binding

**Issuer (assign):** ACTIVE HUMAN direct actor == current Content **owner** == immutable hint-version **creator** (`created_by_principal_id`); guarded append @ pin establishes owner/creator alignment (`worksheet_hint_append.py`). Requires existing submit-for-review authority, proposed **`content.review.assign`** (not at pin; **no production grant** without separate authorization), current issuer class authority, reviewer-eligibility validation, designatee **≠** issuer/creator. **No** auto-assign on submit, round-robin, admin inference, or delegated read in this slice.

**Reviewer use (GET, attestation, APPROVE, REJECT, REQUEST_CHANGES):**

1. Server trusted tenant + principal (JWT does not alone establish tenant authority).
2. ACTIVE HUMAN; **`principal_id == effective_actor_id`**.
3. **`principal_id == reviewer_principal_id`** on active `assignment_id` (**before any private payload**).
4. `content.review.decide` ALLOW; mandatory `class_ref`; reviewer ≠ creator when hints present.
5. Third party with `decide` but **not** the assigned reviewer → **DENY** even if another assignment exists.

**Chief acceptance (a):** No private payload until **ALL** reviewer-use gates pass, not caller match alone.

### O64-04 — Assignment SoR: events + current slot

**Immutable events:** `ASSIGNED` / `REVOKED` with stable `assignment_id`; `REVOKED` references **exact** issuance id (never version/reviewer alone).

**Transactional slot:** Content-owned `current_assignment` keyed `(tenant_id, content_id, content_version_id)` → `active_assignment_id`; updated under **Content-head lock** then slot lock; derived from events, **not** a second SoR.

**Policy:** ≤ **7 days** validity from issuance; **one** active slot per version; **no** reassignment after immutable attestation (ADR-063 §5.3 / GCI-G05 — new ContentVersion + fresh cycle). Expiry evaluated under lock. **No** reversible reactivation of revoked issuance.

**Chief acceptance (b):** Stale revoke must clear slot **only** when slot points at the **exact** revoked `assignment_id` — must not clear a newer slot.

**Chief acceptance (c):** No reassignment after attestation; preserve valid terminal APPROVE and publisher rules.

### O64-05 — Mutations, idempotency, publisher

Enforce assignment on **attestation** and **all** review decisions inside transaction; **GET is not authorization proof**.

Bind attestation/decisions/replay to **original `assignment_id`** and authenticated principal. Immutable attestation schema/digest per ADR-063; `assignment_id` persistence is implementation detail.

**Idempotency:** same principal + command fingerprint + same non-revoked/non-expired `assignment_id` + current authority → **metadata-only receipt**, **no duplicate business** attestation/decision/outbox effect.

**Chief acceptance (d):** Independent **security denial audit** must **not** be suppressed on deny.

**Chief acceptance (e):** Issuer and designatee eligibility verified at **issuance and use**.

**Chief acceptance (f):** Completed/consumed assignment may allow lawful terminal replay **without** current `IN_REVIEW` but **does not** grant read/new decisions; replay requires same `assignment_id` and principal.

**Publisher:** `content.publish` after valid APPROVE — publisher **≠** author **and** **≠** reviewer; requires `content.publish` only; **no** current reviewer assignment check after valid APPROVE.

**Hint-free legacy** review: **unchanged**.

### O64-06 — G1 generic worksheet read hardening (prerequisite)

Before enabling assigned-reviews route or claiming worksheet confidentiality complete or resuming Frontend PR #53 E2E:

Harden generic full worksheet **`@1` / `@2`** read: **trusted current tenant + ACTIVE HUMAN + exact current Content owner** (including **historical owned versions**), fail closed on unavailable authority, non-enumerating denial, **no reviewer fallback** on generic route, **no** generic non-worksheet behavior expansion.

**G1 evidence:** pre-fix and post-fix **actual PG18 HTTP** characterization required — **NOT_TESTED** at freeze; no production incident claim.

**Separate disposition (G1-D0):** generic `HttpAppendContentVersionService.append` replay/integrity concern — **source finding**, not confirmed exploit; **not** silently folded into G1 confidentiality contract.

Alternate private payload paths and non-worksheet types: **inventory and govern separately** — **no blanket privacy claim**.

Learner-safe projections and internal typed ports remain **distinct**.

### O64-07 — HTTP and DTO

Non-enumerating **404** for ineligible resources; **401/403** at auth/tenant boundary; **503** sanitized when authority unavailable; no private answer logging. **`ETag`:** `encode_revision_etag(aggregate_revision)` — distinct from attestation `payload_digest`. Review DTO: minimal fields for worksheet hint QA (including question types/options for MCQ), not arbitrary full payload.

Reviewer locators: **bounded handoff** from issuer — no tenant-wide pending list, no token URL, no owner impersonation.

### O64-08 — Implementation staging (not authorized here)

| Stage | Content |
|-------|---------|
| (1) | D1 proposal + this freeze (complete) |
| (2) | Pre-freeze read-only route inventory + non-prod adversarial characterization for G1 contract |
| (3) | Authority freeze on `main` after merge (this ADR) |
| (4) | G1 implementation + HTTP proof |
| (5) | G2–G5: assignment SoR, assign capability, eligibility port, guarded mutations, dedicated GET/OpenAPI/FE, cross-role E2E, controlled PR #53 resume |

**First governed implementation direction approved:** bounded **G1 Backend-only** candidate after this ADR is on `main`. G2–G5 remain **separately scoped**. No production deployment, production grants, blanket migration, provider actions, or automatic merge.

---

## Consequences

| Topic | Consequence |
|-------|-------------|
| ADR-AIEOS-063 hint review UX | Requires assignment + dedicated read; does not weaken §5.3 attestation |
| Teacher OS Review Queue | Owner UX preserved |
| Authorization kernel | Expect `content.review.assign` registration; no tenant-global decide → read |
| Backend | Migration for events + slot; new services/routes; generic GET hardening |
| OpenAPI | New operation + digest pin after implementation authorization |
| Frontend PR #53 | Held until G1 proof + G2–G5 gates |
| SP02A | Unchanged deferral; no scenario promotion from freeze |

---

## Explicit non-authorizations

- Production grants, tenant-wide capabilities, ERP/Admin UI for assignment  
- Merge Frontend PR #53 or rerun its CI from this freeze  
- Claim G1 complete without executed PG18 HTTP proof  
- Modify frozen ADR-AIEOS-063 / ADR-048 / ADR-AIEOS-062 bodies  
- Generic append mutation contract changes under G1 scope  

---

## Historical proposal (non-normative archive)

The reviewed R3 proposal at SHA `096efdc9b2ab5db19d864e62dbe7e8d8458823dd` remains in `AIEOS/AIEOS-V1-HINT-CI03-D1-REVIEWER-READ-AUTHORITY-PROPOSAL.md` as **historical evidence**. **This ADR** is the **authoritative frozen policy** after Founder approval.