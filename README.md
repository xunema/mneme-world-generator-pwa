# Mneme World Generator PWA

**A Progressive Web App for procedural world and star system generation using the Mneme World Generator rules.**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Status](https://img.shields.io/badge/Status-M3%20In%20Progress-yellow)](https://github.com/xunema/mneme-world-generator-pwa)

**Source Material:** [Mneme World Generator — DriveThruRPG](https://www.drivethrurpg.com/en/product/403824/mneme-world-generator) by Justin Aquino and Nicco Salonga
**Wiki (authoritative rules):** https://wiki.gi7b.org/index.php/Mneme_World_Generator
**Spreadsheet Version:** [Google Sheet](https://docs.google.com/spreadsheets/d/1YiFA-THVnSGyMltVcDvS9nGlF4k8RFrjg89ZGNSw7ZM/edit?gid=1542365405#gid=1542365405)

---

## 📋 Documentation State

| Document | Purpose | Status |
|----------|---------|--------|
| [PRD.md](./PRD.md) | Product Requirements Document — functional specs, milestones, UI standard | ✅ Current |
| [PROJECT_NOTES.md](./PROJECT_NOTES.md) | Dev log, architecture decisions, GI7B UI Standard, problems & solutions | ✅ Current |
| [Mneme_World_Generator_Wiki_Sync.md](./Mneme_World_Generator_Wiki_Sync.md) | Knowledge base sync instructions — wiki chapters, change notes, sync log | ✅ Synced 2026-03-04 |
| `docs/knowledge/` | Local copies of all wiki chapters (Ch 0–10 + 3 supplemental) | ✅ Synced 2026-03-04 |
| [INSTRUCTIONS.md](./INSTRUCTIONS.md) | Developer setup guide — tech stack, component patterns, TypeScript conventions | ✅ Reference |

> **Knowledge Base:** All generation rules come from the Mneme World Generator wiki. Run the sync instructions in `Mneme_World_Generator_Wiki_Sync.md` before implementing generation logic. Never hardcode rules without a corresponding wiki reference.

---

## 🛣️ Milestones

| Milestone | Scope | Status |
|-----------|-------|--------|
| **M1: Preparation** | Project setup, tech stack, initial structure | ✅ Complete |
| **M2: UI Stage** | Layout, routing, theme toggle, landing page, shadcn/ui components | ✅ Complete |
| **M3: Star Generation** | Star type, luminosity, companion stars, export | 🔄 In Progress |
| **M3.1: Star Generation Phase** | Generation rules per wiki Chapter 2 | 🔄 In Progress |
| **M3.2: Persistence** | Export only (JSON) | 🔄 In Progress |
| **M4: Primary World Generation** | Full UWP, trade codes, starport, export | ⏳ Pending |
| **M5: Save/Load & Library** | IndexedDB, search, filter, import/export | ⏳ Pending |
| **M6: Disks & Full System** | Gas giants, belts, planetary orbits, moons | ⏳ Pending |
| **M7: UI Alignment** | Align to [GI7B Generator UI Standard](https://github.com/xunema/ce-shipgen/blob/main/PROJECT_NOTES.md#gi7b-generator-ui-standard) — tile system, settings sections, layout/theme toggle | ⏳ Pending |

---

## 🎯 GI7B Generator Suite

This app is part of the GI7B Generator Suite. All three generators share the same navigation structure and UI standard (see M7):

| Generator | Repo | Status |
|-----------|------|--------|
| **CE ShipGen** _(canonical UI reference)_ | [xunema/ce-shipgen](https://github.com/xunema/ce-shipgen) | ✅ M2 Complete |
| **CE CharacterGen** | [xunema/cecharactergen](https://github.com/xunema/cecharactergen) | 🔄 M2 In Progress |
| **Mneme World Gen** _(this repo)_ | [xunema/mneme-world-generator-pwa](https://github.com/xunema/mneme-world-generator-pwa) | 🔄 M3 In Progress |

---

## 🧭 GI7B UI Standard (Navigation Tree)

```
Landing Page (/)
│
├── 🌙/☀️ Theme Toggle      [header — always visible]
├── 🖥️/📱 Layout Toggle     [header — always visible]
│
├── ✨ Generate Now (/generate)
│   └── Star → World → System generation — tile-based
│
├── 📚 Library (/library)
│   └── Saved systems — search, filter, export
│
└── ⚙️ Settings (/settings)
    ├── 📄 JSON Tables        (/settings/tables)
    ├── 🧩 Mechanics Modules  (/settings/mechanics)
    ├── 🎲 Generation Options (/settings/options)
    └── 🔧 Other Settings     (/settings/other)
```

### Tile System
| State | Description |
|-------|-------------|
| **Collapsed** | Summary only |
| **Expanded** | Full content |
| **Focused** | Full-screen overlay — ESC to exit |

---

## 🚀 Tech Stack

- **React 19** + TypeScript + Vite 7
- **shadcn/ui** (Radix UI) + Tailwind CSS v4
- **React Router DOM v7**
- **Node.js 22 LTS** required (Vite 7 dependency)
- **pnpm** (recommended) or npm

---

## 🛠️ Development

### Prerequisites

```bash
# Install Node 22 via nvm (Linux/macOS)
nvm install 22 && nvm use 22
corepack enable && corepack prepare pnpm@latest --activate
```

### Setup

```bash
pnpm install
pnpm dev        # http://localhost:5173
```

### Build

```bash
pnpm build
pnpm preview    # preview production build
```

### Mobile Testing

```bash
pnpm dev --host   # exposes LAN IP — open http://<LAN-IP>:5173 on phone
```

---

## 🧭 Project Structure

```
mneme-world-generator-pwa/
├── README.md                              ← START HERE — milestones, docs state
├── PRD.md                                 ← Product requirements & UI spec
├── PROJECT_NOTES.md                       ← Dev log, architecture, GI7B UI Standard
├── Mneme_World_Generator_Wiki_Sync.md     ← Wiki sync instructions & change log
├── INSTRUCTIONS.md                        ← Developer/component guide
├── docs/
│   └── knowledge/                         ← Local wiki chapters (sync first!)
│       ├── 00_index.md
│       ├── 04_determine_star.md
│       ├── 05_determine_main_world.md
│       ├── 06_determine_habitability.md
│       ├── 07_determine_position.md
│       ├── 08_determine_inhabitants.md
│       ├── 09_determine_planetary_system.md
│       ├── S3_logic_spec_260222.md        ← canonical orbital mechanics (v2.1)
│       └── ...
├── data/                                  ← JSON generation tables (extracted from wiki)
└── src/
    ├── components/
    │   ├── layout/   ← MainLayout, CenteredLayout
    │   ├── shared/   ← Header, Footer
    │   └── ui/       ← shadcn/ui components
    ├── pages/        ← Route-level page components
    ├── lib/          ← Utilities (cn, etc.)
    └── routes.tsx
```

---

## 📚 Troubleshooting

| Issue | Fix |
|-------|-----|
| Vite not found | `pnpm install` |
| `crypto.hash` error | Upgrade Node to 22, reinstall |
| LAN not reachable | Check firewall / subnet |
| Generation rules unclear | Run `Mneme_World_Generator_Wiki_Sync.md` to sync knowledge base |

---

## 👤 Credits

**Steven Tiu** — Original Author
**Justin Cesar Aquino** — Project Sponsor, Rules Author

---

## 📝 License

GPL v3 — See [LICENSE](./LICENSE)

---

## 🧾 Spreadsheet Version

The Google Sheets version has a built-in JavaScript roller and encoder:

1. Go to *File → Make a Copy*
2. Click *Generate System* — approve script permissions on first run
3. Right-click the *World Sheet* tab → *Copy to → New Spreadsheet* to save results

> [Open Spreadsheet](https://docs.google.com/spreadsheets/d/1YiFA-THVnSGyMltVcDvS9nGlF4k8RFrjg89ZGNSw7ZM/edit?gid=1542365405#gid=1542365405)
