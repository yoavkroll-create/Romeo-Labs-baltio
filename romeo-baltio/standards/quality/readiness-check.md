# Readiness Check Engine

A reusable, stage-agnostic validation system that determines whether a Romeo Baltio stage is ready to progress.

## Overview

The readiness check runs at the end of any methodology step and produces a binary result:
- **READY** — All required criteria pass. Recommendation: `proceed`.
- **NOT_READY** — One or more required criteria fail. Recommendation: `refine_and_rerun`.

## How It Works

1. Each stage defines its own **criteria configuration** (see Stage Criteria below).
2. The readiness engine evaluates each criterion against the stage deliverables.
3. Results are aggregated using a simple rule: **all required criteria must pass**.
4. The engine outputs a structured result with per-criterion details and missing items.

## Readiness Result Shape

Every readiness check produces this exact structure:

```json
{
  "stage": "{stage-name}",
  "status": "READY | NOT_READY",
  "timestamp": "{ISO date}",
  "criteria_results": [
    {
      "key": "{criterion-key}",
      "name": "{Criterion Name}",
      "required": true,
      "passed": true,
      "explanation": "{Why it passed or failed — be specific}",
      "missing_item": null
    },
    {
      "key": "{criterion-key}",
      "name": "{Criterion Name}",
      "required": true,
      "passed": false,
      "explanation": "{What is missing or insufficient}",
      "missing_item": "{Specific item that needs to be added or fixed}"
    }
  ],
  "missing_items": [
    "{Aggregated list of all missing items from failed criteria}"
  ],
  "recommendation": "proceed | refine_and_rerun",
  "summary": "{One-sentence summary of the readiness state}"
}
```

## Aggregation Rule

```
IF all criteria where required=true have passed=true
  THEN status = "READY", recommendation = "proceed"
ELSE
  THEN status = "NOT_READY", recommendation = "refine_and_rerun"
```

Optional (non-required) criteria that fail produce warnings but do not block progression.

## How to Run a Readiness Check

When Baltio reaches the end of a stage (after DoD evaluation), execute this procedure:

### 1. Load Stage Criteria
Read the stage's DoD file from `romeo-baltio/standards/quality/{stage}-dod.md` and map each criterion to the readiness check format.

### 2. Evaluate Each Criterion
For each criterion:
- Check the deliverable(s) it applies to
- Determine pass/fail with a specific explanation
- If failed, identify the specific missing item

### 3. Aggregate Results
Apply the aggregation rule to determine overall status.

### 4. Present Results
Output the readiness result in the structured format above, followed by a human-readable summary:

```markdown
## Readiness Check: {Stage Name}

**Status:** {READY / NOT_READY}
**Recommendation:** {proceed / refine_and_rerun}

| # | Criterion | Required | Result | Notes |
|---|-----------|----------|--------|-------|
| 1 | {Name} | Yes | PASS | {Explanation} |
| 2 | {Name} | Yes | FAIL | {What's missing} |
| 3 | {Name} | No | PASS | {Explanation} |

### Missing Items
{If NOT_READY, list each missing item with what needs to happen to fix it.}
1. {Missing item} — {Action needed}
2. {Missing item} — {Action needed}

### Next Steps
{If READY: "Proceed to {next stage command}"}
{If NOT_READY: "Address the missing items above, then rerun the readiness check."}
```

### 5. Record in State
Save the readiness result to `.romeo-state.json`:
```json
{
  "stages": {
    "{stage}": {
      "readiness": {
        "status": "READY | NOT_READY",
        "timestamp": "{ISO date}",
        "passed_count": {N},
        "failed_count": {N},
        "missing_items": [...]
      }
    }
  }
}
```

---

## Stage Criteria Configurations

### Baseline (`baseline`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `problem_specific` | Problem is specific and validated | Yes | Problem statement has who, what, why — not generic |
| `users_defined` | Target users are clearly defined | Yes | At least 2 personas with role, context, pain points, goals |
| `current_journey` | Current journey is mapped | Yes | Step-by-step description of current state |
| `solution_direction` | Solution direction is clear | Yes | Conceptual approach with **Our Solution:** pattern |
| `happy_flow` | Happy flow is complete | Yes | Trigger → steps → outcome, all touchpoints covered |
| `capabilities_system` | Capabilities are system-level | Yes | No UI components in capability list |
| `no_premature_detail` | No premature feature detail | Yes | No UI layouts, architecture, or detailed features |
| `research_questions` | Research questions target gaps | Yes | Questions are specific, actionable, not rhetorical |
| `research_prompts` | Research prompts ready to use | Yes | Prompts can be pasted directly into research tools |
| `deliverables_exist` | All 5 deliverables exist | Yes | baseline-spec.md, capability-list.md, happy-flow.md, research-questions.md, research-prompts.md |

