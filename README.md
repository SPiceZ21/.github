<div align="center">

<img src="https://github.com/SPiceZ21/spz-core-media-kit/blob/main/Banner/wip-banner.png?raw=true" alt="SPiceZ-Core Banner" width="100%"/>

**An open-source racing core for FiveM — modular, lightweight, and built purely for racing.**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-orange.svg?style=flat-square)](https://www.gnu.org/licenses/gpl-3.0)
[![FiveM](https://img.shields.io/badge/FiveM-Compatible-orange?style=flat-square)](https://fivem.net)
[![Lua](https://img.shields.io/badge/Lua-5.4-blue?style=flat-square&logo=lua)](https://lua.org)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=flat-square)]()

</div>

---

## What is SPiceZ-Core?

**SPiceZ-Core** (`spz-*`) is a racing-only FiveM framework built for competitive street
racing — no jobs, no housing, no crime. Every feature lives in its own repository and can
be enabled or removed independently; modules talk to each other only through events and
exports, and the server owns every decision that affects a race result.

---

## Repositories

### Framework

| Repository | Version | Purpose |
|---|---|---|
| [spz-core](https://github.com/SPiceZ21/spz-core) | `1.0.0` | Bootstrap, sessions, routing buckets, permissions, database migrations, player profiles, appearance, spawning, analytics |
| [spz-vehicles](https://github.com/SPiceZ21/spz-vehicles) | `1.0.0` | Vehicles: registry, classes, spawning, upgrades, garage, tuner, indicators |
| [spz-discord](https://github.com/SPiceZ21/spz-discord) | `2.0.0` | Discord: race feeds, logs, rich presence, whitelist, role-based admin |

### Racing

| Repository | Version | Purpose |
|---|---|---|
| [spz-races](https://github.com/SPiceZ21/spz-races) | `1.9.0` | Race engine — queue, vote, countdown, checkpoints, sectors, results, race HUD, leaderboard, progression, spectate, replays, speed cameras |
| [spz-raceline](https://github.com/SPiceZ21/spz-raceline) | `1.4.0` | Racing-line trainer and ghost car |


### Vehicle and driving

| Repository | Version | Purpose |
|---|---|---|
| [spz-physics](https://github.com/SPiceZ21/spz-physics) | `1.4.0` | Powertrain sim — torque curves, gears, clutch, turbo, LSD, PP rating |
| [spz-carfx](https://github.com/SPiceZ21/spz-carfx) | `1.0.0` | Custom vehicle particle effects |
| [spz-hud](https://github.com/SPiceZ21/spz-hud) | `0.1.0` | Every UI on one page: race HUD, speedometer, pause menu, nametags, chat, emotes, TAB hub, layout editor |

### World and client

| Repository | Version | Purpose |
|---|---|---|
| [spz-vegetation](https://github.com/SPiceZ21/spz-vegetation) | `1.0.0` | Proximity vegetation streamer |
| [spz-fpscap](https://github.com/SPiceZ21/spz-fpscap) | `1.0.0` | 60 FPS fairness cap |
| [spz-loading](https://github.com/SPiceZ21/spz-loading) | `1.2.1` | Loading screen |

### Tooling and assets

| Repository | Purpose |
|---|---|
| [spz-ui](https://github.com/SPiceZ21/spz-ui) | Shared NUI design system consumed at build time |
| [spz-txrecipe](https://github.com/SPiceZ21/spz-txrecipe) | txAdmin recipe and generated `server.cfg` |
| [spz-core-media-kit](https://github.com/SPiceZ21/spz-core-media-kit) | Logos, banners, fonts |
| [.github](https://github.com/SPiceZ21/.github) | Org-wide issue and PR templates, funding docs |

---

## Quick start

### txAdmin recipe (recommended)

1. txAdmin → **Server Setup** → **Remote URL Template**.
2. Paste:
   ```
   https://raw.githubusercontent.com/SPiceZ21/spz-txrecipe/main/spz-recipe.yaml
   ```
3. Follow the wizard — it installs the dependencies (`oxmysql`, `ox_lib`,
   `fivem-appearance`, `pma-voice`) and every `spz-*` module, and writes `server.cfg` in
   the right order.
4. Boot the server. `spz-core` applies its migrations automatically; there is no SQL to
   import.

### Manual install

Order matters:

```cfg
# ── Dependencies ─────────────────────────────
ensure oxmysql
ensure ox_lib
ensure fivem-appearance
ensure pma-voice
ensure screenshot-basic      # optional

# ── Core ─────────────────────────────────────
ensure spz-loading
ensure spz-core
ensure spz-hud

# ── Racing ───────────────────────────────────
ensure spz-vehicles
ensure spz-races
ensure spz-physics
ensure spz-fpscap
ensure spz-raceline

# ── Admin (last) ─────────────────────────────
ensure vMenu
```

---

## Design principles

- **No bloat** — racing only.
- **Module-first** — every feature is a standalone repository.
- **Event-driven** — modules communicate through events and exports.
- **Config-driven** — tunables live in each module's `config.lua`.
- **Server-authoritative** — the client never decides a race outcome.
- **One schema owner** — all SQL lives in `spz-core/migrations/`.

---

## Tech stack

| Layer | Technology |
|---|---|
| Server runtime | FiveM / Cfx server |
| Language | Lua 5.4 |
| Database | MySQL via `oxmysql` |
| Shared utilities | `ox_lib` |
| NUI frontend | Vite · Preact · TypeScript (`spz-ui`) |
| World isolation | FiveM routing buckets |

---

## Contributing

1. Check the [Project Board](https://github.com/orgs/SPiceZ21/projects/1) for open tasks.
2. Open an issue before starting large work.
3. Keep changes inside one module where possible.

Before submitting a PR:

- Test on a local FiveM server with the full stack loaded.
- Check no other `spz-*` module breaks.
- Add a new migration rather than editing an applied one.
- Update the module README and `CHANGELOG.md` when you change an export, event or command.

---

## License

All SPiceZ-Core repositories are licensed under the **GNU GPL v3**. You may not sell
SPiceZ-Core or its modules as a closed-source product.

<div align="center">

Built for the FiveM racing community.

**[Project Board](https://github.com/orgs/SPiceZ21/projects/1)**

</div>
