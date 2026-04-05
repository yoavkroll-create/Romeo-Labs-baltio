# Romeo Baltio — Production Workplan

## Context

Romeo Baltio is at ~85% maturity but has **never been tested end-to-end by anyone**. The goal is to transform it from Yoav's solo creation into a team-driven, production-quality framework — shaped by PM team feedback, not built in isolation.

Three parallel tracks:
1. **Framework Quality** — Battle-test, fix, refine with lean loops
2. **Business Model** — Use Romeo Baltio to scope itself (dogfooding)
3. **Visual Interface** — Lightweight web viewer so PMs don't need IDE/CLI

**Approach:** Atomic lean strategy — every phase has a hypothesis, test, and learning. The PM team (6-10 PMs) co-designs the framework through structured feedback loops.

**Team:** Yoav (PM lead), 1 Dev, Manager (team lead)
**Timeline:** 8 weeks (started 2026-03-22)
**agentOS 2:** Active — handoff must work e2e

---

## Phase 1: Discover (Weeks 1-2)

### Hypothesis
"The framework can guide a PM through all 8 stages and produce development-ready output."

### Track A: First Full Run (Yoav)

| # | Task | Est. |
|---|------|------|
| 1.1 | Select test project (real Moveo product, medium complexity) | 0.5d |
| 1.2 | Create `friction-log.md` template in repo | 0.5h |
| 1.3 | Run all 8 stages end-to-end: start → baseline → research → deep-research → initial-prd → prototype → validate → iterate → final-prd → handoff | 8-10d |
| 1.4 | Test agentOS 2 handoff: feed output into real project, run `shape-spec` on 2+ features | 1d |
| 1.5 | Compile Master Friction Log (categorized by: Command Quality, State Management, Session Continuity, Quality Gates, Output Format, Workflow, agentOS 2) | 0.5d |

### Track B: Team Kickoff (Yoav + Manager)

| # | Task | Est. |
|---|------|------|
| 1.6 | Present Romeo Baltio to PM team (30-min intro session) — explain vision, show early output, ask for 2-3 volunteer early adopters | 0.5d |
| 1.7 | Run a **co-design workshop** with early adopters: "What does your ideal scoping workflow look like? What are your biggest scoping pain points?" | 0.5d |
| 1.8 | Capture team's wish list and pain points → feed into Phase 2 priorities | 0.5d |

### Track C: Viewer Foundations (Dev)

| # | Task | Est. |
|---|------|------|
| 1.9 | Read framework, understand `.romeo-state.json` schema (defined in `commands/0-project-initialization/start.md`) | 1d |
| 1.10 | Research tech stack for lightweight viewer (Next.js/Vite + file-system reader, local-first) | 1d |
| 1.11 | Prototype: basic web page that reads `.romeo-state.json` and renders project status | 2d |

### Track D: Technical Specification Thread (Yoav + Senior Tech)

Tech spec is not a new stage — it's a thread woven through Baseline → Research → Initial PRD → Prototype → Final PRD. The work here is adding the right questions to each existing command so technical decisions are made progressively, and the Final PRD locks the full tech spec.

| # | Task | Est. |
|---|------|------|
| 1.12 | Interview senior tech: "Given a Final PRD, what technical decisions still need to be made before a dev can start?" — capture as a question inventory per stage | 0.5d |
| 1.13 | Map which questions belong at which stage: Baseline (constraints), Research (feasibility), Initial PRD (direction), Prototype (confirm), Final PRD (lock) | 0.5d |
| 1.14 | Define what "dev-ready tech spec" means — what does a complete Final PRD tech section look like? Create a checklist | 0.5d |

### Measure (End of Week 2)
- Did the pipeline complete? Which stages broke?
- How many hours of PM time did it take?
- What did the PM team say about the concept?
- Can the viewer prototype read and display state?

### Learn → Adjust
- Prioritized friction log feeds Phase 2
- Team workshop insights shape which commands/standards to refine first
- If pipeline is too broken to complete, identify the 3 worst stages and focus Phase 2 there

---

## Phase 2: Fix & Co-Design (Weeks 3-4)

