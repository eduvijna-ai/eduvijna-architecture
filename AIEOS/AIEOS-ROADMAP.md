# AIEOS — Roadmap

**Purpose:** High-level roadmap for EduVijna AIEOS  
**Rule:** Do **not** invent an artificial detailed roadmap. Use existing repository blueprint / PA phases.  
**Rule:** Discovery recommendations are **not** approved implementation.

---

## Authority note

Conflict preference:

1. Approved architecture decisions  
2. Approved product / engineering documents  
3. Current source code / contracts  
4. AIEOS orientation documents

Labels used below:

- **Approved** — authorized / accepted decision or closed approved slice  
- **Proposed** — discovery or blueprint-derived recommendation pending architecture authorization  
- **Deferred** — consciously not now  
- **Future** — vision / later phase

---

## Completed

| Item | Status | Notes |
|------|--------|-------|
| AIEOS product identity orientation | Approved (project context) | EduVijna = AIEOS complete product |
| Teacher OS product architecture foundation (PA-001 / TLM-001) | Approved (product docs) | Teacher OS subsystem model |
| Engineering Constitution EBP-000 v1.0 | Approved / Frozen | Implementation standards |
| ADR-042 … ADR-048 | Approved | Teacher OS architecture set |
| EBP-001.1 Teacher OS Shell | Approved | Closed slice |
| EBP-001.2 Today's Mission | Approved | Closed UX slice (mock-backed data) |
| EBP-001.3 Teaching Intent | Approved | Closed UX slice |
| EBP-001.4 Intent → Preparing Bridge | Approved | Closed bridge slice |
| EBP-001.5 Review Queue | Approved | Closed UX/semantics; mock SoR |
| EBP-001.6 Continuous Context | Approved | Session Context; not Memory |
| EBP-001.7 Mission Service Hardening | Approved | Closed hardening slice |
| EBP-001.8 Teacher / School Context | Approved (slice tracking) | Read surface; not Memory |
| TOS-DEV04 — Prepare Tomorrow native implementation | Approved / Complete | Backend `origin/main` `06e05277e73e0c71172cae4904efb37d771c3fad` |
| TOS-DEV06 — TeachingAssignment native implementation + Product E2E | Approved / Complete | Backend `06e05277e73e0c71172cae4904efb37d771c3fad`; Frontend `89ee9f1330f635de3186d21e0102cb63c5c698e1` (TOS-DEV06-I05) |
| TOS-DEV09 — Class-level Improve & Remediation | Approved / Complete | ADR-AIEOS-056 Frozen / Approved; DEV09-I01–I04 formally closed; Backend `62733e3ad0d48887f3cd1e1a4486839170a5d651`; Frontend `732c0b5f88b7342d27e6ee7f103cb1d182ed310b`; Alembic `tosd090002` |
| TOS-DEV10 — Teacher OS Development Ready | Approved / Complete | ADR-AIEOS-057 Frozen / Approved; I01–I04 / I04R1 formally closed; Backend `0bb2a9cb09bda41370b89c2e4dcc3239074bcc92`; Frontend `070276145623c889d5db6346150cf420735b04f1`; OpenAPI `4BF6C88B662D99F1E0E21E6F0AF2D267B39644300D85D99A859A7720F1568411`; Alembic `tosd100001`; **Development Ready ≠ Production Ready** |
| TOS-CX01 — Teacher OS Client Showcase Ready | Approved / Complete | I01–I03 MERGED / POST-MERGE VERIFIED / FOUNDER VERIFIED / CLOSED; I04 Founder Real-AI Experience Accepted **2026-09-07** PASS; no new ADR; Backend `611f683140ee779cb9453f6310bf30f9f1df572d`; Frontend `6daf18db239069847697e74669ce0bbed30f7951`; OpenAPI SHA-256 `D5CC3A53C789406C69D0207CB0A8778C2730FBE9544C567503EB256BDA92CEFB`; Alembic `tosd100001`; **TEACHER OS — CLIENT SHOWCASE READY**; **Client Showcase Ready ≠ Production Ready** |
| **AIEOS360-S01-I01 through I04R1** — Student assignment consumption / LearnerAttempt / LearnerSubmission | Approved / Complete | ADR-AIEOS-058 Frozen / Approved (historical body unchanged); Backend `921d35eb08890a4e1d86cf95daf9d38cdfc4a13c`; Frontend `65b59a0bd30d254fce92c322c0a7f437a90b08af`; OpenAPI SHA-256 `4691D6BADA2157D436435BB5CCDD6797EA670D1A87543D42CA39A478F940F330`; Alembic `a360s010002`; **I04R1 = CLOSED** |
| **AIEOS360-S01-I05** — Learner Assessment Intelligence & Teacher Improve handoff | Approved / Complete | ADR-AIEOS-059 Frozen / Approved (historical body unchanged); **B1 → B2 → B3 → F1 → E2E COMPLETE / CLOSED**; Backend `3d25bb2d7ae3a6a95affdf075a75f20db48a6959`; Frontend `2fe17e349bfcf772377bebd0718e1094936adaae`; OpenAPI SHA-256 `7B51CE21725651B8D556B9DD6D264473DF0A2E7CAF30D722E1CC776C651FAFBB`; Alembic `a360s010004` |
| **AIEOS360-S02** — Principal / School Intelligence | Approved / Complete | ADR-AIEOS-060 Frozen / Approved (historical body unchanged); **I01 → I02 → I03 → I04 CLOSED**; Architecture merge `423fd6683b86c8b36798f870a739864fed387f4b`; Backend `e2bfce86afece6772eaf7c2f1eb18e2dd2240f1b`; Frontend `1b4263d0668f66d84cc261c79a2e81883375219e`; OpenAPI SHA-256 `BE60CC2A4612F77AB333088D264B9501B9AB842995AEC1539DA89EA0E8462B47`; Alembic `a360s010004`; program closeout **AIEOS360-S02-C01** |
| **AIEOS360-S03** — Parent Intelligence | Approved / Complete | ADR-AIEOS-061 Frozen / Approved (historical body unchanged); **I01 → I02 / I02R1 → I03 → I04 CLOSED**; Architecture merge `67f4020b78cacdf1716e18d83f4410cb16fdcb4d`; Backend `138f37bfa7a44c33b206c6b78118154bbb9bc8eb`; Frontend `20a06f048510a2519e0487d12ea7c16f59e7fd7c`; OpenAPI SHA-256 `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`; Alembic `a360s010004`; **Development Slice Complete = YES; Production Ready = NO**; program closeout **AIEOS360-S03-C01** |

