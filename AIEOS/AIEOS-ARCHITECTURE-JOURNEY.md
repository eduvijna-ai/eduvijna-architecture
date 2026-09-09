# AIEOS — Architecture Journey

**Purpose:** Chronological record of AIEOS architecture evolution  
**Rule:** Do not invent historical facts. Where evidence is missing: *Not established by current repository evidence.*

---

## Authority note

Conflict preference:

1. Approved architecture decisions  
2. Approved product / engineering documents  
3. Current source code / contracts  
4. AIEOS orientation documents

---

## 1. AIEOS product vision

| Field | Content |
|-------|---------|
| **Objective** | Establish EduVijna as an Artificial Intelligence Engineering Education Operating System (AIEOS) — complete product identity — with Teacher OS as a subsystem. |
| **Architectural reason** | Orient the ecosystem as an education OS, not a feature collection; keep architecture ahead of implementation. |
| **What was implemented** | Product vision / Teacher OS PA docs, North Star, Engineering Constitution, ADRs 042–048, EBP-001 blueprint; AIEOS orientation folder (this permanent knowledge foundation). |
| **What was deliberately NOT implemented** | Treating Teacher OS as the entire product; premature Agents/MCP/Orchestration/Memory platforms. |
| **Governing decisions** | Approved project identity (AIEOS); ADR-042…048; EBP-000; PA-001 / TLM-001 foundations. |
| **Current status** | Vision and governance active; AIEOS orientation documents established in `eduvijna-architecture/AIEOS/`. |

---

## 2. Teacher OS foundation

| Field | Content |
|-------|---------|
| **Objective** | Define Teacher OS as the teacher-centric operating subsystem (Mission, Intent, Memory, School Context, Daily Loop, Review Queue). |
| **Architectural reason** | Replace tool-zoo mental model with Intent → orchestration → Review Queue; preserve existing capability engines. |
| **What was implemented** | Product architecture package PA-001; feature boundaries; Continuous Context model; Artifact model; EBP-001 Wave 1 blueprint targeting `Quiz-React` + `eduvijna-api`. |
| **What was deliberately NOT implemented** | New Teacher OS application repository; Student/Parent/Principal OS in Wave 1; major DB redesign in Wave 1 scope. |
| **Governing decisions** | PA-001; FEATURE_BOUNDARIES; ENGINEERING_CONSTITUTION; later ADR-042…048. |
| **Current status** | Foundation approved as product/architecture direction; Wave 1 delivery in progress. |

---

## 3. EBP-001.1 — Teacher OS Shell

| Field | Content |
|-------|---------|
| **Objective** | Ship flag-gated Teacher OS chrome (shell, nav, routes, extension slots) without breaking classic EduVijna. |
| **Architectural reason** | Shell owns UX only; additive rollout; reusable foundation before features (ADR-042 / ADR-043 / EDR-002). |
| **What was implemented** | TeacherShell, TeacherOsRoutes, TeacherNavigation, TeacherOsFlagProvider, TeacherOsContext selections, telemetry façade; API `teacher_os_enabled` flag exposure. |
| **What was deliberately NOT implemented** | Generators inside shell; Mission as forced production default landing; Review badge live data; AI/Memory. |
| **Governing decisions** | ADR-042; EDR-002; EBP-000; EBP-001 Sprint 0. |
| **Current status** | APPROVED / CLOSED (EBP-001.9 discovery status). |

---

## 4. EBP-001.2 — Today's Mission

| Field | Content |
|-------|---------|
| **Objective** | Provide Today's Mission landing as the teacher briefing experience. |
| **Architectural reason** | Mission-first home vs module tile menu; compose day briefing through MissionService façade (ADR-044 service boundary). |
| **What was implemented** | TodayMissionPage and Mission cards; mock MissionService adapter path. |
| **What was deliberately NOT implemented** | Full ERP/timetable mission aggregate API as hard dependency; durable AI-prepared kits. |
| **Governing decisions** | PA Today's Mission; ADR-044; EBP-001 Sprint 1. |
| **Current status** | APPROVED / CLOSED as Mission UX slice; Mission data still mock-backed (partial vs blueprint ERP depth). |

---

## 5. EBP-001.3 — Teaching Intent

| Field | Content |
|-------|---------|
| **Objective** | Capture teacher goals via Teaching Intent experience (Prepare outcome language). |
| **Architectural reason** | Teaching Intent owns goals; generators are capabilities (ADR-045 / ADR-047). |
| **What was implemented** | Intent landing + wizard UX; mock Intent adapter. |
| **What was deliberately NOT implemented** | Orchestration; Review Queue; Agents; MCP; APIs; DB; AI generation. |
| **Governing decisions** | ADR-045; ADR-047; EBP-001.3. |
| **Current status** | APPROVED / CLOSED (UX). |

---

## 6. EBP-001.4 — Intent → Preparing Bridge

| Field | Content |
|-------|---------|
| **Objective** | Bridge Continue from Intent into Preparing Kit / Review Queue entry experience. |
| **Architectural reason** | Keep Intent → kit → Review path coherent without claiming full orchestration. |
| **What was implemented** | PreparingKitPage and Review Queue entry bridge; mock artifacts. |
| **What was deliberately NOT implemented** | Real content generation; full Review Queue (landed as 001.5); custom free-text Intent (deferred). |
| **Governing decisions** | ADR-045; EBP-001.4 review package notes. |
| **Current status** | APPROVED / CLOSED as bridge UX; generation not wired. |

---

## 7. EBP-001.5 — Review Queue

| Field | Content |
|-------|---------|
| **Objective** | Deliver Review Queue as approval cockpit (teacher judgement). |
| **Architectural reason** | Review Queue owns approval; Approved ≠ Published; one queue for all Artifact types (ADR-048 / ADR-046). |
| **What was implemented** | Review Queue list/detail UX; approve / reject / request-changes actions on mock Artifact service. |
| **What was deliberately NOT implemented** | Publish/assign; generation ownership; orchestration; durable Content SoR wiring. |
| **Governing decisions** | ADR-048; ADR-046; EBP-001.5. |
| **Current status** | APPROVED / CLOSED as UX/semantics slice; **not** durable generator integration. |

