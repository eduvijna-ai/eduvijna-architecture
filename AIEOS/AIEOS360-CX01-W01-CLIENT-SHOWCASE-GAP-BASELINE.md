# AIEOS360-CX01-W01 — Client Showcase Acceptance & Gap-Closure Baseline

**Identity:** `AIEOS360-CX01-W01`  
**Mode:** Architecture / programme discovery + record synchronization only  
**Programme:** AIEOS 360 CLIENT SHOWCASE (development readiness target **2026-11-20** — **not** a production date)  
**Nature:** Evidence-backed acceptance contract, capability matrix, canonical scenario, environment need, UX gap map, and ordered next implementation packages. **Does not authorize implementation.**

---

## Authority note

Conflict preference:

1. Approved architecture decisions  
2. Approved product / engineering documents  
3. Current source code / contracts  
4. AIEOS orientation documents

**Non-claims (binding):** Development Slice Complete ≠ Client Showcase Ready ≠ Production Ready. This workday does **not** claim Production Ready, production deployment, production ERP/SIS integration, Admin OS, full Educational Intelligence System, or broad Agent Framework / MCP / AI Engineering Platform completion (**2027-04-23**). Bounded v1 preparation orchestration (DEV04) and Contextual AI Assistant v1 remain **in** the November showcase baseline.

---

## Governed source gate (branch creation)

Recorded at workday execution against remote `origin/main`:

| Authority | Expected | Verified | Method |
|-----------|----------|----------|--------|
| Architecture `main` | `22dac0483bb39caf1c58bc7551732168722b113c` | **MATCH** | `git fetch origin main` + `gh api` commit |
| Backend `main` (`eduvijna-aieos-backend`) | `637583f42b7c475ef83f6f99bca7e65e665a253d` | **MATCH** | `gh api` + shallow clone |
| Frontend `main` (`eduvijna-aieos-frontend`) | `80125be6cf172afb5137e845752c5b4505e5a97f` | **MATCH** | `gh api` + shallow clone |
| Infrastructure `main` (`eduvijna-aieos-infrastructure`) | `a8654e5bc680eac1fa93cf8308d7cad904f4d7b9` | **MATCH** | `gh api` |
| Product `main` (`eduvijna-product`) | `b4b3048fb7a6a1c50ae8619dc490743714f2e3e2` | **MATCH** | `gh api` commit on public `eduvijna-ai/eduvijna-product` |
| OpenAPI SHA-256 (`contracts/openapi/aieos-v1.json`) | `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0` | **MATCH** | `sha256sum` on Backend `637583f42…` |
| Alembic head | `a360s010004` | **MATCH** | `migrations/versions/a360s010004_*.py` on Backend `637583f42…` |

**Gate result:** **PASS** — all governed authorities match independently (including Product `main`).

---

## 1. Showcase acceptance contract (reconstructed)

Reconstructed from [AIEOS-CURRENT-STATE.md](AIEOS-CURRENT-STATE.md), [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md), TOS-CX01-C01, AIEOS360-S01–S04 closeouts, and Frozen / Approved ADR-AIEOS-052…062 (historical ADR bodies unchanged).

### 1.1 Programme intent

| Element | Contract |
|---------|----------|
| **Outcome** | **AIEOS 360 Client Showcase Ready** — a thin but **REAL** integrated development vertical demonstrable to a client audience by **2026-11-20** |
| **Strategy** | Shared vertical scenario across roles — **not** sequential completion of whole Student OS → Principal OS → Parent OS products |
| **Vertical spine** | Teacher → Publish / Assign → Student → Attempt / Practice / Submit → Learning Evidence → Assessment Intelligence → Teacher Improve → Principal / School Intelligence → Parent Intelligence → Admin / ERP Context (current authority) |
| **Teacher baseline** | **TEACHER OS — CLIENT SHOWCASE READY** (TOS-CX01-C01): teacher-readable artifacts, Prepare/Review UX, Groq Real AI via Model Gateway (development/showcase), Founder Real-AI acceptance **2026-09-07** |
| **AIEOS360 development slices** | S01–S04 **DEVELOPMENT SLICE COMPLETE / CLOSED** at governed pins above; **Option A — External Master + AIEOS Current-Authority Adapter** is the approved ADR-AIEOS-062 ownership model; `DevelopmentCoherentSchoolContextProvider` is the **Option D coherent NON_PRODUCTION provider** — the implementation specialization of approved Option A (not a different ownership model) |
| **Bounded agentic showcase baseline** | DEV04 bounded multi-artifact preparation orchestration + Contextual AI Assistant v1 (READ/REASON/SUGGEST) — **preserved**; separate Planner Agent and broad Agent Framework / MCP platform **not** in scope |
| **Proof standard** | Real-stack journeys with shared PostgreSQL 18 and **zero** `/api` Playwright mocks for integrated proofs (S01-I05-E2E, S04-I03-E2E) |
| **Explicit exclusions** | Production Ready; production deployment; production credentials; production ERP/SIS adapter; Admin OS; `PrincipalKind.ADMIN`; evaluation/mastery disclosure to Parent; Principal learner drill-down; **broad** Agent Framework / MCP / AI Engineering Platform (**2027-04-23**); full Educational Intelligence + Knowledge programme (**2027-03-26**) |