---

## Current

| Item | Status | Notes |
|------|--------|-------|
| **AIEOS 360 CLIENT SHOWCASE** | **Active next product programme** | Target **2026-11-20** (development readiness only — **not** a production date). Shared vertical scenario: Teacher → Publish / Assign → Student → Attempt / Practice / Submit → Learning Evidence → Assessment Intelligence → Teacher Improve → Principal / School Intelligence → Parent Intelligence → Admin/ERP Context. Thin but REAL integrated path; no fake clickable prototype. **Not** sequenced as finish Student OS completely, then Principal OS completely, then Parent OS completely. |
| **AIEOS360-S01-I04R1** | **CLOSED** | Student assignment consumption / LearnerAttempt / LearnerSubmission closed against ADR-AIEOS-058 Frozen / Approved |
| [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) — Learner Assessment Intelligence & Teacher Improve Handoff Authority | **Frozen / Approved** · **I05 COMPLETE / CLOSED** | AIEOS360-S01P2R2; OPTION D; v1.0.2; Founder / Product Architecture **2026-09-09**; Chief Architect **ACCEPTED / PASS**; historical ADR body unchanged; **AIEOS360-S01-I05 = COMPLETE / CLOSED** (B1 → B2 → B3 → F1 → E2E); Backend `3d25bb2d7ae3a6a95affdf075a75f20db48a6959`; Frontend `2fe17e349bfcf772377bebd0718e1094936adaae`; Alembic `a360s010004`; OpenAPI SHA-256 `7B51CE21725651B8D556B9DD6D264473DF0A2E7CAF30D722E1CC776C651FAFBB` |
| [ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) — Principal / School Intelligence Authority | **Frozen / Approved** · **S02 DEVELOPMENT SLICE COMPLETE / CLOSED** | AIEOS360-S02P1F; v1.0.1; Founder / Product Architecture approval: **2026-09-16**; Chief Architect architecture review: **ACCEPTED / PASS**; historical ADR body unchanged; **I01–I04 CLOSED**; Architecture merge `423fd6683b86c8b36798f870a739864fed387f4b`; Backend `e2bfce86afece6772eaf7c2f1eb18e2dd2240f1b`; Frontend `1b4263d0668f66d84cc261c79a2e81883375219e`; OpenAPI SHA-256 `BE60CC2A4612F77AB333088D264B9501B9AB842995AEC1539DA89EA0E8462B47`; Alembic `a360s010004`; program closeout **AIEOS360-S02-C01** |
| [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) — Parent Intelligence & Learner Access Authority | **Frozen / Approved** · **S03 DEVELOPMENT SLICE COMPLETE / CLOSED** | AIEOS360-S03P3F; v1.0.1; Founder / Product Architecture approval **2026-09-17**; Chief Architect exact-head review **ACCEPTED / PASS**; historical ADR body unchanged; **I01–I04 CLOSED**; Architecture merge `67f4020b78cacdf1716e18d83f4410cb16fdcb4d`; Backend `138f37bfa7a44c33b206c6b78118154bbb9bc8eb`; Frontend `20a06f048510a2519e0487d12ea7c16f59e7fd7c`; OpenAPI SHA-256 `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`; Alembic `a360s010004`; program closeout **AIEOS360-S03-C01**; **Development Slice Complete = YES; Production Ready = NO** |
| [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) — Admin / ERP School Context Current-Authority Boundary | **Frozen / Approved** | AIEOS360-S04P3F; v1.0.1; Founder / Product Architecture approval **2026-09-17**; Chief Architect architecture review **AIEOS360-S04P2R1 ACCEPTED / PASS**; **IMPLEMENTATION NOT AUTHORIZED**; **S04-I01 = NOT STARTED / NOT AUTHORIZED**; **AIEOS360-S04P1 = DISCOVERY ACCEPTED / PASS**; Option A approved architecture direction |
| **AIEOS360-S03 — Parent Intelligence** | **DEVELOPMENT SLICE COMPLETE / CLOSED** | ADR-AIEOS-061 **Frozen / Approved** v1.0.1; historical ADR body unchanged; I01–I04 CLOSED. Does **not** claim Production Ready, production Parent access, or a complete Parent OS product. |
| **AIEOS360-S04 — Admin/ERP Context** | **ARCHITECTURE FROZEN / APPROVED** | **AIEOS360-S04P1 = DISCOVERY ACCEPTED / PASS.** [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) **Frozen / Approved** v1.0.1 (AIEOS360-S04P3F; Founder / Product Architecture approval **2026-09-17**; Chief Architect **AIEOS360-S04P2R1 ACCEPTED / PASS**). Option A approved architecture direction; external master + current-authority adapter; no Admin OS; no AIEOS school SoR; production remain fail closed. **S04 implementation = NOT AUTHORIZED.** **S04-I01 = NOT STARTED / NOT AUTHORIZED.** **S03 remains DEVELOPMENT SLICE COMPLETE / CLOSED. Production Ready = NO.** |
| Teacher OS behind `teacher_os_enabled` | Approved (flagged rollout path) | Default off pattern |
| EBP-001.9 Wave 1 next-slice discovery & preflight | Historical / superseded | Not current programme |
| Persistence / Content SoR design for durable Review Queue | **SATISFIED / HISTORICAL** | Native Generic Content + Review Queue path exists; do not reopen as active gap |