---

## 8. EBP-001.6 — Continuous Context

| Field | Content |
|-------|---------|
| **Objective** | Preserve session/Intent work thread across Preparing Kit and Review Queue navigation. |
| **Architectural reason** | Continuous Context is session continuity — distinct from Teacher Memory and School Context (PA + EDR-001). |
| **What was implemented** | ContinuousContext provider mounted once at Teacher OS layout; threadId shared across SPA navigation. |
| **What was deliberately NOT implemented** | Teacher Memory; AI; durable persistence; Content AI session binding depth. |
| **Governing decisions** | EDR-001; PA Continuous Context; EBP-001.6. |
| **Current status** | APPROVED / CLOSED as session React Context; not durable Memory. |

---

## 9. EBP-001.7 — Mission Service Hardening

| Field | Content |
|-------|---------|
| **Objective** | Harden MissionService as stable read-composition façade and Mission UX behaviours. |
| **Architectural reason** | Stable product services before deeper AI (ADR-043 / ADR-044); Mission must not own engines. |
| **What was implemented** | MissionService hardening (mock adapter), Continuous Context snapshot plumbing, outcome CTA / empty-state fixes evidenced in tests. |
| **What was deliberately NOT implemented** | Backend Mission aggregate as mandatory; Agents/MCP; ERP deep integration. |
| **Governing decisions** | ADR-043; ADR-044; EBP-001.7. |
| **Current status** | APPROVED / CLOSED. |

---

## 10. EBP-001.8 — Teacher / School Context

| Field | Content |
|-------|---------|
| **Objective** | Provide Teacher/School Context **read surface** using existing school identity APIs. |
| **Architectural reason** | Institutional context inheritance without claiming Teacher Memory; reuse existing `my-school` authorization/tenancy. |
| **What was implemented** | School name hydration via existing `GET /api/v1/school-management/my-school`; School/Teacher Context cards; no new DB/API. |
| **What was deliberately NOT implemented** | Teacher Memory; preferences; inferred personalization; MissionService/ContinuousContext redesign; Agents/MCP/Orchestration. |
| **Governing decisions** | EBP-001.8 package; ADR-042 shell context boundary; PA School Context vs Memory distinction. |
| **Current status** | Implemented — awaiting architecture review per product package; discovery status lists APPROVED / CLOSED for Wave 1 slice tracking. **Not** Teacher Memory. |

---

## 11. EBP-001.9 — Discovery / preflight

| Field | Content |
|-------|---------|
| **Objective** | Determine the next correct Wave 1 engineering slice after 001.8 from blueprint + repository evidence; inspect content/review/persistence contracts. |
| **Architectural reason** | Do not invent roadmap; close Wave 1 acceptance gaps before premature AI/Memory/Agents; respect ADR-044 service boundary. |
| **What was implemented** | Discovery only: Phase 0 alignment; open-question resolution; content contract preflight; persistence preflight (**DB CHANGE REQUIRED**); Content SoR verification (Scenario C — no generic Content SoR). |
| **What was deliberately NOT implemented** | Code, APIs, flags, migrations, DB creation, ADRs/EDRs, Review Queue durable integration. |
| **Governing decisions** | Existing ADR-042…048; EBP-001 acceptance criteria; discovery recommendations **not** equal to implementation authorization. |
| **Current status** | **Discovery / architecture review.** Recommended next feature: Review Queue ↔ Existing Generators Integration. **Persistence architecture is under architecture review. DB creation is NOT authorized.** |

---

## 12. ADR-AIEOS-048 — First-production App runtime & OCI delivery

| Field | Content |
|-------|---------|
| **Objective** | Freeze first-production App Platform worker topology, dedicated BLR1 VPC, Preview compute exception, OCI digest authority, and Temporal secret destinations for WORKFLOW_DISPATCHER and TEMPORAL_WORKER. |
| **Architectural reason** | Prevent improvisation from default-blr1 reuse, mutable `latest` tags, shared Temporal keys, or Preview SKUs without bounded Founder/Chief acceptance. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-048](../decisions/ADR-AIEOS-048-aieos-first-production-app-runtime-oci-delivery-contract.md) deposited; catalogue/ledger/current-state updated. Distinct from Teacher OS ADR-048. |
| **What was deliberately NOT implemented** | App Platform apps; VPC creation; DOCR `aieos-backend` repository; OCI publication; secret injection; OpenTofu plan/apply; production deployment. |
| **Governing decisions** | ADR-AIEOS-048; binding prior ADR-AIEOS-022/026/029/037/040R1/044R2/045/046/047. |
| **Current status** | **Architecture Frozen / Approved** as historical/base App runtime contract. Current App Platform **naming** authority is [ADR-AIEOS-048R1](../decisions/ADR-AIEOS-048R1-aieos-app-platform-provider-compliant-naming.md). Current App Platform **ownership/deployment** authority is [ADR-AIEOS-048R2](../decisions/ADR-AIEOS-048R2-aieos-app-platform-runtime-ownership-boundary.md). Cloud / App / OCI / deployment mutation **not authorized**. |

---

## 13. Workflow plane source & Temporal provisioning status reconciliation

| Field | Content |
|-------|---------|
| **Objective** | Keep journey/current-state aligned after PED-I12 Backend merge and WPI-A01 Temporal Cloud first-production apply without rewriting ADR-AIEOS-047 historical freeze text. |
| **Architectural reason** | Historical ADR freeze status ≠ current implementation/provisioning status. |
| **What was implemented** | WORKFLOW_DISPATCHER Backend runtime source (**PED-I12**) = **IMPLEMENTED / MERGED** at Backend `8f4dd172e6a0ba8b4ad944b0ae22060442356342`. Temporal Cloud Namespace `eduvijna-aieos-prod.w97q1` + WORKFLOW_DISPATCHER and TEMPORAL_WORKER service accounts (**WPI-A01**) = **PROVISIONED / CONFORMED / FORMALLY CLOSED**. |
| **What was deliberately NOT implemented** | Temporal runtime API-key issuance/injection; App Platform worker deployment; dedicated VPC creation; governed production OCI publication; production workflow execution. |
| **Governing decisions** | ADR-AIEOS-047 (architecture freeze retained); ADR-AIEOS-048 (App runtime architecture freeze); separately authorized PED-I12 / WPI-A01 execution gates. |
| **Current status** | Source + Namespace/SA provisioning closed; runtime keys, App Platform deployment, and production execution **not authorized**. |

