# Project Index: CodePilot

Generated: 2026-04-14  
Version: 0.50.1  
License: BUSL-1.1

## Overview

CodePilot is a multi-model AI Agent desktop client built on Electron 40 + Next.js 16 (App Router). It provides a ChatGPT-like interface that supports multiple AI providers (Anthropic, OpenAI, Google, Bedrock, Vertex), with IM bridge integration (Telegram, Feishu/Lark), built-in tools, and a plugin/skills system.

## Project Structure

```
controlplane-ai/
├── src/                    # Main application source (619 TS/TSX files)
│   ├── app/                # Next.js App Router (pages + 25 API route groups)
│   │   ├── api/            # REST endpoints: chat, bridge, media, plugins, settings, etc.
│   │   ├── chat/           # Main chat interface (pages)
│   │   ├── plugins/        # Plugin/MCP management
│   │   ├── settings/       # App settings
│   │   ├── bridge/         # IM bridge config
│   │   ├── gallery/        # Media gallery
│   │   ├── skills/         # Skills marketplace
│   │   └── cli-tools/      # CLI tools management
│   ├── components/         # React components (16 subdirectories)
│   │   ├── ui/             # Radix primitives (Button, Dialog, Tabs...)
│   │   ├── chat/           # Chat UI (MessageList, CodeBlock, ImageThumbnail...)
│   │   ├── ai-elements/    # AI response renderers (artifact, reasoning, tool, task...)
│   │   ├── layout/         # Shell, Header, NavRail, ChatListPanel
│   │   ├── assistant/      # Assistant workspace UI
│   │   ├── bridge/         # Bridge settings UI
│   │   ├── plugins/        # Plugin management UI
│   │   ├── settings/       # Settings panel
│   │   ├── skills/         # Skills marketplace UI
│   │   ├── project/        # Project file tree
│   │   ├── gallery/        # Gallery view
│   │   ├── git/            # Git integration UI
│   │   ├── terminal/       # Terminal UI
│   │   ├── cli-tools/      # CLI tools UI
│   │   ├── setup/          # Onboarding/setup
│   │   └── patterns/       # Shared UI patterns
│   ├── lib/                # Core business logic (~90 modules)
│   │   ├── db.ts           # SQLite DB (2840 lines, 12 tables, WAL mode)
│   │   ├── claude-client.ts# Claude Agent SDK wrapper (1800 lines)
│   │   ├── stream-session-manager.ts  # SSE stream lifecycle
│   │   ├── conversation-registry.ts   # Active SDK session registry
│   │   ├── provider-resolver.ts       # Multi-provider routing
│   │   ├── provider-doctor.ts         # Provider diagnostics (5 probes)
│   │   ├── error-classifier.ts        # 16-class structured errors
│   │   ├── bridge/         # IM Bridge subsystem (Telegram, Feishu)
│   │   ├── channels/       # Structured channel plugins (ChannelPlugin<T>)
│   │   ├── runtime/        # Agent runtime abstraction (native/SDK)
│   │   ├── tools/          # Built-in tool implementations
│   │   ├── builtin-tools/  # Additional built-in tools
│   │   ├── theme/          # Theme engine (12 themes)
│   │   ├── remote/         # Remote host/controller/session contracts
│   │   └── ...             # Context, skills, workspace, MCP, etc.
│   ├── hooks/              # 33 React hooks (useSSEStream, useSettings, etc.)
│   ├── types/              # TypeScript types (index.ts: 1229 lines)
│   └── i18n/               # i18n (en.ts + zh.ts)
├── electron/               # Electron main process
│   ├── main.ts             # Window, IPC, Utility Process
│   ├── preload.ts          # contextBridge (install/updater APIs)
│   ├── terminal-manager.ts # Terminal management
│   └── updater.ts          # Auto-updater
├── apps/site/              # Documentation site (workspace)
├── scripts/                # Build scripts
│   ├── after-pack.js       # Recompile better-sqlite3 for Electron ABI
│   ├── after-sign.js       # Code signing
│   └── build-electron.mjs  # Electron build
├── themes/                 # 12 JSON theme definitions
└── docs/                   # Project documentation
    ├── exec-plans/         # Execution plans (active + completed)
    ├── handover/           # Technical handover docs
    ├── insights/           # Product thinking docs
    ├── research/           # Research & feasibility docs
    └── future/             # Future feature plans
```

## Entry Points

- **Web dev server**: `npm run dev` (Next.js on localhost:3000)
- **Electron dev**: `npm run electron:dev` (Next.js + Electron)
- **Electron main**: `electron/main.ts` → `dist-electron/main.js`
- **Next.js pages**: `src/app/page.tsx` (root), `src/app/chat/page.tsx` (chat)
- **API layer**: `src/app/api/` (25 route groups, ~52 endpoints)

## Pages (13)

| Route | Page |
|-------|------|
| `/` | Root/redirect |
| `/chat` | Chat interface (main UI) |
| `/chat/[id]` | Specific chat session |
| `/settings` | App settings |
| `/plugins` | Plugin management |
| `/plugins/mcp` | MCP server management |
| `/mcp` | MCP alternate route |
| `/bridge` | IM Bridge configuration |
| `/gallery` | Media gallery |
| `/skills` | Skills marketplace |
| `/cli-tools` | CLI tools management |
| `/extensions` | Extensions |
| `/design-system` | Design system reference |

