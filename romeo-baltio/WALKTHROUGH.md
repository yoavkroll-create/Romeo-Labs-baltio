# Romeo Baltio — Framework Walkthrough

> This document is designed for a guided conversation. Open it with your manager and scroll through together.

---

## What Romeo Baltio Is

Romeo Baltio is a structured scoping framework powered by an AI agent (Baltio). A PM opens their project in an IDE, runs a slash command, and Baltio guides them through a conversation — asking the right questions, challenging weak assumptions, and producing structured deliverables at each stage.

The result is a complete product specification — from raw idea to developer-ready SDD — with every decision documented, validated, and quality-checked. Not a one-shot generation. A collaborative process, stage by stage.

---

## The Pipeline

```
/romeo-start
     ↓
1. Baseline Spec        ← Define what we're building + capture tech context
2a. Market Research     ← Understand the space + technical feasibility
2b. Deep Research       ← Go further on specific questions
     ↓
3. Initial PRD          ← Shape the product + tech direction forming
4. Prototype Spec       ← Data model, integrations, confirm stack
5. Validate Prototype   ← Test assumptions, score confidence
6. Iterate              ← Apply validation findings
     ↓
7. Final PRD            ← Lock product definition + lock tech spec
     ↓
8. Dev Handoff          ← Deliver to agentOS 2 / dev team
```

**Tech spec is not a separate stage.** It's a thread that runs through the entire pipeline — starting with constraints at Baseline, explored in Research, shaped in the Initial PRD, confirmed in the Prototype flow, and locked in the Final PRD. By the time a developer receives the handoff, every technical decision has been made progressively, not retroactively.

---

## Stage by Stage

### Stage 0 — Project Init (`/romeo-start`)

**What Baltio does:** Creates the project workspace. Asks for the product name, a short description, and the agentOS 2 path for later handoff. Initializes `.romeo-state.json` to track all progress.

**What gets saved:** Project folder, state file, session context.

---

### Stage 1 — Baseline Spec (`/romeo-baseline`)

**What Baltio does:** Interviews the PM about the product idea. Asks: who is the user, what problem are we solving, what does success look like, what are the must-have capabilities? Challenges vague answers with real-world analogies and pushback.

**Example questions asked:**
- "Who specifically is the primary user — what's their job and what are they doing the moment they feel this pain?"
- "What's the single most important thing this product must do on day one?"
- "Is there an existing product they're using today to solve this? What's broken about it?"
- "Are there existing systems this must integrate with or build on? Any hard tech constraints?"
- "What's the team's tech background — are there stack preferences or things that are non-negotiable?"

**Deliverables:**
- `baseline-spec.md` — System definition, users, problem, core capabilities, constraints, initial tech context
- `capability-list.md` — Prioritized list of what the product can do
- `happy-flow.md` — Step-by-step ideal user journey
- `research-questions.md` — Open questions to answer in research
- `research-prompts.md` — Pre-formatted prompts for the research stage

---

### Stage 2a — Market Research (`/romeo-research`)

**What Baltio does:** Uses the research questions from Baseline to guide structured market research. Asks the PM to run the research prompts, then works with the PM to synthesize findings into a structured report.

**Deliverables:**
- `research-report.md` — Competitive landscape, user insights, market context, key findings

---

### Stage 2b — Deep Research (`/romeo-deep-research`)

**What Baltio does:** Goes deeper on specific unknowns from Baseline — technical feasibility, niche user segments, edge cases. Runs in parallel with Research.

**Deliverables:**
- `deep-research-report.md` — Focused analysis on specific open questions

---

### Stage 3 — Initial PRD (`/romeo-initial-prd`)

**What Baltio does:** Takes all Baseline + Research findings and co-creates the first full product definition. Proposes scope cuts, challenges feature creep, applies MoSCoW/RICE thinking to prioritize.

**Example questions asked:**
- "You've listed 12 capabilities — if you could only ship 4, which are the ones users would pay for on day one?"
- "This flow assumes the user has already done X — is that a safe assumption or does the product need to handle it?"

