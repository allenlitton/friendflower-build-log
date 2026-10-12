# How I work with Claude Code

What I do on Friend Flower so I can ship quickly without breaking things. Each point is visible in the repo history or the setup files.

## 1. Guardrails in the repo

- `CLAUDE.md` imports `AGENTS.md`, so every session starts with the same project rules.
- `AGENTS.md` tells the model to read the bundled Next.js docs before writing code, because the version in use has breaking changes (see [`claude-setup/`](../claude-setup)).
- Supabase is connected over MCP and scoped to the one project (`.mcp.json`). Claude can inspect tables, read logs and advisors, and run migrations without me copy-pasting between dashboards. The commit that added it is "Add Supabase MCP connection (friendflower project only)".

## 2. Verify, don't trust

Privacy is the product, so the tests matter most where Claude writes the most SQL.

- `npm run test:db` applies every migration to an in-memory Postgres and plays out scenarios as different users: friends, strangers, blocked users, hidden trips.
- Tests assert the failures as well as the successes, for example "people outside the chat can see, suggest or pick nothing", "the raw tables are closed too", and "after a block, suggesting and picking stop".
- `npm run typecheck` and `npm run lint` run before a PR.

The feature in [case study 1](case-studies/01-concierge-watch-and-meet-times.md) added 944 lines across 14 files, and 298 of those lines were tests.

## 3. Slice by user-visible behaviour

PR #6 contains two features, built in two steps (Concierge watch, then find-a-time), each with its own migration and its own tests. A reviewer can read it one slice at a time.

## 4. Fast loop for UI

For visual tweaks, I iterate in tiny PRs, run the app and look at it. The World screen went from a bunch of overlapping avatars to a grid in one PR, then got names under the avatars in the next ([case study 2](case-studies/02-world-grid-iteration.md)).

## 5. Keep the commit trail honest

Commits written with Claude carry a `Co-Authored-By` trailer, so the history shows which work was done together.

## 6. Decisions stay mine

Claude proposes and writes. I decide what the product does: for example, that the AI concierge stays "coming soon" while the non-AI Concierge watch ships, and that the live-distance switch is a single control rather than two.