---

## Approved Next

No new implementation slice is recorded here as **Approved** solely because discovery suggested it.

| Item | Status | Notes |
|------|--------|-------|
| [ADR-AIEOS-052](../decisions/ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md) — Prepare Tomorrow multi-artifact kit architecture (TOS-DEV04) | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-08-28**; **TOS-DEV04 native implementation COMPLETE** (Backend `06e05277e73e0c71172cae4904efb37d771c3fad`); TOS-CX01-I03 development/showcase Groq Real AI via Model Gateway is implemented; production provider credentials remain **not** claimed |
| [ADR-AIEOS-053](../decisions/ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) — Teaching Assignment & Classroom Delivery Authority (TOS-DEV06) | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-08-31**; **TOS-DEV06 native implementation + Product E2E COMPLETE** (Backend `06e05277e73e0c71172cae4904efb37d771c3fad`; Frontend `89ee9f1330f635de3186d21e0102cb63c5c698e1`); external LMS / Student OS delivery deferred |
| [ADR-AIEOS-046R1](../decisions/ADR-AIEOS-046R1-aieos-production-event-plane-multi-domain-publisher-scope-revision.md) — Production Event Plane Multi-Domain Publisher Scope Revision | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-08-31**; TeachingAssignment outbox events **implemented** in TOS-DEV06-I03; production EVENT activation / NATS provisioning **NOT authorized** |
| [ADR-AIEOS-054](../decisions/ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) — Teaching Execution & Observation Authority (TOS-DEV07) | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-09-01**; HYBRID / Option D; TeachingExecution SoR; Assigned ≠ Taught ≠ Assessed ≠ Mastered; **TOS-DEV07 implementation COMPLETE** (DEV07-I01–I04 formally closed; real-stack Product E2E complete); program closeout synchronized by **TOS-DEV07-C01**; learner-specific / attendance / assessment / mastery / production NATS remain **not authorized** |
| [ADR-AIEOS-055](../decisions/ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) — Assessment & Learning Evidence Authority (TOS-DEV08) | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-09-03**; OPTION D class-level-first ClassroomAssessment; **TOS-DEV08 implementation COMPLETE** (DEV08-I01–I04 formally closed; real-stack Product E2E complete); program closeout synchronized by **TOS-DEV08-C01**; Backend `1fe28f4fd1a2a2070aa69d67daa49cd53ba5820d`; Frontend `30c94f3e0403b9a5a2e955c706766035490598f9`; Alembic `tosd080002`; learner-specific / mastery / Improve / production remain **not authorized** |
| [ADR-AIEOS-056](../decisions/ADR-AIEOS-056-aieos-improve-remediation-authority.md) — Improve & Remediation Authority (TOS-DEV09) | **Architecture Frozen / Approved** · **IMPLEMENTATION COMPLETE** | Founder / Product Architecture approval **2026-09-04**; Chief Architect architecture review **ACCEPTED — 2026-09-04**; OPTION B frozen; TeachingWork + `remediate_class` + immutable origin with `source_class_result_level_snapshot`; class-level only; **TOS-DEV09 implementation COMPLETE** (DEV09-I01–I04; real-stack Product E2E); Backend `62733e3ad0d48887f3cd1e1a4486839170a5d651`; Frontend `732c0b5f88b7342d27e6ee7f103cb1d182ed310b`; Alembic `tosd090002` |
| [ADR-AIEOS-057](../decisions/ADR-AIEOS-057-aieos-teacher-os-development-complete-experience-authority.md) — Teacher OS Development-Complete Experience Authority (TOS-DEV10) | **Architecture Frozen / Approved** · **IMPLEMENTATION COMPLETE** · **TEACHER OS DEVELOPMENT READY** | Founder / Product Architecture approval **2026-09-06**; Chief Architect architecture review **ACCEPTED**; TOS-DEV10A COMPLETE; **TOS-DEV10 implementation COMPLETE** (I01–I04 / I04R1 formally closed; program closeout synchronized by **TOS-DEV10-C01**); Library v1 / Teacher Memory v1 / contextual AI Assistant v1 / Mission remediation presentation; Backend `0bb2a9cb09bda41370b89c2e4dcc3239074bcc92`; Frontend `070276145623c889d5db6346150cf420735b04f1`; OpenAPI SHA-256 `4BF6C88B662D99F1E0E21E6F0AF2D267B39644300D85D99A859A7720F1568411`; Alembic `tosd100001`; Backend CI `34081972651` SUCCESS; Frontend CI `34082275817` SUCCESS including Product E2E; **Development Ready ≠ Production Ready**; production / Student OS / Parent OS / Principal OS / broad MCP / Planner Agent remain **not authorized** |
| TOS-DEV04 live provider proof (DEV04-I10) | **Not a production claim** | TOS-CX01-I03 delivered development/showcase Groq Real AI via Model Gateway; production provider credentials / production live-provider certification remain **not** claimed |
| Review Queue ↔ Existing Generators Integration (derived EBP-001.9 candidate) | **SATISFIED / HISTORICAL CANDIDATE** | Native TOS-DEV03/DEV04 + Generic Content implementation now provides the durable generate → ContentVersion(IN_REVIEW) → Review Queue path; old EBP-001.9 gap is superseded by current implementation. Historical record retained; no new implementation package. |
| Sprint 4 hardening / GA readiness (EBP-001) | **Proposed** (blueprint) | Production hardening remains deferred under Development Outcome First; not selected by TOS-CX01 |
| [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) — Student Assignment Consumption & Learner Attempt Authority (AIEOS360-S01) | **Architecture Frozen / Approved** | Founder / Product Architecture approval **2026-09-08**; Chief Architect architecture review **ACCEPTED / PASS**; v1.0.2; historical ADR body unchanged; **AIEOS360-S01-I01 through I04R1 = CLOSED**; Backend `921d35eb08890a4e1d86cf95daf9d38cdfc4a13c`; Frontend `65b59a0bd30d254fce92c322c0a7f437a90b08af`; Alembic `a360s010002`; OpenAPI SHA-256 `4691D6BADA2157D436435BB5CCDD6797EA670D1A87543D42CA39A478F940F330` |
| [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) — Learner Assessment Intelligence & Teacher Improve Handoff Authority (AIEOS360-S01P2) | **Architecture Frozen / Approved** · **I05 COMPLETE / CLOSED** | OPTION D Assessment-owned durable `LearnerAssessmentEvaluation` + derived Teacher Assessment Intelligence; ADR-AIEOS-056 Improve unchanged; Founder / Product Architecture **2026-09-09**; Chief Architect **ACCEPTED / PASS**; v1.0.2; historical ADR body unchanged; **AIEOS360-S01-I05 = COMPLETE / CLOSED** (B1 → B2 → B3 → F1 → E2E); Backend `3d25bb2d7ae3a6a95affdf075a75f20db48a6959`; Frontend `2fe17e349bfcf772377bebd0718e1094936adaae`; Alembic `a360s010004`; OpenAPI SHA-256 `7B51CE21725651B8D556B9DD6D264473DF0A2E7CAF30D722E1CC776C651FAFBB` |
| [ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) — Principal / School Intelligence Authority (AIEOS360-S02P1) | **Frozen / Approved** · **S02 DEVELOPMENT SLICE COMPLETE / CLOSED** | Cross-domain derived-on-request Principal / School Intelligence projection; not a business SoR; distinct School Scope Current Authority; `school.intelligence.read`; HUMAN; zero learner identities; no teacher ranking; learner-sensitive outcome aggregates deferred; Founder / Product Architecture approval: **2026-09-16**; historical ADR body unchanged; **I01–I04 CLOSED**; Backend `e2bfce86afece6772eaf7c2f1eb18e2dd2240f1b`; Frontend `1b4263d0668f66d84cc261c79a2e81883375219e`; OpenAPI SHA-256 `BE60CC2A4612F77AB333088D264B9501B9AB842995AEC1539DA89EA0E8462B47`; Alembic `a360s010004`; program closeout **AIEOS360-S02-C01** |
| [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) — Parent Intelligence & Learner Access Authority (AIEOS360-S03P3) | **Frozen / Approved** · **S03 DEVELOPMENT SLICE COMPLETE / CLOSED** | AIEOS360-S03P3F; v1.0.1; Founder / Product Architecture approval: **2026-09-17**; Chief Architect exact-head review: **ACCEPTED / PASS**. DERIVED_ON_REQUEST privacy-safe learner-scoped read projection; not a family/custody/Parent business SoR; `parent.intelligence.read` plus Parent Learner Access Current Authority; HUMAN adult actor; learner `learner_principal_id` only; authorization ≠ presentation; `EVALUATION_EXISTENCE = NO`; NATS/Temporal/Parent Agent = NO. Historical ADR body unchanged; **I01–I04 CLOSED**; Backend `138f37bfa7a44c33b206c6b78118154bbb9bc8eb`; Frontend `20a06f048510a2519e0487d12ea7c16f59e7fd7c`; OpenAPI SHA-256 `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`; Alembic `a360s010004`; program closeout **AIEOS360-S03-C01**; **Development Slice Complete = YES; Production Ready = NO** |
| [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) — Admin / ERP School Context Current-Authority Boundary (AIEOS360-S04P2) | **Frozen / Approved** | AIEOS360-S04P3F; v1.0.1; Founder / Product Architecture approval: **2026-09-17**; Chief Architect architecture review: **AIEOS360-S04P2R1 ACCEPTED / PASS**; **IMPLEMENTATION NOT AUTHORIZED**; **S04-I01 = NOT STARTED / NOT AUTHORIZED**; **AIEOS360-S04P1 = DISCOVERY ACCEPTED / PASS**; Option A external master + current-authority adapter is now the **approved architecture direction**; four existing School Context ports preserved; coherent NON_PRODUCTION provider is not an AIEOS school SoR; no Admin OS / `PrincipalKind.ADMIN` / `admin.*` capability; production remain fail closed; production ERP/SIS integration remains deferred |

