---
name: Group trip website
description: >-
  When the user wants a shared website for a group trip (itinerary, meetups,
  voting, budget and splitting, tickets, map, weather) that classmates or
  friends can open and edit together, built and hosted for free.
---
# Group trip website

Build a mobile-first, shared trip site that a whole group can use without logging in, then host it for free on a permanent URL.

## 1. Clarify (grill-me style, one option widget at a time)
Ask only what changes the build; decide sensible defaults yourself and let the user adjust.
- Trip basics: destination, dates, group size, lodging, budget per person, currencies.
- Visual style (ask for a reference image if they have one) and layout feel.
- Features to include. Default set:
  - Itinerary with day tabs (one day at a time; opens on today's day during the trip). Personal free-time plans stay off the site; free slots just say free time.
  - Free-time meetups: anyone posts a plan (what, when, where to meet, link, note, host name), others tap to join with their name.
  - Voting/polls (e.g. restaurants).
  - Budget page split into tabs: budget overview, group fund spending log (total and per-person share), advances ledger (payer, amount in either currency, equal or custom split, roster checkboxes), settlement (minimal transfers, both currencies).
  - Tickets and checklist, map of spots, weather (historical averages until the forecast window opens).
- Optional, only when asked: self-service flight list (each person adds their own flight and times, sorted by arrival).
- Permissions default: anyone can add/edit shared data (meetups, votes, ledger); an organizer passcode (env var) protects itinerary edits and the roster.
- Leave out what the user doesn't want (rosters, task lists, phrasebooks, order numbers and other private data).

## 2. Build
- Hand the build to a cloud coding agent with a new repo: Next.js + Node 22, Postgres via `DATABASE_URL` in production with SQLite fallback locally, editable content file per day, tests for money math, screenshots of every page.
- Never hardcode secrets or real names; organizer passcode only from an env var.

## 3. Host for free
- Always ask which free host to use (option widget). Recommend Vercel Hobby deployed from the CLI (`vercel deploy --prod` with a token, avoiding a paid Git integration) plus a free Neon Postgres.
- The user creates the hosting and database accounts, then supplies tokens and the organizer passcode through secure secret inputs (never in chat).
- Make the site publicly openable (turn off deployment protection) and give it a friendly domain.
- After each deploy, verify every page and API returns 200, data persists, and the error log is clean; clean up any test data.

## 4. Iterate
- Plan detailed days in chat first, then push content updates to the site.
- Every change, big or small: describe it, build, send screenshots, get the user's explicit yes, then deploy, verify, and send the live link. Never update the live site without that approval.
