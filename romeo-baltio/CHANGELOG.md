# Changelog

All notable changes to the Romeo Baltio framework are documented here.

Format: [Semantic Versioning](https://semver.org/). Stages: Pre-release (0.x), Production (1.x+).

---

## [0.9.0] — 2026-03-22

### Added
- **Production workplan** (`WORKPLAN.md`) — 8-week plan for v1.0 release
- **Friction log template** (`friction-log.md`) — Structured template for capturing issues during e2e testing
- **Validation DoD** (`standards/quality/validation-dod.md`) — 8 criteria for prototype validation stage
- **Iteration DoD** (`standards/quality/iteration-dod.md`) — 9 criteria for prototype iteration stage
- **Readiness check criteria** for Validation, Iteration, and Handoff stages in `readiness-check.md`
- **Multi-session continuity** section in `interaction-protocol.md` — guidance for maintaining context across sessions
- **Framework versioning** — `VERSION` file and `CHANGELOG.md`

### Fixed
- **Empty deliverable schemas** — Validation, Iteration, and Handoff stages in `.romeo-state.json` now have proper deliverable entries instead of empty `{}`

### Previous (unversioned)
- All 11 command files (start, status, baseline, research, deep-research, initial-prd, prototype, validate-prototype, iterate-prototype, final-prd, handoff)
- 5 DoD files (baseline, research, initial-prd, prototype, final-prd)
- Readiness check engine with criteria for 5 stages
- Standards: interaction protocol, file writing format, naming conventions, scope classification, estimation guide, cross-reference rules
- Templates: feature list, spec, research prompt
- System prompt and CLAUDE.md loader
