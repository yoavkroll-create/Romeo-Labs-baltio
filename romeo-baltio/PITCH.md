# Romeo Baltio — Manager Overview

## What is it?

Romeo Baltio is an **AI-powered product scoping agent** that guides PMs from a raw product idea to a developer-ready SDD — in a fraction of the time it takes today.

A PM runs structured slash commands in their IDE. The AI asks the right questions, challenges assumptions, and co-creates all the artifacts needed to hand off to developers.

---

## The Problem It Solves

| Today (Without Romeo Baltio) | With Romeo Baltio |
|------------------------------|-------------------|
| PRDs are vague, dev asks 50 questions | Every deliverable passes a Definition of Done |
| Scoping takes days of fragmented back-and-forth | Structured stages with clear outputs |
| Each PM scopes differently | Consistent framework across the team |
| Dev handoff is a bottleneck | Ready-to-code SDD with tech stack, architecture, data models |
| Business context gets lost between stages | State tracked end-to-end across sessions |

---

## How It Works — 8 Stages

```
Idea → Baseline → Research → Initial PRD → Prototype → Validate → Iterate → Final PRD → Dev Handoff
         ↓              ↓           ↓            ↓                             ↓
    [tech constraints][feasibility][direction][confirm stack]          [lock tech spec]
```

Each stage has:
- A slash command (e.g. `/romeo-baseline`)
- An AI-guided conversation that asks the right questions
- Deliverables that pass a structured quality gate (DoD)
- State saved between sessions — pick up exactly where you left off

Technical specification isn't a separate stage — it's a thread that starts at Baseline (existing systems, constraints, preferences) and gets confirmed through the Prototype flow, locking into the Final PRD.

**Key outputs at the end:** Final PRD with locked technical SDD (tech stack, architecture, data model, integration map, service map, environment config) + feature specs ready for dev

---

## Current Status

- Framework is ~85% built, never tested end-to-end
- 8-stage command structure is complete
- Quality gates (DoD) defined for all stages
- **Week 1 of 8** — about to run the first full end-to-end test

---

## 8-Week Plan (Summary)

| Phase | Weeks | Goal |
|-------|-------|------|
| Discover | 1–2 | First full pipeline run, PM team intro, identify friction |
| Fix & Co-Design | 3–4 | Fix top issues, 2 co-design sessions with early adopters |
| Onboard & Scale | 5–6 | Reference project, PM guide, independent usage by 2+ PMs |
| Adopt & Validate | 7–8 | 4+ PMs using it, manager sign-off, v1.0 release |

**v1.0 milestone:** 4+ PMs producing development-ready output independently, manager rates quality as "dev-ready."

---

## The Big Picture

If this works, every PM on the team has a structured, repeatable scoping process. Every dev handoff is developer-ready from day one. And the framework itself can be packaged as a standalone product.