### Research (`research`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `market_data` | Market overview has data | Yes | Numbers or evidence, not generic claims |
| `problem_validated` | Problem is validated externally | Yes | Evidence confirms the problem exists |
| `competitors_analyzed` | Minimum 4 competitors | Yes | At least 4 real, identifiable competitors |
| `feature_landscape` | 5+ feature categories covered | Yes | Major capability categories mapped |
| `opportunities_specific` | Opportunity areas are specific | Yes | Concrete enough to inform features |
| `insights_connected` | Insights connect to Baseline | Yes | References to Baseline problem/users |
| `sources_identified` | Sources are listed | Yes | Research sources documented |

### Initial PRD (`initial-prd`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `vision_compelling` | Vision is compelling and quotable | Yes | 2-3 sentences, immediately clear |
| `problem_research_backed` | Problem cites research evidence | Yes | Specific findings referenced |
| `personas_enriched` | Personas refined with research | Yes | Not just copied from Baseline |
| `principles_exist` | Product principles defined | Yes | 3-5 guiding principles |
| `mvp_minimal` | MVP is genuinely minimal | Yes | Only core-validation features |
| `feature_format` | Feature list uses correct format | Yes | 8-column format per template |
| `features_traced` | Every feature traces to a need | Yes | Connected to Baseline/Research |
| `flows_complete` | Core flows documented | Yes | Minimum 3, with trigger/steps/success/error |
| `ux_defined` | UX direction documented | Yes | Design principles, interaction model, IA |
| `prototype_prompts` | Both prototype prompts ready | Yes | MVP and Future prompts are self-contained, include core rules, have distinct scopes |
| `deliverables_exist` | All 6 deliverables exist | Yes | PRD, feature list, flows, UX, prototype-prompt-mvp, prototype-prompt-future |
| `scope_explicit` | Scope boundaries explicit | Yes | MVP, V2, V3, Out of Scope defined |

### Prototype (`prototype`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `goals_defined` | Prototype goals defined | Yes | Clear, measurable goals |
| `scope_split` | Two separate specs exist with distinct scopes | Yes | MVP spec and Future spec exist as separate files with non-overlapping scope assignments |
| `future_extends_mvp` | Future spec explicitly references MVP | Yes | Future spec has "Extends MVP" section listing additions over MVP |
| `flows_specified` | All MVP flows specified | Yes | Every core flow has prototype implementation in MVP spec |
| `screens_complete` | Screen structure complete | Yes | All screens listed with purpose across both specs |
| `data_model` | Data model supports flows | Yes | Entities and relationships for all flows, Vision-only entities marked `[Future]` |
| `sample_data` | Sample data is realistic | Yes | Multiple types, states, realistic content, entries have `"scope": "mvp"` or `"scope": "future"` |
| `integrations` | Integration strategy defined | Yes | Mock/sandbox/real for each dependency, MVP/Future scope noted |
| `demo_mode` | MVP demo mode works e2e | Yes | MVP golden-path defined, self-contained. Future has demo scenario defined. |
| `tech_setup` | Technical setup specified | Yes | Stack, dependencies, run instructions |
| `deliverables_exist` | All 5 deliverables exist | Yes | prototype-spec-mvp.md, prototype-spec-future.md, data-model.md, data-samples.json, integration-strategy.md |

### Final PRD (`final-prd`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `system_complete` | System definition complete | Yes | Pitch, mission, problem, solution, differentiators |
| `scope_explicit` | Scope boundaries explicit | Yes | MVP, V2, V3, Out of Scope |
| `feature_format` | Feature list uses correct format | Yes | 9-column or roadmap-style format |
| `estimates_complete` | All MVP features estimated | Yes | Dev and Design estimates for every MVP feature |
| `validation_reflected` | Features reflect validation | Yes | Status: Validated/Adjusted/New/Removed |
| `flows_error_handling` | Flows include error handling | Yes | Success and error paths documented |
| `architecture_defined` | Architecture documented | Yes | System overview, tech stack, decisions |
| `roles_permissions` | Roles and permissions specified | Yes | Role definitions, permission matrix |
| `domain_model` | Domain model complete | Yes | Entities, relationships, state machines |
| `integrations_specified` | Integrations specified | Yes | API contracts, mock/prod approach |
| `analytics_framework` | Analytics framework exists | Yes | Metrics, events, dashboards |
| `execution_plan` | Execution plan realistic | Yes | Phases, dependencies, risks |
| `validation_captured` | Prototype learnings captured | Yes | Changes from Initial PRD documented |
| `self_contained` | Document is self-contained | Yes | Developer can understand full product |

