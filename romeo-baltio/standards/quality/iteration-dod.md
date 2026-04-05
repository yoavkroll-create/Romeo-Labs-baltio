# Prototype Iteration — Definition of Done

## Criteria

| # | Criterion | Description |
|---|-----------|-------------|
| 1 | **Validation findings reviewed** | The latest validation report's critical issues, recommended iterations, and scope adjustments have been reviewed with the PM. |
| 2 | **PM alignment confirmed** | PM has agreed on iteration priorities and any scope changes before the plan is generated. |
| 3 | **Changes trace to validation** | Every change in the iteration plan cites a specific finding from the validation report. |
| 4 | **Iteration plan is structured** | Plan includes: flow improvements, feature adjustments, UX improvements, data model changes, and integration updates — each with priority levels. |
| 5 | **Scope discipline maintained** | Iterations fix validated issues — no new features added unless PM explicitly requests and the feature list is updated first. |
| 6 | **Iteration comparison documented** | Side-by-side comparison of before/after: total screens, features implemented, flows working, known issues. |
| 7 | **Iteration DoD defined** | Specific, checkable criteria for what "done" means for this iteration round. |
| 8 | **Iteration plan saved** | Plan is saved to `prototype/iterations/iteration-{variant}-round-{N}.md` with correct metadata. |
| 9 | **Guardrails checked** | If this is round 5+, PM has been flagged that iteration limit is reached and re-scoping should be considered. |

## Evaluation

- All 9 criteria must pass (criterion 9 only applies at round 5+).
- The iteration plan is a delta — it should be clear what changed and why, not a full rewrite of the prototype spec.
- After implementing iteration changes, the PM should run `/romeo-validate-prototype` to validate the new round.
