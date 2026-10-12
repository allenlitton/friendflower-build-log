# DB test harness

- `harness.mjs` applies every Supabase migration, in order, to an in-memory Postgres ([PGlite](https://pglite.dev)). It stubs the `auth` and `storage` schemas and the Supabase roles, and provides `as(db, userId, fn)` to run a query as a signed-in user, the way PostgREST would.
- `meet-times.test.mjs` is a real scenario file from PR #6. It reads like a story: two friends, a trip, a proposal, a tap, a block.

These files depend on the private repo's migrations, so they're shown for reading, not running.