Architecture for multi-artifact Prepare Tomorrow is Frozen / Approved and **native TOS-DEV04 implementation is complete**. **ADR-AIEOS-054 (TOS-DEV07) is Frozen / Approved and TOS-DEV07 implementation (DEV07-I01 through DEV07-I04) is COMPLETE.** **ADR-AIEOS-055 (TOS-DEV08 Assessment) is Frozen / Approved** and **TOS-DEV08 implementation (DEV08-I01 through DEV08-I04) is COMPLETE**. **ADR-AIEOS-056 (TOS-DEV09 Improve & Remediation) is Frozen / Approved** and **TOS-DEV09 implementation (DEV09-I01 through DEV09-I04) is COMPLETE** (Backend `62733e3ad0d48887f3cd1e1a4486839170a5d651`; Frontend `732c0b5f88b7342d27e6ee7f103cb1d182ed310b`; Alembic `tosd090002`). **ADR-AIEOS-057 (TOS-DEV10 Development-Complete Experience) is Frozen / Approved** and **TOS-DEV10 implementation (I01–I04 / I04R1) is COMPLETE — TEACHER OS DEVELOPMENT READY** (Backend `0bb2a9cb09bda41370b89c2e4dcc3239074bcc92`; Frontend `070276145623c889d5db6346150cf420735b04f1`; OpenAPI SHA-256 `4BF6C88B662D99F1E0E21E6F0AF2D267B39644300D85D99A859A7720F1568411`; Alembic `tosd100001`; program closeout **TOS-DEV10-C01**). **TOS-CX01 is COMPLETE — TEACHER OS CLIENT SHOWCASE READY** (no new ADR; Backend `611f683140ee779cb9453f6310bf30f9f1df572d`; Frontend `6daf18db239069847697e74669ce0bbed30f7951`; OpenAPI SHA-256 `D5CC3A53C789406C69D0207CB0A8778C2730FBE9544C567503EB256BDA92CEFB`; Alembic `tosd100001`; program closeout **TOS-CX01-C01**). **Development Ready ≠ Client Showcase Ready ≠ Production Ready.** Production hardening remains deferred. Next active product programme is **AIEOS 360 CLIENT SHOWCASE** (target **2026-11-20**). **AIEOS360-S01-I04R1 = CLOSED** under [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) Frozen / Approved. [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) is **Frozen / Approved** and **AIEOS360-S01-I05 = COMPLETE / CLOSED** (B1 → B2 → B3 → F1 → E2E; Backend `3d25bb2d7ae3a6a95affdf075a75f20db48a6959`; Frontend `2fe17e349bfcf772377bebd0718e1094936adaae`; Alembic `a360s010004`; OpenAPI SHA-256 `7B51CE21725651B8D556B9DD6D264473DF0A2E7CAF30D722E1CC776C651FAFBB`; historical ADR-059 body unchanged). [ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) is **Frozen / Approved** (Founder / Product Architecture approval: **2026-09-16**; historical ADR body unchanged) and **AIEOS360-S02 = DEVELOPMENT SLICE COMPLETE / CLOSED** (I01–I04; Architecture merge `423fd6683b86c8b36798f870a739864fed387f4b`; Backend `e2bfce86afece6772eaf7c2f1eb18e2dd2240f1b`; Frontend `1b4263d0668f66d84cc261c79a2e81883375219e`; OpenAPI SHA-256 `BE60CC2A4612F77AB333088D264B9501B9AB842995AEC1539DA89EA0E8462B47`; Alembic `a360s010004`; program closeout **AIEOS360-S02-C01**). School Intelligence remains a derived-on-request privacy-safe read projection, not a business SoR. [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) is **Frozen / Approved** (Founder / Product Architecture approval: **2026-09-17**; historical ADR body unchanged) and **AIEOS360-S03 = DEVELOPMENT SLICE COMPLETE / CLOSED** (I01–I04; Architecture merge `67f4020b78cacdf1716e18d83f4410cb16fdcb4d`; Backend `138f37bfa7a44c33b206c6b78118154bbb9bc8eb`; Frontend `20a06f048510a2519e0487d12ea7c16f59e7fd7c`; OpenAPI SHA-256 `4042FB2725DA70A02A70EE09563B7698AE2E5DA82927614CAF1B5F7E6AA7C1D0`; Alembic `a360s010004`; program closeout **AIEOS360-S03-C01**). Parent Intelligence remains a derived-on-request privacy-safe learner-scoped read projection, not a family/custody/Parent business SoR. **Development Slice Complete = YES. Production Ready = NO. Production deployment = NOT AUTHORIZED.** **AIEOS360-S04P1 = DISCOVERY ACCEPTED / PASS.** [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) is **Frozen / Approved** v1.0.1 (AIEOS360-S04P3F; Founder / Product Architecture approval: **2026-09-17**; Chief Architect architecture review: **AIEOS360-S04P2R1 ACCEPTED / PASS**). **AIEOS360-S04 Admin / ERP Context architecture = FROZEN / APPROVED.** **S04 implementation = NOT AUTHORIZED.** **S04-I01 = NOT STARTED / NOT AUTHORIZED.** Production ERP/SIS integration remains **NOT IMPLEMENTED / NOT AUTHORIZED.** This freeze/closeout does **not** convert locked development-readiness dates into production dates.

