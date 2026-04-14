# CodePilot — Project Overview

## Purpose
CodePilot is a **multi-model AI Agent desktop client** (v0.50.1). It provides a ChatGPT-like interface supporting multiple AI providers (Anthropic, OpenAI, Google, Bedrock, Vertex), with IM bridge integration (Telegram, Feishu/Lark, Discord), built-in agent tools, a plugin/MCP system, and a skills marketplace.

## Tech Stack
| Layer | Technology |
|-------|------------|
| Desktop shell | Electron 40 |
| Frontend | Next.js 16 (App Router) + React 19 |
| Styling | Tailwind CSS 4 + Radix UI |
| Database | better-sqlite3 (WAL mode), data dir: `~/.codepilot/` |
| AI integration | Claude Agent SDK (`@anthropic-ai/claude-agent-sdk`), Vercel AI SDK (`ai` v6), `@ai-sdk/*` adapters |
| IM integration | Telegram Bot API, Feishu SDK (`@larksuiteoapi/node-sdk`), Discord.js |
| Code highlighting | Shiki |
| Markdown | react-markdown, streamdown, markdown-it |
| Bundling | electron-builder (DMG + NSIS) |
| Testing | Playwright (E2E), tsx + node:test (unit) |
| Error tracking | Sentry |
| Icons | Phosphor Icons (NOT lucide-react) |

## Monorepo Structure
- Root workspace with `apps/*` and `packages/*`
- Currently only `apps/site` (documentation site) exists as secondary workspace
- Main app is at the root level

## Key Stats
- 619 TypeScript/TSX files in `src/`
- 51 unit test files, 9 E2E specs
- 25 API route groups (~52 endpoints)
- 13 pages, 12 DB tables, 12 themes, 33 React hooks
- 16 component subdirectories

## License
BUSL-1.1 (Business Source License)