### Hypothesis
"Fixing the top friction items + incorporating PM team feedback will make the framework reliable and intuitive for any PM."

### Track A: Framework Fixes (Yoav)

| # | Task | Est. |
|---|------|------|
| 2.1 | Fix all Critical friction items from Phase 1 | 2d |
| 2.2 | Fix all Major friction items | 2d |
| 2.3 | Add missing DoD files: `standards/quality/validation-dod.md` + `iteration-dod.md` | 0.5d |
| 2.4 | Fix empty deliverable schemas in state for validation/iteration/handoff stages | 0.5d |
| 2.5 | Refine command prompts based on output quality findings | 2d |
| 2.6 | Add multi-session continuity to `interaction-protocol.md` | 0.5d |

### Track B: PM Co-Design Sessions (Yoav + Early Adopters)

| # | Task | Est. |
|---|------|------|
| 2.7 | **Dogfooding kickoff**: Run `/romeo-start` on "Romeo Baltio Viewer" product — use the framework to scope its own UI | 1d |
| 2.8 | Co-design session #1: Show early adopters real Baseline + Research output from Phase 1 → "Is this useful? What's missing? What's confusing?" | 0.5d |
| 2.9 | Co-design session #2: Walk through feature-list and PRD templates → "Does this match how you'd want to hand off to devs?" | 0.5d |
| 2.10 | Incorporate co-design feedback into command refinements | 1d |
| 2.11 | Have 1-2 early adopters run `/romeo-start` + `/romeo-baseline` on their own projects | ongoing |

### Track C: Viewer MVP (Dev)

| # | Task | Est. |
|---|------|------|
| 2.12 | Build viewer v0.1: project list → stage progress → deliverable viewer (read markdown files, render nicely) | 5-6d |
| 2.13 | Add Gantt/timeline view of stage progression | 2d |
| 2.14 | Deploy locally (runs on `localhost`, reads from project directory) | 1d |

### Track D: Technical Specification — Build (Yoav + Senior Tech)

| # | Task | Est. |
|---|------|------|
| 2.15 | Add tech context questions to `commands/1-baseline/baseline.md`: existing systems, stack constraints, team preferences | 0.5d |
| 2.16 | Add technical feasibility questions to `commands/2-research/research.md` and `deep-research.md` | 0.5d |
| 2.17 | Enhance `commands/3-initial-prd/initial-prd.md`: tech direction section — services needed, data model sketch, stack direction | 0.5d |
| 2.18 | Enhance `commands/4-prototype/prototype.md`: confirm stack, finalize data model, scope integrations, identify all services + credentials needed | 1d |
| 2.19 | Expand Final PRD tech section in `commands/5-final-prd/final-prd.md`: full SDD — architecture, tech stack, services map, env config, DB schema, API contracts, ADRs | 1.5d |
| 2.20 | Write `standards/templates/tech-spec-template.md` — SDD section template for the Final PRD's tech spec output | 0.5d |

### Measure (End of Week 4)
- Can a PM (not Yoav) complete Baseline successfully?
- Do the co-design changes improve output quality?
- Does the viewer make project state more visible than `.romeo-state.json`?
- Is the "Romeo Baltio Viewer" dogfood project producing useful scoping output?

### Learn → Adjust
- Early adopter feedback shapes Phase 3 onboarding
- Viewer usability findings inform next viewer iteration
- Dogfood project validates/invalidates the framework on a meta level

---

## Phase 3: Onboard & Scale (Weeks 5-6)

### Hypothesis
"With a reference project, onboarding guide, and viewer, any PM on the team can start using Romeo Baltio independently."

### Track A: Reference & Docs (Yoav)

| # | Task | Est. |
|---|------|------|
| 3.1 | Polish Phase 1 test project as the reference example (every deliverable exemplary) | 2-3d |
| 3.2 | Write "Romeo Baltio PM Guide" — what it is, when to use it, what to expect, time commitment | 1d |
| 3.3 | Write "Your First Project" tutorial (step-by-step with screenshots from viewer) | 1d |
| 3.4 | Add FAQ + Tips based on all friction + co-design learnings | 0.5d |