### 1.2 Semantic boundaries (showcase)

- **Published ≠ Assigned ≠ Attempted ≠ Submitted ≠ Evaluated ≠ Mastered** ([ADR-AIEOS-053](../decisions/ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md), [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md), [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md), [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)).
- **Assigned ≠ Taught ≠ Assessed ≠ Mastered** ([ADR-AIEOS-054](../decisions/ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md), [ADR-AIEOS-055](../decisions/ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md)).
- **School / Parent Intelligence** = DERIVED_ON_REQUEST read projections — not business SoRs ([ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md), [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md)).
- **Admin / ERP Context** = external current-authority boundary — not Admin OS ([ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)).
- **Real AI** = configured `StructuredModelGateway` providers (Groq development/showcase; Fake deterministic) — Teacher OS not coupled to Groq ([ADR-044](../decisions/ADR-044-ai-platform-behind-stable-services.md), TOS-CX01-I03).

### 1.3 Acceptance criteria for “Client Showcase Ready” (AIEOS 360)

When implementation packages derived from this baseline complete, the programme expects:

1. **Deterministic rehearsal** — one-command (or equivalent) reset/reseed of the canonical scenario on shared local/non-production data.
2. **Role entry points** — deliberate entry into Teacher, Student, Principal, and Parent experiences bound to the **same** coherent school story (ADR-AIEOS-062 §6 fact model).
3. **Human walkthrough** — a Founder/client can traverse the full vertical spine **without** engineering-only DEV session wiring or per-role ad hoc URLs.
4. **Showcase presentation** — Student / Principal / Parent surfaces meet client-demo quality (Teacher OS already at TOS-CX01 bar).
5. **Mode clarity** — deterministic vs real-AI provider mode is explicit and safe for rehearsal (extends TOS-CX01-I03/I04 pattern).
6. **Evidence** — integrated real-stack proof retained or superseded by showcase rehearsal harness; **no** claim of production readiness.

---

## 2. Capability evidence matrix

Classification legend:

- **A** — IMPLEMENTED + PROVEN  
- **B** — IMPLEMENTED BUT NOT SHOWCASE-INTEGRATED  
- **C** — PRESENTATION / UX GAP  
- **D** — MISSING + REQUIRED FOR SHOWCASE  
- **E** — DEFERRED BEYOND SHOWCASE  

Evidence pins: Backend `637583f42b7c475ef83f6f99bca7e65e665a253d`; Frontend `80125be6cf172afb5137e845752c5b4505e5a97f`; OpenAPI SHA-256 `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`; Alembic `a360s010004`.