---

## Deferred

| Item | Status | Notes |
|------|--------|-------|
| Teacher Memory v1 (durable explicit preferences) | Complete (DEV10) | TOS-DEV10-I03 under ADR-AIEOS-057; inferred personalization remains deferred |
| Personalization / inferred preferences | Deferred | Beyond Memory v1 explicit preferences |
| Agents | Deferred | ADR-044; not premature |
| MCP | Deferred | ADR-044; MCP-READY posture retained; not MCP-EVERYTHING |
| AI Assistant platforms beyond DEV10 v1 | Deferred | Contextual Assistant v1 complete (DEV10-I04 / I04R1); broader expansion deferred |
| External learner delivery / LMS / full Student OS | Deferred beyond thin S01 assignment consumption | Published ≠ Assigned; Assigned ≠ Attempted ≠ Submitted ([ADR-AIEOS-053](../decisions/ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md)); [ADR-AIEOS-058](../decisions/ADR-AIEOS-058-aieos-student-assignment-consumption-learner-attempt-authority.md) Frozen / Approved; **I04R1 = CLOSED** |
| Learner-level Assessment Intelligence | **AIEOS360-S01-I05 = COMPLETE / CLOSED** | [ADR-AIEOS-059](../decisions/ADR-AIEOS-059-aieos-learner-assessment-intelligence-teacher-improve-handoff-authority.md) **Frozen / Approved**; historical ADR body unchanged; B1 → B2 → B3 → F1 → E2E COMPLETE |
| Principal / School Intelligence | **AIEOS360-S02 DEVELOPMENT SLICE COMPLETE / CLOSED** | [ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) **Frozen / Approved**; historical ADR body unchanged; I01–I04 CLOSED. Deferred beyond this slice: learner-sensitive Principal outcome analytics; mastery / competency rollups; learner drill-down; teacher ranking/comparison; class-vs-class learner outcome comparison; materialized School Intelligence model; School Intelligence events / Temporal; Principal AI narrative/agent; production ERP/SIS School Context adapter; roster-derived submission-rate semantics; invented small-cohort minimum-N; production Principal authentication |
| Parent Intelligence | **AIEOS360-S03 DEVELOPMENT SLICE COMPLETE / CLOSED** | [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) **Frozen / Approved**; historical ADR body unchanged; I01–I04 CLOSED. Deferred beyond this slice: production Parent access; production ERP/SIS Parent Learner Access provider; family/custody/guardian master data; evaluation/mastery disclosure; Parent persistence; Parent mutations; NATS; Temporal; Parent Agent. **Development Slice Complete = YES. Production Ready = NO.** |
| Admin/ERP AIEOS360 path | **ARCHITECTURE FROZEN / APPROVED** | **AIEOS360-S04P1 = DISCOVERY ACCEPTED / PASS.** [ADR-AIEOS-062](../decisions/ADR-AIEOS-062-aieos-admin-erp-school-context-current-authority-boundary.md) **Frozen / Approved** v1.0.1. Option A approved architecture direction; external School Context master preserved; no AIEOS school SoR; no Admin OS; production remain fail closed. **S04 implementation = NOT AUTHORIZED.** **S04-I01 = NOT STARTED / NOT AUTHORIZED.** Production ERP/SIS integration remains deferred. |
| Student OS / Parent OS / Principal OS as sequential complete products | Not the AIEOS 360 strategy | Shared vertical scenario, not finish-each-OS-completely sequencing |
| New generators | Deferred | Distinct from configured Model Gateway providers |
| Major database redesign / unauthorized Content SoR creation | Deferred / blocked | Under architecture review |