### Track B: Dogfooding Sprint (Yoav + Early Adopters)

| # | Task | Est. |
|---|------|------|
| 3.5 | Continue "Romeo Baltio Viewer" dogfood: run through Initial PRD + Prototype stages | 2-3d |
| 3.6 | **Business model exploration**: During Initial PRD, define target market, pricing hypotheses, GTM approach | Part of 3.5 |
| 3.7 | 2-3 early adopters run their projects through stages 1-3 independently | ongoing |
| 3.8 | Weekly feedback retro with early adopters: "What worked? What blocked you? What would you change?" | 0.5d |

### Track C: Viewer v0.2 (Dev)

| # | Task | Est. |
|---|------|------|
| 3.9 | Viewer v0.2: deliverable quality indicators (DoD pass/fail), better markdown rendering | 3d |
| 3.10 | Add readiness check visualization (green/red per criterion) | 2d |
| 3.11 | Framework versioning: VERSION file + CHANGELOG.md | 0.5d |

### Track D: Technical Specification — Validate (Yoav + Dev)

| # | Task | Est. |
|---|------|------|
| 3.12 | Have early adopter run Baseline → Prototype with the new tech questions — do they flow naturally or feel forced? | ongoing |
| 3.13 | Validate Final PRD tech section: share with a real dev — would they start building from this without a kickoff meeting? Capture gaps | 0.5d |
| 3.14 | Add tech spec criteria to `standards/quality/final-prd-dod.md` — what does a dev-ready tech spec section require? | 0.5d |

### Measure (End of Week 6)
- Can a PM complete stages 1-3 using only the guide + viewer (no hand-holding)?
- How many PMs are actively using the framework?
- Is the dogfood project producing a coherent business model?
- Does the viewer make PMs more confident about project state?

### Learn → Adjust
- If PMs still need hand-holding → simplify commands further
- If business model is forming → accelerate external roadmap
- If viewer is popular → plan more features for v0.3

---

## Phase 4: Adopt & Validate (Weeks 7-8)

### Hypothesis
"The framework is production-ready when 4+ PMs are using it on real projects and producing development-ready output."

### Track A: Team Adoption (Yoav + Manager)

| # | Task | Est. |
|---|------|------|
| 4.1 | Team-wide demo: reference project + viewer + onboarding walkthrough | 0.5d |
| 4.2 | Pair with 2 new PMs on their first projects (stages 1-3) | 2-3d |
| 4.3 | Collect structured feedback from all active PM users | 0.5d |
| 4.4 | Apply final round of feedback to commands + standards | 1d |
| 4.5 | Manager reviews 2+ completed projects for quality bar | 1d |

### Track B: Business Model & External Prep (Yoav)

| # | Task | Est. |
|---|------|------|
| 4.6 | Complete dogfood project through Final PRD → extract business model | 2d |
| 4.7 | Synthesize: target market, value prop, pricing model, GTM strategy | 1d |
| 4.8 | Document what changes for external packaging (separate repo, remove Moveo-specific refs, generic agentOS bridge) | 0.5d |

### Track C: Viewer v0.3 + Polish (Dev)

| # | Task | Est. |
|---|------|------|
| 4.9 | Viewer v0.3: cross-project dashboard (see all team projects at a glance) | 3d |
| 4.10 | Add project comparison view (which projects are stuck, which are progressing) | 2d |
| 4.11 | Bug fixes + polish from PM feedback | 2d |

### Track D: Technical Specification — Polish (Yoav)

| # | Task | Est. |
|---|------|------|
| 4.12 | Update `system-prompt.md` to reflect tech spec as a progressive thread, document which questions belong at which stage | 0.5d |
| 4.13 | Verify `/romeo-handoff` correctly consumes the tech spec sections from Final PRD into agentOS 2 `tech-stack.md` and feature spec files | 0.5d |
| 4.14 | Manager + senior tech review a completed Final PRD tech section — does a dev team lead consider this "start building" ready? | 0.5d |

### Milestone — v1.0 Release (End of Week 8)
- 4+ PMs actively using the framework
- 3+ projects completed 4+ stages
- Manager sign-off on output quality
- Viewer deployed for team use
- Business model defined (from dogfood project)
- v1.0 tagged

