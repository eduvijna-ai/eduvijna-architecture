---
id: ADR-AIEOS-057
title: AIEOS Teacher OS Development-Complete Experience Authority
owner: EduVijna Enterprise Architecture Office · Chief AI Enterprise Architect
status: approved
version: 1.0.2
created: 2026-09-05
last_updated: 2026-09-06
reviewers:
  - Chief AI Enterprise Architect
  - Founder / Product Architecture
---

# ADR-AIEOS-057 — AIEOS Teacher OS Development-Complete Experience Authority

**Status:** Frozen / Approved  
**Chief Architect architecture review:** ACCEPTED  
**Founder / Product Architecture freeze:** APPROVED — 2026-09-06  
**Date:** 2026-09-06  
**Related:** [ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md) · [ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md) · [ADR-AIEOS-025](ADR-AIEOS-025-aieos-api-contract-integration-implementation-baseline.md) · [ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md) · [ADR-044](ADR-044-ai-platform-behind-stable-services.md) · [ADR-AIEOS-052](ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md) · [ADR-AIEOS-053](ADR-AIEOS-053-aieos-teaching-assignment-classroom-delivery-authority.md) · [ADR-AIEOS-054](ADR-AIEOS-054-aieos-teaching-execution-observation-authority.md) · [ADR-AIEOS-055](ADR-AIEOS-055-aieos-assessment-learning-evidence-authority.md) · [ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) · [ADR-042](ADR-042-teacher-os-shell-owns-ux.md) · [ADR-045](ADR-045-teaching-intent-owns-goals.md) · [ADR-046](ADR-046-artifact-status-lifecycle.md) · [ADR-048](ADR-048-review-queue-owns-approval.md)

**Catalogue note:** Frozen / Approved is **ARCHITECTURE AUTHORITY ONLY**. This ADR freezes the **AIEOS Teacher OS Development-Complete Experience Authority** for Teacher OS **TOS-DEV10 — Teacher OS Development Complete**. Founder / Product Architecture approval was granted **2026-09-06**. Architecture freeze ≠ Backend implementation authorization ≠ Frontend implementation authorization ≠ migration authorization ≠ OpenAPI authorization ≠ deployment authorization ≠ production mutation authorization. This architecture freeze does **not** itself authorize implementation. **TOS-DEV10-I02+** requires separate Chief Architect implementation authorization **after** ADR-057 architecture merge and post-merge closure. Library / Teacher Memory / AI Assistant implementation slices are **NOT AUTHORIZED** by this freeze alone.

**ID family note:** `ADR-AIEOS-057` is part of the AIEOS platform ADR family (`ADR-AIEOS-*`). It is distinct from Teacher OS product ADR-042–048 language decisions.

**Architecture programme:** **TOS-DEV10 — Teacher OS Development Complete**. TOS-DEV10A readiness audit is **COMPLETE / ACCEPTED**. This ADR **freezes** the experience boundary for Development Ready (not Production Ready).

Does **not** reopen or rewrite historical text of: ADR-AIEOS-056 (Improve); ADR-AIEOS-052–055; ADR-AIEOS-027; ADR-044 / ADR-042–048.

TOS-DEV10P1 design deposit and TOS-DEV10P1R1 Memory-owner / Proposed-wording correction were deposited as Proposed (v1.0.0 / v1.0.1) before freeze. Founder / Product Architecture approval was granted on **2026-09-06**. This freeze does **not** authorize implementation.

---

## Context

TOS-DEV10A established that the Teacher OS Daily Learning Loop through Improve is implemented on governed Backend/Frontend with real-stack Product E2E, while Development Ready still requires architecture + implementation for:

- Library v1
- Teacher Memory v1
- Contextual AI Assistant v1
- Mission remediation-aware presentation (ADR-AIEOS-056 authority; no new Mission SoR)
- Coherent primary-nav honesty (no knowingly unfinished Library / AI Assistant placeholders when those capabilities are in scope)

Educational Intelligence depth beyond deterministic educational-quality baselines, a separate Planner Agent, and a broad MCP ecosystem are **not** Development Ready prerequisites.

---

## Decision

### 1. Development-Complete product boundary

Teacher OS **Development Ready** requires a coherent working journey:

