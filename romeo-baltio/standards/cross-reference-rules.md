# Cross-Reference Rules

How stages in Romeo Baltio build on each other and cite prior artifacts.

---

## Principle

Each stage builds on prior artifacts. Every claim, feature, decision, and recommendation must trace back to evidence from earlier stages. **Never generate content in a vacuum** — always connect forward from what's been established.

---

## Per-Stage Citation Requirements

### Research → Baseline
- Must reference Baseline Spec's problem definition, target users, and research questions
- Research prompts must target the specific gaps identified in `research-questions.md`
- Competitor analysis must relate back to the capabilities defined in `capability-list.md`

### Deep Research → Baseline
- Must use research questions from Baseline as the starting point
- Research prompts must target gaps not covered by standard Research
- Findings must map back to Baseline's problem and user definitions

### Initial PRD → Baseline + Research
- Must synthesize Baseline Spec + Research findings — not just repeat them
- Feature list must trace back to validated capabilities from Baseline
- Every feature must connect to a user need validated by Research evidence
- Problem statement must be strengthened with research data
- Personas must be enriched (not just copied) from Baseline based on research

### Prototype → Initial PRD
- Must implement features from Initial PRD's feature list
- Data model must support the defined user flows from `core-user-flows.md`
- MVP/Future split must match the scope defined in Initial PRD
- Prototype prompts must be based on the prompts generated in Initial PRD

### Validation → Initial PRD + Prototype
- Must evaluate against Initial PRD's success metrics
- Must evaluate against prototype goals defined in the Prototype Spec
- Validation criteria must map to specific features and flows

### Iteration → Validation
- Must address specific findings from Validation reports
- Every iteration action must trace to a validation finding
- Must not introduce new features — only fix/adjust validated issues

### Final PRD → All Prior Stages
- Must incorporate all validated changes from the prototype cycle
- Feature list must reflect final approved scope (features added, removed, adjusted)
- Must document what changed from Initial PRD and why
- Architecture decisions must account for prototype learnings

### Handoff → Final PRD
- Must map Final PRD sections to agentOS 2 format precisely
- No information loss in the translation
- Every MVP feature must have a corresponding handoff feature description

---

## Citation Format

When referencing prior artifacts, use explicit citations:

**Good citations:**
- "Per the Baseline Spec's capability list, the system must support multi-tenant data isolation."
- "Research finding #3 (Competitor Analysis) shows that 4 of 5 competitors lack real-time collaboration — this validates our differentiator."
- "The Initial PRD's success metric of 'onboarding < 3 minutes' was not met in prototype validation (actual: 7 minutes). Adjusted flow removes 2 steps."

**Bad citations:**
- "As previously discussed..." (vague — which artifact? which decision?)
- "Based on our research..." (which research? which finding?)
- No citation at all (where did this claim come from?)

---

## Data Continuity: Confirm, Don't Re-Ask

When starting a new stage, **scan all existing deliverables** in the project folder before asking the PM anything.

**The inheritance rule:** If a section relates to information already provided in a previous stage (e.g., scope, user personas, vision, problem definition), you MUST pull that data forward automatically.

**How to handle inherited data:**
1. **Present it for confirmation** — don't re-ask. Say: "Based on the Baseline Spec, I've pulled this info: {Summary}. Does this still hold for this stage, or has anything changed?"
2. **Enrich, don't copy** — inherited data should be synthesized and strengthened with new context from the current stage, not pasted verbatim.
3. **Flag staleness** — if inherited data seems outdated based on what the PM has said in conversation, flag it: "The Baseline says X, but based on our research discussion it sounds like Y might be more accurate now. Which should we use?"

**Consistency check:** If a new answer from the PM contradicts a previous deliverable, point it out immediately and ask which one should be updated. Never silently accept contradictions.

---

## Contradiction Handling

If a later stage needs to contradict an earlier artifact:

1. **Flag it explicitly** — "This contradicts the Baseline Spec's assumption that X."
2. **Explain why** — "Prototype validation showed that X doesn't hold because Y."
3. **Get PM alignment** — "Should we update the Baseline to reflect this, or keep it as-was for the record?"
4. **Document the change** — Track the contradiction in `.romeo-state.json` and in the stage deliverable.

Never silently contradict a prior artifact. The PM must be aware of and approve any directional changes.