**Deliverables:**
- `initial-prd.md` — Full product definition, scope (MVP/V2/V3), user flows
- `feature-list.md` — Every feature with scope tag, effort estimate, priority
- `core-user-flows.md` — Detailed step-by-step flows with error paths
- `ux-design-direction.md` — UX principles, interaction patterns, design references
- `prototype-prompt-mvp.md` — Ready-to-use prompt for building MVP prototype
- `prototype-prompt-future.md` — Ready-to-use prompt for future vision prototype

---

### Stage 4 — Prototype Spec (`/romeo-prototype`)

**What Baltio does:** Defines exactly what to build for the prototype — not the UI itself, but the specification for it. Focuses on data model, integrations, and what the prototype needs to prove.

**Deliverables:**
- `prototype-spec-mvp.md` — MVP prototype specification (screens, flows, demo mode)
- `prototype-spec-future.md` — Future vision prototype specification
- `data-model.md` — Entity definitions, relationships, state machines
- `data-samples.json` — Mock data with realistic examples
- `integration-strategy.md` — External service dependencies and API contracts

---

### Stage 5 — Validate Prototype (`/romeo-validate-prototype`)

**What Baltio does:** After the PM runs the prototype (built separately), Baltio helps score validation results. Was the hypothesis proven? What surprised users? What needs to change?

**Deliverables:**
- `validation-report.md` — Hypothesis results, user feedback synthesis, confidence scores

---

### Stage 6 — Iterate (`/romeo-iterate-prototype`)

**What Baltio does:** Takes validation findings and creates a concrete iteration plan. What changes, what stays, what gets cut from MVP.

**Deliverables:**
- `iteration-plan.md` — Prioritized list of changes based on validation

---

### Stage 7 — Final PRD (`/romeo-final-prd`)

**What Baltio does:** Produces the definitive product specification. Locks scope, flows, and execution plan. Critically — this is also where the **tech spec is finalized and locked**. By this point the stack has been explored across Baseline, Research, and the Prototype flow; the Final PRD consolidates all of that into a complete technical picture alongside the product decisions.

**Tech spec locked here includes:** architecture overview, full tech stack with rationale, services and integrations, domain model, database schema direction, API contract structure, deployment and infra decisions.

**Deliverables:**
- `final-prd.md` — 11-section comprehensive PRD including: system definition, scope, roadmap, features, flows, **full architecture + tech spec**, roles, domain model, integrations, analytics, execution plan
- `approved-feature-list.md` — Final locked feature list with effort estimates
- `execution-plan.md` — Phased delivery plan with dependencies

---

### Stage 8 — Dev Handoff (`/romeo-handoff`)

**What Baltio does:** Packages all outputs into agentOS 2 format. The dev team picks up a complete, structured set of files and starts building with shape-spec.

**Deliverables (agentOS 2 format):**
- `mission.md` — Product vision, users, problems, differentiators
- `roadmap.md` — Feature list with effort estimates
- `tech-stack.md` — Technology choices
- Per-feature spec files — Ready for `shape-spec`

---

## The Tech Spec Thread

Technical specification is woven through the pipeline — not bolted on at the end.

| Stage | What Gets Asked / Decided |
|-------|--------------------------|
| **Baseline** | Existing systems to integrate with, hard tech constraints, team's stack preferences |
| **Research** | Technical feasibility of key features, competitor tech choices, infrastructure patterns |
| **Initial PRD** | Tech direction forming — which services are needed, what the data model looks like at a high level |
| **Prototype** | Stack confirmed, data model defined with fields and types, integration contracts scoped, services identified |
| **Final PRD** | **Full tech spec locked** — architecture, tech stack with versions and rationale, services map, env config, DB schema, API contracts, deployment strategy, ADRs |
| **Handoff** | Tech spec consumed as-is — fed directly into agentOS 2 format |

By the time a dev picks up the handoff package, every technical decision has been made with the PM and confirmed against the product requirements — not filled in by the dev team during sprint 1.

---

## The Framework Inside

### Quality Gates (DoD)

Every stage has a **Definition of Done** checklist. After generating deliverables, Baltio evaluates each criterion and presents a pass/fail result. A stage is only marked `completed` when all critical items pass.

