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
| [spz-core](https://github.com/SPiceZ-Core/spz-core) | Core engine, player sessions, routing bucket manager, event bus |
| [spz-lib](https://github.com/SPiceZ-Core/spz-lib) | Shared utilities – callbacks, timers, math helpers |
| [spz-identity](https://github.com/SPiceZ-Core/spz-identity) | Player profiles, driver licenses, crew tags |
| [spz-vehicles](https://github.com/SPiceZ-Core/spz-vehicles) | Vehicle registry, stat sheets, spawn & despawn |
| [spz-races](https://github.com/SPiceZ-Core/spz-races) | Lobby system, poll, countdown, checkpoints, timing engine |
| [spz-progression](https://github.com/SPiceZ-Core/spz-progression) | XP, driver ranks, license unlocks, safety rating |
| [spz-leaderboard](https://github.com/SPiceZ-Core/spz-leaderboard) | Per‑track records, global standings, session history |
| [spz-weather](https://github.com/SPiceZ-Core/spz-weather) | Race‑synced weather & time‑of‑day schedules |
| [spz-hud](https://github.com/SPiceZ-Core/spz-hud) | Speedometer, race overlay, poll UI, countdown, post‑race stats (React + Vite) |
| [spz-menu](https://github.com/SPiceZ-Core/spz-menu) | Mode choice screen, freeroam spawner, garage menus |
| [spz-admin](https://github.com/SPiceZ-Core/spz-admin) | Staff panel, force end race, spectate, ban management |
| [spz-txrecipe](https://github.com/SPiceZ-Core/spz-txrecipe) | txAdmin recipe + auto‑generated `server.cfg` |
| [.github](https://github.com/SPiceZ-Core/.github) | Org‑wide issue & PR templates, funding docs |

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
   https://raw.githubusercontent.com/SPiceZ-Core/spz-txrecipe/main/spz-recipe.yaml
   ```
3. Follow the wizard – it installs all required dependencies (`oxmysql`, `ox_lib`), pulls every `spz-*` module, and creates the database tables automatically.
4. Edit `resources/spz-core/config.lua` to fine‑tune your server settings.

### Manual Install
Add the following resources to your `server.cfg` **in the exact order**:

```cfg
# ── Dependencies ──────────────────────────────────────
ensure oxmysql
ensure ox_lib
ensure screenshot-basic        # optional

# ── Core ───────────────────────────────────────
ensure spz-lib
ensure spz-core

# ── Modules ───────────────────────────────────────────
ensure spz-identity
ensure spz-vehicles
ensure spz-progression
ensure spz-races
ensure spz-leaderboard
ensure spz-weather            # optional

# ── UI ────────────────────────────────────────────────
ensure spz-hud
ensure spz-menu

# ── Admin (always last) ───────────────────────────────
ensure spz-admin
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
| spz-lib | 🟢 In Development |
| spz-core | 🟢 In Development |
| spz-identity | 🟢 In Development |
| spz-vehicles | 🟢 In Development |
| spz-hud | 🟡 Testing |
| spz-races | 🔵 Designing |
| spz-progression | ⚪ Planned |
| spz-weather | ⚪ Planned |
| spz-admin | ⚪ Planned |
| spz-menu | ⚪ Planned |
| spz-docs | ⚪ Planned |

---

## 🤝 Contributing

We welcome contributions of any kind:
1. Read the [Contributing Guide](.github/CONTRIBUTING.md).
2. Check the [Project Board](https://github.com/orgs/SPiceZ-Core/projects/1) for open tasks.
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

**[Docs](https://github.com/SPiceZ-Core/spz-docs) · [Discord](https://discord.gg/) · [Project Board](https://github.com/orgs/SPiceZ-Core/projects/1) · [Contributing](.github/CONTRIBUTING.md)**

</div>
