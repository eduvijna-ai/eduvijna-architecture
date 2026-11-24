# AIEOS-V1-HINT-CI03-D1 — Cross-Owner Reviewer Read-Authority Proposal

**Status:** **PROPOSED / NOT APPROVED / NOT FROZEN / NO CODE AUTHORIZATION**  
**Provenance:** **NEWLY RECONSTRUCTED (2026-11-24)** — independent replacement for the prior agent’s unreachable local commit `cfbed35db14f2889615189701cf9efcc5421fe85` (not on GitHub; branch `ea-ci03-d1-exact-reviewer-read-candidate` absent). This artifact follows the [CI03-D1 governed handoff](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/issues/52#issuecomment-7122342874) and [Chief D0 conditional Option A direction](https://github.com/eduvijna-ai/eduvijna-architecture/issues/70#issuecomment-7122330292). **Does not modify** frozen [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) or [ADR-048](../decisions/ADR-048-review-queue-owns-approval.md).

**Workday linkage:** [Architecture Issue #70](https://github.com/eduvijna-ai/eduvijna-architecture/issues/70) (D0 discovery) · [Frontend Issue #52](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/issues/52) · [Frontend Draft PR #53](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/pull/53) (OPEN / DRAFT / RED — **no CI rerun authorized here**)

**Exact pins (read-only evidence base):**

| Surface | SHA / identifier |
|---------|------------------|
| Architecture `origin/main` (parent for this candidate) | `3c0a66aa0a06835e12bb6eeb0da64b7fe147999f` |
| Backend `origin/main` | `5bbc09bc895407b71a61f9ba86a7209ff9c10ffa` |
| Frontend `origin/main` | `e3a6b4a307edf359a00e027fd50f872751934f5b` |
| Frontend Draft PR #53 head | `cd4f8e3134fac3574249d787cd9cb8eb73af88f6` |
| Infrastructure `origin/main` | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` |
| Product (historical; connector unverified) | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` |
| Authoritative OpenAPI SHA-256 | `0061BCF6065FAFA184F196829A87AF98ADEDFCE6B633D45704141A5B48045D22` |
| Alembic head | `a360s010005` |
| Third real-stack PG18 CI run | [GitHub Actions #45327386458](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/45327386458) |
| Sanitized artifact (partial) | `14890905290` |

**SP02A disposition:** **65 NOT_TESTED + 2 DEFERRED** (S30/S31). This proposal does **not** promote scenario outcomes. Phase C HTTP 404 is **evidence of current contract behavior**, not proof that reviewer could complete approve/publish/Student paths.

---

## 1. Trigger / immutable evidence

### 1.1 PG18 E2E Phase C failure (third run)

At Frontend PR head `cd4f8e3134fac3574249d787cd9cb8eb73af88f6`, the PK-V1-HINT real-stack job [45327386458](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/actions/runs/45327386458) reports:

| Phase | Outcome |
|-------|---------|
| A (seed / environment) | PASS |
| B (author submit-for-review UI) | PASS |
| C (independent reviewer review detail GET) | **FAIL** — `REVIEW_DETAIL_HTTP_404` |
| D–J | **NOT RUN** |

The sanitized artifact confirms primary PG18 seed and Phases A/B only; it does **not** demonstrate reviewer approve, publish, assignment, Student consumption, Assessment, or Improve.

### 1.2 Current HTTP call chain (owner-filtered review detail)

Frontend `ReviewDetailPage` (PR #53) calls the existing Teacher OS review-queue **detail** operation. At Backend pin `5bbc09bc…`:

1. **Route:** `GET /api/v1/teacher-os/review-queue/{content_id}/versions/{version_id}` passes `TrustedSecurityContext.principal_id` to the read service (`src/aieos/domains/content/api/v1/routes.py` L767–790 @ pin).
2. **Service:** `GetTeacherReviewQueueItemService.get(execution_tenant_id, principal_id, content_id, version_id)` forwards the **authenticated principal** as `owner_principal_id` (`src/aieos/domains/content/application/review_queue.py` L48–69 @ pin).
3. **Repository:** `SqlAlchemyReviewQueueReadRepository.get_item` requires, among other predicates, `contents.owner_principal_id == owner_principal_id`, `stewardship_state == IN_REVIEW`, exact current content/version, tenant scope, and no prior terminal review decision (`src/aieos/domains/content/infrastructure/persistence/repositories.py` L841–878 @ pin).

In the PG18 fixture, **Content owner/author principal ≠ independent reviewer principal**. The owner-equality gate is therefore **expected** to return no row → `ReviewQueueItemNotFound` → HTTP **404**. This is **not** a Frontend timing defect; it is a **cross-owner read-authority gap** relative to ADR-063’s requirement for a **distinct HUMAN reviewer** (§5.3).

### 1.3 Phase B success implies review submit reached IN_REVIEW

`SubmitContentForReviewService` (and related transition) at pin requires a genuine `GENERATED → IN_REVIEW` transition (`src/aieos/domains/content/application/review.py` L687–726 @ pin). Phase B PASS therefore supports that the version is **IN_REVIEW** and current for the owner’s queue — but **does not** make it visible to a non-owner reviewer via owner-scoped detail.

### 1.4 Frozen architecture constraints (unchanged)

From [ADR-AIEOS-063](../decisions/ADR-AIEOS-063-aieos-learner-safe-instructional-hints-authority.md) (on Architecture main) and Chief D0 review:

- Hint-bearing `education.worksheet@2` requires **HUMAN reviewer ≠ version author** (`author_principal_id` / `created_by_principal_id` alignment — §5.3).
- Immutable payload-bound per-question attestation before same-version APPROVE.
- **No** adoption of Review Queue free-text as hint source ([ADR-048](../decisions/ADR-048-review-queue-owns-approval.md) preserves approval judgment semantics).
- Publisher remains **separate** from reviewer (`content.publish` vs `content.review.decide`).

---

## 2. Trust subjects and protected data

| Subject | Role in reviewer read |
|---------|------------------------|
| `execution_tenant_id` | Tenant isolation; all gates fail closed on mismatch |
| Authenticated **current HUMAN** reviewer | Intended consumer of private review payload; must match security SoR active classification |
| `effective_actor` | Must align with reviewer principal on mutations (attestation / APPROVE) |
| **Immutable version author** | `content_versions.created_by_principal_id` — **author for §5.3 inequality**; may differ from Content aggregate owner |
| **Content owner** | `contents.owner_principal_id` — drives **owner-only** Review Queue list/detail today |
| `content_id`, `content_version_id` | Exact resource key; stale or non-current versions **invisible** |
| `payload_digest` | SHA-256 of canonical worksheet `@2` payload at attestation time (ADR-063 §5.3) |
| Stewardship | `IN_REVIEW`, **current** version, **no** terminal `ReviewDecision` yet |
| Private fields in review DTO | Full worksheet payload including `answer`, `explanation`, and optional `learner_hint` per question |
| School/class scope | Contextual binding for entitlement validation — **not** a substitute for reviewer assignment |
| Publisher principal | Distinct actor; must not be conflated with reviewer session |

**Non-goals:** Student workloads, Parent/Principal intelligence, generic content browsing, or tenant-wide enumeration of pending reviews.

---

## 3. Reviewer-scoped entitlement authority

### 3.1 Kernel capability is necessary but not sufficient

`KernelReviewAuthorization.authorize` at Backend pin explicitly documents:

```text
_ = (content_id, version_id)  # resource context only; not authority
```

(`src/aieos/platform/security/authorization/content_adapters.py` L51–58 @ `5bbc09bc…`)

`AuthorizationKernel.decide_capability(principal_id, tenant_id, capability)` decides **tenant + principal + capability** only. A tenant-wide **ALLOW** for `content.review.decide` does **not** confer read access to **every** teacher’s private answer/explanation-bearing worksheet awaiting review.

**Architecture rule (proposed):** Reviewer read requires **both**:

1. Baseline capability check (`content.review.decide` and/or a narrowly scoped read capability — see §4), **and**
2. A **verifiable, current, revocable, exact-resource assignment** binding `(tenant_id, content_id, content_version_id, reviewer_principal_id [, optional class_ref])`.

### 3.2 Source inspection — no content review-assignment SoR at pin

Search of Backend pin `5bbc09bc…` finds **no** `content_review_assignments` (or equivalent) store, port, or migration governing hint/content review delegation. Assessment-domain uses “review assignment” wording for unrelated evaluation workflows — **not** Content reviewer binding.

**Conclusion:** A **new** reviewer-assignment authority is required for privacy-complete cross-owner read. **Migration-free** implementation is **not** proven at pin.

### 3.3 What is **not** reviewer entitlement evidence

| Artifact | Finding |
|----------|---------|
| `authoring_class_ref` in `worksheet_hint_append.py` provenance | **Contextual metadata** on the version — not authorization SoR |
| `SchoolContextClassAuthority.require_assignable_class_ref` | Teacher **assignment CREATE** gate — not reviewer assignment proof |
| Owner-scoped Review Queue membership | Proves owner visibility only |
| Review Queue free-text | Prohibited hint carrier (ADR-063 §5.3) |

### 3.4 Implementation candidates (assignment SoR)

| ID | Model | Summary | Migration |
|----|-------|---------|-----------|
| **C-A** | `content_review_assignments` table (+ repository port) | Append-only rows: tenant, content_id, content_version_id, reviewer_principal_id, issuer_principal_id, optional `class_ref`, `assigned_at`, `revoked_at` (nullable). Unique active assignment per version+reviewer. | **Required** (Alembic) |
| **C-B** | Signed, short-lived **review delegation token** issued at submit-for-review | Opaque bearer bound to exact version + reviewer; verified in read service. | Token service + audit; still needs issuer rules |

**Selection (proposed): C-A** with explicit security rationale:

- Durable, auditable, revocable entitlement matches fail-closed 404 semantics.
- Avoids wildcard bearer tokens and reduces TOCTOU versus ad hoc JWT claims.
- Aligns with ADR-063 immutable version binding and digest-bound attestation (assignment scoped to **exact** `content_version_id`).

**Issuer (proposed, subject to Founder gate):** On successful `submit-for-review`, system records assignment for the **designated reviewer principal** chosen by product rules (e.g. configured delegate, round-robin within school — **TBD in implementation packet**). Issuer must hold a **separately governed** capability (e.g. `content.review.assign` — **new**, not invented at pin). **PG18 non-prod seeds** may insert assignment rows only under explicit non-production grant policy — **not authorized in this document**.

### 3.5 Authorization evaluation order (proposed)

1. Authenticate JWT → trusted tenant + principal + HUMAN classification.
2. `decide_capability` for required capability(ies).
3. Load **active** `content_review_assignment` for `(tenant, content_id, version_id, principal_id)`.
4. Validate version row: current, `IN_REVIEW`, undecided, worksheet `@2` with hint context.
5. Enforce `reviewer_principal_id != content_versions.created_by_principal_id` when any non-empty hint.
6. Optional: validate `class_ref` against School Context **for reviewer** (distinct from assignable-class create gate).
7. Only then load private payload for DTO assembly.

Any failure → **non-enumerating 404** (or uniform deny policy consistent with existing Review Queue hidden-resource semantics).

---

## 4. Proposed read operation (Option A — preferred)

Chief D0 selected **Option A (direction only):** preserve legacy owner-only:

- `teacher_os_review_queue_list`
- `teacher_os_review_queue_get`

…and add a **separate, non-enumerating, exact-version reviewer read**.

### 4.1 Indicative HTTP surface (not OpenAPI-authorized)

```http
GET /api/v1/teacher-os/assigned-reviews/{content_id}/versions/{version_id}
```

**Suggested operation id:** `teacher_os_assigned_review_get` (new; digest change after separate sign-off).

**Initial scope:** Hint-bearing `education.worksheet` with `schema_version == 2` in `IN_REVIEW` only. Other artifact types **404** until explicitly extended.

### 4.2 Gate checklist (all required)

| Gate | Requirement |
|------|----------------|
| Principal | ACTIVE **HUMAN**; effective actor alignment |
| Tenant | JWT execution tenant matches Content row |
| Capability | `content.review.decide` ALLOW (and/or dedicated read capability if split) |
| Assignment | Active `content_review_assignment` for exact triple |
| Author separation | Reviewer ≠ `created_by_principal_id` when hints present |
| Version | Exact id matches Content.current version |
| Stewardship | `IN_REVIEW`; no terminal decision |
| Schema | Registered worksheet `@2` with hint review panel semantics |
| Class/school | Optional validated scope per §3.5 |

**Rejected paths:**

- Routing reviewer through owner `review_queue_get` after owner impersonation.
- Using generic `GetContentVersionService.get(tenant_id, content_id, version_id)` without principal-scoped policy (see §7).
- Broadening owner queue SQL to `OR assigned_reviewer_id = :principal`.

### 4.3 Consistency with mutation authorization

Attestation record (`WorksheetLearnerHintVersionAttestationV1`) and `content.review.decide` APPROVE must use the **same** reviewer principal and version binding established for read. Read entitlement MUST NOT outlive revocation of assignment or terminal APPROVE/REJECT.

---

## 5. Response contract and HTTP semantics

### 5.1 Review DTO (minimal private review projection)

Return only fields required for `WorksheetHintReviewPanel` semantic QA at Frontend PR #53:

- Content/version identifiers and stewardship metadata
- Per-question: `question_id`, stem text, `answer`, `explanation`, `learner_hint` (if present)
- Attestation status summary hooks (read-only; mutations remain separate operations)
- **No** student attempt data; **no** publisher-only publish state beyond review needs

### 5.2 Caching and concurrency

- **`ETag`** over aggregate revision (version payload digest + review state generation).
- Downstream **attestation** and **APPROVE** mutations retain existing **`If-Match`** / **`Idempotency-Key`** semantics (ADR-063 §5.3).
- **No** logging of raw response bodies containing answers/explanations.

### 5.3 Errors

| Condition | HTTP (proposed) |
|-----------|-----------------|
| Not assigned / ineligible / stale | **404** non-enumerating |
| Authz infrastructure unavailable | **503** fail-closed (no payload) |
| Authenticated but wrong tenant | **404** or **403** per existing Teacher OS policy (must not leak cross-tenant existence) |

---

## 6. Alternatives and tradeoffs

| Option | Verdict | Rationale |
|--------|---------|-----------|
| **A — Separate reviewer GET** | **Preferred (conditional)** | Additive; preserves ADR-048 owner-centric Today’s Mission queue |
| **B — Extend owner queue list/detail** | **Rejected** | Would broaden owner SQL visibility to all assignees; higher regression risk |
| **Generic `content_version_get` workaround** | **Rejected** | No principal-scoped authorization in service at pin; see §7 |
| **Author session / owner impersonation** | **Rejected** | Violates ADR-063 reviewer ≠ author |
| **Tenant-global `content.review.decide` → read any IN_REVIEW** | **Rejected** | Authorization widening; Chief D0 defect #1 |

**Hypothesis vs proven:** Owner-only 404 for cross-owner reviewer at Phase C is **proven by CI**. Generic ContentVersion GET bypass is **classified**, not **exploited** (§7).

---

## 7. Generic ContentVersion read bypass threat model

### 7.1 Source fact

`GetContentVersionService.get` in `http_append.py` (L248–264 @ `5bbc09bc…`) accepts `execution_tenant_id`, `content_id`, `version_id` **without** reviewer principal or resource-read authorization in that service layer.

### 7.2 Threat classification

**`PRIVATE_CONTENT_VERSION_GENERIC_READ_BYPASS` — BLOCKING for confidentiality-complete reviewer-read sign-off** (remediation order **before** claiming private worksheet confidentiality on the basis of reviewer GET alone).

### 7.3 Required adversarial HTTP experiments (future, non-prod)

| Actor | Target | Expected if gap exists | Expected after hardening |
|-------|--------|------------------------|--------------------------|
| Same-tenant HUMAN without owner/assignment | Generic version GET | **Must not** return private answers | **404/403** |
| Independent assigned reviewer | New assigned-reviews GET | **200** with full review DTO | **200** |
| Student principal | Either route | **Deny** | **Deny** |
| Other tenant | Either route | **Deny** | **Deny** |
| Service workload identity | Either route | **Deny** | **Deny** |

**D1 scope:** Document only; **no** route changes at pin. Any required generic-GET hardening is a **separate governed packet**.

---

## 8. Adversarial acceptance matrix (reviewer read)

| Case | Expected |
|------|----------|
| Authorized assigned reviewer, exact version, IN_REVIEW | **ALLOW** read |
| Same-tenant HUMAN with `content.review.decide` but **no** assignment | **DENY** |
| Wrong school/class scope for reviewer | **DENY** |
| Publisher-only principal | **DENY** read (publish ≠ review read) |
| Version author attempting review read | **DENY** when hints present |
| Content owner ≠ version creator; reviewer ≠ creator | **ALLOW** only if assignment + all gates pass |
| Cross-tenant | **DENY** |
| Revoked membership mid-session | **DENY** on next read (TOCTOU bounded by assignment + membership re-check) |
| Revoked assignment | **DENY** |
| Inactive / non-HUMAN principal | **DENY** |
| Terminal APPROVE/REJECT already recorded | **DENY** |
| Non-current version id | **DENY** |
| `GENERATED` / `APPROVED` without IN_REVIEW | **DENY** |
| Owner queue list/detail as owner | **Unchanged** (regression sentinel) |
| Owner queue as non-owner reviewer | **404** on owner detail; **200/404** on assigned-reviews per assignment |

---

## 9. Constrained implementation DAG

**No step authorized by this proposal.**

| Step | Deliverable |
|------|-------------|
| **(i)** | Reviewer assignment SoR (C-A migration + port), issuer capability, negative security tests |
| **(ii)** | Backend `GetAssignedReviewDetailService`, scoped SQL, HTTP route, OpenAPI addition |
| **(iii)** | New OpenAPI digest pin, Frontend generated client, `ReviewDetailPage` calls **assigned-reviews** not owner detail |
| **(iv)** | Fresh PG18 cross-owner HTTP + Student/adversarial matrix (§7–§8) |
| **(v)** | Resume Frontend Draft PR #53 E2E only after (i)–(iv) Chief gate |

**Frontend PR #53:** remains **HELD / RED** — no CI rerun here.

---

## 10. Decision ledger and open questions

| Item | Disposition |
|------|-------------|
| Implementation status | **NOT_IMPLEMENTED** |
| ADR freeze | **None** — this file is a **candidate** only |
| Reviewer assignment issuer rules (PG18 vs production) | **OPEN** — requires Founder/Chief security gate |
| Dedicated read capability vs `content.review.decide` reuse | **OPEN** — lean toward separate `content.review.read_assigned` if decide remains mutation-only in kernel catalog |
| Generic ContentVersion GET hardening | **BLOCKING** parallel track (§7) |
| Migration cost for C-A | **Acknowledged** — unavoidable at current pin |
| Risk owner | Enterprise Architecture / Backend security |
| CI02R1 note | Out-of-whitelist four-line static change in `src/pkV1HintE2e.pins.test.ts` on Frontend PR #53 — **recorded, not edited here** |

### 10.1 Unresolved questions for Chief / Founder gate

1. Who may issue reviewer assignments (owner delegate, admin, automated on submit)?
2. Must assignment include `class_ref` mandatory or optional for v1 hint slice?
3. Does Option A endpoint path above match Teacher OS URL taxonomy long-term?
4. Is non-enumerating 404 sufficient for all deny cases vs mixed 403?
5. When is generic GET hardening a **prerequisite merge** vs parallel?

---

## Source path index (Backend @ `5bbc09bc895407b71a61f9ba86a7209ff9c10ffa`)

| Topic | Path (line refs indicative) |
|-------|-----------------------------|
| Owner review queue get | `src/aieos/domains/content/application/review_queue.py` |
| Owner SQL predicate | `src/aieos/domains/content/infrastructure/persistence/repositories.py` ~841–878 |
| Review queue HTTP | `src/aieos/domains/content/api/v1/routes.py` ~767–790 |
| Generic version get | `src/aieos/domains/content/application/http_append.py` ~248–264 |
| Submit for review | `src/aieos/domains/content/application/review.py` ~687–726 |
| Kernel review auth | `src/aieos/platform/security/authorization/content_adapters.py` |

---

**Terminal classification:** `CI03-D1 — REVIEWER-READ SECURITY CONTRACT CANDIDATE (RECONSTRUCTED) / NOT FROZEN / NO BACKEND OR FRONTEND CODE / FRONTEND PR #53 HELD`