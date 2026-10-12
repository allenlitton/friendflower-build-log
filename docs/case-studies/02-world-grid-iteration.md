# Case study 2: World screen, two small PRs

PRs #7 and #8, both merged 2026-10-09. One file changed in each.

## The problem

The World tab showed each city's friends as a row of overlapping avatars, capped at five with a "+N" for the rest. Friends past the fifth were hidden, and you couldn't tell who anyone was without tapping.

## PR #7: show everyone, evenly spaced

- Replaced the overlapping row with a 4-column grid that shows **every** friend in the city.
- Dropped the cap and the "+N".
- Moved the city note and the call-to-action button to their own row beneath the grid.

PR #7 changed 7 lines added, 7 removed. See the real diff in [`excerpts/world-grid/world-page.diff`](../../excerpts/world-grid/world-page.diff).

## PR #8: put a name under each avatar

- Added each friend's first name under their avatar, so the grid reads as people and not as flowers.
- 11 lines added, 8 removed.

## Why show this

It's a small example of the loop I use for UI work: change one thing, look at it in the app, open a small PR, and move on. The change is easy to review and easy to revert.

<!-- TODO(Allen): add before/after screenshots in /assets. -->
