<div align="center">

<img src="https://github.com/SPiceZ21/spz-core-media-kit/blob/main/Banner/Banner%232.png?raw=true" alt="SPiceZ-Core Banner" width="100%"/>

<br/>
<br/>

**An open source racing core for FiveM — modular, lightweight, and built purely for racing.**

<br/>

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-orange.svg?style=flat-square)](https://www.gnu.org/licenses/gpl-3.0)
[![FiveM](https://img.shields.io/badge/FiveM-Compatible-orange?style=flat-square)](https://fivem.net)
[![Lua](https://img.shields.io/badge/Lua-5.4-blue?style=flat-square&logo=lua)](https://lua.org)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=flat-square)]()
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/)

</div>

---

## What is SPiceZ-Core?

SPiceZ-Core (`spz-*`) is a **racing-only FiveM framework** — no jobs, no housing, no crime. Every system is designed from the ground up for one thing: competitive street racing.

Inspired by the multi-repo structure of [qb-core](https://github.com/qbcore-framework/qb-core), SPiceZ-Core is a collection of standalone, opt-in modules that talk to each other through a clean exports and event API. Install only what you need. Replace what you don't like.

> Think **Project Street** meets **Project Race** — but open source, fully modular, and built for the community.

---

## How It Works

```
Player joins → Safe Zone → Choose Mode
                               │
              ┌────────────────┴─────────────────┐
              │                                  │
          Freeroam                          Race Queue
        Spawn car                        Poll opens (track + car)
        Free drive                       Highest votes win
                                         TP → isolated race world
                                         Countdown → Race (no collision)
                                         Finish → Stats + XP screen
                                              │
                                    TP back → Safe Zone
                                    Intermission timer
                                         │
                                    ← Repeat →
```

Race worlds are fully isolated using **FiveM routing buckets** — racers exist in a separate dimension with no entity bleed from freeroam. No collision between racers is enforced server-side.

---

## Modules

All modules are separate repositories under this organization. Each one is opt-in — just add or remove it from your `server.cfg`.

### Core

| Repository | Description |
|---|---|
| [spz-core](https://github.com/SPiceZ-Core/spz-core) | Bootstrap, player sessions, state machine, routing bucket manager, event bus |
| [spz-lib](https://github.com/SPiceZ-Core/spz-lib) | Shared utility library — callbacks, notify, timers, math helpers |

### Modules

| Repository | Description |
|---|---|
| [spz-identity](https://github.com/SPiceZ-Core/spz-identity) | Player profiles, driver licenses, crew tags |
| [spz-vehicles](https://github.com/SPiceZ-Core/spz-vehicles) | Vehicle class registry, stat sheets, spawn and despawn |
| [spz-garage](https://github.com/SPiceZ-Core/spz-garage) | Owned vehicles, storage, impound |
| [spz-tuning](https://github.com/SPiceZ-Core/spz-tuning) | Performance upgrades, dyno, engine / tires / aero |
| [spz-races](https://github.com/SPiceZ-Core/spz-races) | Lobbies, poll system, countdown, checkpoints, timing engine, race state machine |
| [spz-economy](https://github.com/SPiceZ-Core/spz-economy) | Credits wallet, entry fees, prize payouts, betting |
| [spz-progression](https://github.com/SPiceZ-Core/spz-progression) | XP, driver rank tiers, license unlocks, reputation |
| [spz-leaderboard](https://github.com/SPiceZ-Core/spz-leaderboard) | Per-track records, global stats, session history |
| [spz-weather](https://github.com/SPiceZ-Core/spz-weather) | Race-synced weather and time-of-day schedules |
| [spz-admin](https://github.com/SPiceZ-Core/spz-admin) | Staff panel, force end race, spectate, ban management |

### UI / NUI

| Repository | Description |
|---|---|
| [spz-hud](https://github.com/SPiceZ-Core/spz-hud) | Speedometer, race overlay, poll UI, countdown display, post-race stats |
| [spz-menu](https://github.com/SPiceZ-Core/spz-menu) | Choice screen, freeroam spawner menu, garage menus |

### Infrastructure

| Repository | Description |
|---|---|
| [spz-recipe](https://github.com/SPiceZ-Core/spz-recipe) | txAdmin YAML recipe + `server.cfg` template |
| [spz-docs](https://github.com/SPiceZ-Core/spz-docs) | Documentation site — API reference, install guide, module docs |
| [.github](https://github.com/SPiceZ-Core/.github) | Org-wide issue templates, PR templates, funding |

---

## Quick Start

The fastest way to get running is via the **txAdmin recipe**.

1. Open **txAdmin** → _New Server_ → _Remote URL Template_
2. Paste the recipe URL:
   ```
   https://raw.githubusercontent.com/SPiceZ-Core/spz-recipe/main/recipe.yaml
   ```
3. Follow the setup wizard — the recipe installs all dependencies (`oxmysql`, `ox_lib`) and all `spz-*` modules automatically.
4. Edit `resources/spz-core/config.lua` to configure your server.

### Manual Install (custom setups)

Load order matters. Follow this sequence in `server.cfg`:

```cfg
# ── Dependencies ──────────────────────────────────────
ensure oxmysql
ensure ox_lib
ensure screenshot-basic        # optional

# ── SPiceZ Core ───────────────────────────────────────
ensure spz-lib
ensure spz-core

# ── Modules ───────────────────────────────────────────
ensure spz-identity
ensure spz-vehicles
ensure spz-economy
ensure spz-garage
ensure spz-tuning
ensure spz-races
ensure spz-progression
ensure spz-leaderboard
ensure spz-weather             # optional

# ── UI ────────────────────────────────────────────────
ensure spz-hud
ensure spz-menu

# ── Admin (always last) ───────────────────────────────
ensure spz-admin
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Server runtime | [FiveM](https://fivem.net) / [cfx-server](https://github.com/citizenfx/fivem) |
| Language | Lua 5.4 |
| Database | MySQL via [oxmysql](https://github.com/overextended/oxmysql) |
| Shared utilities | [ox_lib](https://github.com/overextended/ox_lib) |
| NUI (frontend) | React + Vite |
| World isolation | FiveM routing buckets |

---

## Design Principles

**No bloat.** SPiceZ-Core is racing-only. There are no job systems, housing, or crime mechanics — and there never will be.

**Module-first.** Every feature lives in its own repository. You can run `spz-core` + `spz-races` + `spz-hud` with nothing else and have a working race server.

**Event-driven.** Modules communicate only through registered events and exports. No module imports another module's files directly. This makes swapping or replacing any module straightforward.

**Config-driven.** All tunable values live in `config.lua` files. Nothing is hardcoded. Hot-reload is supported for non-structural config keys.

**Server-authoritative.** Race positions, state transitions, and routing bucket assignments are all validated server-side. The client is never trusted for anything that affects race integrity.

---

## Project Status

SPiceZ-Core is actively in development. Here's where things stand:

| Module | Status |
|---|---|
| spz-lib | 🟢 In Development |
| spz-core | 🟢 In Development |
| spz-identity | 🟢 In Development |
| spz-vehicles | 🟢 In Development |
| spz-hud | 🟡 Testing |
| spz-races | 🔵 Designing |
| spz-economy | ⚪ Planned |
| spz-progression | ⚪ Planned |
| spz-garage | ⚪ Planned |
| spz-tuning | ⚪ Planned |
| spz-leaderboard | ⚪ Planned |
| spz-admin | ⚪ Planned |
| spz-hud (full) | ⚪ Planned |
| spz-menu | ⚪ Planned |
| spz-docs | ⚪ Planned |

> Track progress on our [GitHub Project Board](https://github.com/orgs/SPiceZ-Core/projects/1)

---

## Contributing

We welcome contributions of all kinds — bug reports, feature suggestions, documentation, and code.

1. Read the [Contributing Guide](.github/CONTRIBUTING.md)
2. Check the [Project Board](https://github.com/orgs/SPiceZ-Core/projects/1) for open tasks
3. Open an issue before starting work on a large feature so we can discuss the approach
4. Follow the Lua style guide in each repository's `CONTRIBUTING.md`

**Before submitting a PR:**
- Test on a local FiveM server
- Make sure no other `spz-*` module is broken by your change
- Add or update documentation if you're changing an export or event

---

## Repository Layout

```
SPiceZ-Core (org)
├── spz-core/
│   ├── shared/        ← events, states, logger, emitter
│   ├── server/        ← sessions, state machine, buckets, permissions
│   └── client/        ← config sync, error relay
├── spz-lib/
│   ├── shared/        ← callbacks, notify, timer, math
├── spz-races/
│   ├── shared/
│   ├── server/        ← state machine, poll, bucket, timing, checkpoints
│   └── client/        ← checkpoint renders, NUI bridge
├── spz-hud/
│   ├── client/        ← NUI triggers
│   └── ui/            ← React + Vite frontend
└── ...
```

---

## Community

- **Discord:** [Join our server](https://discord.gg/) — support, dev chat, announcements
- **Issues:** Use the issue tracker in the relevant module repository
- **Discussions:** [GitHub Discussions](https://github.com/orgs/SPiceZ-Core/discussions) for ideas and questions

---

## License

All SPiceZ-Core repositories are licensed under the **GNU General Public License v3.0**.

See [LICENSE](LICENSE) for details. You are free to use, modify, and distribute this software under the same license. You may **not** sell SPiceZ-Core or its modules as a closed-source product.

---

<div align="center">

Built with passion for the FiveM racing community.

**[Docs](https://github.com/SPiceZ-Core/spz-docs) · [Discord](https://discord.gg/) · [Project Board](https://github.com/orgs/SPiceZ-Core/projects/1) · [Contributing](.github/CONTRIBUTING.md)**

</div>