---

## 14. ADR-AIEOS-048R1 — Provider-compliant App Platform naming

| Field | Content |
|-------|---------|
| **Objective** | Correct first-production App Platform application names so they satisfy the DigitalOcean App Platform naming constraint without changing any other ADR-AIEOS-048 contract. |
| **Architectural reason** | WPI-AP-I01 implementation review found ADR-AIEOS-048 names `eduvijna-aieos-prod-*` incompatible with the provider naming constraint. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-048R1](../decisions/ADR-AIEOS-048R1-aieos-app-platform-provider-compliant-naming.md) deposited. CURRENT names `aieos-prod-workflow-dispatcher` (length 30) and `aieos-prod-temporal-worker` (length 26). ADR-AIEOS-048 historical body not rewritten. |
| **What was deliberately NOT implemented** | Infrastructure PR #12 modification or merge; App Platform apps; VPC creation; DOCR / OCI publication; secret injection; OpenTofu plan/apply; production deployment. |
| **Governing decisions** | ADR-AIEOS-048R1 (current naming); ADR-AIEOS-048 (historical/base non-naming authority). |
| **Current status** | **Architecture Frozen / Approved.** Current naming authority. Cloud / App / OCI / deployment mutation **not authorized**. |

---

## 15. ADR-AIEOS-048R2 — App Platform runtime ownership boundary

| Field | Content |
|-------|---------|
| **Objective** | Reject production OpenTofu ownership of DigitalOcean App Platform applications after empiric proof that provider 2.99.1 materializes out-of-band encrypted secrets into plan/state; move App lifecycle to a governed state-free deployment plane while preserving ADR-AIEOS-048/048R1 topology and naming. |
| **Architectural reason** | WPI-AP-SV01 / WPI-AP-SV01R1 disposable validation classified **B. FAIL_OPEN_TOFU_SECRET_MATERIAL**: refresh-only plan JSON contained `EV[...]` for an out-of-band `SECRET` while HCL had zero env blocks. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-048R2](../decisions/ADR-AIEOS-048R2-aieos-app-platform-runtime-ownership-boundary.md) deposited. Production OpenTofu `digitalocean_app` ownership REJECTED. Encrypted `EV[...]` classified as secret material. State-free deployment plane required. ADR-048/048R1 historical bodies not rewritten. |
| **What was deliberately NOT implemented** | Infrastructure reconciliation; deployment-plane implementation; App Platform apps; VPC creation; DOCR / OCI publication; secret injection; OpenTofu plan/apply; production deployment. |
| **Governing decisions** | ADR-AIEOS-048R2 (current ownership/deployment); ADR-AIEOS-048R1 (current naming); ADR-AIEOS-048 (historical/base topology). |
| **Current status** | **Architecture Frozen / Approved.** WPI-AP-SV01/R1 = FORMALLY CLOSED — FAIL_OPEN_TOFU_SECRET_MATERIAL. WPI-AP-I02 Infrastructure reconciliation = FORMALLY CLOSED. Detailed deployment-plane behavior = [ADR-AIEOS-049](../decisions/ADR-AIEOS-049-aieos-app-platform-state-free-deployment-plane.md). Cloud / App / OCI / deployment mutation **not authorized**. |

---

## 16. ADR-AIEOS-049 — App Platform state-free deployment plane

| Field | Content |
|-------|---------|
| **Objective** | Freeze the WPI-AP-DP01 design for the governed state-free App Platform deployment plane required by ADR-AIEOS-048R2: direct DigitalOcean REST release controller with one App per process/release, transient in-memory secret/`EV[...]` handling, exact allowlist reconciliation, durable per-App lease plus double-read fence, independent dispatcher/worker credentials and secrets, immutable OCI digest authority, native rollback, and redacted evidence. |
| **Architectural reason** | After OpenTofu `digitalocean_app` ownership was rejected and removed (WPI-AP-I02), production App lifecycle requires an explicit state-free controller contract before any implementation. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-049](../decisions/ADR-AIEOS-049-aieos-app-platform-state-free-deployment-plane.md) deposited. Design frozen/approved. Historical ADR-048 / 048R1 / 048R2 bodies not rewritten. |
| **What was deliberately NOT implemented** | Deployment-controller implementation; durable lease implementation; secret-delivery product selection; disposable live validation; production credentials; App/VPC/OCI/Temporal-key mutation; production deployment. |
| **Governing decisions** | ADR-AIEOS-049 (current detailed deployment-plane behavior); ADR-AIEOS-048R2 (ownership boundary); ADR-AIEOS-048R1 (naming); ADR-AIEOS-048 (base topology). |
| **Current status** | **Architecture Frozen / Approved.** Design frozen; implementation and disposable empirical validation = **REQUIRED / NOT AUTHORIZED**. Production App Platform deployment **not authorized**. Release-controller implementation architecture = [ADR-AIEOS-050](../decisions/ADR-AIEOS-050-aieos-app-platform-release-controller-implementation-architecture.md). |

---

## 17. ADR-AIEOS-050 — App Platform release controller implementation architecture