| Capability area | Classification | Evidence summary |
|-----------------|----------------|------------------|
| **Teacher OS — daily loop** (Intent → Prepare → Review → Publish → Assign → Teach → Assess → Improve) | **A** | TOS-DEV04…DEV10 + TOS-CX01; Backend/Frontend pins; Product E2E history |
| **Teacher OS — client showcase bar** (ArtifactRenderer, Prepare/Review UX, Real AI) | **A** | TOS-CX01-C01; Founder acceptance **2026-09-07** |
| **Student Intelligence — assignment consumption** | **A** | AIEOS360-S01-I04R1; ADR-AIEOS-058 |
| **Learner Assessment Intelligence** | **A** | AIEOS360-S01-I05; ADR-AIEOS-059; cross-role E2E |
| **Teacher Improve handoff** (post learner evaluation) | **A** | AIEOS360-S01-I05-E2E; ADR-AIEOS-056 path unchanged |
| **Principal / School Intelligence** | **A** / **B** | S02 I01–I04 closed; GET `principal_os_school_intelligence_get` — **proven in E2E** but **not** integrated into a unified client rehearsal shell (**B**) |
| **Parent Intelligence** | **A** / **B** | S03 I01–I04 closed; Parent Home/Child GET — **proven in E2E** but **not** showcase-integrated (**B**) |
| **Admin / ERP School Context** | **A** (substrate) | S04-I01/I02: `DevelopmentCoherentSchoolContextProvider`; no user-facing Admin OS (**E** for Admin OS) |
| **Cross-role learning loop (data plane)** | **A** | S04-I03 integrated cross-role real-stack E2E; shared PostgreSQL; zero API mocks |
| **Cross-role learning loop (human showcase)** | **D** | No unified launcher; separate DEV session / multi-origin E2E harness |
| **Unified Founder / Showcase environment** | **D** | See §4 — required for repeatable client rehearsal |
| **Student OS UX — showcase polish** | **C** | Functional attempt path proven; presentation below TOS-CX01 client bar |
| **Principal OS UX — showcase polish** | **C** | Read journey proven; minimal shell vs Teacher showcase depth |
| **Parent OS UX — showcase polish** | **C** | Read-only journey proven; client narrative layer thin |
| **Cross-role UX continuity** (shared story, handoffs, role switching) | **C** | No canonical cross-role navigation or scenario progress indicator |
| **Contextual AI Assistant (Teacher)** | **A** | TOS-DEV10-I04 / TOS-CX01 Real-AI verification; READ/REASON/SUGGEST |
| **Educational Intelligence — deterministic baseline** | **A** | Preparation Educational Quality v1 + OpenAPI types; bounded DEV04/DEV10 scope |
| **Educational Intelligence — knowledge / EIS programme** | **E** | Locked **2027-03-26**; `eduvijna-education-intelligence-engine` not part of Nov showcase |
| **Bounded agentic behaviours (v1 showcase baseline)** | **A** | TOS-DEV04 bounded preparation-kit orchestration ([ADR-AIEOS-052](../decisions/ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md)); Contextual AI Assistant v1 ([ADR-AIEOS-057](../decisions/ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md)); TOS-CX01 Real-AI verification; **no** Planner Agent; **no** new agent SoR/runtime/API |
| **Planner Agent** | **E** | Explicitly out of DEV10 / showcase baseline |
| **Agents / MCP / AI Engineering Platform (broad)** | **E** | ADR-044 deferred platform; MCP-READY posture only; locked **2027-04-23** |
| **Content / Generic Content SoR** | **A** | TOS-DEV03/DEV04 durable ContentVersion + Review Queue |
| **Asset / BlobStore production plane** | **E** | Architecture frozen; production composition **NOT AUTHORIZED** |
| **Workflow / Event production planes** | **E** | PED-I11/I12 source merged; production NATS/Temporal activation **NOT AUTHORIZED** |
| **Teacher Memory v1** | **A** | TOS-DEV10-I03 explicit preferences |
| **Production deployment / ERP live integration** | **E** | Explicit non-claims across ADRs and closeouts |

---

## 3. Canonical client-showcase school scenario

**Scenario ID:** `AIEOS360-CX-SCENARIO-01`  
**Authority:** ADR-AIEOS-062 §5–§7 coherent showcase fact model + AIEOS360-S04-I03-E2E realization  
**School-context source:** `DevelopmentCoherentSchoolContextProvider` — **Option D** coherent NON_PRODUCTION provider (implementation specialization of approved **Option A**); canonical defaults (not “the ERP”)

### 3.1 Narrative (one coherent school story)

One tenant contains a **HUMAN teacher**, **HUMAN learner(s)**, **HUMAN principal**, and **HUMAN parent/adult**, linked through **one ClassRef** such that:

- the teacher may assign to that class;
- the learner holds current membership in that class;
- the principal’s school scope includes that class;
- the adult’s parent access includes that learner.

### 3.2 Walkthrough beats (ordered)