---

## Gantt Overview

```
Week:    1    2    3    4    5    6    7    8
         |----|----|----|----|----|----|----|

FRAMEWORK
Yoav:    [= Full Pipeline Run =][Fix+Refine][Ref+Docs ][Final Polish]

TEAM CO-DESIGN
Team:    [Intro][Workshop]  [Co-design x2] [Adopters run own projects ...]
                                            [Retros   ][Team rollout ]

DOGFOODING (Baltio scopes itself)
Yoav:              [Start+BL][iPRD+Proto  ][FinalPRD→BizModel]

VIEWER
Dev:     [Research][Proto v0.1][=== v0.2 ===][=== v0.3 ===]

TECH SPEC THREAD (woven through pipeline, locked at Final PRD)
Yoav:    [Gap+Q  ][Enhance   ][Enhance     ][Validate ][Polish+Lock ]
         [map    ][Baseline  ][iPRD+Proto  ][w/ dev   ][in FinalPRD ]
                 [+Research  ][+FinalPRD   ]

MANAGER
Manager: [Pick prj][Check]    [Check]       [Quality Review+Signoff]
```

---

## Priority Matrix

### Must Have (blocks v1.0)
1. 1 project through all 8 stages e2e
2. All Critical/Major friction items fixed
3. DoD for ALL stages (add validation + iteration)
4. State schema handles all stage deliverables
5. PM co-design feedback incorporated (at least 2 sessions)
6. Reference project with polished deliverables
7. PM Onboarding Guide
8. agentOS 2 handoff verified e2e
9. Lightweight viewer v0.2 (project state + deliverables + DoD)
10. 4+ PMs have used it
11. Business model first draft (from dogfood)

### Should Have
12. Viewer v0.3 (cross-project dashboard)
13. Framework versioning + changelog
14. Multi-session continuity guidance
15. Stage retrospective mechanism
16. Project validator script

### Nice to Have (defer to post-v1.0)
17. CLI wrapper for slash commands
18. Readiness check V2 scoring
19. External packaging
20. Viewer auth + cloud deployment

---

## Success Criteria (v1.0 Production Ready)

**Hard requirements:**
- [ ] 1+ project completed all 8 stages with 20+ deliverables passing DoD
- [ ] agentOS 2 handoff used in real project (2+ features through `shape-spec`)
- [ ] 2+ PMs (not Yoav) completed 4+ stages with minimal hand-holding
- [ ] Manager rates Final PRD output as "development-ready"
- [ ] PM co-design insights incorporated into at least 5 command/standard changes
- [ ] Viewer deployed and used by team

**Soft requirements:**
- [ ] Full pipeline <20 hours PM active time
- [ ] Active PMs say "would use again"
- [ ] New PM can start first project within 30 min
- [ ] Business model hypothesis defined with pricing + target market

---

## Key Files Modified (Phase 1 Setup)

- `romeo-baltio/standards/quality/validation-dod.md` — New DoD for validation stage
- `romeo-baltio/standards/quality/iteration-dod.md` — New DoD for iteration stage
- `romeo-baltio/commands/0-project-initialization/start.md` — Fixed empty deliverable schemas
- `romeo-baltio/standards/interaction-protocol.md` — Added multi-session continuity
- `romeo-baltio/standards/quality/readiness-check.md` — Added validation, iteration, handoff criteria
- `romeo-baltio/friction-log.md` — Friction log template for e2e testing
- `romeo-baltio/VERSION` — Framework version tracking
- `romeo-baltio/CHANGELOG.md` — Change history

---

## Start Tomorrow

1. **Yoav:** Pick the test project (real Moveo product, medium complexity)
2. **Yoav:** Create `friction-log.md` template in repo ✅
3. **Yoav:** Schedule PM team intro session for end of Week 1
4. **Yoav:** Run `/romeo-start` on test project
5. **Dev:** Read framework, explore `.romeo-state.json` schema, research viewer tech stack
6. **Manager:** Schedule Week 1 checkpoint + help identify early adopter PMs