| Field | Content |
|-------|---------|
| **Objective** | Freeze the WPI-AP-DP02 release-controller implementation architecture required to realize ADR-AIEOS-049: Infrastructure-isolated Python 3.14 / `uv` tool; GitHub-hosted `ubuntu-24.04` only; two fixed `workflow_dispatch` workflows and Environments; per-App durable lease via Actions concurrency; direct DigitalOcean v2 REST via controlled `httpx` with zero automatic mutation retries; closed typed mutation allowlist; four PAT classes; Environment secret-delivery boundary; sanitized `release-receipt.json` (90-day retention); credential-free offline CI; mandatory WPI-AP-DP-TV01 before production. |
| **Architectural reason** | ADR-AIEOS-049 froze deployment-plane behavior but left placement, runtime, workflow/Environment identities, lease technology, secret delivery, HTTP posture, credential scopes, evidence sink, and offline CI proof areas unselected; those must be frozen before separated implementation gates. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-050](../decisions/ADR-AIEOS-050-aieos-app-platform-release-controller-implementation-architecture.md) deposited. WPI-AP-DP02 design complete/frozen. Historical ADR-048 / 048R1 / 048R2 / 049 bodies not rewritten. |
| **What was deliberately NOT implemented** | Controller source; workflow YAML; GitHub Environments/secrets; DigitalOcean PATs; Temporal keys; WPI-AP-DP-TV01; production App bootstrap; any cloud/state mutation. |
| **Governing decisions** | ADR-AIEOS-050 (current release-controller implementation architecture); ADR-AIEOS-049 (deployment-plane behavior); ADR-AIEOS-048R2 (ownership boundary); ADR-AIEOS-048R1 (naming); ADR-AIEOS-048 (base topology). |
| **Current status** | **Architecture Frozen / Approved.** WPI-AP-DP02 = **DESIGN COMPLETE / FROZEN**; implementation = **NOT AUTHORIZED**; WPI-AP-DP-TV01 = **AUTHORIZED BUT PAUSED ON OCI MANIFEST DIGEST** (see ADR-AIEOS-051); production App deployment **not authorized**. |

---

## 18. ADR-AIEOS-051 — Backend production OCI build, provenance & first-publication architecture

| Field | Content |
|-------|---------|
| **Objective** | Freeze the production Backend OCI build / provenance / first-publication architecture: one common `eduvijna-registry` / `aieos-backend` image for WORKFLOW_DISPATCHER and TEMPORAL_WORKER; exact clean Backend Git SHA source; future `Dockerfile.backend-runtime` (Python 3.14.7 / uv 0.12.4 / non-root / fail-closed default); OCI identity labels; sanitized provenance receipt; source-SHA tag convenience with immutable digest authority; separated WPI-OCI-I01 (source/offline) and WPI-OCI-P01 (live publication) gates. |
| **Architectural reason** | ADR-048/049/050 require immutable OCI digest authority for App Platform release, but no production OCI build/provenance/publication architecture was frozen; TV01 is blocked on that digest. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-051](../decisions/ADR-AIEOS-051-aieos-backend-production-oci-build-provenance-first-publication-architecture.md) deposited. Historical ADR-048 / 048R1 / 048R2 / 049 / 050 bodies not rewritten. |
| **What was deliberately NOT implemented** | Production Dockerfile; provenance tooling; offline CI; registry login; publication credential; OCI push/promote; TV01 App CREATE; App Platform mutation; production deployment. |
| **Governing decisions** | ADR-AIEOS-051 (CURRENT Backend production OCI architecture); ADR-AIEOS-048 (base OCI delivery); ADR-AIEOS-049 / 050 (digest-consuming release plane). |
| **Current status** | **Architecture Frozen / Approved.** Production Backend OCI architecture = **DESIGN FROZEN**. **WPI-OCI-I01** = AUTHORIZED **SOURCE / OFFLINE IMPLEMENTATION ONLY** (after deposition merge). **WPI-OCI-P01** = **NOT AUTHORIZED**. **WPI-AP-DP-TV01** = **AUTHORIZED BUT PAUSED ON OCI MANIFEST DIGEST**. Production deployment **not authorized**. |

---

## 19. ADR-AIEOS-052 — Preparation kit & multi-artifact generation architecture

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture for Teacher OS TOS-DEV04 Prepare Tomorrow: one outcome action → `education.generate_preparation_kit` → atomic six-artifact Generic Content materialization; provenance V2 with mandatory `artifact_kind`; capability/revision-aware GenerationRun fences (DEV03 worksheet coexistence); FAILED terminal replay vs stale RUNNING reclaim; no PreparationKit aggregate; no AI payload staging; no `generation_artifacts` canonical bridge. |
| **Architectural reason** | Teacher OS ADR-047 deferred multi-artifact Prepare Tomorrow orchestration pending architecture review; TOS-DEV03 proved single-worksheet path but cannot express one execution → six governed artifacts without material architecture decisions. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-052](../decisions/ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md) deposited and Frozen / Approved **2026-08-28**. |
| **What was deliberately NOT implemented** | Backend; Frontend; migrations; OpenAPI; live provider proof; production Content catalog activation. |
| **Governing decisions** | ADR-AIEOS-052 (CURRENT multi-artifact Prepare Tomorrow architecture); ADR-AIEOS-027 (Content authority); ADR-AIEOS-026 (no workflow as SoR); Teacher OS ADR-044–048 (outcome-first, review semantics). |
| **Current status** | **Architecture Frozen / Approved.** TOS-DEV04 native implementation = **IMPLEMENTED / COMPLETE** (Backend `origin/main` `06e05277e73e0c71172cae4904efb37d771c3fad`). Live provider proof requires separate gate (**DEV04-I10**). |

---

## 20. ADR-AIEOS-053 — Teaching Assignment & Classroom Delivery Authority

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture for Teacher OS TOS-DEV06: Publication ≠ Assignment; TeachingAssignment Teaching-domain intent SoR; immutable exact ContentVersion bind with published_version_id precondition; ClassRef via AIEOS School Context façade; command Idempotency-Key semantics; ACTIVE/CLOSED/CANCELLED; no LMS delivery-attempt persistence in DEV06 core; narrow clarification of ADR-046 / ADR-AIEOS-052 delivery wording only. |
| **Architectural reason** | Implemented Teacher OS publish path is governance eligibility, not classroom delivery; Product/ADR wording that collapses Published with assign/send must not remain current precedence; Class/Roster remain Admin/ERP/SIS masters. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-053](../decisions/ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) Frozen / Approved by Founder **2026-08-31**. |
| **What was deliberately NOT implemented** | Backend; Frontend; Product; migrations; OpenAPI; School Context provider; LMS connector; deployment; production mutation. |
| **Governing decisions** | ADR-AIEOS-053 (Frozen / Approved); ADR-AIEOS-027 (Content / Publication); ADR-AIEOS-052 (preparation; delivery wording clarified); ADR-046 (lifecycle vocabulary; Published wording clarified); ADR-048 (Review Queue). |
| **Current status** | **Architecture Frozen / Approved.** Founder approved **2026-08-31**. TOS-DEV06 native TeachingAssignment implementation + Product E2E = **COMPLETE** (Backend `06e05277e73e0c71172cae4904efb37d771c3fad`; Frontend `89ee9f1330f635de3186d21e0102cb63c5c698e1`). External LMS / Student OS delivery remains deferred. |