```text
Today's Mission
  → Teaching Work / Intent
  → Prepare
  → educational-quality checked preparation kit
  → Review
  → Publish
  → Assign
  → Teach / Observe
  → Assess
  → Improve
  → remediation Teaching Work
  → next Mission
```

**plus:**

- Library v1
- Teacher Memory v1
- contextual AI Assistant v1

**Bounded planning:** Existing DEV04 preparation-kit orchestration is **sufficient** as Teacher OS v1 bounded planning when current source continues:

```text
Teaching goal
  → approved preparation capability
  → coherent bounded artefact set
  → educational-quality checks
  → ContentVersion
  → human Review
```

A separate autonomous Planner Agent is **NOT** required for Development Ready.  
Broad MCP ecosystem is **NOT** required.

**MCP posture:** **MCP-READY**, **NOT MCP-EVERYTHING**.

---

### 2. Library authority

Teacher OS Library is a **read / reuse EXPERIENCE** over authoritative **Generic Content**.

It is **NOT**:

- a new Library SoR
- a new Content authority
- a DAM
- a CMS replacement
- a second version system
- a second publication system

**Authority remains:**

| Concern | Authority |
|---------|-----------|
| Content aggregate | Generic Content ([ADR-AIEOS-027](ADR-AIEOS-027-aieos-generic-content-implementation-baseline.md)) |
| Version payload | ContentVersion |
| Teacher approval | ReviewDecision ([ADR-048](ADR-048-review-queue-owns-approval.md)) |
| Publication | Publication |

Library v1 may **project** teacher-authorized Content including:

- content identity
- content type
- created/updated time
- stewardship state
- current version
- published version
- relevant TeachingWork relationship when available

Teacher-facing baseline:

- browse
- open
- preview
- state/type filtering
- reuse/navigation into existing governed surfaces

The Library boundary **must be teacher-authorized**. Do **NOT** expose a raw tenant-wide Content catalogue merely because a generic Content list endpoint can technically return tenant content.

**No new Library persistence is authorized.** Prefer an application/read façade over Generic Content.

---

### 3. Teacher Memory authority

Teacher Memory v1 is a **durable teacher-owned preference profile**.

It is **distinct from**:

- Continuous Context
- React/session state
- School Context
- current selected class/work
- JWT/session material
- security audit
- AI conversation history
- arbitrary behavioural surveillance

Teacher Memory v1 **SHALL** contain only explicit / teacher-controlled preference classes needed for current Teacher OS development, such as:

- teaching style preferences
- preferred difficulty
- preparation preferences
- output preferences
- presentation/format preferences

Use a governed **typed / schema-versioned** model.

**Required Teacher Memory owner identity boundary:**

The durable Teacher Memory **owner** SHALL be the **represented HUMAN teacher Principal**.

```text
tenant
  +
represented HUMAN teacher Principal
```

Do **not** define Memory ownership as the transport caller, authenticated workload, executing service, delegated actor, or audit effective actor merely because that actor performs the request.

**Security provenance remains separate** and must stay compatible with existing AIEOS identity/security authority ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md), [ADR-AIEOS-028](ADR-AIEOS-028-security-audit-mutation-accountability.md)):

- authenticated principal / caller
- represented principal
- effective actor where applicable
- delegation
- workload / service identity
- audit provenance

A delegated or service caller **MAY** be authorized to perform an operation only under existing security authority, but **MUST NOT** become the durable Teacher Memory owner by default.

This ADR does **not** redesign ADR-AIEOS-023R1.

It must carry ordinary aggregate revision / optimistic concurrency semantics consistent with AIEOS persistence architecture ([ADR-AIEOS-024](ADR-AIEOS-024-aieos-data-resource-sor-implementation-baseline.md)).

Teacher Memory is **server-authoritative durable state**. Frontend local storage is **NOT** Teacher Memory authority.

Teacher Memory v1 **MUST NOT** automatically infer permanent preferences from every teacher action or edit. Learn-from-edit / inferred personalization remains **future work**.

Teacher must be able to **inspect and deliberately change** durable preferences.

No learner-specific private profile data belongs in Teacher Memory v1.

---

### 4. Contextual AI Assistant authority

Teacher OS AI Assistant v1 is a **contextual AIEOS application capability**.

**Frontend:**