| Step | Role | Action | Proof hook |
|------|------|--------|------------|
| 1 | Teacher | Prepare multi-artifact kit → Review → Approve → Publish | TOS-CX01 presentation; Generic Content SoR |
| 2 | Teacher | Assign published content to ClassRef | TeachingAssignment ADR-AIEOS-053 |
| 3 | Teacher | (Optional) Teach + class-level Assess | ADR-AIEOS-054/055 |
| 4 | Student | Start attempt → Save → Submit | ADR-AIEOS-058; LearnerSubmission durable |
| 5 | System | Current-policy learner evaluation | ADR-AIEOS-059; `LearnerAssessmentEvaluation` |
| 6 | Teacher | View Assessment Intelligence → deliberate Improve | ADR-AIEOS-059 → ADR-AIEOS-056 handoff |
| 7 | Principal | Refresh School Intelligence aggregates | ADR-AIEOS-060; privacy-safe counts |
| 8 | Parent | Home → authorized child detail (lifecycle vocabulary only) | ADR-AIEOS-061; `EVALUATION_EXISTENCE = NO` |
| 9 | (Implicit) | All roles reflect same ClassRef / learner facts | ADR-AIEOS-062 coherent provider |

### 3.3 Automated reference proof (by authority — do not over-merge)

| Walkthrough coverage | Governing proof | Steps |
|----------------------|-----------------|-------|
| **Teacher Publish / Assign → Student submit → learner evaluation → Principal / Parent reads** with coherent School Context | **AIEOS360-S04-I03-E2E** (`integrated-cross-role.product.spec.ts`) | Canonical scenario steps **2**, **4**, **5**, **7**, **8**, and implicit **9**; deterministic worksheet seeding; shared PostgreSQL; canonical `DevelopmentCoherentSchoolContextProvider` defaults; **zero** harness-local School Context maps |
| **Teacher Assessment Intelligence → deliberate Improve handoff** | **AIEOS360-S01-I05-E2E** | Step **6** — not asserted by S04-I03 |
| **Teacher Prepare (step 1)** | **TOS-CX01** + Teacher Product E2E history | Step **1** — not the S04-I03 integrated proof |
| **Optional Teach + class-level Assess** | **ADR-AIEOS-054 / ADR-AIEOS-055** + TOS-DEV07/DEV08 proofs | Step **3** — optional in the narrative; **not** part of S04-I03 |

S04-I03 proves the **integrated cross-role path** from assignment through learner evaluation to Principal / School Intelligence and Parent Intelligence reads under coherent current authority. It does **not** subsume S01-I05 Improve handoff or optional class-level Teach/Assess evidence.

---

## 4. Unified showcase environment need

| Question | Classification |
|----------|----------------|
| Is a current-main unified Founder/Showcase launcher **required**? | **YES — REQUIRED FOR SHOWCASE (classification D)** |

### 4.1 Rationale (evidence)