---

## 21. ADR-AIEOS-046R1 — Production Event Plane Multi-Domain Publisher Scope Revision

| Field | Content |
|-------|---------|
| **Objective** | Narrow forward revision of ADR-AIEOS-046: expand production EVENT publisher PUB authority from Content-only to a closed multi-domain set (Content + Teaching) required by ADR-AIEOS-053 TeachingAssignment events; preserve all other ADR-AIEOS-046 invariants; forbid platform-wide `io.eduvijna.aieos.>` publisher wildcard. |
| **Architectural reason** | ADR-AIEOS-053 requires TeachingAssignment mutation events under `io.eduvijna.aieos.teaching....`; ADR-AIEOS-046 A46-INV-03 limited publisher scope to Content only; minimum Teaching-domain permission added without granting unrelated domain authority. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-046R1](../decisions/ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) Frozen / Approved by Founder **2026-08-31**. |
| **What was deliberately NOT implemented** | Backend; Infrastructure; NATS mutation; credential creation/regeneration; stream creation/update; DigitalOcean mutation; deployment; production EVENT execution; TeachingAssignment application/API; OpenAPI; Frontend; LMS integration. |
| **Governing decisions** | ADR-AIEOS-046R1 (Frozen / Approved); ADR-AIEOS-046 (historical/base); ADR-AIEOS-053 (TeachingAssignment event requirement); ADR-AIEOS-025 (outbox/CloudEvents). |
| **Current status** | **Architecture Frozen / Approved.** Founder approved **2026-08-31**. ADR-AIEOS-046 historical body unchanged. TeachingAssignment application/API + outbox events = **IMPLEMENTED** in TOS-DEV06-I03 (Backend `06e05277e73e0c71172cae4904efb37d771c3fad`). Production EVENT activation / NATS provisioning = **NOT AUTHORIZED**. |

---

## 22. ADR-AIEOS-054 — Teaching Execution & Observation Authority

| Field | Content |
|-------|---------|
| **Objective** | Propose architecture for Teacher OS TOS-DEV07: Assigned ≠ Taught; TeachingExecution Teaching-domain execution SoR; immutable exact ContentVersion bindings; PRIVATE_EXECUTION_NOTE + CLASS_OBSERVATION only; no timetable dependency; execution lifecycle IN_PROGRESS/COMPLETED/CANCELLED; HYBRID / Option D (AIEOS owns execution; ERP/SIS remains Class master). |
| **Architectural reason** | TOS-DEV07A discovery accepted; TeachingAssignment and TeachingWork must not be repurposed as lesson execution truth; Teach UI at ADR freeze time was assignment administration only. |
| **What was implemented at architecture freeze** | Architecture source: [ADR-AIEOS-054](../decisions/ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) deposited **2026-09-01**; Chief Architect review **ACCEPTED 2026-09-01**; Founder / Product Architecture **Frozen / Approved 2026-09-01**. |
| **What was deliberately NOT implemented at freeze time** | Backend; Frontend; Product; migration; OpenAPI; NATS change; deployment; production mutation; DEV07 implementation slices. *(Historical freeze-time boundary — not a current-status claim.)* |
| **Governing decisions** | ADR-AIEOS-054 (Frozen / Approved); ADR-AIEOS-053 (TeachingAssignment); ADR-AIEOS-052 (preparation); ADR-AIEOS-046R1 (event scope — no 046R2 required). |
| **Subsequent authorized implementation** | **TOS-DEV07 COMPLETE** under ADR-AIEOS-054. **DEV07-I01** — TeachingExecution domain/persistence SoR (executions, exact ContentVersion bindings, observations; Alembic through `tosd070002`). **DEV07-I02** — Teach composition/application/API (START, read/list, observation create/correct, COMPLETE/CANCEL, Teach context, School Context ClassRef composition; OpenAPI `7D7D0E7C7115667757A31CFEB5474F7498ECC7198FB812DE5EF14A0E9F2D289A`; Backend `551e46e004233421746e4df2789c07367702528b`). **DEV07-I03** — Teacher OS Teach UX (work/class selection, START with exact binding, observations, COMPLETE/CANCEL, terminal read-only, revision-sensitive deliberate retry). **DEV07-I04** — real-stack Product E2E (Browser → Vite `/api` → FastAPI → PostgreSQL 18; zero API mocks; Assignment regression + TeachingExecution journey; Frontend merge `1c243cae4395a4546b5440a8b194023ff31d0a7d`; post-merge CI `33756532004`; 17 product tests: 6 Assignment + 11 TeachingExecution). |
| **Current status** | **Architecture Frozen / Approved.** Founder approved **2026-09-01**. **TOS-DEV07 implementation COMPLETE** (DEV07-I01–I04 formally closed). Architecture record synchronization = **TOS-DEV07-C01**. Assigned ≠ Taught ≠ Assessed ≠ Mastered preserved. Learner-specific observation, attendance, assessment, mastery, timetable, LMS delivery, observation events, additional NATS provisioning, and production deployment remain **not authorized**. |

---

## 23. ADR-AIEOS-055 — Assessment & Learning Evidence Authority

