# Code Style & Conventions

## TypeScript
- **Strict mode** enabled (`"strict": true` in tsconfig)
- Target: ES2017, module: ESNext, moduleResolution: bundler
- Path alias: `@/*` maps to `./src/*`
- Incremental compilation enabled

## Component Architecture
- **UI primitives** in `src/components/ui/` — Radix-based (Button, Dialog, Tabs, etc.)
- **Business components** in feature directories (chat/, settings/, bridge/, etc.)
- **Pattern components** in `src/components/patterns/` — pure presentation only (no hooks or lib imports except `cn()`)
- **AI response renderers** in `src/components/ai-elements/`
- **Component file size limit**: 500 lines (warn) for business components (excludes ui/ and ai-elements/)

## Icons
- **Use Phosphor Icons** (`@phosphor-icons/react`) — NOT lucide-react (ESLint error)
- Business components should import from `@/components/ui/icon` (ESLint warn for direct Phosphor imports)

## HTML Elements
- **Use UI components** instead of native HTML: `<Button>` not `<button>`, `<Input>` not `<input>`, etc.
- ESLint warns on native `<button>`, `<input>`, `<select>`, `<textarea>` in business components

## Colors
- Avoid raw Tailwind color classes (e.g., `bg-green-500`, `text-red-600`) in business components
- Use `// lint-allow-raw-color` comment to exempt intentional cases (e.g., diff syntax)
- Enforced via `npm run lint:colors` (grep-based)

## Naming
- Conventional commits for git messages (feat/fix/refactor/chore)
- React hooks: `use{Name}.ts` pattern
- API routes: `src/app/api/{feature}/route.ts`
- Pages: `src/app/{feature}/page.tsx`

## i18n
- Bilingual: English (`src/i18n/en.ts`) + Chinese (`src/i18n/zh.ts`)
- Both files must be kept in sync

## Imports
- Path alias `@/` for all src imports
- ESLint enforces import restrictions per component layer
