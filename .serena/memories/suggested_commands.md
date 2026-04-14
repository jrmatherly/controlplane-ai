# Suggested Commands

## Development
- `npm run dev` — Start Next.js dev server (localhost:3000)
- `npm run electron:dev` — Start Electron + Next.js (concurrently)
- `PORT=3001 npm run dev` — Dev server on alternate port (for worktree isolation)

## Testing
- `npm run test` — Typecheck + unit tests (~4s, no dev server needed)
- `npm run test:unit` — Unit tests only (`tsx --test src/__tests__/unit/*.test.ts`)
- `npm run test:smoke` — Smoke tests (~15s, needs dev server)
- `npm run test:e2e` — Full E2E with Playwright (~60s+, needs dev server)
- `npm run test:visual` — Visual regression tests

## Code Quality
- `npm run lint` — ESLint
- `npm run typecheck` — TypeScript type checking (`tsc --noEmit`)
- `npm run lint:colors` — Grep-based check for raw color usage in components

## Building
- `npm run build` — Next.js production build
- `npm run electron:build` — Next.js build + Electron esbuild
- `npm run electron:pack` — Full build + electron-builder (all platforms)
- `npm run electron:pack:mac` — macOS only (DMG arm64 + x64)
- `npm run electron:pack:win` — Windows only (NSIS installer)
- `npm run electron:pack:linux` — Linux only
- Before building: `rm -rf release/ .next/`

## Pre-commit Hook (automatic)
The `.husky/pre-commit` hook runs:
1. `npx lint-staged` — ESLint fix on staged `.ts`/`.tsx` files
2. `npx tsc --noEmit` — Type checking
3. `npx tsx --test src/__tests__/unit/*.test.ts` — All unit tests

## System Utilities (macOS / Darwin)
- `git` — Version control
- `ls`, `find`, `grep` — File operations (BSD variants on macOS)
- `open .` — Open directory in Finder
- `pbcopy` / `pbpaste` — Clipboard operations
