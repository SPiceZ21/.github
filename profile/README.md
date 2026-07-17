<div align="center">

<img src="https://github.com/SPiceZ21/spz-core-media-kit/blob/main/Banner/wip-banner.png?raw=true" alt="SPiceZ-Core Banner" width="100%"/>

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

## 🎮 What is SPiceZ-Core?

**SPiceZ-Core** (`spz-*`) is a **racing‑only FiveM framework** built from the ground up for competitive street racing. It follows a **module‑first** architecture: each feature lives in its own repository and can be enabled or disabled independently.

---

## 📦 Current Modules

| Repository | Description |
|---|---|
| [spz-core](https://github.com/SPiceZ21/spz-core) | Core engine, player sessions, routing bucket manager, event bus, database migrations |
| [spz-identity](https://github.com/SPiceZ21/spz-identity) | Player profiles, driver licenses, crew tags |
| [spz-appearance](https://github.com/SPiceZ21/spz-appearance) | Outfit persistence and crew uniforms on top of `fivem-appearance` |
| [spz-spawn](https://github.com/SPiceZ21/spz-spawn) | Spawn menu, idle animation, cinematic spawn camera |
| [spz-vehicles](https://github.com/SPiceZ21/spz-vehicles) | Vehicle registry, stat sheets, customization persistence |
| [spz-races](https://github.com/SPiceZ21/spz-races) | Queue, poll, countdown, checkpoints, timing engine, time trial |
| [spz-progression](https://github.com/SPiceZ21/spz-progression) | XP, driver ranks, license unlocks, safety rating |
| [spz-leaderboard](https://github.com/SPiceZ21/spz-leaderboard) | Per‑track records, global standings, session history |
| [spz-raceUI](https://github.com/SPiceZ21/spz-raceUI) | Race overlay, 3D checkpoint pill, player list, post‑race stats |
| [spz-poll](https://github.com/SPiceZ21/spz-poll) | Track vote UI between race cycles |
| [spz-nametag](https://github.com/SPiceZ21/spz-nametag) | Minimal 3D player nameplates |
| [spz-speedometer](https://github.com/SPiceZ21/spz-speedometer) | Speedometer HUD |
| [spz-speedcam](https://github.com/SPiceZ21/spz-speedcam) | Speed cameras, personal bests, global records |
| [spz-physics](https://github.com/SPiceZ21/spz-physics) | Standalone powertrain sim — torque curves, gears, clutch, rev limiter, PP rating |
| [spz-carspawner](https://github.com/SPiceZ21/spz-carspawner) | ox_lib vehicle spawn menu |
| [spz-carfx](https://github.com/SPiceZ21/spz-carfx) | Custom vehicle particle effects |
| [spz-nos](https://github.com/SPiceZ21/spz-nos) | Nitrous system |
| [spz-vehfunc](https://github.com/SPiceZ21/spz-vehfunc) | Vehicle functions — indicators and lights |
| [spz-fpscap](https://github.com/SPiceZ21/spz-fpscap) | 60 FPS fairness cap |
| [spz-raceline](https://github.com/SPiceZ21/spz-raceline) | Racing-line trainer — paints your line on the road (green throttle / red brake) |
| [spz-loading](https://github.com/SPiceZ21/spz-loading) | Loading screen (local video + audio) |
| [spz-rpc](https://github.com/SPiceZ21/spz-rpc) | Discord rich presence |
| [spz-log](https://github.com/SPiceZ21/spz-log) | Logging system |
| [spz-ui](https://github.com/SPiceZ21/spz-ui) | Shared UI components consumed at build time by the NUI resources |
| [spz-txrecipe](https://github.com/SPiceZ21/spz-txrecipe) | txAdmin recipe + auto‑generated `server.cfg` |
| [.github](https://github.com/SPiceZ21/.github) | Org‑wide issue & PR templates, funding docs |

---

## ⚙️ Workflow Overview

The repository uses **GitHub Actions** to automate CI, linting, and release publishing:

- **`ci.yml`** – Runs on every push/PR, checks Lua syntax, runs unit tests (if any) and validates workflow definitions.
- **`release.yml`** – Triggered when a new tag is pushed. It builds the release assets, creates a GitHub Release, and updates the `spz-txrecipe` YAML with the new version.

> **Note:** All module repositories have their own CI pipelines; the central repo only validates shared assets and documentation.

---

## 🚀 Quick Start

### Using the txAdmin Recipe (recommended)
1. Open **txAdmin** → *New Server* → *Remote URL Template*.
2. Paste the recipe URL:
   ```
   https://raw.githubusercontent.com/SPiceZ21/spz-txrecipe/main/spz-recipe.yaml
   ```
3. Follow the wizard – it installs all required dependencies (`oxmysql`, `ox_lib`, `fivem-appearance`, `pma-voice`) and pulls every `spz-*` module. The database schema applies itself on first boot via spz-core migrations.
4. Edit `resources/spz-core/config.lua` to fine‑tune your server settings.

### Manual Install
Add the following resources to your `server.cfg` **in the exact order**:

```cfg
# ── Dependencies ──────────────────────────────────────
ensure oxmysql
ensure ox_lib
ensure fivem-appearance
ensure pma-voice
ensure screenshot-basic        # optional

# ── Core ──────────────────────────────────────────────
ensure spz-rpc
ensure spz-loading
ensure spz-core
ensure spz-identity
ensure spz-appearance
ensure spz-spawn

# ── Racing Modules ────────────────────────────────────
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

# ── Admin (always last) ───────────────────────────────
ensure vMenu
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Server runtime | FiveM / Cfx‑server |
| Language | Lua 5.4 |
| Database | MySQL via `oxmysql` |
| Shared utilities | `ox_lib` |
| NUI frontend | React 18 + Vite + Framer Motion |
| World isolation | FiveM routing buckets |

---

## 🎨 Design Principles

- **No bloat** – Racing‑only, no jobs/housing/crime.
- **Module‑first** – Every feature is a standalone repo.
- **Event‑driven** – Modules communicate exclusively through events/exports.
- **Config‑driven** – All tunable values live in `config.lua` files; hot‑reload supported.
- **Server‑authoritative** – Core race logic runs on the server; the client never decides race outcomes.

---

## 📈 Project Status

| Module | Status |
|---|---|
| spz-core | 🟡 Testing |
| spz-identity | 🟡 Testing |
| spz-appearance | 🟡 Testing |
| spz-spawn | 🟡 Testing |
| spz-vehicles | 🟡 Testing |
| spz-races | 🟡 Testing |
| spz-raceUI | 🟡 Testing |
| spz-poll | 🟡 Testing |
| spz-progression | 🟢 In Development |
| spz-leaderboard | 🟢 In Development |
| spz-nametag | 🟡 Testing |
| spz-speedometer | 🟡 Testing |
| spz-speedcam | 🟢 In Development |
| spz-physics | 🟢 In Development (v0.4) |
| spz-carspawner | 🟡 Testing |
| spz-nos / spz-vehfunc / spz-carfx | 🟢 In Development |
| spz-fpscap / spz-loading / spz-rpc | 🟡 Testing |
| spz-raceline | 🟢 In Development (v0.1) |
| spz-admin | ⚪ Planned |
| spz-docs | ⚪ Planned |

---

## 🤝 Contributing

We welcome contributions of any kind:
1. Read the [Contributing Guide](.github/CONTRIBUTING.md).
2. Check the [Project Board](https://github.com/orgs/SPiceZ21/projects/1) for open tasks.
3. Open an issue before starting large work.
4. Follow the Lua style guide in each repo’s `CONTRIBUTING.md`.

**Before submitting a PR:**
- Test on a local FiveM server.
- Ensure no other `spz-*` module is broken by your change.
- Update documentation if you modify an export or event.

---

## 📄 License

All SPiceZ‑Core repositories are licensed under the **GNU GPL v3**. See the [LICENSE](LICENSE) file for details. You may **not** sell SPiceZ‑Core or its modules as a closed‑source product.

---

<div align="center">

Built with passion for the FiveM racing community.

**[Docs](https://github.com/SPiceZ21/spz-docs) · [Discord](https://discord.gg/) · [Project Board](https://github.com/orgs/SPiceZ21/projects/1) · [Contributing](.github/CONTRIBUTING.md)**

</div>
