# Documentation Structure

## Root Files
- `CLAUDE.md` — Project rules and development workflow (authoritative)
- `ARCHITECTURE.md` — Architecture, directory structure, data flow, touchpoints
- `AGENTS.md` — Agent configuration
- `README.md` / `README_CN.md` / `README_JA.md` — Public READMEs (EN/CN/JA)
- `CHANGELOG.md` — Change log
- `RELEASE_NOTES.md` — Current release notes (used by CI for GitHub Release body)

## docs/ Directory
- `docs/exec-plans/active/` — Active execution plans (16 plans)
- `docs/exec-plans/completed/` — Completed execution plans
- `docs/exec-plans/tech-debt-tracker.md` — Known technical debt
- `docs/handover/` — Technical handover docs (for developers taking over modules)
- `docs/insights/` — Product thinking docs (design rationale, user problems)
- `docs/research/` — Research & feasibility analysis
- `docs/future/` — Future feature plans

## Documentation Rules
- New features require BOTH handover + insights docs with cross-links
- Medium/large features (3+ modules, schema changes) require exec plans first
- Check each directory's README.md before searching
- Update indexes after adding/removing files