- **MUST** call AIEOS application API only ([ADR-044](ADR-044-ai-platform-behind-stable-services.md))
- **MUST NOT** directly call OpenAI, another model provider, MCP server, Agent runtime, or provider SDK

Assistant context is composed **server-side** from only currently authorized data. Eligible context may include, where applicable:

- Today's Mission
- Teaching Work
- Generic Content / ContentVersion
- Review state
- Publication state
- School/Class context
- TeachingAssignment
- TeachingExecution
- ClassroomAssessment
- remediation origin
- Teacher Memory v1

Receiving context does **NOT** grant new authority. Every context read remains subject to current tenant/principal authorization ([ADR-AIEOS-023R1](ADR-AIEOS-023R1-aieos-identity-tenant-security-canonical-restatement.md), [ADR-AIEOS-031](ADR-AIEOS-031-production-authorization-kernel.md)).

Assistant v1 is primarily **READ / REASON / SUGGEST**.

It **MUST NOT** silently:

- publish
- assign
- start teaching
- record assessment
- create remediation
- alter Teacher Memory
- mutate authoritative business state

Any business effect must continue through an existing explicit AIEOS command and teacher confirmation.

Assistant may produce explanation, contextual answer, proposed teaching intent, suggested next action, or draft text — **proposal ≠ committed business state**.

Use the existing provider-neutral Model Gateway / AI application boundary. Do **not** freeze OpenAI as architecture.

---

### 5. Assistant conversation durability

Teacher OS Development Ready does **NOT** require durable chat history.

For Assistant v1, conversation continuity may remain **browser/session scoped**.

Do **NOT** create a permanent Chat SoR merely to ship DEV10.

Teacher Memory stores durable preferences.  
**Assistant conversation history ≠ Teacher Memory.**

A future durable conversation/history architecture may be separately governed.

---

### 6. Bounded agentic planning

Existing DEV04 preparation-kit orchestration ([ADR-AIEOS-052](ADR-AIEOS-052-aieos-preparation-kit-multi-artifact-generation-architecture.md)) is sufficient as the bounded Teacher OS v1 planning capability under the conditions in §1.

Do **NOT** introduce an autonomous open-ended Agent solely to satisfy the word “agentic”.

```text
GenerationRun  ≠  Agent
Temporal       ≠  Agent
MCP            ≠  Agent
```

A future Planner Agent remains allowed **behind** stable AIEOS services but is **not** a DEV10 Development Ready prerequisite.

---

### 7. Educational Intelligence boundary

Current deterministic educational-quality baseline is **sufficient** for the Teacher OS Development Ready milestone.

Do **NOT** block DEV10 on:

- every board/country curriculum
- full curriculum SoR breadth
- comprehensive competencies platform
- autonomous pedagogy agent
- full knowledge/RAG platform

Positive curriculum-profile and deeper Educational Intelligence remain valid **future** depth.

Do **not** remove or weaken existing educational-quality checks.

---

### 8. Mission loop (presentation only)

[ADR-AIEOS-056](ADR-AIEOS-056-aieos-improve-remediation-authority.md) remains authority for Improve/remediation.

- No new Mission SoR is authorized.
- Today's Mission remains **derived-on-read**.
- When the selected active TeachingWork has `intent_type = remediate_class`, the teacher experience must identify it as remediation/improvement work rather than generic preparation.

This is **presentation / derived-next-action semantics**.

Do **NOT** create an Improve aggregate.  
Do **NOT** create Mission persistence.

---

### 9. Development Ready claim

Teacher OS must **NOT** be declared Development Ready while primary navigation contains knowingly unfinished Library or AI Assistant placeholders if those capabilities are part of the declared Development Ready scope.

**Settings** remains outside the required DEV10 completion gate unless separate evidence makes it necessary.

**Development Ready is NOT Production Ready.**

The following remain **outside** ADR-057 / DEV10:

- production deployment
- UAT certification
- HA/DR
- load/stress certification
- production hardening
- Student OS
- Parent OS
- Principal OS
- full ERP
- learner mastery
- broad MCP platform
- multi-provider routing
- broad RAG platform

---

## Consistency validation (freeze-time)