## API Route Groups (25)

`app, bridge, chat, claude-auth, claude-sessions, claude-status, claude-upgrade, cli-tools, dashboard, doctor, files, git, health, media, openai-oauth, plugins, providers, sdk, settings, setup, skills, tasks, uploads, usage, workspace`

## Database (SQLite, 12 tables)

`chat_sessions, messages, settings, tasks, api_providers, media_generations, media_tags, media_jobs, media_job_items, media_context_events, channel_bindings, channel_offsets`

Data dir: `~/.codepilot/`, WAL mode + foreign keys.

## Core Modules (Key Files)

| Module | Lines | Purpose |
|--------|-------|---------|
| `lib/db.ts` | 2840 | Schema, migrations, CRUD for all 12 tables |
| `lib/claude-client.ts` | 1800 | Agent SDK conversation, SSE streaming |
| `types/index.ts` | 1229 | All business types |
| `lib/stream-session-manager.ts` | — | SSE stream lifecycle management |
| `lib/provider-resolver.ts` | — | Multi-provider model routing |
| `lib/agent-loop.ts` | — | Agent execution loop |
| `lib/context-assembler.ts` | — | Context window management |
| `lib/bridge/bridge-manager.ts` | — | Bridge lifecycle orchestration |
| `lib/runtime/` | — | Native/SDK runtime abstraction |

## Subsystems

### Bridge (IM Integration)
`src/lib/bridge/` — Connects Telegram & Feishu to CodePilot sessions.
- Adapters → Router → ConversationEngine → DeliveryLayer
- Permission broker for interactive approval via IM buttons
- Markdown rendering pipeline (MD → IR → channel-specific format)

### Channels (Plugin Layer)
`src/lib/channels/` — Structured channel plugins with `ChannelPlugin<T>` contract.
- Feishu: modular (gateway, inbound, outbound, identity, policy, card-controller)

### Runtime
`src/lib/runtime/` — Agent runtime abstraction.
- `native-runtime.ts` — Direct Claude Code CLI
- `sdk-runtime.ts` — Claude Agent SDK
- `registry.ts` — Runtime selection

### Theme Engine
`src/lib/theme/` + `themes/` — 12 built-in themes (JSON definitions).
- Loader, CSS renderer, code theme mapping

### Tools
`src/lib/tools/` — Core tools (agent, bash, edit, glob, grep, read, write, skill)
`src/lib/builtin-tools/` — Extended tools (cli-tools, dashboard, media, memory-search, etc.)

## Tech Stack

| Layer | Technology |
|-------|------------|
| Desktop shell | Electron 40 |
| Frontend | Next.js 16 (App Router) + React 19 |
| Styling | Tailwind CSS 4 + Radix UI |
| Database | better-sqlite3 (WAL) |
| AI integration | Claude Agent SDK, @ai-sdk/* (anthropic, openai, google, bedrock, vertex) |
| IM integration | Telegram Bot API, Feishu SDK, Discord.js |
| Code highlighting | Shiki |
| Markdown | react-markdown, streamdown, markdown-it |
| Bundling | electron-builder (DMG + NSIS) |
| Testing | Playwright (E2E), tsx + node:test (unit) |
| Error tracking | Sentry |

## Key Dependencies

| Package | Purpose |
|---------|---------|
| `@anthropic-ai/claude-agent-sdk` | Claude Agent SDK |
| `ai` (v6) | Vercel AI SDK |
| `@ai-sdk/*` | Multi-provider AI adapters |
| `better-sqlite3` | Local SQLite database |
| `discord.js` | Discord integration |
| `@larksuiteoapi/node-sdk` | Feishu/Lark API |
| `shiki` | Syntax highlighting |
| `streamdown` | Streaming markdown |
| `motion` | Animations |
| `electron-updater` | Auto-update |

## Test Coverage

- **Unit tests**: 51 files (`src/__tests__/unit/*.test.ts`)
- **E2E tests**: 9 specs (`src/__tests__/e2e/*.spec.ts`)
- **Test helpers**: `src/__tests__/helpers.ts`
- **Smoke test**: `src/__tests__/smoke-test.ts`

## Quick Commands

```bash
npm run dev              # Start Next.js dev server
npm run electron:dev     # Start Electron + Next.js
npm run test             # Typecheck + unit tests (~4s)
npm run test:smoke       # Smoke tests (~15s, needs dev server)
npm run test:e2e         # Full E2E (~60s+, needs dev server)
npm run electron:pack    # Build distributable
```

## Key Documentation

| Doc | Path |
|-----|------|
| Architecture | `ARCHITECTURE.md` |
| Project rules | `CLAUDE.md` |
| Bridge system | `docs/handover/bridge-system.md` |
| Provider architecture | `docs/handover/provider-architecture.md` |
| Tech debt | `docs/exec-plans/tech-debt-tracker.md` |
| Active plans | `docs/exec-plans/active/` (16 plans) |
| Research | `docs/research/` |