| Need | Current-main evidence | Gap |
|------|----------------------|-----|
| Deterministic reset/reseed | E2E scripts (`scripts/aieos360-s04-i03-e2e/`, `aieos360-i05-e2e/`) | Engineering harness only — not a unified operator surface |
| Role-specific entry points | Separate shells (`teacher-os`, `student-os`, `principal-os`, `parent-os`) + DEV session panel ([LOCAL-DEVELOPMENT.md](https://github.com/eduvijna-ai/eduvijna-aieos-frontend/blob/80125be6cf172afb5137e845752c5b4505e5a97f/docs/LOCAL-DEVELOPMENT.md) pattern) | No single showcase launcher mapping roles to principals |
| Shared database | S04-I03 / Product E2E use shared PostgreSQL 18 | Documented for E2E; not packaged for client rehearsal |
| Deterministic vs real-AI mode | `FakeStructuredModelGateway` + Groq via env composition; Provider Aggregator read-only | No showcase-level mode switch documented for full vertical |
| Repeatable client rehearsal | TOS-CX01 Founder Real-AI path is Teacher-only | AIEOS 360 needs **cross-role** rehearsal parity |

### 4.2 Architecture direction (no new ADR)

Package as **NON_PRODUCTION composition + UX** only: extend existing dev/E2E patterns; do **not** introduce Admin OS, new domain SoRs, or production ERP integration. Any implementation slice requires separate Chief Architect authorization.

---

## 5. Cross-role UX continuity gap map

| Gap ID | Description | Classification | Notes |
|--------|-------------|----------------|-------|
| UX-01 | No unified scenario launcher / progress map across roles | **D** | Blocks client rehearsal |
| UX-02 | DEV session connector is engineering-facing | **C** | Founder local docs assume manual tenant/bearer setup |
| UX-03 | Teacher dual chrome (classic + TeacherShell) | **C** | Known risk in current-state |
| UX-04 | Student / Principal / Parent visual polish vs TOS-CX01 | **C** | Functional correctness proven |
| UX-05 | No explicit “handoff” affordances (e.g., “view as principal after submit”) | **C** | Presentation only — no new domain semantics |
| UX-06 | Improve step visibility in cross-role narrative | **C** | Data plane proven in I05-E2E; showcase story weak |
| UX-07 | Real-AI vs deterministic labeling outside Teacher Prepare | **C** | Extend TOS-CX01 provider transparency pattern |
| UX-08 | Production ERP / Admin mutation UI | **E** | Explicitly out of scope |

---

## 6. Ordered implementation workdays / slices (from gaps only)

**Not authorized by this document.** Sequence closes **real** gaps above without reopening ADR-AIEOS-058…062 bodies.

| Order | Package | Objective | Primary repos | Depends on |
|-------|---------|-----------|---------------|------------|
| 1 | **AIEOS360-CX01-I01** | Showcase rehearsal environment — deterministic reseed + shared DB contract + operator docs | Frontend, Backend (composition only) | W01 baseline |
| 2 | **AIEOS360-CX01-I02** | Unified NON_PRODUCTION showcase launcher — role entry points bound to `AIEOS360-CX-SCENARIO-01` | Frontend (+ thin Backend dev aids if needed) | I01 |
| 3 | **AIEOS360-CX01-I03** | Cross-role UX continuity shell (scenario map, handoffs; no new APIs) | Frontend | I02 |
| 4 | **AIEOS360-CX01-I04** | Student OS showcase presentation uplift to client-demo bar | Frontend | I03 |
| 5 | **AIEOS360-CX01-I05** | Principal + Parent showcase presentation uplift | Frontend | I03 |
| 6 | **AIEOS360-CX01-I06** | Showcase mode governance — deterministic vs real-AI toggle + Provider Aggregator visibility | Frontend, Backend config surface | I02 |
| 7 | **AIEOS360-CX01-I07** | Integrated showcase rehearsal proof — human script + automated guard (extends S04-I03) | Frontend | I01–I06 |
| 8 | **AIEOS360-CX01-I08** | Founder Client Showcase acceptance + architecture closeout (CX01-C01) | Architecture, Product record | I07 |

**Deferred unchanged:** Experience Depth (**2027-01-29**), ERP/School Ops (**2027-02-26**), Educational Intelligence + Knowledge (**2027-03-26**), Agentic AI + MCP (**2027-04-23**), Ecosystem (**2027-05-21**), Full Original Development Complete (**2027-05-28**).

---

## 7. Locked programme targets (preserved)

| Programme | Target | Status after W01 |
|-----------|--------|------------------|
| AIEOS 360 Client Showcase | **2026-11-20** | **ACTIVE** — gap baseline established; implementation not started |
| AIEOS v1 Development Ready | **2026-12-18** | **PRESERVED** |
| Experience Depth Complete | **2027-01-29** | **PRESERVED (deferred)** |
| ERP / School Operations Complete | **2027-02-26** | **PRESERVED (deferred)** |
| Educational Intelligence + Knowledge | **2027-03-26** | **PRESERVED (deferred)** |
| Agentic AI + MCP + AI Engineering Platform | **2027-04-23** | **PRESERVED (deferred)** |
| Ecosystem / Founder / Developer / cross-platform | **2027-05-21** | **PRESERVED (deferred)** |
| Full Original AIEOS Development Complete | **2027-05-28** | **PRESERVED (deferred)** |

---

## 8. ADR / implementation authority

| Item | Result |
|------|--------|
| New ADR required? | **NO** — gaps expressible under existing Frozen / Approved ADR-AIEOS-052…062 and TOS-CX01 record |
| ADR-AIEOS-058…062 reopened? | **NO** |
| Backend / Frontend / Product / Infrastructure change in W01? | **NO** |

---

## Related

- [AIEOS-CURRENT-STATE.md](AIEOS-CURRENT-STATE.md)
- [AIEOS-ROADMAP.md](AIEOS-ROADMAP.md)
- [AIEOS-ARCHITECTURE-JOURNEY.md](AIEOS-ARCHITECTURE-JOURNEY.md)
- [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md)
