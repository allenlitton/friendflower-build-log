# Case study 1: Concierge watch and find-a-time

PR #6, merged 2026-10-08. 14 files, +944 lines.

## The problem

Friend Flower shows who is where, but you still had to notice that a friend was visiting your city, then work out when you were both free. I wanted the app to say so, and to let two people settle on a time in the chat. I wanted no AI for this release, just taps. (The AI concierge stays "coming soon".)

## What shipped

**Concierge watch (World tab)**
- Flags saved friends who are in your city now, will be, or live where you're visiting.
- Computed from declared trips and home cities at read time, so it always follows the live privacy rules.
- A dot on the tab shows until you've seen new overlaps.

**Find a time (1:1 chats)**
- A pill at the top of a direct chat shows when you're both in the same city.
- "Find a time" lets you tap morning, lunch, evening or night slots on those shared days.
- The picks post to the chat as one card. The other person taps the ones that work, and slots you both pick turn green.

## Design constraints I set

| Rule | How it's enforced |
|---|---|
| Direct chats only | In the database, not just the UI |
| Nobody reads picks outside their own chats | New tables have all privileges revoked from `anon` and `authenticated`. Access is only through functions |
| Respect hidden trips | The shared-days function uses the same `whereabouts` check as every other read |
| Blocks stop everything | Suggest and pick both fail after a block |

## How it was verified

Two new test files (298 lines) run against the real migrations in in-memory Postgres. A selection of what they assert, from [`meet-times.test.mjs`](../../excerpts/db-test-harness/meet-times.test.mjs):

- With no trips, a New Yorker and a San Franciscan share no days.
- A visit makes the shared days appear for both people.
- A trip hidden from you adds no shared days.
- Suggesting posts one message, in day order with duplicates removed, and the suggester counts as free.
- The other person can tap what works and take it back.
- Only days you'll both be in the same city can be suggested, and only valid times of day.
- A time that wasn't suggested can't be picked.
- People outside the chat can see, suggest or pick nothing, and the raw tables are closed to them.
- After a block, suggesting and picking stop.

## Shape of the PR

```
supabase/migrations/…14_concierge_watch.sql   +145
supabase/migrations/…15_meet_times.sql        +197
tests/db/concierge-watch.test.mjs             +160
tests/db/meet-times.test.mjs                  +138
app/(full)/chat/[id]/meet-times.tsx           +139
app/(tabs)/world/page.tsx                      +56
app/(full)/chat/[id]/chat-view.tsx             +57
…and small changes to the tab bar, types, formatters and README
```

<!-- TODO(Allen): add a screenshot or GIF of the Concierge card and the time-picking card to /assets and embed them here. -->
<!-- TODO(Allen): add what you asked Claude for, one thing it got wrong or you changed, and how long this took end to end. -->
