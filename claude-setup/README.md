# Claude Code setup

How Claude Code is configured in the private repo.

## `CLAUDE.md`

```md
@AGENTS.md
```

One line. It imports `AGENTS.md`, so there's a single source of project rules.

## `AGENTS.md`

Guards against stale framework knowledge. Written and kept up to date by `next dev`, it says:

> This is NOT the Next.js you know. This version has breaking changes. APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.

## MCP: Supabase, scoped to one project

[`mcp.example.json`](mcp.example.json) shows the shape of `.mcp.json`. It connects Claude to the Supabase project for docs, database, debugging, development and functions. The project reference is removed here.

Why: Claude can check the live schema before writing a migration, and read logs and advisors when something misbehaves, instead of me pasting from the dashboard.

## Scripts that back the workflow

```json
"test:db":   "node --test tests/db/*.test.mjs",
"typecheck": "tsc --noEmit",
"lint":      "eslint"
```
