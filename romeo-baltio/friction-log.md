# Friction Log Template

Use this log to capture every point of friction during an end-to-end pipeline run. One entry per issue. Compile into a Master Friction Log at the end of the run.

---

## How to Use

1. During each stage, note any moment where the framework feels broken, confusing, slow, or wrong.
2. Fill in one row per issue — be specific about what happened and what you expected.
3. At the end of the run, categorize all entries and prioritize (Critical → Major → Minor).

---

## Friction Log: {Project Name}

**PM:** {Name}
**Start Date:** {Date}
**End Date:** {Date}

### Log Entries

| # | Stage | Command | Category | Severity | What Happened | What I Expected | Suggested Fix |
|---|-------|---------|----------|----------|---------------|-----------------|---------------|
| 1 | {stage} | {/romeo-xxx} | {category} | {Critical/Major/Minor} | {Describe the friction point} | {What should have happened} | {Your idea for fixing it} |
| 2 | | | | | | | |
| 3 | | | | | | | |

### Categories

| Category | Description |
|----------|-------------|
| **Command Quality** | The command prompt produced poor, incomplete, or wrong output |
| **State Management** | `.romeo-state.json` was wrong, out of sync, or missing data |
| **Session Continuity** | Context was lost between sessions or stages |
| **Quality Gates** | DoD or readiness check was missing, too strict, too lenient, or didn't catch real issues |
| **Output Format** | Deliverable format was wrong, inconsistent, or didn't match templates |
| **Workflow** | The stage order, prerequisites, or transitions felt wrong |
| **agentOS 2** | Handoff files didn't match agentOS 2 format or `shape-spec` couldn't use them |
| **UX/Interaction** | The conversation flow was awkward, too many questions, or unclear guidance |

### Severity Definitions

| Severity | Definition |
|----------|------------|
| **Critical** | Blocks pipeline progression. Cannot complete the stage without a workaround. |
| **Major** | Significantly degrades output quality or PM experience. Needs fixing before team rollout. |
| **Minor** | Annoyance or rough edge. Can live with it but should be polished. |

---

## Master Summary (fill after completing all stages)

### By Category

| Category | Critical | Major | Minor | Total |
|----------|----------|-------|-------|-------|
| Command Quality | | | | |
| State Management | | | | |
| Session Continuity | | | | |
| Quality Gates | | | | |
| Output Format | | | | |
| Workflow | | | | |
| agentOS 2 | | | | |
| UX/Interaction | | | | |
| **Total** | | | | |

### By Stage

| Stage | Critical | Major | Minor | Total | Time Spent |
|-------|----------|-------|-------|-------|------------|
| Start | | | | | |
| Baseline | | | | | |
| Research | | | | | |
| Deep Research | | | | | |
| Initial PRD | | | | | |
| Prototype | | | | | |
| Validation | | | | | |
| Iteration | | | | | |
| Final PRD | | | | | |
| Handoff | | | | | |
| **Total** | | | | | |

### Top 5 Issues to Fix First

1. {Issue} — {Why it's the highest priority}
2.
3.
4.
5.

### Overall Assessment

- **Pipeline completion:** {Yes/No — which stages completed?}
- **Total PM time:** {hours}
- **Biggest surprise:** {What you didn't expect}
- **Framework readiness:** {Ready for team / Needs X fixes first / Major rework needed}