| Field | Content |
|-------|---------|
| **Objective** | Propose architecture for Teacher OS TOS-DEV08: Taught ≠ Assessed ≠ Mastered; Assessment-domain ClassroomAssessment SoR; class-level-first OPTION D; atomic RECORD → RECORDED / VOIDED; exact ContentVersion Cases A/B/C; Bootstrap ClassRef teaching-target authority; no learner identity / attempts / mastery / Improve / events / Temporal / AI grading. |
| **Architectural reason** | TOS-DEV08A discovery + TOS-DEV08P1 design/validation accepted as freeze-candidate input; TeachingExecution must not be repurposed as assessment truth; `/teacher-os/assess` was PlaceholderPage at ADR freeze time; no roster/learner SoR exists for learner-specific baseline. |
| **What was implemented at architecture freeze** | Architecture source only: [ADR-AIEOS-055](../decisions/ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) Frozen / Approved **2026-09-03**. Chronology: TOS-DEV08A discovery → TOS-DEV08P1 design + validation → TOS-DEV08P2 freeze candidate → TOS-DEV08P2R1 authority correction → Founder freeze approved **2026-09-03**. |
| **What was deliberately NOT implemented at freeze time** | Backend; Frontend; Product; migration; OpenAPI; DEV08-I01+; Improve; learner-specific Assessment; Mastery; events; Temporal; AI grading; production deployment. `/teacher-os/assess` was PlaceholderPage. *(Historical freeze-time boundary — not a current-status claim.)* |
| **Governing decisions** | ADR-AIEOS-055 (Frozen / Approved); ADR-AIEOS-054 (TeachingExecution); ADR-AIEOS-053 (TeachingAssignment / Future Student / Learning attempt-submission); ADR-AIEOS-027 (Content); ADR-AIEOS-023R1 / 024 / 025 / 028 / 031. |
| **Subsequent authorized implementation** | **TOS-DEV08 COMPLETE** under ADR-AIEOS-055. **DEV08-I01** — ClassroomAssessment domain + persistence (schema `assessment`; Alembic through `tosd080002`). **DEV08-I02** — ClassroomAssessment application/API + authority composition (RECORD / read / list / CORRECT / VOID; OpenAPI SHA-256 `824B389D6D4EDB2EA5D8ED3A9E5411087B566DFDCA09C2AB0CD4FDED51C4D89D`; Backend `1fe28f4fd1a2a2070aa69d67daa49cd53ba5820d`). **DEV08-I03 / I03R1** — Teacher OS Assess UX + concurrency / 409 correction (deliberate Assess after TeachingExecution COMPLETED; RECORD → RECORDED; CORRECT under optimistic concurrency; optional VOID → VOIDED). **DEV08-I04** — real-stack Product E2E (Browser → Vite `/api` → FastAPI → PostgreSQL; Frontend merge `30c94f3e0403b9a5a2e955c706766035490598f9`; parents `398710f168c81cf6fb1f6aebe2b667a1a0bfc575` + `7b9c5af6f2a7cde248eaa40b4535ae6b130ab86c`; post-merge CI `33853706361` SUCCESS: Typecheck, lint, unit, build, e2e, product-e2e). |
| **Current status** | **Architecture Frozen / Approved.** Founder / Product Architecture approved **2026-09-03**. **TOS-DEV08 implementation COMPLETE** (DEV08-I01–I04 formally closed). Architecture record synchronization = **TOS-DEV08-C01**. Generated ≠ Approved ≠ Published ≠ Assigned ≠ Taught ≠ Assessed ≠ Mastered preserved. ClassroomAssessment remains class-level only. Learner-specific assessment, mastery, Improve, Assessment events, Temporal Assessment workflow, Teacher Memory, Notification Center, Student Intelligence, and production deployment remain **not authorized**. |

---

## 24. ADR-AIEOS-056 — Improve & Remediation Authority

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture for Teacher OS TOS-DEV09: close Prepare → Teach → Assess → Improve → Prepare again at class level; teacher-deliberate remediation TeachingWork; immutable Assessment-origin provenance; no Improve SoR; no learner/mastery/Memory. |
| **Architectural reason** | TOS-DEV09A discovery accepted; `/teacher-os/improve` is PlaceholderPage; ADR-AIEOS-055 read handoff exists but Improve implementation authority is missing; least new state is TeachingWork + new IntentType rather than a second aggregate. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-056](../decisions/ADR-AIEOS-056-aieos-improve-remediation-authority.md) Frozen / Approved **2026-09-04** (v1.0.2). Chronology: TOS-DEV09A discovery → TOS-DEV09P1 design + adversarial validation → TOS-DEV09P1R1 provenance + AI-input correction (Proposed v1.0.0 / v1.0.1) → Chief Architect architecture review **ACCEPTED 2026-09-04** → Founder / Product Architecture **Frozen / Approved 2026-09-04**. |
| **What was deliberately NOT implemented at architecture freeze time** | Backend; Frontend; Product; migration; OpenAPI; DEV09-I01+; Teacher Memory; learner groups; mastery; Improve NATS events; Temporal; auto-recommendations; Assessment note/Observation body Teaching copies; production deployment. `/teacher-os/improve` was PlaceholderPage. *(Historical freeze-time boundary — not a current-status claim.)* |
| **Governing decisions** | ADR-AIEOS-056 (Frozen / Approved); ADR-AIEOS-055 (Assessment ownership); ADR-AIEOS-054 / 053 / 052 / 027; ADR-045; ADR-048. |
| **Current status** | **Architecture Frozen / Approved.** Founder / Product Architecture approved **2026-09-04**. Chief Architect review **ACCEPTED — 2026-09-04**. OPTION B frozen. Origin pins Assessment revision + `source_class_result_level_snapshot`. Teacher-confirmed `goal_text` is sole remediation generator instruction. **TOS-DEV09 implementation COMPLETE** (DEV09-I01–I04 formally closed; real-stack Product E2E COMPLETE). Governed pins: Backend `62733e3ad0d48887f3cd1e1a4486839170a5d651`; Frontend `732c0b5f88b7342d27e6ee7f103cb1d182ed310b`; Alembic `tosd090002`. Historical ADR-AIEOS-056 body unchanged. |

