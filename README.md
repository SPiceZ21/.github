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
| [spz-core](https://github.com/SPiceZ21/spz-core) | `2.0.0` | Bootstrap, sessions, routing buckets, permissions, database migrations |
| [spz-identity](https://github.com/SPiceZ21/spz-identity) | `1.5.0` | Profiles, citizen IDs, licenses, crews, character creation |
| [spz-appearance](https://github.com/SPiceZ21/spz-appearance) | `2.0.0` | Ped models, personal outfits, crew uniforms |
| [spz-spawn](https://github.com/SPiceZ21/spz-spawn) | `2.1.0` | Play menu, spawn points, world entry |
| [spz-vehicles](https://github.com/SPiceZ21/spz-vehicles) | `2.0.0` | Vehicle registry, classes, spawning, upgrades |

### Racing

| Repository | Version | Purpose |
|---|---|---|
| [spz-races](https://github.com/SPiceZ21/spz-races) | `1.9.0` | Race engine — queue, poll, countdown, checkpoints, sectors, results |
| [spz-progression](https://github.com/SPiceZ21/spz-progression) | `2.1.0` | XP, ranks, SR, iRating, licenses, seasons |
| [spz-leaderboard](https://github.com/SPiceZ21/spz-leaderboard) | `1.0.0` | Standings, class tables, records, activity |
| [spz-poll](https://github.com/SPiceZ21/spz-poll) | `1.1.2` | Track and vehicle vote |
| [spz-raceUI](https://github.com/SPiceZ21/spz-raceUI) | `2.0.0` | Countdown, overlay, splits, post-race stats |
| [spz-raceline](https://github.com/SPiceZ21/spz-raceline) | `0.4.0` | Racing-line trainer and ghost car |
| [spz-speedcam](https://github.com/SPiceZ21/spz-speedcam) | `1.0.0` | Speed cameras with records |
| [spz-betting](https://github.com/SPiceZ21/spz-betting) | `1.0.0` | Live pari-mutuel spectator betting |
| [spz-spectate](https://github.com/SPiceZ21/spz-spectate) | `1.0.0` | Spectator overlay |

### Vehicle and driving

| Repository | Version | Purpose |
|---|---|---|
| [spz-physics](https://github.com/SPiceZ21/spz-physics) | `0.4.0` | Powertrain sim — torque curves, gears, clutch, turbo, LSD, PP rating |
| [spz-tunners](https://github.com/SPiceZ21/spz-tunners) | `1.0.0` | Keyboard-driven tuning menu |
| [spz-nos](https://github.com/SPiceZ21/spz-nos) | `1.0.5` | Nitrous (cosmetic) |
| [spz-carspawner](https://github.com/SPiceZ21/spz-carspawner) | `1.1.0` | ox_lib vehicle spawn menu |
| [spz-carfx](https://github.com/SPiceZ21/spz-carfx) | `1.0.0` | Custom vehicle particle effects |
| [spz-vehfunc](https://github.com/SPiceZ21/spz-vehfunc) | `1.0.1` | Indicators, hazards, taunts, idle cam |
| [spz-speedometer](https://github.com/SPiceZ21/spz-speedometer) | `1.1.2` | Speedometer HUD |

### World and client

| Repository | Version | Purpose |
|---|---|---|
| [spz-nametag](https://github.com/SPiceZ21/spz-nametag) | `1.1.6` | 3D player nameplates |
| [spz-vegetation](https://github.com/SPiceZ21/spz-vegetation) | `1.0.0` | Proximity vegetation streamer |
| [spz-fpscap](https://github.com/SPiceZ21/spz-fpscap) | `1.0.0` | 60 FPS fairness cap |
| [spz-loading](https://github.com/SPiceZ21/spz-loading) | `1.2.1` | Loading screen |
| [spz-rpc](https://github.com/SPiceZ21/spz-rpc) | `1.0.1` | Discord rich presence |
| [spz-log](https://github.com/SPiceZ21/spz-log) | `1.0.1` | Discord webhook logging |

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
ensure spz-rpc
ensure spz-loading
ensure spz-core
ensure spz-identity
ensure spz-appearance
ensure spz-spawn

# ── Racing ───────────────────────────────────
ensure spz-speedcam
ensure spz-vehicles
ensure spz-races
ensure spz-progression
ensure spz-nametag
ensure spz-poll
ensure spz-raceUI
ensure spz-leaderboard
ensure spz-carspawner
ensure spz-physics
ensure spz-fpscap
ensure spz-raceline
ensure spz-speedometer
ensure spz-nos
ensure spz-vehfunc
ensure spz-tunners
ensure spz-spectate
ensure spz-betting

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
