# Timeline

Taken from the private repo's git history (36 commits). Dates are commit dates.

## Sep 25: v1 in one push
- Scaffolded from Create Next App, then shipped **Friend Flower v1**: friend graph, privacy rules, mutual-friend verification and all the design screens.
- The first three migrations hold the schema, about 50 Postgres functions for who-can-see-what, and reference data (cities, neighbourhoods, venues).

## Sep 26: Beta feedback
- Home-city options, circle places, and finding a friend by email or phone.
- Neighbourhood became required for live-map cities.
- Sign-in accepts the default Supabase email links and leads with the emailed code.

## Sep 27: Busiest day (about 20 commits)
- **Live distance:** opt-in live location shows real distances on Nearby and profiles. A later commit removed the old "Show my distance" switch, so there is only one way to share.
- **Nearby** shows only people with live distance on.
- **Database performance:** wrapped the signed-in-user check once per query in row-level security and indexed common foreign keys.
- Peninsula and SF neighbourhoods, a units setting, and invite-sharing polish for iOS Copy and link previews.
- Wired up the Supabase MCP connection, scoped to the one project.

## Sep 28: Live anywhere
- Pick **any city in the world** as home, with one city picker reused for trips.
- Live distance now updates your current city and asks for trip dates.
- Trip dates became editable, and the You screen shows the city you're in today, not home.

## Oct 5: Retention and polish
- Stay signed in, remember your email, and offer **Add to Home Screen** after sign-in.
- Larger icons and labels in the bottom menu.

## Oct 8: Concierge watch and find-a-time (PR #6)
A full vertical slice: two migrations, UI, and two test files. See [case study 1](case-studies/01-concierge-watch-and-meet-times.md).

## Oct 9: World screen iteration (PRs #7 and #8)
An evenly spaced grid, then first names under avatars. See [case study 2](case-studies/02-world-grid-iteration.md).

---

### Shape of the work
- Early work was big pushes (v1 in a day).
- Later work moved to feature branches and PRs, each one small and reviewable.
- The tests cover the privacy rules, so risky database changes get checked before they ship.