---

## 25. ADR-AIEOS-057 — Teacher OS Development-Complete Experience Authority

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture for Teacher OS TOS-DEV10 Development Ready experience boundary: Library v1 Content façade, Teacher Memory v1 preferences, contextual AI Assistant v1, Mission remediation presentation, DEV04 bounded planning sufficiency, MCP-READY posture. |
| **Architectural reason** | TOS-DEV10A readiness audit accepted; loop through Improve is implemented; Development Ready still requires Library / Memory / Assistant authority without inventing parallel SoRs, FE→provider paths, or Planner/MCP platforms. |
| **What was implemented at architecture freeze** | Architecture source only: [ADR-AIEOS-057](../decisions/ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md) **Frozen / Approved** **2026-09-06** (v1.0.2). Chronology: TOS-DEV10A → TOS-DEV10P1 Proposed deposit (v1.0.0) → TOS-DEV10P1R1 Memory-owner / Proposed-wording correction (v1.0.1) → Chief Architect architecture review **ACCEPTED** → Founder / Product Architecture **Frozen / Approved 2026-09-06**. |
| **What was deliberately NOT implemented at architecture freeze time** | Backend/Frontend Library/Memory/Assistant implementation; Chat SoR; Planner Agent; broad MCP; curriculum platform; production work; TOS-DEV10-I02+. *(Historical freeze-time boundary — ADR-057 architecture freeze did not itself authorize implementation; not a current-status claim.)* |
| **Governing decisions** | ADR-AIEOS-057 (Frozen / Approved); ADR-AIEOS-056–052; ADR-AIEOS-027; ADR-044; ADR-042–048. |
| **Subsequent authorized implementation** | **TOS-DEV10 COMPLETE** under ADR-AIEOS-057 — **TEACHER OS DEVELOPMENT READY**. **I01** — Mission remediation-aware presentation (derived-on-read; remediation/improvement work framing; ADR-AIEOS-056 retained). **I02** — Library v1 (Generic Content read/reuse façade; no Library SoR). **I03** — Teacher Memory v1 (durable represented-HUMAN teacher-owned explicit preference state; ≠ Continuous Context). **I04 / I04R1** — Contextual AI Assistant v1 (AIEOS application API only; READ/REASON/SUGGEST; no silent authoritative mutations; session-scoped history; no Chat SoR) + NON_PRODUCTION demo-data substrate. Final evidence: Backend `0bb2a9cb09bda41370b89c2e4dcc3239074bcc92`; Frontend `070276145623c889d5db6346150cf420735b04f1`; OpenAPI SHA-256 `4BF6C88B662D99F1E0E21E6F0AF2D267B39644300D85D99A859A7720F1568411`; Alembic `tosd100001`; Backend CI `34081972651` SUCCESS; Frontend CI `34082275817` SUCCESS including Product E2E. Architecture record synchronization = **TOS-DEV10-C01**. |
| **Current status** | **Architecture Frozen / Approved.** Founder / Product Architecture **APPROVED — 2026-09-06**. Chief Architect architecture review **ACCEPTED**. **TOS-DEV10 implementation COMPLETE** (I01–I04 / I04R1 formally closed). Teacher OS **DEVELOPMENT READY**. **Development Ready ≠ Production Ready.** Historical ADR-AIEOS-057 normative body unchanged. Production deployment, Student OS / Parent OS / Principal OS / full ERP, broad MCP / Planner Agent / RAG / learner mastery remain **not authorized**. |

---

## 26. TOS-CX01 — Teacher OS Client Showcase Ready

| Field | Content |
|-------|---------|
| **Objective** | Record implemented Teacher OS Client Showcase Ready product state against existing architecture, without reopening Teacher OS domain authority or inventing a new ADR. |
| **Architectural reason** | TOS-DEV10 closed Development Ready. TOS-CX01 closed teacher-readable presentation, Prepare/Review UX excellence, Groq Real AI via the existing Model Gateway, and Founder Real-AI experience acceptance. Those outcomes do not require a new domain ADR. |
| **What was implemented** | **TOS-CX01 COMPLETE — TEACHER OS CLIENT SHOWCASE READY.** **I01** — shared `ArtifactRenderer` (`lesson_plan`, `worksheet`, `quiz`, `homework`, `answer_key`, `teacher_notes`); structured payload internally, teacher-readable presentation externally; normal Library/Work Artifact views no longer expose raw JSON. **I02** — teacher-first Prepare; professional six-resource Preparation Kit; human-readable Educational Quality; technical validation codes hidden from primary teacher presentation; teacher-centered Review Queue; `ArtifactRenderer` in Review Detail; ETag/schema/aggregate-revision hidden from normal teacher UI; Generated ≠ Approved ≠ Published retained; Review remains Approve / Request Changes / Reject. **I03** — AIEOS Model Gateway Groq provider adapter (`provider_id` = `groq`; development/showcase model `openai/gpt-oss-120b`); OpenAI remains supported; Fake remains deterministic CI/development-test; Teacher OS → AIEOS application capability → `StructuredModelGateway` → configured provider; Provider Aggregator read-only runtime observability; no provider mutation UI; no frontend provider credential access. **I04** — Founder Real-AI Experience Accepted **2026-09-07** PASS. Evidence pins: Backend `611f683140ee779cb9453f6310bf30f9f1df572d`; Frontend `6daf18db239069847697e74669ce0bbed30f7951`; OpenAPI SHA-256 `D5CC3A53C789406C69D0207CB0A8778C2730FBE9544C567503EB256BDA92CEFB`; Alembic `tosd100001`. Accepted Real-AI evidence: Provider Aggregator REAL / Groq / `openai/gpt-oss-120b`; fresh Fractions and Photosynthesis six-artifact scenarios; cross-scenario artifacts meaningfully different; generation provenance `provider_id` = `groq`, `model_id` = `openai/gpt-oss-120b`; Contextual AI Assistant real provider verified; Assistant remains READ / REASON / SUGGEST. Architecture record synchronization = **TOS-CX01-C01**. |
| **What was deliberately NOT claimed** | Production Ready; production deployment; production credentials; production UAT; HA/DR certification; load/performance certification; production security completion; Student Intelligence implementation; Learner Attempt; Learner Submission; learner-level Assessment Intelligence; Principal / School Intelligence; Parent Intelligence; Admin/ERP AIEOS360 path; a new ADR. |
| **Governing decisions** | Existing ADR-042…048; ADR-044 Model Gateway / provider independence; ADR-AIEOS-052…057. **No new ADR.** |
| **Current status** | **TEACHER OS — CLIENT SHOWCASE READY.** Functional Development **COMPLETE**. Development Ready **YES**. Client Showcase Ready **YES**. Production Ready **NO**. Next active product programme = **AIEOS 360 CLIENT SHOWCASE** (target **2026-11-20**). **AIEOS360-S01-I04R1 = CLOSED** under [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md). [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) = **Frozen / Approved**. Learner Assessment Intelligence implementation **NOT STARTED / NOT AUTHORIZED**. **AIEOS360-S01-I05-B1** = **NEXT CANDIDATE — NOT YET AUTHORIZED**. |