---

## Future / Vision

From product architecture roadmap phases (vision sequencing — **Future**, not sprint commits):

| Phase | Status | Outcome (product docs) |
|-------|--------|------------------------|
| Phase 1 — Teacher OS Foundation | **Complete — Teacher OS DEVELOPMENT READY** (TOS-DEV10-C01) **and CLIENT SHOWCASE READY** (TOS-CX01-C01) | Daily loop through Improve + Library / Memory / Assistant v1 + teacher-readable artifacts + Groq Real AI via Model Gateway; Development Ready / Client Showcase Ready ≠ Production Ready; locked wider AIEOS dates unchanged |
| Phase 2 — Teaching Assistant | Future / AIEOS 360 shared vertical | Daily Loop depth; Observe/Assess/Improve; notifications — not a sequential “finish this OS completely” gate before Student |
| Phase 3 — Student Intelligence | AIEOS 360 shared vertical | Thin assignment consumption **AIEOS360-S01-I04R1 = CLOSED** (ADR-AIEOS-058 Frozen / Approved); Learner Assessment Intelligence **Frozen / Approved** (ADR-AIEOS-059) and **AIEOS360-S01-I05 = COMPLETE / CLOSED**; teacher-mediated personalisation / Learner Intelligence remain later depth |
| Phase 4 — School Intelligence | AIEOS 360 shared vertical | **AIEOS360-S02 DEVELOPMENT SLICE COMPLETE / CLOSED**; [ADR-AIEOS-060](../decisions/ADR-AIEOS-060-aieos-principal-school-intelligence-authority.md) **Frozen / Approved**; historical ADR body unchanged; I01–I04 CLOSED; derived-on-request evidence-flow projection (`GET /api/v1/principal-os/school-intelligence`); not mastery; not a business SoR; Principal OS evidence-flow aggregates on the shared vertical, not after Student OS is “complete” |
| Phase 5 — Parent Intelligence | AIEOS 360 shared vertical | **AIEOS360-S03 DEVELOPMENT SLICE COMPLETE / CLOSED**; [ADR-AIEOS-061](../decisions/ADR-AIEOS-061-aieos-parent-intelligence-learner-access-authority.md) **Frozen / Approved**; historical ADR body unchanged; I01–I04 CLOSED; derived-on-request learner-scoped read projection (`GET /api/v1/parent-os/home`, `GET /api/v1/parent-os/children/{learner_principal_id}`); not evaluation; not a family/custody SoR; Parent OS on the shared vertical, not after Principal OS is “complete”; **Development Slice Complete = YES; Production Ready = NO** |