| Check | Result |
|-------|--------|
| Library does not become another SoR | **PASS** — façade over Generic Content |
| Memory ≠ Continuous Context / audit / surveillance | **PASS** — explicit preference profile only |
| Assistant cannot bypass application authorization | **PASS** — server-side context + existing auth |
| Assistant suggestions ≠ implicit business mutations | **PASS** — READ/REASON/SUGGEST only |
| Assistant conversation ≠ permanent Memory | **PASS** — session-scoped chat; Memory separate |
| MCP is not a frontend dependency | **PASS** — ADR-044; MCP-READY only |
| Generic Content remains authoritative | **PASS** — ADR-AIEOS-027 unchanged |
| Mission remains derived, not persisted | **PASS** — §8; ADR-AIEOS-056 Improve authority retained |
| Aligns with ADR-AIEOS-052–056 journey authorities | **PASS** — no reopen of Assign/Teach/Assess/Improve SoRs |

No exception invented where a conflict would exist.

---

## Consequences

### Positive

- Clear Development Ready experience boundary for TOS-DEV10 without conflating Production Ready.
- Library / Memory / Assistant can be implemented under explicit future authorization without inventing parallel SoRs or FE→provider paths.
- Mission remediation presentation can proceed under existing ADR-AIEOS-056 without new aggregates.

### Negative / constraints

- Architecture freeze alone does **not** authorize Library / Memory / Assistant implementation — **TOS-DEV10-I02+** remains separately gated.
- Tenant-wide Content list endpoints are insufficient as Library without teacher-authorization façade semantics.
- Durable chat SoR deferred — Assistant continuity is intentionally thinner for DEV10.

---

## Authorization boundary

This ADR is **Frozen / Approved**.

Frozen / Approved ≠ implementation authorization. **TOS-DEV10-I02+ is NOT AUTHORIZED.** Implementation requires a separate Chief Architect governed package after this architecture PR is merged and closure verified.

Architecture freeze ≠ Backend implementation authorization ≠ Frontend implementation authorization ≠ migration authorization ≠ OpenAPI authorization ≠ deployment authorization ≠ production mutation authorization.

Does **not** authorize: Backend, Frontend, Product, migration, OpenAPI, NATS, Temporal, Teacher Memory implementation, Library implementation, AI Assistant implementation, MCP ecosystem, DigitalOcean mutation, or production deployment.

---

## Founder decision

Founder / Product Architecture **APPROVED** AIEOS Teacher OS Development-Complete Experience Authority on **2026-09-06**.

Chief Architect architecture review: **ACCEPTED**.

This freeze freezes (architecture authority only):

- Teacher OS Development-Complete experience boundary
- Library v1 as Generic Content façade / read-reuse experience (no new Library SoR)
- Teacher Memory v1 durable represented-HUMAN-teacher preference profile
- contextual AI Assistant v1 through AIEOS application APIs only
- READ / REASON / SUGGEST assistant boundary (no silent authoritative business mutations)
- browser/session-scoped chat continuity acceptable for v1
- bounded DEV04 planning sufficient for Development Ready
- MCP-READY, not MCP-everything
- current deterministic Educational Intelligence baseline sufficient for Development Ready
- Mission remains derived-on-read

This freeze does **not** authorize Backend, Frontend, Product, migration, OpenAPI, TOS-DEV10-I02+, Library / Teacher Memory / AI Assistant implementation, Planner Agent, broad MCP, or production deployment.

---

## Programme status (orientation)

| Item | Status |
|------|--------|
| TOS-DEV10A | READINESS AUDIT COMPLETE / ACCEPTED |
| TOS-DEV10 | ACTIVE |
| ADR-AIEOS-057 | **Frozen / Approved** |
| DEV10 Library / Memory / Assistant implementation | **NOT YET IMPLEMENTED** / **NOT AUTHORIZED** by this freeze alone |
| Teacher OS Development Ready claim | **NOT CLAIMED** |
| Production readiness | **NOT CLAIMED** |

---

## References

- TOS-DEV10A — Teacher OS Development-Complete Readiness Audit (ACCEPTED / CLOSED)
- ADR-AIEOS-056 — Improve & Remediation Authority (Frozen / Approved; historical body unchanged)
- ADR-AIEOS-052 — Preparation Kit (bounded planning sufficiency)
- ADR-044 — AI platform behind stable product services