---

## 27. ADR-AIEOS-058 — Student Assignment Consumption & Learner Attempt Authority

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture authority for the first AIEOS 360 Student Intelligence vertical: eligible student consumes exact assigned ContentVersion, LearnerAttempt, immutable LearnerSubmission, Learning Evidence boundary — without reopening TeachingAssignment or class-level ClassroomAssessment. |
| **Architectural reason** | ADR-AIEOS-053 deferred learner visibility / roster live-vs-snapshot / attempt / submission. ADR-AIEOS-055 reserved attempt/submission for Student / Learning. TOS-CX01 closed Teacher OS Client Showcase Ready. AIEOS360-S01 discovery ACCEPTED. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) **Frozen / Approved** (v1.0.2, Founder **2026-09-08**; Chief Architect **ACCEPTED / PASS**; AIEOS360-S01P1R1 retained: S01 lifecycle `IN_PROGRESS` → `SUBMITTED`; `ABANDONED` deferred; membership check-time race semantics). |
| **What was deliberately NOT implemented at architecture freeze time** | Backend; Frontend; Product; migration; OpenAPI; S01-I01+; roster SoR; student Principal kind; Temporal; Groq/Model Gateway on submit; Student Agent; MCP; production NATS Learning publication. Architecture freeze did **not** itself authorize implementation. |
| **Governing decisions** | ADR-AIEOS-058 (Frozen / Approved); ADR-AIEOS-053 (TeachingAssignment unchanged); ADR-AIEOS-055 (ClassroomAssessment class-level); ADR-AIEOS-023R1 (HUMAN Principal); ADR-AIEOS-024; ADR-AIEOS-025; ADR-AIEOS-027; ADR-AIEOS-046R1 (production Learning PUB HOLD). |
| **Subsequent authorized implementation** | **AIEOS360-S01-I01 through I04R1 = CLOSED.** I01 learner-membership façade; I02 Learning persistence; I03 Student-os / Learning APIs; I04 Student OS attempt UX; I04R1 additive Student real-stack product E2E. Evidence: Backend `921d35eb08890a4e1d86cf95daf9d38cdfc4a13c`; Frontend `65b59a0bd30d254fce92c322c0a7f437a90b08af`; OpenAPI SHA-256 `4691D6BADA2157D436435BB5CCDD6797EA670D1A87543D42CA39A478F940F330`; Alembic `a360s010002`. Historical ADR-AIEOS-058 body unchanged. |
| **Current status** | **Architecture Frozen / Approved.** **I04R1 = CLOSED.** Learner Assessment Intelligence architecture is **Frozen / Approved** under ADR-AIEOS-059. Implementation remains **NOT STARTED / NOT AUTHORIZED**. **AIEOS360-S01-I05-B1** = **NEXT CANDIDATE — NOT YET AUTHORIZED**. |

---

## 28. ADR-AIEOS-059 — Learner Assessment Intelligence & Teacher Improve Handoff Authority

| Field | Content |
|-------|---------|
| **Objective** | Freeze architecture for Assessment-owned durable `LearnerAssessmentEvaluation` plus derived Teacher Assessment Intelligence, composing with existing ClassroomAssessment and ADR-AIEOS-056 Improve without moving grades into Learning or inventing an Improve SoR. |
| **Architectural reason** | AIEOS360-S01-I04R1 closed raw LearnerSubmission. Teachers still lack trustworthy submission-scoped evaluation evidence. AIEOS360-S01-I05A ACCEPTED OPTION D. |
| **What was implemented** | Architecture source only: [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) **Frozen / Approved** (v1.0.2, AIEOS360-S01P2R2; Founder / Product Architecture **2026-09-09**; Chief Architect **ACCEPTED / PASS**). Prior Proposed deposit (v1.0.0) and unanswered-evidence correction (v1.0.1) retained as accepted semantics. |
| **What was deliberately NOT claimed** | Backend; Frontend; Product; migration; OpenAPI; NATS; Temporal; I05-B1+ implementation; mastery; AI grading; automatic Improve; learner evaluation self-read; Principal / Parent intelligence; Production Ready. |
| **Governing decisions** | ADR-AIEOS-059 (Frozen / Approved); ADR-AIEOS-058 Learning ownership; ADR-AIEOS-055 ClassroomAssessment class-level; ADR-AIEOS-056 Improve unchanged; ADR-AIEOS-023R1 / 024 / 025 / 028 / 031 / 053 / 054. |
| **Current status** | **Frozen / Approved.** Learner Assessment Intelligence implementation **NOT STARTED / NOT AUTHORIZED**. **AIEOS360-S01-I05-B1** = **NEXT CANDIDATE — NOT YET AUTHORIZED**. |

---

## Gaps / missing chronology

Where older pre-Teacher-OS platform history (earlier Platform AI packages, ERP modules, etc.) is relevant but not part of this AIEOS journey spine: **Not established by current repository evidence** as a fully sequenced AIEOS chronology in this folder — treat as adjacent capability history under product/API repos.
