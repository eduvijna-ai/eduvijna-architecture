# AIEOS-V1-HINT-CI03-D1 — Cross-Owner Reviewer Read-Authority Proposal

**Status:** **PROPOSED / NOT APPROVED / NOT FROZEN / NO CODE AUTHORIZATION**  
**Revision:** **CI03-D1-R3** (final bounded authority clarification on [Architecture PR #71](https://github.com/eduvijna-ai/eduvijna-architecture/pull/71))  
**Provenance:** Reconstructed (2026-11-24) at parent `3c0a66aa…`; R2 @ `702172f…`; **R3** closes literal contract ambiguities R3-A–C only (no scope growth). **Does not modify** frozen [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md), [ADR-048](../decisions/ADR-048-review-queue-owns-approval.md), or [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md).

**Workday linkage:** [Architecture Issue #70](https://github.com/eduvijna-ai/eduvijna-architecture/issues/70) · [Frontend Issue #52](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/issues/52) · [Frontend Draft PR #53](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/53) (OPEN / DRAFT / RED — **no CI rerun authorized here**)

**Exact pins (read-only evidence base):**

| Surface | SHA / identifier |
|---------|------------------|
| Architecture `origin/main` | `3c0a66aa0a06835e12bb6eeb0da64b7fe147999f` |
| Backend `origin/main` | `5bbc09bc895407b71a61f9ba86a7209ff9c10ffa` |
| Frontend `origin/main` | `e3a6b4a307edf359a00e027fd50f872751934f5b` |
| Frontend Draft PR #53 head (PG18 harness) | `cd4f8e3134fac3574249d787cd9cb8eb73af88f6` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Product (historical; connector unverified) | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| OpenAPI SHA-256 | `0061BCF6065FAFA184F196829A87AF98ADEDFCE6B633D45704141A5B48045D22` |
| Alembic head | `a360s010005` |

**PG18 real-stack runs (evidence, not success claims):**

| Run | ID | Relevant outcome |
|-----|-----|------------------|
| First | [45325104208](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/45325104208) | Earlier failure mode (distinct from third run) |
| Second | [45325904897](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/45325904897) | Intermediate failure (distinct evidence) |
| Third | [45327386458](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/45327386458) | Phase A/B PASS; Phase C `REVIEW_DETAIL_HTTP_404`; D–J NOT RUN |

Sanitized artifact `14890905290` (third run): **partial** — does not prove reviewer approve, publish, Student, Assessment, or Improve.

**SP02A disposition:** **65 NOT_TESTED + 2 DEFERRED** (S30/S31). No scenario promotion.

---

## 1. Trigger / immutable evidence (F5)

### 1.1 What PG18 demonstrates today

At Draft PR #53 head, the harness exercises a **baseline worksheet publication path (Phase A)**, **hint-bearing version append plus submit-for-review (Phase B)**, then an **independent reviewer** attempting **owner-scoped** review detail (Phase C). The third run proves cross-owner **404** on `teacher_os_review_queue_get`, not that the reviewer could attest, decide, publish, or reach Student paths.

### 1.2 Current HTTP call chain (owner-filtered review detail)

The PG18 harness drives the **Teacher OS Review Detail route** in the current Frontend source at PR #53 head (product route/page that invokes generated `teacher_os_review_queue_get`, not an architecture-only name). At Backend pin:

1. **Route:** `GET /api/v1/teacher-os/review-queue/{content_id}/versions/{version_id}` — `resolve_trusted_context` then passes `TrustedSecurityContext.principal_id` (`src/aieos/domains/content/api/v1/routes.py` ~767–790).
2. **Service:** `GetTeacherReviewQueueItemService.get` forwards authenticated principal as `owner_principal_id` (`src/aieos/domains/content/application/review_queue.py` L48–69).
3. **Repository:** `SqlAlchemyReviewQueueReadRepository.get_item` requires `contents.owner_principal_id == owner_principal_id`, current version, `IN_REVIEW`, tenant scope, undecided (`src/aieos/domains/content/infrastructure/persistence/repositories.py` ~841–878).

**ADR-048** governs review **judgment** semantics; it does **not** freeze owner-only SQL. Owner-only list/detail is **existing implementation preserved** by Option A, not an ADR-mandated predicate.

PG18 seeds **Content owner ≠ independent reviewer** → expected **404** → gap vs ADR-063 §5.3 distinct reviewer requirement.

### 1.3 Authority trust chain (current platform)

For all proposed operations, preserve the actual ordering:

1. **Authenticate** bearer → identity claims.
2. **Server** resolves **trusted execution tenant** and principal (`TrustedSecurityContext` — `src/aieos/platform/security/context.py` @ pin). **JWT does not by itself establish tenant authority**; tenant access is server-validated membership/grant.
3. **Current** principal kind/classification (ACTIVE HUMAN) and **capability** decisions via `AuthorizationKernel`.
4. **Resource-specific** entitlement (assignment row) for hint-bearing worksheet `@2` cross-owner paths only.

### 1.4 Frozen interlocks (unchanged)

ADR-063 §5.3 / §7.3: reviewer ≠ immutable author; digest-bound attestation before APPROVE; separate publisher; no Review Queue free-text as hint carrier.

---

## 2. Trust subjects and protected data (F1, F5)

| Subject | Role |
|---------|------|
| `execution_tenant_id` | Server-validated tenant; fail closed on mismatch |
| **Issuer** | ACTIVE HUMAN direct actor == Content owner == hint-version creator (§3.2) |
| **Assigned reviewer** | Exactly **one** ACTIVE HUMAN per slot; **`caller principal_id` must equal** `reviewer_principal_id` on use; ≠ creator when hints present |
| `canonical_class_ref` | **Mandatory** — from governed immutable authoring provenance, revalidated at assignment issue and sensitive reads/mutations |
| `content_id`, `content_version_id` | Exact resource keys |
| `payload_digest` | Attestation digest (ADR-063) — **separate** from HTTP `ETag` |
| Private worksheet fields | `answer`, `explanation`, optional `learner_hint`, question type/options for QA |
| Publisher | Distinct; `content.publish` without reviewer assignment after valid APPROVE (§4.4) |

---

## 3. Reviewer-scoped entitlement authority (F1, F2)

### 3.1 Kernel capability: `content.review.decide` only

`KernelReviewAuthorization` @ pin: `content_id` / `version_id` are **resource context only, not authority** (`content_adapters.py` L51–58).

**Proposed narrow rule:** For this hint-bearing worksheet `@2` slice, **`content.review.decide` ALLOW** plus **exact active assignment** is the **sole capability baseline** for **both** assigned-reviews **read** and review **decision** commands. **No additional read capability** in this design.

**Assignment is always required** in addition to capability — never tenant-global decide → all IN_REVIEW worksheets.

### 3.2 Issuer scope (explicit candidate policy)

For the **limited hint-bearing worksheet `@2` slice only**:

| Rule | Requirement |
|------|-------------|
| Who may issue | Current ACTIVE HUMAN **direct actor** == current **Content owner** == immutable hint-version **creator** (`created_by_principal_id`); guarded append @ pin enforces owner alignment and sets creator (`worksheet_hint_append.py` L136–166, L330 @ `5bbc09bc…`) |
| Pre-issuer gates | Existing **submit-for-review** capability; new proposed **`content.review.assign`** (not at pin; no production grant); **current** class issuer authority; reviewer-eligibility port for designatee; designatee **≠** issuer/creator |
| Reviewer count | **ONE** independent eligible HUMAN reviewer designated **explicitly** per exact **current** submitted version |
| Prohibited | Auto-assignment on submit; self-issuance by reviewer; reviewer self-assignment; tenant admin inference; round-robin; blanket grants; ERP/admin UI expansion; **delegated read** in this slice |

**Issuer trust rationale:** Only the hint-version creator-owner who controls submit can bind a reviewer to **that exact version**.

**Issuer invalidation (fail closed):** Pending entitlement becomes **ineligible** when issuer loses ACTIVE HUMAN status, owner/creator alignment, tenant membership, submit or assign capability, or class authority — **no implicit persistence**, no automatic replacement reviewer, **no admin bypass**. Same re-check applies to reviewer: ACTIVE HUMAN, membership, `content.review.decide`, mandatory `class_ref` eligibility.

**Revocation (issuer-only):** Current owner issuer (with assign authority) may **REVOKED** an issuance **even when** the designatee is already ineligible or version is terminal/stale (ineligibility already blocks **new** reviewer effects). **No** reversible reactivation of a revoked `assignment_id`; fresh issuance only under §3.4 rules. Revoke is **not** blocked because the target reviewer can no longer act.

### 3.3 School Context reviewer-eligibility port (new, Content-facing)

**Not present at Backend pin.** Proposed port over **trusted current school facts** ([ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) compatible):

- Confirms designated reviewer is a **current eligible HUMAN** in the **canonical `class_ref`** (from version provenance, not client label).
- Confirms issuer held **current class authority** at issuance.
- **Does not** use `SchoolContextClassAuthority.require_assignable_class_ref` (Teaching assignment-create check) as reviewer permission.
- **Does not** introduce new school master/ERP SoR.

Deny when School Context provider unavailable or malformed — **no fallback**.

### 3.4 Assignment SoR — **C-A** (events + current slot)

**Rejected:** C-B tokens; mutable fields on immutable event rows; **time-dependent partial unique index** on events alone to represent “active” (expiry/revocation are not index-friendly); migration-free claims; second independent SoR.

**Selected minimal shape (proposed, not at pin):**

1. **Immutable event log** `content_review_assignment_events`:
   - **`ASSIGNED`:** stable unique `assignment_id`, `tenant_id`, `content_id`, `content_version_id`, `reviewer_principal_id`, `issuer_principal_id`, `class_ref`, server `issued_at`, `valid_until` (≤ **7 days** — proposed policy).
   - **`REVOKED`:** references **exact** `assignment_id` of the issuance (never version/reviewer alone), `revoked_at`, `revoked_by_principal_id`.

2. **Transactional current slot** `content_review_current_assignment` (Content-owned): PK `(tenant_id, content_id, content_version_id)` → `active_assignment_id` (nullable). **Derived** from event history under lock — **not** a second authority source of truth.

**Atomic update rules (under Content-head lock, then slot/authority lock):**

- Create slot if absent; evaluate **expiry** against server time under lock.
- **New issuance** only when no unconsumed attestation, prior binding revoked or expired, version still current and eligible (not terminal/stale for **new** issue).
- Slot points at one `assignment_id`; history remains append-only for audit.

**Cardinality:** ONE active slot per exact version. Reassign only **before** attestation per §3.5.

**Lock order:** Content aggregate → current-assignment slot → (read/attest/decide body). Same order for issue/revoke. Re-check external School Context / kernel **immediately before** protected payload disclosure or mutation effect — local DB ordering does **not** imply cross-provider atomicity.

**RLS, idempotent issue/revoke, tenant-consistent FKs**; no cross-domain direct SQL in application layer.

**Race / negative proof cases (future):** two distinct reviewers racing issue on same version; expiry mid-read; **stale revoke** of superseded `assignment_id` after reassignment; issuer authority loss; class-eligible `decide` holder **without** assignment denied.

### 3.5 Attestation coupling (ADR-063 §5.3 / GCI-G05)

After immutable **unique** attestation exists for a version:

- **Only** the attestation-bound `reviewer_principal_id` may APPROVE with digest/QA interlocks.
- Revoked/expired assignment or **different** reviewer **cannot** approve or replace attestation.
- Changing reviewer requires **new immutable ContentVersion** and full fresh review cycle.
- **No** retroactive change to valid completed approval/publication.

### 3.6 Predicates — issuance/revocation vs reviewer use

**A. Issue predicate** (assign command — **no** pre-existing active assignment required):

1. Authenticate → server trusted tenant + principal.
2. Caller: ACTIVE HUMAN; `effective_actor_id == principal_id`.
3. Caller == current Content **owner** == `created_by_principal_id` for the hint version.
4. `content.review.assign` ALLOW; submit authority facts satisfied; issuer **class authority** current; version current, eligible for **new** bind (not blocked by existing unconsumed attestation / active slot rules in §3.4).
5. Designatee passes reviewer-eligibility port (`class_ref` from version provenance); designatee **≠** caller/creator.
6. Append `ASSIGNED` + update slot under Content lock.

**B. Revoke predicate** (issuer only):

1. Same issuer identity/authority as §3.2 (owner-issuer with assign capability).
2. Target `assignment_id` valid for version; emit `REVOKED` referencing that id; clear/update slot. **Not** denied because designatee already ineligible.

**C. Reviewer-use predicate** (assigned-reviews **GET**, attestation, **APPROVE / REJECT / REQUEST_CHANGES** — identical core):

1. Authenticate → server trusted tenant + principal.
2. Caller: ACTIVE HUMAN; **`principal_id == effective_actor_id`** (no delegated read in this slice).
3. **`principal_id == reviewer_principal_id`** on the **active** slot’s `assignment_id` (explicit caller-to-assignee binding — mandatory before any private payload).
4. `content.review.decide` ALLOW; tenant/content/version/`class_ref` match issuance; slot not expired/revoked; issuer eligibility rules satisfied for **consumption** (or assignment void).
5. **`principal_id != created_by_principal_id`** when hints present.
6. Version/stewardship checks (`IN_REVIEW` for **new** read/mutation effects; see §4.5 for lawful terminal replay).
7. **Deny** if another principal holds `decide` but is **not** the assigned reviewer (third party with class eligibility still **DENY**).

**No worksheet private payload before step 3 succeeds.**

**External TOCTOU:** Re-evaluate membership, kind, capability, School Context at step immediately preceding disclosure/effect; deny on unavailable/malformed authority.

**HTTP posture:** **404** for ineligible/missing assignment/resource; **401/403** at auth/tenant boundary; **503** sanitized when authority infrastructure unavailable; no response-body logging.

---

## 4. Proposed read operation and mutation consistency (F1, F3, F5)

### 4.1 Option A — separate assigned-reviews GET

Preserve owner-only `teacher_os_review_queue_list` and `teacher_os_review_queue_get`.

```http
GET /api/v1/teacher-os/assigned-reviews/{content_id}/versions/{version_id}
```

Non-enumerating; hint-bearing `education.worksheet` `schema_version == 2`; `IN_REVIEW` only. Operation id indicative (`teacher_os_assigned_review_get`); OpenAPI digest change only after freeze/sign-off.

### 4.2 Reviewer resource locator (no broad discovery)

Assigned reviewer obtains `(content_id, version_id)` only through **authorized bounded handoff** from issuer workflow (explicit designate response or secure product handoff — **no** tenant-wide pending list, **no** token-in-URL bearer, **no** owner impersonation). Publisher uses **existing publication API** without assigned-reviews read.

### 4.3 Review DTO (WorksheetHintReviewPanel alignment)

Minimal private projection sufficient for semantic QA on PR #53 **WorksheetHintReviewPanel**: content/version ids, stewardship/etag fields, per-question `question_id`, stem/prompt, **question type and options** where needed for MCQ QA, `answer`, `explanation`, `learner_hint`, attestation summary hooks — **not** arbitrary full undocumented payload, **not** stem-only insufficient DTO.

### 4.4 ETag and digest

- **`ETag`:** existing `encode_revision_etag(aggregate_revision)` pattern (`src/aieos/platform/api/etag.py` @ pin) — **not** payload digest concatenated with review state.
- **`payload_digest`:** remains attestation field per ADR-063 §5.3.

### 4.5 Direct command bypass — assignment on **all** hint-bearing paths (F3)

**Current pin facts (no assignment check today):**

| Service | Checks assignment? |
|---------|-------------------|
| `RecordWorksheetLearnerHintAttestationService.record` | HUMAN, actor, tenant, capability, locked current version — **no** assignment (`worksheet_hint_attestation_record.py` @ pin) |
| `ReviewCommandService._decide` | Capability before UoW; APPROVE runs hint interlock — **no** assignment (`review.py` @ pin) |

**Proposed mandatory enforcement** for hint-bearing worksheet `@2`:

- **Inside transaction** before attestation and **all** review decisions (including negative): recheck reviewer-use predicate (§3.6C) including **`principal_id == reviewer_principal_id`** and **exact `assignment_id`** on active slot.
- **GET is not authorization proof** for mutation; prior read **insufficient**.
- **Attestation / decisions** bind to **original `assignment_id`** and authenticated principal. Existing immutable attestation **schema/digest** unchanged (ADR-063); any new `assignment_id` persistence field is **later implementation detail**, not claimed at pin.
- **APPROVE:** attestation reviewer == slot reviewer; digest/QA interlocks unchanged.
- **Idempotency replay:** same principal + exact prior command fingerprint + **same non-revoked/non-expired `assignment_id`** + current authority → **metadata-only receipt**, **no** new attestation/decision/audit/outbox side effect. **Deny** on different `assignment_id`, expiry, or revocation.
- **Completed/consumed assignment:** lawful **terminal decision replay** may return prior outcome **without** requiring current `IN_REVIEW`, but **does not** grant read or new decision access. Distinguish completed receipt from unauthorized command.
- **Reassignment after attestation:** prohibited — new ContentVersion + fresh cycle (§3.5). Valid completed APPROVE stands.
- **Publisher:** `content.publish` after valid APPROVE — publisher **≠** author **and** **≠** reviewer; requires `content.publish` only; **no** current reviewer entitlement check.
- **Denied/replayed unauthorized commands:** **no** extra attestation, decision, audit, or outbox records.
- **Hint-free legacy** review: **unaffected**.

**Negative HTTP tests (future):** caller ≠ assigned reviewer despite `decide`; direct command bypass; revoke/expiry races; stale revoke of old `assignment_id`.

---

## 5. Alternatives (resolved — F6)

| Option | Verdict |
|--------|---------|
| A — Separate assigned-reviews GET | **Selected** |
| B — Extend owner queue SQL | **Rejected** |
| Generic `content_version_get` workaround | **Rejected** |
| Separate read capability | **Rejected** for this slice (`decide` + assignment) |
| Auto-assign on submit | **Rejected** |
| C-B delegation tokens | **Rejected** |

---

## 6. Generic private ContentVersion read — prerequisite closure (F4)

### 6.1 Verified call chain @ pin

`content_version_get` route: `resolve_trusted_context` → `GetContentVersionService.get(context.tenant_id, content_id, version_id)` — **caller principal not passed**; service loads by tenant UoW only (`routes.py`, `http_append.py` @ pin). `TrustedSecurityContext` carries tenant/principal from JWT resolution; **does not** embed class/school entitlement.

### 6.2 Threat classification

**`PRIVATE_CONTENT_VERSION_GENERIC_READ_BYPASS`**

| State | Meaning |
|-------|---------|
| Adversarial PG18 executed | **Not yet** |
| Confirmed exploit | **Not claimed** |
| If gap exists today | Same-tenant unauthorized HUMAN **may** receive **200** with **full private worksheet payload** on generic GET — architecture risk, not proven incident |

### 6.3 Corrected threat matrix (post-fix expectations)

| Actor | Generic version GET (today risk) | After hardening (proposed) | Assigned-reviews GET |
|-------|----------------------------------|----------------------------|----------------------|
| Unrelated same-tenant HUMAN | **200 possible** if gap | **404/403** | **404** without assignment |
| Content owner | May work today | **Owner-authorized HUMAN read** for `@1/@2` | N/A unless also assigned reviewer |
| Assigned reviewer | Should not rely on generic | **Deny** full generic private payload; use dedicated endpoint | **200** review DTO |
| Student / Parent / Principal | Deny expected | Deny | Deny |
| Other tenant | Deny | Deny | Deny |

### 6.4 Prerequisite ordering (not optional parallel)

Before **enabling** cross-owner assigned-reviews endpoint or claiming worksheet confidentiality complete or **resuming PR #53 E2E**:

1. **Inventory** every private full-worksheet read route/consumer @ pin.
2. **Execute** real HTTP negative proof on generic GET (and alternates).
3. **Harden** minimum: generic full worksheet `@1/@2` → **owner-only** current authorized HUMAN read; **no** non-owner reviewer fallback on generic route.
4. Document other legitimate consumers; if compatibility requires non-owner read, **separate narrow authorization contract** — no blind global widening.
5. Learner-safe projections / internal typed ports remain **distinct**.

Other private content types: separate inventory/governance; **no** global read widening from this slice.

**Logging:** No private answers in logs or CI artifacts.

---

## 7. Adversarial acceptance matrix (F2, F3, F4 consolidated)

| Case | Expected |
|------|----------|
| Assigned reviewer (`caller == reviewer_principal_id`), active slot, all gates | **ALLOW** GET; mutations with decide |
| `content.review.decide` holder, **not** assigned reviewer | **DENY** (even if class-eligible third party) |
| `content.review.decide` without assignment | **DENY** read and mutations |
| Issuer lost owner/assign/class authority before reviewer acts | **DENY** (pending assignment void) |
| Expired assignment (>7d) | **DENY** |
| Owner revoked assignment | **DENY** |
| Second reviewer while active assignment exists | **DENY** assign; **DENY** read |
| Reviewer = version author with hints | **DENY** |
| Wrong `class_ref` / ineligible reviewer | **DENY** |
| Publisher without decide grant | **DENY** assigned-reviews; publish via publish API after APPROVE |
| Attestation exists; different reviewer | **DENY** APPROVE |
| Attestation exists; assignment revoked | **DENY** further reviewer mutations; valid past APPROVE unchanged |
| Non-current version / terminal decision | **DENY** |
| Owner queue as owner | **Unchanged** |
| Owner queue as non-owner | **404**; use assigned-reviews if assigned |
| Generic GET unrelated HUMAN | **Deny after hardening**; **200 risk before** |
| Revoke races read/attest/approve | **Serialized**; one winner per lock order |
| Student/Parent/Principal/workload/wrong tenant | **DENY** |

---

## 8. Staged gates (F6 / R3-C — non-circular)

**Nothing authorized by this document.** **Merging Draft PR #71 is not** implementation authority, ADR freeze, or proof of G1 completion.

| Stage | Purpose | Status |
|-------|---------|--------|
| **(1) D1 proposal closure** | Chief/Founder review of **this candidate** text | **In progress** (R3) |
| **(2) Pre-freeze evidence (read-only)** | Separately authorized inventory of private worksheet routes + **non-production** adversarial HTTP characterization to **define** G1 contract | **Not started**; **not** required to merge proposal doc |
| **(3) Authority / freeze gate** | Explicit Founder/Chief freeze of security contract | **Not started** |
| **(4) G1 implementation + proof** | Generic private-read hardening per §6 + post-fix negative/positive HTTP proof | **Prerequisite** to enabling assigned-reviews route or resuming PR #53 E2E |
| **(5) G2–G5 implementation** | Assignment SoR/slot, assign capability, eligibility port, guarded mutations → dedicated GET/OpenAPI/FE → cross-role E2E → PR #53 controlled resume | **Blocked behind (3)+(4)** |

**Held:** Draft PR #53 RED; **65 NOT_TESTED + 2 DEFERRED**; historical CI failures unchanged; no grants/production; **no Architecture CI** claimed (none configured on repo unless separately verified).

**Residual (proposed vs current source):**

| Item | Classification |
|------|----------------|
| Owner-only review queue 404 @ PG18 | **Current source fact** |
| Generic GET lacks principal gate @ pin | **Current source fact** |
| `content.review.assign`, slot SoR, eligibility port | **Proposed** (not at pin) |
| Adversarial generic GET executed | **Not done** |
| Assign/revoke HTTP operation ids | **Later implementation detail** |

**CI02R1:** `pkV1HintE2e.pins.test.ts` — recorded, not edited.

---

## 9. Decision ledger (F6)

| Item | Disposition |
|------|-------------|
| Implementation | **NOT_IMPLEMENTED** |
| ADR freeze | **None** |
| Option A + C-A | **Chief accepted in substance** (R2); R3 clarifies actor/slot/receipt gates — **candidate only**, not frozen |
| D1 PR merge | **Does not** authorize code, G1, or ADR freeze |
| Issuer / capability / class rules | **Closed in this doc** (candidate policy) |
| Dedicated read capability | **Not required** (`decide` + assignment) |
| Generic GET hardening | **Prerequisite G1**, not parallel optional |
| Risk owner | Enterprise Architecture / Backend security |

---

## 10. Review closure maps

### 10.1 F1–F6 (R2)

| Finding | Primary sections |
|---------|------------------|
| **F1** Issuer, `content.review.assign`, decide-only, mandatory class, eligibility port | §3.1–3.3, §4.1 |
| **F2** Append-only lifecycle, one active/version, 7d, locks, attestation coupling | §3.4–3.5, §3.6, §7 |
| **F3** Mutation enforcement, idempotency, publisher separation | §4.5, §7 |
| **F4** Generic GET inventory, corrected matrix, G1 prerequisite | §6 |
| **F5** Auth chain, ETag, DTO, PG18 phases/runs, ADR-048 note, FE attribution | §1, §2, §4.2–4.4 |
| **F6** Staged gates, resolved alternatives, residual risks | §5, §8–9 |

### 10.2 R3-A–C (this revision)

| Control | Primary sections |
|---------|------------------|
| **R3-A** Caller == assigned reviewer; issue vs use predicates; issuer owner==creator; revoke rules | §3.2, §3.6 |
| **R3-B** Events + current slot; `assignment_id`; no time-dependent partial index; races | §3.4, §7 |
| **R3-C** Non-circular stages (1)–(5); source vs proposed; remove F8 label | §8, §7, §9 |

---

## Source path index (Backend @ `5bbc09bc895407b71a61f9ba86a7209ff9c10ffa`)

| Topic | Path |
|-------|------|
| Trusted context | `src/aieos/platform/security/context.py` |
| Kernel review auth | `src/aieos/platform/security/authorization/content_adapters.py` |
| Owner review queue | `src/aieos/domains/content/application/review_queue.py` |
| Review queue SQL | `src/aieos/domains/content/infrastructure/persistence/repositories.py` |
| Review commands | `src/aieos/domains/content/application/review.py` |
| Hint attestation | `src/aieos/domains/content/application/worksheet_hint_attestation_record.py` |
| Hint append (owner/creator) | `src/aieos/domains/content/application/worksheet_hint_append.py` |
| Generic version get | `src/aieos/domains/content/application/http_append.py`, `routes.py` |
| ETag helper | `src/aieos/platform/api/etag.py` |
| Teaching class authority | `src/aieos/domains/teaching/application/school_context.py` |

---

**Terminal classification:** `CI03-D1-R3 — FINAL PROPOSAL CLARIFIED / DRAFT PR #71 / READY FOR CHIEF CLOSURE / NOT FROZEN / NO CODE`