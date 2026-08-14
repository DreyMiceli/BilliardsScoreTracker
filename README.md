# Billiards Score Tracker

A lightweight, mobile-friendly web app for tracking multi-player billiards (pool) round-robin tournaments. Record match winners, breakers, and game times as you play — then review standings, history, and shareable summaries.

**Live:** https://billiards.azureweb.workers.dev/

## What it does

Set up 2–8 players, start a session, and the app builds a full round-robin schedule (every player vs every other player). As each match finishes you tap the winner; the app advances to the next pairing, keeps live scores, and tracks how long each game took. When you’re done, end the session for a tournament summary you can share or revisit later from history.

Sessions resume automatically if you leave mid-tournament — unfinished play is restored from local storage on the next visit.

## Features

### Session setup
- **2–8 players** with add/remove controls
- **Default names** loaded from the last saved session (or `Player 1` / `Player 2` when there’s no history)
- **Shuffled player order** each new tournament so the schedule isn’t always the same
- **Round-robin schedule** generated automatically for all unique pairings

### Live match tracking
- **Current match display** with both players and a live game timer
- **Game / Set counter** (e.g. `Game 5 - Set 2 (2/3)`) so you always know where you are in the cycle
- **Breaker assignment** with fair initial breakers and **automatic alternation** on rematches
- **Tap-to-flip breaker** if you need to override who breaks
- **One-tap winner buttons** colored per player
- **Short-match confirmation** if a result is recorded under 30 seconds (cancel keeps the timer running)
- **Per-player win totals** updated after every game
- **Quick result chips** for completed games — tap a chip to edit the winner or delete the result
- **Expandable games list** with breaker, winner, pairing, and duration for each match
- **Looping schedule** — after a full set, pairings repeat for another round

### Session lifecycle
- **End session** opens a summary (or deletes an empty session)
- **Resume or fully close** from the summary modal
- **Unfinished sessions auto-restore** on page load
- **Empty-session cleanup** when ending with no games played

### Tournament summary
- Standings with win counts
- Matches played, total time, and average time per match
- Full/partial round progress
- Match log with breaker `(B)` and winner `(W)` tags
- **Share** via the device share sheet or clipboard copy

### History
- List of completed sessions with date, players, wins, game count, and timing stats
- Open any past session for its full summary
- Share or delete individual history entries
- Viewing history does **not** overwrite an active unfinished session

### Data & reliability
- All data stored in **browser `localStorage`** (no account required)
- Safe load/save with corrupt-data recovery
- Legacy 2-player session format still supported
- Null-safe timer and DOM handling for stable mobile use
- Raw backup editor at `/Storage.html` — view, validate, save, share, download, or import the `billiardsSessions` JSON

### UI
- Dark, mobile-first layout (Tailwind CSS)
- Distinct player colors across scores, buttons, and history
- Custom 8-ball favicon

## How to use

1. Open the app and confirm or edit player names on the start screen.
2. Optionally add more players (up to 8).
3. Tap **Start Round-Robin Tournament**.
4. For each match: note the breaker, play, then tap the winner.
5. Review scores and the games list as you go; edit past results if needed.
6. Tap **End Session** → review the summary → **End Session** again to save, or **Resume** to keep playing.
7. Use the **History** tab to revisit, share, or delete completed tournaments.

## Tech stack

| Piece | Detail |
|--------|--------|
| App | Single-page vanilla HTML / CSS / JavaScript |
| Styling | [Tailwind CSS](https://tailwindcss.com/) (CDN) |
| Icons | [Font Awesome](https://fontawesome.com/) |
| Storage | `localStorage` key `billiardsSessions` |
| Hosting | Static assets on [Cloudflare Workers](https://workers.cloudflare.com/) via Wrangler |

## Local development

Open `index.html` in a browser, or serve the folder with any static server:

```bash
# example
npx serve .
```

Deploy with Wrangler (see `wrangler.jsonc`):

```bash
npx wrangler deploy
```

## Project files

```
BilliardsScoreTracker/
├── index.html      # App UI + logic
├── Storage.html    # Raw localStorage backup / JSON editor
├── favicon.svg     # App icon
├── wrangler.jsonc  # Cloudflare Workers static deploy config
└── README.md
```

## Privacy

Everything stays on the device. No backend database, analytics, or accounts — clearing site data removes session history.