### Validation (`validation`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `inputs_gathered` | Validation inputs gathered | Yes | PM has provided prototype feedback (built prototype or spec-level review) |
| `dimensions_scored` | All 6 dimensions scored | Yes | Problem-Solution Fit, User Flow Clarity, Product Experience, Feature Completeness, Data & Integration, Demo Readiness — each scored 1–5 |
| `scores_evidence` | Scores are evidence-based | Yes | Every score has specific justification, not gut feeling |
| `features_assessed` | Feature completeness assessed | Yes | Every MVP feature checked with Working/Partial/No status |
| `critical_issues` | Critical issues identified | Yes | All blocking issues listed with descriptions and suggested fixes |
| `scope_adjustments` | Scope adjustments documented | Yes | Feature priority changes listed with evidence-based reasons |
| `next_action` | Next action determined | Yes | Clear recommendation: proceed (≥ 4.0), iterate (3.0–3.9), or re-scope (< 3.0) |
| `report_saved` | Validation report saved | Yes | Report saved to `prototype/validation/validation-{variant}-round-{N}.md` |

### Iteration (`iteration`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `findings_reviewed` | Validation findings reviewed | Yes | Latest validation report's issues and recommendations reviewed with PM |
| `pm_aligned` | PM alignment confirmed | Yes | PM agreed on priorities and scope changes before plan generation |
| `changes_traced` | Changes trace to validation | Yes | Every change cites a specific validation finding |
| `plan_structured` | Iteration plan is structured | Yes | Includes flow improvements, feature adjustments, UX, data model, integrations |
| `scope_discipline` | Scope discipline maintained | Yes | No new features unless PM explicitly requests and feature list updated |
| `comparison_documented` | Iteration comparison documented | Yes | Before/after comparison of screens, features, flows, issues |
| `iteration_dod` | Iteration DoD defined | Yes | Specific criteria for what "done" means for this round |
| `plan_saved` | Iteration plan saved | Yes | Plan saved to `prototype/iterations/iteration-{variant}-round-{N}.md` |
| `guardrails_checked` | Guardrails checked | No | At round 5+, PM flagged about iteration limit |

### Handoff (`handoff`)

| Key | Criterion | Required | What to Check |
|-----|-----------|----------|---------------|
| `final_prd_complete` | Final PRD is complete | Yes | Final PRD stage passed all DoD criteria |
| `mission_generated` | Mission file generated | Yes | `mission.md` follows agentOS 2 format: Pitch → Users → Problem → Differentiators → Key Features |
| `roadmap_generated` | Roadmap file generated | Yes | `roadmap.md` uses numbered checkbox items with effort estimates |
| `tech_stack_generated` | Tech stack file generated | Yes | `tech-stack.md` includes specific versions, grouped by layer |
| `feature_specs_generated` | Feature spec files generated | Yes | Every MVP feature has a feature description in `handoff/features/` |
| `format_validated` | Format matches agentOS 2 | Yes | Files match real CherryClipz/CO-IN/Testchair format conventions |
| `no_info_lost` | No information lost | Yes | All relevant Final PRD content captured in handoff files |
| `handoff_summary` | Handoff summary presented | Yes | Complete summary with file list, feature mapping, and agentOS 2 usage guide |

---

## Extending the Engine

### Adding a New Stage

To add readiness criteria for a new stage:

1. Create a DoD file in `romeo-baltio/standards/quality/{stage}-dod.md` with criteria.
2. Add a criteria configuration section in this file following the pattern above.
3. The readiness engine will automatically use the new criteria when the stage is evaluated.

### Future: Scoring (V2)

The current engine is binary (PASS/FAIL per criterion, READY/NOT_READY overall). A future V2 can add:
- **Weighted scoring** — criteria have different weights (1-5)
- **Confidence levels** — LOW/MEDIUM/HIGH per criterion
- **Quality score** — 0-100 aggregate score
- **Trend tracking** — how scores change across readiness check reruns
- **Stage comparison** — benchmarking against past projects

The result shape is designed to support this extension without breaking changes — just add `weight`, `confidence`, and `score` fields to the criteria result.
