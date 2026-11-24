# AIEOS-V1-HINT-CI03-D1 — Cross-Owner Reviewer Read-Authority Proposal

**Status:** **PROPOSED / NOT APPROVED / NOT FROZEN / NO CODE AUTHORIZATION**  
**Revision:** **CI03-D1-R2** (Chief consolidated correction on [Architecture PR #71](https://github.com/eduvijna-ai/eduvijna-architecture/pull/71))  
**Provenance:** Initial candidate **reconstructed** (2026-11-24) at parent `3c0a66aa…`; prior unreachable commit `cfbed35d…` never on GitHub. **This revision** closes Chief findings F1–F6 in one pass. **Does not modify** frozen [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md), [ADR-048](../decisions/ADR-048-review-queue-owns-approval.md), or [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md).

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
| **Issuer** | ACTIVE HUMAN **Content owner** acting as **direct actor** with verified creator/owner provenance (see §3.2) |
| **Assigned reviewer** | Exactly **one** ACTIVE HUMAN per version binding; ≠ `created_by_principal_id` when hints present |
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
| Who may issue | Current ACTIVE HUMAN **Content owner** (direct actor; creator provenance verified against `created_by_principal_id` / ownership facts) |
| Pre-issuer gates | Existing **submit-for-review** authority; current **owner** stewardship; **trusted authoring class authority** for the version’s provenance `class_ref`; new proposed **`content.review.assign`** capability (code-governed; **not registered at pin**; **no production grant** before separate authorization) |
| Reviewer count | **ONE** independent eligible HUMAN reviewer designated **explicitly** per exact **current** submitted version |
| Prohibited | Auto-assignment on submit; self-issuance by reviewer; reviewer self-assignment; tenant admin inference; round-robin; blanket grants; ERP/admin UI expansion in this slice |

**Issuer trust rationale:** Only the steward who submitted the version for review can bind a reviewer to **that exact version**, limiting cross-owner read to an owner-initiated, auditable delegation.

**Issuer invalidation (fail closed):** If before reviewer action the issuer loses **current** owner status, **`content.review.assign`**, or **authoring/class authority** required at issuance, any **pending** assignment for that version is **ineligible** (deny read/mutations; no implicit persistence). Re-validation at sensitive points (§3.6).

### 3.3 School Context reviewer-eligibility port (new, Content-facing)

**Not present at Backend pin.** Proposed port over **trusted current school facts** ([ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) compatible):

- Confirms designated reviewer is a **current eligible HUMAN** in the **canonical `class_ref`** (from version provenance, not client label).
- Confirms issuer held **current class authority** at issuance.
- **Does not** use `SchoolContextClassAuthority.require_assignable_class_ref` (Teaching assignment-create check) as reviewer permission.
- **Does not** introduce new school master/ERP SoR.

Deny when School Context provider unavailable or malformed — **no fallback**.

### 3.4 Assignment SoR — **C-A** (append-only lifecycle)

**Rejected:** C-B bearer tokens; mutable `revoked_at` on a single “immutable” row; migration-free claims.

**Selected model:** Content-owned **append-only** `content_review_assignment_events` (names indicative):

| Event | Records |
|-------|---------|
| `ASSIGNED` | `tenant_id`, `content_id`, `content_version_id`, `reviewer_principal_id`, `issuer_principal_id`, `class_ref`, server `issued_at`, `valid_until` (**max 7 calendar days** from issuance — proposed policy) |
| `REVOKED` | Same keys + `revoked_at`, `revoked_by_principal_id` (authorized owner issuer) |

**Cardinality:** **ONE active assignment** per exact `content_version_id` (not per reviewer row). Reassign only **before** attestation: revoke/expiry, then fresh explicit `ASSIGNED` under new grant.

**Enforcement:** PostgreSQL unique partial index / constraint for single active binding; transactional lock **Content aggregate first**, then assignment authority row — consistent for issue, revoke, read, attest, decide.

**Automatic ineligibility:** Non-current version; terminal review decision; expiry; revocation; issuer/reviewer authority loss at re-check.

**RLS:** Tenant-safe exact refs. Idempotent assign/revoke. Audit trail append-only.

**PG18 / dev:** Explicit non-prod fixture or seed insert **only** under separately governed grant — not authorized here.

### 3.5 Attestation coupling (ADR-063 §5.3 / GCI-G05)

After immutable **unique** attestation exists for a version:

- **Only** the attestation-bound `reviewer_principal_id` may APPROVE with digest/QA interlocks.
- Revoked/expired assignment or **different** reviewer **cannot** approve or replace attestation.
- Changing reviewer requires **new immutable ContentVersion** and full fresh review cycle.
- **No** retroactive change to valid completed approval/publication.

### 3.6 Authorization evaluation order (read and mutations)

1. Authenticate → **server** trusted tenant + principal.
2. ACTIVE HUMAN classification; actor alignment on commands.
3. `content.review.decide` (reviewer) or `content.review.assign` (issuer on assign only).
4. Load **current active** assignment for `(tenant, content_id, version_id)` — not expired, not revoked, issuer still eligible.
5. Reviewer-eligibility port: reviewer + mandatory `class_ref`.
6. Version: current, `IN_REVIEW`, worksheet `@2` hint-bearing scope.
7. `reviewer_principal_id != created_by_principal_id` when any non-empty hint.

**External TOCTOU:** DB locks do **not** make external School Context / kernel providers atomic. Re-evaluate membership, kind, capability, and School Context at sensitive points; deny on staleness.

**HTTP posture:** Same **404** for authenticated but ineligible/missing assignment/resource. **401/403** only at authentication/tenant boundary. Uniform sanitized **503** when authority infrastructure unavailable (no private payload). No response-body logging.

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

- **Inside transaction** before **attestation record**, **APPROVE**, **REJECT**, and **REQUEST_CHANGES**: recheck **exact active assignment** and current issuer/reviewer authority.
- **GET is not authorization proof** for mutation; prior successful read **insufficient**.
- **APPROVE:** same reviewer as immutable attestation; digest/QA; actor alignment.
- **Idempotency:** identical authorized replay → metadata-only, no duplicate effects; deny when entitlement revoked/expired; distinguish legitimate terminal receipt from unauthorized replay (do not blindly require `IN_REVIEW` on completed decision receipt).
- **Publisher:** `content.publish` after valid APPROVE — **does not** revalidate expired reviewer assignment; publisher **does not** need reviewer assignment or `content.review.decide`.
- **Hint-free legacy** review commands: **unaffected**.

**Negative HTTP tests (future):** direct POST decide/attest without assignment; reviewer mismatch; revocation/expiry between read and approve; race revoke vs read/attest/approve.

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

## 7. Adversarial acceptance matrix (F2, F3, F4, F8 consolidated)

| Case | Expected |
|------|----------|
| Assigned reviewer, active assignment, all gates | **ALLOW** assigned-reviews GET; mutations if decide + assignment |
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

## 8. Implementation DAG and freeze readiness (F6)

**Nothing authorized by this document.**

| Order | Gate |
|-------|------|
| **G0** | This proposal reviewed; Founder/authority freeze as applicable (**not** this PR merge) |
| **G1** | Generic private-read inventory + HTTP negative proof + bounded hardening (**G1 blocks G3–G5**) |
| **G2** | Assignment SoR (append-only), `content.review.assign`, reviewer-eligibility port, guarded mutations (migration, audit, PG18 fixtures under grant) |
| **G3** | Assigned-reviews GET + OpenAPI + typed Frontend client |
| **G4** | Cross-role positive/negative E2E (matrix §7 + §6) |
| **G5** | Fresh PR #53 re-pin, harness scope correction, controlled resume |

**Held:** Draft PR #53; **65 NOT_TESTED + 2 DEFERRED**; no new grants/production; no fake completion.

**Residual risks (honest):**

- School Context port semantics need implementation-time ADR-062 alignment proof.
- Exact assign/revoke HTTP surface not specified here (later implementation packet).
- Adversarial generic GET outcomes remain **unexecuted** until G1.

**CI02R1:** `pkV1HintE2e.pins.test.ts` whitelist note on PR #53 — recorded, not edited.

---

## 9. Decision ledger (F6)

| Item | Disposition |
|------|-------------|
| Implementation | **NOT_IMPLEMENTED** |
| ADR freeze | **None** |
| Option A + C-A | **Chief accepted in principle**; design **not freeze-ready** until G0–G1 evidence |
| Issuer / capability / class rules | **Closed in this doc** (candidate policy) |
| Dedicated read capability | **Not required** (`decide` + assignment) |
| Generic GET hardening | **Prerequisite G1**, not parallel optional |
| Risk owner | Enterprise Architecture / Backend security |

---

## 10. Chief F1–F6 closure map

| Finding | Primary sections |
|---------|------------------|
| **F1** Issuer, `content.review.assign`, decide-only, mandatory class, eligibility port | §3.1–3.3, §4.1 |
| **F2** Append-only lifecycle, one active/version, 7d, locks, attestation coupling | §3.4–3.5, §3.6, §7 |
| **F3** Mutation enforcement, idempotency, publisher separation | §4.5, §7 |
| **F4** Generic GET inventory, corrected matrix, G1 prerequisite | §6 |
| **F5** Auth chain, ETag, DTO, PG18 phases/runs, ADR-048 note, FE attribution | §1, §2, §4.2–4.4 |
| **F6** DAG G0–G5, resolved alternatives, residual risks | §5, §8–9 |

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
| Generic version get | `src/aieos/domains/content/application/http_append.py`, `routes.py` |
| ETag helper | `src/aieos/platform/api/etag.py` |
| Teaching class authority | `src/aieos/domains/teaching/application/school_context.py` |

---

**Terminal classification:** `CI03-D1-R2 — REVIEWER-READ CANDIDATE CORRECTED / NOT FROZEN / NO CODE / PR #53 HELD / STOP FOR CHIEF FINAL EXACT-HEAD REVIEW`