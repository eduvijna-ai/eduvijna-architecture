---
id: ADR-AIEOS-064
title: AIEOS Exact-Version Reviewer & Private Content Read Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: approved
version: 1.0.1
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

**Workday:** **CI03-FZ01** → **CI03-FZ01R1** (normative fidelity) — canonical freeze record ([Architecture Issue #70](https://github.com/eduvijna-ai/eduvijna-architecture/issues/70)).

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

### O64-03 — Authority predicates (issue, revoke, reviewer-use)

Normative restatement of approved R3 §§3.2–3.6. JWT supplies identity claims only; **server** establishes trusted execution tenant and capability (ADR-AIEOS-031). **No** stale-cache fallback when School Context or kernel authority is unavailable or malformed — **fail closed** with sanitized **503** where applicable.

#### O64-03-A — Issue predicate (`content.review.assign` command)

**No** pre-existing active assignment required for first issue. All required before `ASSIGNED` event + slot update under Content lock:

| # | Gate |
|---|------|
| 1 | Authenticate → **server** trusted `execution_tenant_id` + principal |
| 2 | Caller: **ACTIVE HUMAN**; `effective_actor_id == principal_id` |
| 3 | Caller == current Content **owner** == immutable hint-version **`created_by_principal_id`** (guarded append @ pin: `worksheet_hint_append.py` @ `5bbc09bc…`) |
| 4 | **Current tenant membership** for issuer |
| 5 | **`content.review.assign` ALLOW** (proposed capability — **not at pin**; **no production grant** without separate authorization) |
| 6 | Current **`content.review.submit` ALLOW** and submit-for-review authority facts satisfied for version |
| 7 | Issuer **current class authority** for mandatory **`class_ref`** from **immutable governed authoring provenance** (not client label) |
| 8 | Version: **current**, hint-bearing **`education.worksheet` `schema_version == 2`**, **`IN_REVIEW`**, **no terminal decision**, **no unconsumed attestation**, slot rules in O64-04 permit new bind |
| 9 | Designatee: **ACTIVE HUMAN**, **current tenant membership**, **`content.review.decide` ALLOW**, passes **Content-facing School Context reviewer-eligibility port** for mandatory `class_ref`, designatee **≠** issuer/creator |

**Reviewer-eligibility port (proposed, not at Backend pin):** reads **trusted current school facts** per [ADR-AIEOS-062](ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md). **Must not** substitute `SchoolContextClassAuthority.require_assignable_class_ref` (Teaching assignment-create). **Must not** create school/ERP master SoR.

**Prohibited at issue:** auto-assign on submit; self-issuance by reviewer; tenant admin inference; round-robin; blanket grants; ERP/admin UI; **delegated read**.

**Issuer invalidation (pending entitlement):** Fail closed if issuer loses ACTIVE HUMAN status, owner/creator alignment, membership, submit/assign capability, or class authority — **no implicit persistence**, **no automatic replacement reviewer**, **no admin bypass**.

#### O64-03-B — Revoke predicate (issuer only)

| # | Gate |
|---|------|
| 1 | Current ACTIVE HUMAN direct actor == original owner-issuer, still current Content owner and immutable version creator, current tenant membership, submit/assign capability and issuer class authority; target reviewer eligibility and new-issuance lifecycle predicates are NOT revoke prerequisites |
| 2 | Target **`assignment_id`** valid for `(tenant, content_id, content_version_id)` |
| 3 | Emit **`REVOKED`** referencing **exact issuance** `assignment_id` (never version/reviewer alone); clear/update slot per O64-04 |

Revoke is **not** blocked because designatee is already ineligible or version is terminal/stale (ineligibility already blocks **new** reviewer effects). **No** reversible reactivation of revoked `assignment_id`.

#### O64-03-C — Reviewer-use predicate (assigned-reviews GET, attestation, **APPROVE / REJECT / REQUEST_CHANGES**)

**Identical core** for read and all mutation commands. **No worksheet private payload may be disclosed until ALL gates succeed.**

| # | Gate |
|---|------|
| 1 | Authenticate → server trusted tenant + principal |
| 2 | Caller: **ACTIVE HUMAN**; **`principal_id == effective_actor_id`** (no delegated read in this slice) |
| 3 | **`principal_id == reviewer_principal_id`** on **active** slot’s **`assignment_id`** |
| 4 | Exact correlation: `tenant_id`, `content_id`, `content_version_id`, **`assignment_id`**, mandatory **`class_ref`** match issuance |
| 5 | Slot **non-revoked**, **non-expired** (server time under lock at effect); issuer consumption eligibility or assignment void rules satisfied |
| 6 | **`content.review.decide` ALLOW**; **current** reviewer membership, kind, decide, and **class eligibility** revalidated |
| 7 | **`principal_id != created_by_principal_id`** when any non-empty hint |
| 8 | Version: **exact current** `content_version_id`, **`IN_REVIEW`**, hint-bearing registered `education.worksheet` schema version 2 with validated hints, undecided for **new** read/mutation effects (lawful terminal replay per O64-05) |
| 9 | **Deny** any third party with `decide` who is **not** the assigned reviewer (class-eligible but unassigned → **DENY**) |

**Chief acceptance (a):** **ALL** gates above before any private payload — not caller match alone.

**Chief acceptance (e):** Issuer and designatee eligibility verified at **issuance and on every protected use**.

### O64-04 — Assignment SoR: immutable events + transactional slot

**Rejected patterns:** time-dependent partial unique index on events alone; mutable fields on “immutable” event rows; second independent SoR; cross-domain direct SQL in application layer.

#### Immutable event log (`content_review_assignment_events` — indicative names)

| Event | Required fields |
|-------|-----------------|
| **`ASSIGNED`** | Stable unique **`assignment_id`**; `tenant_id`, `content_id`, `content_version_id`, `reviewer_principal_id`, `issuer_principal_id`, mandatory **`class_ref`**, server **`issued_at`**, **`valid_until`** (≤ **7 days** from issuance) |
| **`REVOKED`** | Exact target **`assignment_id`** of issuance; server **`revoked_at`**; **`revoked_by_principal_id`** (authorized owner issuer) |

#### Transactional current slot (`content_review_current_assignment` — Content-owned)

- PK `(tenant_id, content_id, content_version_id)` → **`active_assignment_id`** (nullable).
- **Derived** from append-only event history under lock — **not** a separate authority source of truth.
- **Create slot if absent** under Content-head lock.
- **ONE** active slot per exact version; reassign only **before** attestation (O64-04 + ADR-063 §5.3).

#### Atomic rules (Content-head lock → slot/authority lock)

- Evaluate **expiry** against server time **under lock**.
- **New issuance / reissue** only when: no active unconsumed binding, or prior **revoked/expired**, **no** immutable attestation for version, version still **current and eligible** (not terminal/stale for **new** issue).
- **Stale revoke:** clear slot **only** when current slot’s `active_assignment_id` **equals** the revoked issuance id (**Chief acceptance (b)** — must **not** clear a newer slot).
- **Lock order (consistent):** Content aggregate → current-assignment slot → issue / revoke / read / attest / **all** decide effects.
- Local revocation **serializes** with authorization and disclosure/mutation; **re-check** external School Context / kernel **immediately before** protected disclosure or effect — **no** claim of cross-provider atomicity.
- Tenant-consistent FKs, RLS, idempotent issue/revoke, atomic business audit.

**Attestation coupling (ADR-063 §5.3 / GCI-G05):** After immutable unique attestation exists, **only** attestation-bound reviewer may APPROVE with digest/QA; revoked/expired/different reviewer cannot approve or replace; **no** reassignment after attestation — **new ContentVersion** + fresh cycle (**Chief acceptance (c)**). Valid completed approval/publication **unchanged**.

### O64-05 — Mutations, idempotency, publisher, proof obligations

**Current pin (read-only):** `RecordWorksheetLearnerHintAttestationService` and `ReviewCommandService._decide` do **not** check assignment — implementation **must** enforce O64-03-C inside transaction for hint-bearing `@2`.

| Rule | Requirement |
|------|-------------|
| Assignment on mutations | **Inside transaction** before attestation and **all** review decisions (including negative): full O64-03-C + exact **`assignment_id`** on active slot |
| GET vs mutate | Prior GET neither required nor sufficient; GET is not authorization proof |
| Attestation binding | Preserve immutable ADR-063 attestation schema/digest/QA; bind attestation, all decisions and idempotency receipts to **original `assignment_id`** + authenticated principal (`assignment_id` persistence field = implementation detail) |
| APPROVE | Attestation reviewer == slot reviewer AND attestation's original assignment_id == active slot assignment_id; digest/QA interlocks unchanged |
| Idempotency replay | Same principal + exact command fingerprint + **same non-revoked/non-expired `assignment_id`** + **current authority** → **metadata-only receipt**; **no** duplicate business attestation/decision/audit/outbox (**Chief acceptance (d)** preserves **independent security denial audit** on deny) |
| Terminal replay | Completed/consumed assignment may return lawful terminal outcome **without** current `IN_REVIEW` but **does not** grant read/new decisions (**Chief acceptance (f)**) |
| Denied/unauthorized replay | **No** extra attestation, decision, business audit, or outbox; denial audit **not** suppressed |
| Reassign after attestation | **Prohibited** |
| Publisher | After valid APPROVE: **ACTIVE HUMAN** direct actor; **`content.publish` ALLOW** only; publisher **≠** author **and** **≠** reviewer per existing ADR-063 gates; **no** revalidation of **expired** reviewer assignment |
| Hint-free legacy review | **Unaffected** |

#### O64-05-P — Implementation proof obligations (not executed at freeze)

Future disposable PG18 / adversarial HTTP must cover (minimum): third-party `decide` without assignment; wrong `class_ref`; issuer/reviewer authority loss; expiry; revoke; reassignment; **stale revoke** of superseded `assignment_id`; local race (issue/revoke vs read/attest/approve); direct attest/decide without assignment; idempotent replay vs revoked/different `assignment_id`; **owner queue/Library regression**; **learner-safe projection** non-regression. **All NOT_TESTED** until separately authorized runs.

### O64-06 — G1 generic worksheet read hardening (prerequisite)

**Blocks:** enabling assigned-reviews route, claiming worksheet confidentiality complete, resuming Frontend PR #53 E2E.

| Requirement | Detail |
|-------------|--------|
| Generic full worksheet **`@1` / `@2` GET** | **Trusted current tenant** + **ACTIVE HUMAN** + **exact Content owner** for requested `content_id` / `content_version_id` (including **historical owned versions** of owned content) |
| Correlation | Exact tenant/content/version; **hidden-resource 404** for unauthorized/missing |
| Unavailable authority | **Fail closed**; sanitized **503**; **no** private response caching/logging |
| Reviewer fallback | **Denied** on generic route — assigned reviewer **must** use dedicated assigned-reviews GET |
| Non-worksheet | **No** generic behavior expansion from G1 |
| Owner Queue / Library | **Preserve** existing legitimate owner workflows |
| Learner-safe / internal ports | **Preserve** distinct projections and typed ports |
| OpenAPI / Alembic @ freeze | Remain pinned (`0061BCF6…`, `a360s010005`) until **governed** change; **no** G1 migration/DTO shape change **expected** — verify at implementation |
| G1 evidence | **Mandatory** actual PG18 HTTP **pre-fix and post-fix** positive/negative characterization; consumer compatibility proof — **NOT_TESTED** at freeze |
| G1-D0 append/replay | `HttpAppendContentVersionService.append` fingerprint replay / authorization gap — **separate disposition**, source finding **not** confirmed exploit; **not** silent G1 scope expansion |
| Privacy claim | **No blanket** confidentiality claim; residual alternate private paths **inventory + govern separately** |

### O64-07 — HTTP and DTO (assigned-reviews)

| Concern | Rule |
|---------|------|
| Ineligible / missing resource | Non-enumerating **404** (authenticated) |
| Auth / tenant boundary | **401** / **403** as appropriate |
| Authority infrastructure | Uniform sanitized **503**; **no stale-cache fallback** |
| Logging | **No** private answer/explanation bodies in logs or CI artifacts |
| `ETag` | `encode_revision_etag(aggregate_revision)` — **distinct** from attestation `payload_digest` |
| Review DTO | Minimal fields for worksheet hint QA (question types/options for MCQ, stems, `answer`, `explanation`, `learner_hint`, attestation hooks) — not arbitrary full undocumented payload |
| Locator handoff | Reviewer obtains `(content_id, version_id)` via **issuer bounded handoff** only — no tenant-wide pending list, no token-in-URL, no owner impersonation |

### O64-08 — Implementation staging and authorization boundaries

| Stage | Status at freeze deposit |
|-------|---------------------------|
| (1) D1 proposal + freeze record | **Complete** on Draft PR #71 — **merge to `main` pending** |
| (2) Pre-freeze read-only inventory + non-prod adversarial characterization | **Source inventory accepted/closed** (Backend #75); runtime PG18 characterization **NOT_TESTED**, deferred to governed G1 pre/post proof |
| (3) Canonical ADR on `origin/main` | **Pending** Chief merge verification |
| (4) **G1** Backend implementation + PG18 HTTP proof | **NOT AUTHORIZED** until (3) complete; **first code packet** = bounded G1 Backend-only ([Backend Issue #76](https://github.com/eduvijna-ai/eduvijna-aieos-backend/issues/76)) per Founder direction — **released by Chief after merge verification**, not by this deposit |
| (5) G2–G5 | Assignment SoR, assign capability, eligibility port, guarded mutations, dedicated GET/OpenAPI/FE, cross-role E2E, controlled PR #53 resume — **separately scoped**; **do not start** until preceding gate passes |

**Distinguish:** **Architecture freeze approved** ≠ **runtime implemented** ≠ **PG18 PASS** ≠ **production**. No production deployment, production grants, blanket migration authorization, provider actions, or automatic merge. Frontend PR #53 **HELD**. SP02A **65 NOT_TESTED + 2 DEFERRED**.

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

## Historical proposal (immutable evidence archive)

The reviewed R3 proposal at SHA `096efdc9b2ab5db19d864e62dbe7e8d8458823dd` remains byte-for-byte in `AIEOS/AIEOS-V1-HINT-CI03-D1-REVIEWER-READ-AUTHORITY-PROPOSAL.md` as **immutable workday evidence**. **This ADR** is the **authoritative frozen normative policy** (O64-01–O64-08 incorporate R3 + Chief strict interpretations a–f + G1-D0); the archive is not a substitute for ADR text at implementation time.