AI Engineering Platform sophistication (Agents, MCP, multi-provider routing beyond the current configured Model Gateway) remains **Future** behind stable product services (**ADR-044**). Groq is a configured `StructuredModelGateway` provider (`provider_id` = `groq`); Teacher OS is not coupled to Groq.

---

## Locked development-readiness programme targets

Development readiness only. These are **not** production dates.

| Programme | Target |
|-----------|--------|
| AIEOS 360 Client Showcase | **2026-11-20** |
| AIEOS v1 Development Ready | **2026-12-18** |
| Experience Depth Complete | **2027-01-29** |
| ERP / School Operations Complete | **2027-02-26** |
| Educational Intelligence + Knowledge | **2027-03-26** |
| Agentic AI + MCP + AI Engineering Platform | **2027-04-23** |
| Ecosystem / Founder / Developer / cross-platform | **2027-05-21** |
| Full Original AIEOS Development Complete | **2027-05-28** |

---

## Blueprint reminder (EBP-001 Wave 1)

Planned engineering sequence (not rewritten here):

```text
Sprint 0 flags + shell
  → Sprint 1 nav + Mission
  → Sprint 2 Review Queue (critical path)
  → Sprint 3 Continuous Context + dashboard depth
  → Sprint 4 hardening
```

EBP-001.1–001.8 delivered substantial UI spine; Sprint 2 durable generator→queue acceptance remains the critical unfinished Wave 1 gap per discovery evidence.

---

## Related

- `AIEOS-CURRENT-STATE.md`
- `AIEOS-VISION.md`
- `eduvijna-product/engineering/EBP-001/`
- `eduvijna-product/product-architecture/teacher-os/ROADMAP.md`
