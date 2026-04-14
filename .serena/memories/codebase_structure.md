# Codebase Structure

## Top-Level Layout
```
src/
├── app/            # Next.js App Router (pages + API routes)
├── components/     # React components (16 subdirectories)
├── lib/            # Core business logic (~90 modules)
├── hooks/          # 33 React hooks
├── types/          # TypeScript types (index.ts: 1229 lines)
├── i18n/           # Internationalization (en.ts + zh.ts)
└── __tests__/      # Unit (51) + E2E (9) tests

electron/
├── main.ts         # Electron main process
├── preload.ts      # contextBridge
├── terminal-manager.ts
└── updater.ts

apps/site/          # Documentation site workspace
themes/             # 12 JSON theme definitions
scripts/            # Build scripts (after-pack, after-sign, build-electron)
docs/               # Project documentation
```

## Key Modules in src/lib/
| File | Purpose |
|------|---------|
| `db.ts` (2840 lines) | SQLite schema, 12 tables, migrations, CRUD |
| `claude-client.ts` (1800 lines) | Agent SDK wrapper, SSE streaming |
| `stream-session-manager.ts` | SSE stream lifecycle |
| `provider-resolver.ts` | Multi-provider model routing |
| `agent-loop.ts` | Agent execution loop |
| `error-classifier.ts` | 16-class structured errors |
| `provider-doctor.ts` | Provider diagnostics (5 probes) |
| `context-assembler.ts` | Context window management |

## Subsystems
- **bridge/** — IM integration (Telegram, Feishu) with adapters, router, delivery, permissions
- **channels/** — Structured channel plugins (`ChannelPlugin<T>` contract)
- **runtime/** — Dual agent runtime (native CLI / SDK) with abstraction
- **theme/** — Theme engine (12 themes, loader, CSS renderer)
- **tools/** — Core tools (agent, bash, edit, glob, grep, read, write, skill)
- **builtin-tools/** — Extended tools (cli-tools, dashboard, media, memory-search, etc.)
- **remote/** — Remote host/controller/session contracts

## Pages (13 routes)
/, /chat, /chat/[id], /settings, /plugins, /plugins/mcp, /mcp, /bridge, /gallery, /skills, /cli-tools, /extensions, /design-system

## API Route Groups (25)
app, bridge, chat, claude-auth, claude-sessions, claude-status, claude-upgrade, cli-tools, dashboard, doctor, files, git, health, media, openai-oauth, plugins, providers, sdk, settings, setup, skills, tasks, uploads, usage, workspace

## Database Tables (12)
chat_sessions, messages, settings, tasks, api_providers, media_generations, media_tags, media_jobs, media_job_items, media_context_events, channel_bindings, channel_offsets