Example criteria from Final PRD DoD:
- Every MVP feature has a dev effort estimate (XS–XL)
- Every user flow includes at least one error/edge case path
- Architecture section names a specific tech stack, not just "TBD"
- Execution plan has phases with dependencies, not just a flat feature list

If something fails, Baltio works with the PM to fix it before moving on. No rubber-stamping.

### Readiness Check

After the DoD, a structured **Readiness Check** produces a binary result: **READY** or **NOT_READY**. NOT_READY lists the specific missing items. This result is stored in state and can be re-run as the PM refines deliverables.

### Interaction Philosophy

Baltio is not a document generator — it's a **collaborative PM + tech lead**. Key principles:

1. **Never produces a final deliverable on the first pass.** Every stage follows: Ask → Draft → Review → Refine → Finalize.
2. **Challenges weak assumptions.** If a feature is vague, Baltio asks "what does success look like for a real user in that moment?" It won't fill gaps with optimistic assumptions.
3. **Brings real-world knowledge.** Cites real products, design patterns, and benchmarks. Applies frameworks like RICE, MoSCoW, and ADRs naturally.
4. **Maintains context across sessions.** State is saved after every stage. The PM can close the IDE and pick up exactly where they left off — including all prior decisions.

### Session Continuity

Every project has a `.romeo-state.json` that tracks:
- Current stage and status
- All deliverable file paths
- DoD results per stage
- Timestamps and notes

When a PM opens a session, Baltio reads the state and immediately orients them: "You're at Stage 4. Your last completed action was `data-model.md`. Next step: run `/romeo-validate-prototype`."

---

## The End State — What a Completed Project Looks Like

After all stages, a project folder contains **25+ deliverables** including:

| Category | Files |
|----------|-------|
| Product definition | baseline-spec, capability-list, happy-flow, initial-prd, final-prd |
| Research | research-report, deep-research-report |
| Features | feature-list, approved-feature-list |
| UX | core-user-flows, ux-design-direction |
| Prototype | prototype-specs, validation-report, iteration-plan |
| Tech spec (locked in Final PRD) | architecture decisions, tech stack, services map, env config, database schema, API contracts |
| Dev handoff | mission, roadmap, tech-stack, feature spec files |

A developer receives: product context, locked feature scope, confirmed technical architecture, data schema, service inventory, environment configuration, and per-feature specs — everything needed to start building without a kickoff meeting.

---

## 8-Week Execution Plan

| Phase | Weeks | What Happens |
|-------|-------|--------------|
| **Discover** | 1–2 | First full pipeline run by Yoav. Friction log. PM team intro. Map tech spec gap across stages. |
| **Fix & Co-Design** | 3–4 | Fix top friction. 2 PM co-design sessions. Enhance Baseline → Prototype commands with tech questions. Expand Final PRD tech section. |
| **Onboard & Scale** | 5–6 | Reference project. PM guide. Early adopters run independently. Validate Final PRD tech section with a real dev. |
| **Adopt & Validate** | 7–8 | 4+ PMs using it. Manager + tech lead quality review. Lock Final PRD tech spec standard. v1.0 release. |

```
Week:    1    2    3    4    5    6    7    8
         |----|----|----|----|----|----|----|

FRAMEWORK
Yoav:    [= Full Pipeline Run =][Fix+Refine][Ref+Docs ][Final Polish]

TEAM CO-DESIGN
Team:    [Intro][Workshop]  [Co-design x2] [Adopters run own projects ...]
                                            [Retros   ][Team rollout ]

TECH SPEC THREAD (woven through pipeline, locked at Final PRD)
Yoav:    [Gap   ][Enhance Baseline][Enhance iPRD ][Validate ][Lock in Final PRD]
         [map   ][+ Research      ][+ Prototype  ][w/ dev   ][+ polish handoff ]
                                   [+ Final PRD  ]

VIEWER
Dev:     [Research][Proto v0.1][=== v0.2 ===][=== v0.3 ===]
```

**v1.0 is production-ready when:**
- 4+ PMs produce development-ready output independently
- A real developer picks up a tech-spec + handoff package and starts building without a kickoff meeting
- Manager rates Final PRD + Tech Spec as "dev-ready"
