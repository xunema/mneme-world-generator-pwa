# Mneme World Generator PWA — Project Notes

**Project:** Mneme World Generator PWA
**Status:** M3 In Progress — Star Generation
**Deployed URL:** _(pending deployment setup)_
**Last Updated:** March 4, 2026

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [PAD Structure](#2-pad-structure)
3. [GI7B Generator UI Standard](#3-gi7b-generator-ui-standard)
4. [Tech Stack Decisions](#4-tech-stack-decisions)
5. [Milestone History](#5-milestone-history)
6. [Problems Faced & Solutions](#6-problems-faced--solutions)
7. [Architecture Notes](#7-architecture-notes)
8. [Next Steps](#8-next-steps)

---

## 1. Project Overview

**Goal:** Progressive Web App implementation of the Mneme World Generator rulebook (Justin Aquino / Nicco Salonga). Automates the procedural world generation system including star generation, world classification, system details, and trade economics.

**Source Material:** https://wiki.gi7b.org/index.php/Mneme_World_Generator — see `Mneme_World_Generator_Wiki_Sync.md` for sync instructions.

**Original Author:** Steven Tiu
**Project Sponsor:** Justin Cesar Aquino
**Ecosystem:** Part of the GI7B Generator Suite alongside CE ShipGen and CE CharacterGen

---

## 2. PAD Structure

This project follows **Procedural-Agentic Development (PAD)** — a documentation-first approach where all rules, decisions, and context are written down so that AI assistants and human developers can onboard instantly.

```
mneme-world-generator-pwa/
├── README.md             # Milestones, status, docs state — START HERE
├── PRD.md                # Product Requirements Document (functional specs)
├── PROJECT_NOTES.md      # This file — dev log, decisions, problems
├── Mneme_World_Generator_Wiki_Sync.md          # Instructions for syncing with the wiki knowledge base
├── docs/
│   └── knowledge/        # Local copies of wiki chapters (sync from Mneme_World_Generator_Wiki_Sync.md)
└── src/                  # Application code
```

**Rule:** If it's not written down in one of these files, it doesn't exist as a project requirement.

---

## 3. GI7B Generator UI Standard

All GI7B generators (ShipGen, CharacterGen, WorldGen) share the same UI structure. **CE ShipGen is the canonical reference implementation.** This project must follow the same pattern.

### App Navigation Tree

```
Landing Page / Main Page
│
├── 🖥️/📱  Layout Toggle  (header — persistent)
│         Desktop: three-column (Nav | Tiles | Summary)
│         Mobile:  single-column vertical stack
│
├── 🌙/☀️  Theme Toggle   (header — persistent)
│         Night (dark) / Day (light)
│
├── ⚙️ Settings  (/settings/*)
│   ├── 📄 JSON Tables        (/settings/tables)
│   │      Editable, exportable, renamable/versionable per generation step
│   ├── 🧩 Mechanics Modules  (/settings/mechanics)
│   │      Core rules and rule-variant toggles (e.g. CE RAW vs Mneme Variant)
│   ├── 🎲 Generation Options (/settings/options)
│   │      Presets: "Random Everything", filter constraints
│   └── 🔧 Other Settings     (/settings/other)
│          Theme defaults, layout defaults, version info
│
├── 📚 Library  (/library)
│      Vault of all previously generated worlds — search, filter, export
│
└── ✨ Generate Now  (/generate)
       Main generation flow — tile-based, step-by-step
```

### Tile System

- **Collapsed** — Summary only
- **Expanded** — Full content
- **Focused** — Full-screen overlay (click tile header)
- **ESC** to exit focus mode

### Layout Modes

- **Desktop** — Three columns: Parameters (15%) | Tiles (55%) | Summary/Log (30%)
- **Mobile** — Single column, vertical stack, collapsible parameters panel

### Settings Sections (GI7B Standard)

| Section | Route | Icon | Mneme World Gen Contents |
|---------|-------|------|--------------------------|
| JSON Tables | `/settings/tables` | 📄 | Star tables, world tables, system tables — all editable |
| Mechanics Modules | `/settings/mechanics` | 🧩 | Standard Mneme / house-rule variant toggles |
| Generation Options | `/settings/options` | 🎲 | Presets ("Habitable World", "Random System"), filter locks |
| Other Settings | `/settings/other` | 🔧 | Theme, layout default, version control, PWA install |

### GI7B Generator Suite

| Generator | Repo | UI Role |
|-----------|------|---------|
| CE ShipGen | xunema/ce-shipgen | Canonical UI reference ✅ |
| CE CharacterGen | xunema/cecharactergen | M2 UI alignment in progress |
| Mneme World Gen | xunema/mneme-world-generator-pwa | M7 UI alignment pending |

### Delta: Current vs Target

| Feature | Current State | Target (GI7B Standard) |
|---------|---------------|------------------------|
| Theme Toggle | ✅ Implemented (M2) | 🌙/☀️ in header |
| Layout Toggle | ✅ Implemented (M2) | 🖥️/📱 in header |
| Settings routes | `/my-worlds`, `/create-new` (non-standard) | `/settings/tables`, `/settings/mechanics`, `/settings/options`, `/settings/other` |
| Route: generate | `/create-new/custom` | `/generate` |
| Route: library | `/my-worlds` | `/library` |
| Tile system | shadcn/ui components | GI7B tile system (Collapsed/Expanded/Focused) |

> **UI Alignment Milestone:** Full GI7B route and tile alignment is M7. Settings sections should use standard routes from initial implementation.

### Reference Implementation

See CE ShipGen (`github.com/xunema/ce-shipgen`) — all UI patterns, component names, and routing conventions should match.

---

## 4. Tech Stack Decisions

### Why shadcn/ui + Radix?
- Decision made before GI7B UI Standard was formalized
- CE ShipGen uses plain Tailwind + Lucide; this project uses shadcn/ui components
- **Impact:** UI will look slightly different but follow the same navigation/layout structure
- **Migration path:** Can be aligned to ce-shipgen tile system in a future milestone

### Why pnpm?
- Faster installs, disk-efficient
- Node 22 LTS required (Vite 7 requirement)

### Current vs Target Stack

| Item | Current | CE ShipGen (target pattern) |
|------|---------|-----------------------------|
| React | 19 | 19 ✅ |
| TypeScript | ✅ | ✅ |
| Vite | 7 | 7 ✅ |
| Tailwind | v4 | v3/v4 |
| UI Components | shadcn/ui | Custom tiles |
| State | React Context | Zustand |
| Routing | React Router v7 | React Router ✅ |

---

## 5. Milestone History

| Milestone | Scope | Status | Notes |
|-----------|-------|--------|-------|
| M1: Preparation | Project setup, tech stack, data extraction | ✅ Done | Steven Tiu |
| M2: UI Stage | Layout, routing, theme, landing page | ✅ Done | Steven Tiu |
| M3: Star Generation | Star type generation, primary star rules, persistence | 🔄 In Progress | — |
| M3.1: Star Generation Phase | Star generation rules implementation | 🔄 In Progress | Oct 24–30 |
| M3.2: Persistence | Export only (no save/load yet) | 🔄 In Progress | Oct 17–23 |
| M4: Primary World | World generation and export | ⏳ Pending | Oct 30–Nov 6 |
| M5: Save/Load | Import/export full systems | ⏳ Pending | Nov 7–13 |
| M6: Disks & Planets | Full planetary system generation | ⏳ Pending | Nov 14–20 |
| M7: UI Alignment | Align to GI7B UI Standard (tile system, settings sections) | ⏳ Pending | After M6 |

---

## 6. Problems Faced & Solutions

_(To be populated during development)_

### Template

```
### [Date] — [Problem Title]
**Problem:** Description
**Root Cause:** Why it happened
**Solution:** How it was fixed
**Lesson:** What to remember
```

---

## 7. Architecture Notes

### Current Route Structure
```
/                  — Home / Landing page
/my-worlds         — Library (saved worlds)
/create-new        — World creation mode selection
/create-new/custom — Custom world creation wizard
```

### Target Route Structure (GI7B Standard)
```
/                  — Startup screen
/generate          — Main generation flow
/library           — All generated worlds
/settings          — Settings (redirects to /settings/tables)
/settings/tables   — JSON Tables
/settings/mechanics — Mechanics Modules
/settings/options  — Generation Options
/settings/other    — Other settings
```

### Knowledge Base
All generation rules come from the wiki — see `Mneme_World_Generator_Wiki_Sync.md`. Local copies in `docs/knowledge/` are the in-repo reference. **Do not hardcode generation logic without a corresponding rule in the knowledge base.**

---

## 8. Next Steps

1. **Sync wiki** — Run Mneme_World_Generator_Wiki_Sync.md instructions to populate `docs/knowledge/`
2. **Complete M3.1** — Star generation rules per wiki Chapter 2
3. **Align routes** — Move toward GI7B Standard route structure
4. **Add settings sections** — JSON Tables, Mechanics Modules (M7)
