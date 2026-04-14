# Task Completion Checklist

Before committing any code changes, verify the following:

## Mandatory Checks
1. **Run `npm run test`** — Must pass (typecheck + unit tests)
2. **UI changes** → Run `npm run test:smoke` AND verify with Chrome DevTools MCP (CDP)
   - Start dev server → Navigate to affected page → Screenshot → Check console for errors
   - For interactive changes: simulate clicks/inputs via CDP
   - For responsive layouts: test desktop + mobile viewports via CDP device emulation
3. **Build/packaging changes** → Run full packaging flow to verify artifacts

## Self-Review Checklist
1. **i18n**: Does the change need updates to both `src/i18n/en.ts` and `zh.ts`?
2. **Database**: Does it need schema changes in `src/lib/db.ts` (with migration logic)?
3. **Types**: Does it need updates to `src/types/index.ts`?
4. **Documentation**: Does it need updates to `docs/handover/` handover docs?
5. **New feature / major iteration**: Write both:
   - Technical handover doc → `docs/handover/{feature}.md`
   - Product thinking doc → `docs/insights/{feature}.md`
   - Cross-link the two docs

## Git Conventions
- Use conventional commits: `feat:`, `fix:`, `refactor:`, `chore:`, etc.
- Body: group by file/feature, explain what changed, why, and impact scope
- Bug fixes: explain root cause
- Architecture decisions: briefly explain rationale

## Worktree Rules (if applicable)
- All changes ONLY in the assigned worktree
- No cross-worktree commits
- No `git push` unless user explicitly requests
- Use non-default port (e.g., `PORT=3001`) for dev server
- Check `git status` for untracked/temp files before merging back

## Release Discipline
- Never auto-release. `git push` + `git tag` only on explicit user instruction
