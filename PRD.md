# Mneme World Generator PWA — PRD v1.0
## Product Requirements Document

**Version:** 1.0
**Date:** March 4, 2026
**Status:** Draft — M3 In Progress
**Based On:**
- Mneme World Generator (Justin Aquino / Nicco Salonga)
- Wiki: https://wiki.gi7b.org/index.php/Mneme_World_Generator
- Local knowledge base: `docs/knowledge/` (see `Mneme_World_Generator_Wiki_Sync.md`)
- GI7B Generator UI Standard (reference: CE ShipGen)

---

## 1. EXECUTIVE SUMMARY

### 1.1 Vision Statement
Create a Progressive Web App (PWA) that implements the complete Mneme World Generator procedural system, allowing GMs and players to generate fully detailed star systems, worlds, and economic data on any device. The app follows the **GI7B Generator UI Standard** — the same layout, navigation, and tile system used by CE ShipGen and CE CharacterGen.

### 1.2 Success Criteria
- [ ] Complete star system generation per Mneme World Generator rules
- [ ] Complete world generation (UWP, atmosphere, trade codes, etc.)
- [ ] Export generated systems as JSON, Markdown, and plain text
- [ ] Offline-first PWA functionality
- [ ] Follows GI7B Generator UI Standard (tile system, settings sections, layout toggle)
- [ ] Mobile-responsive design (320px–2560px)
- [ ] All generation tables editable via JSON Tables settings

---

## 2. GI7B GENERATOR UI STANDARD

All GI7B generators share one navigation/layout structure. This app must implement it.

### 2.1 App Navigation Tree

```
Landing Page  (/)
│
├── 🖥️/📱  Layout Toggle  [header — always visible]
│         Desktop: three-column  (Nav 15% | Tiles 55% | Summary 30%)
│         Mobile:  single-column vertical stack
│
├── 🌙/☀️  Theme Toggle   [header — always visible]
│         Night (dark) / Day (light)
│
├── ⚙️ Settings  (/settings)
│   ├── 📄 JSON Tables        (/settings/tables)
│   │      All generation tables — editable, exportable, versionable
│   ├── 🧩 Mechanics Modules  (/settings/mechanics)
│   │      Rule variant toggles (standard / Mneme variant)
│   ├── 🎲 Generation Options (/settings/options)
│   │      Presets: "Random Everything", filter constraints
│   └── 🔧 Other Settings     (/settings/other)
│          Theme defaults, version info, PWA install
│
├── 📚 Library  (/library)
│      All previously generated worlds — search, filter, export
│
└── ✨ Generate Now  (/generate)
       Main generation flow — tile-based, step-by-step
```

### 2.2 Tile System
- **Collapsed** — Summary label only
- **Expanded** — Full tile content
- **Focused** — Full-screen overlay (click tile header to focus)
- **ESC** to exit focus mode

### 2.3 Layout Modes
- **Desktop** — Three-column layout
- **Mobile** — Single-column, collapsible parameters, vertical tile stack

### 2.4 Settings Sections (GI7B Standard)

| Section | Route | Icon | Purpose |
|---------|-------|------|---------|
| JSON Tables | `/settings/tables` | 📄 | Edit all generation tables (canonical + custom) |
| Mechanics Modules | `/settings/mechanics` | 🧩 | Rule variant toggles (standard Mneme / house rules) |
| Generation Options | `/settings/options` | 🎲 | Presets, filter constraints, "Random Everything" |
| Other Settings | `/settings/other` | 🔧 | Theme, layout default, version control, PWA install |

### 2.5 GI7B Generator Suite

| Generator | Repo | UI Role |
|-----------|------|---------|
| CE ShipGen | xunema/ce-shipgen | Canonical UI reference ✅ |
| CE CharacterGen | xunema/cecharactergen | M2 UI alignment in progress |
| Mneme World Gen | xunema/mneme-world-generator-pwa | M7 UI alignment pending |

---

## 3. FUNCTIONAL REQUIREMENTS

### FR-001: Star Generation
**Priority:** Critical — M3
**Source:** Wiki Ch. 4 — Determine Star (see `docs/knowledge/04_determine_star.md`)

Generate primary and companion stars for a system:
- Star type (O/B/A/F/G/K/M)
- Luminosity class
- Companion star probability and orbit
- Star age and evolution stage

**Acceptance:** Output matches wiki tables for all star types.

---

### FR-002: World Generation (UWP)
**Priority:** Critical — M4
**Source:** Wiki Ch. 5–8 (see `docs/knowledge/05_determine_main_world.md`, `06_determine_habitability.md`, `08_determine_inhabitants.md`)

Generate Universal World Profile:
- Size (0–A)
- Atmosphere (0–F)
- Hydrographics (0–A)
- Population (0–C)
- Government (0–F)
- Law Level (0–9)
- Tech Level (0–F)
- Starport type (A–E, X)
- Trade codes (Ag, In, Ri, etc.)

**Acceptance:** UWP string generated correctly, trade codes match population/atmosphere/hydrographics.

---

### FR-003: System Details
**Priority:** High — M5
**Source:** Wiki Ch. 9 + S3 (see `docs/knowledge/09_determine_planetary_system.md`, `S3_logic_spec_260222.md`)

- Gas giants, asteroid belts
- Planetary orbits (inner, habitable, outer zones)
- Moons and satellites
- Travel times (standard and Mneme physics)

**Acceptance:** Orbital distances and travel times match reference tables.

---

### FR-004: Trade & Economy
**Priority:** Medium — M6+
**Source:** Wiki Ch. 10 — Appendix (see `docs/knowledge/10_appendix.md`)

- Trade volume between systems
- Market prices and fluctuations
- Freight and passenger demand
- Economic events

---

### FR-005: Tile-Based Generation UI
**Priority:** Critical — M7 (UI Alignment)

Implement GI7B tile system:
- Each generation step is a tile (Collapsed / Expanded / Focused)
- Desktop: three-column layout
- Mobile: vertical stack
- Layout toggle (Desktop ↔ Mobile) in header
- Theme toggle (Night ↔ Day) in header

---

### FR-006: JSON Tables Editor
**Priority:** High — M7

Settings → JSON Tables:
- View and edit all generation tables
- Dual view: JSON source / Spreadsheet table
- Export individual tables as JSON
- Import custom tables
- Tables In Play — select which table drives each step

---

### FR-007: Mechanics Modules
**Priority:** Medium — M7

Settings → Mechanics Modules:
- Rule variant toggles (standard Mneme / house rules)
- Editable rule definitions

---

### FR-008: Generation Options
**Priority:** Medium — M7

Settings → Generation Options:
- "Random Everything" — instant full system generation
- Filter: lock specific values before generating
- Named presets (e.g., "Habitable World", "Gas Giant System")

---

### FR-009: Library
**Priority:** High — M5
**Ref:** CE ShipGen Library pattern

- Save all generated systems to localStorage / IndexedDB
- Search and filter saved systems
- Export as JSON, Markdown, plain text
- Delete with confirmation
- Auto-save on generation

---

### FR-010: PWA / Offline Support
**Priority:** High

- Service worker for offline use
- "Install App" prompt
- Works on mobile via "Add to Home Screen"
- Auto-update notification

---

## 4. DATA TABLES

All tables come from the Mneme World Generator wiki. Local copies in `docs/knowledge/`.

**Tables required for generation (to be populated during wiki sync):**

| Table | Wiki Chapter | Local Knowledge File | Status |
|-------|-------------|----------------------|--------|
| Star Type Roll | Ch. 4 — Determine Star | `docs/knowledge/04_determine_star.md` | ✅ Synced |
| Luminosity Class | Ch. 4 — Determine Star | `docs/knowledge/04_determine_star.md` | ✅ Synced |
| World Type / Size | Ch. 5 — Determine Main World | `docs/knowledge/05_determine_main_world.md` | ✅ Synced |
| Atmosphere / Hydrographics / Temp | Ch. 6 — Determine Habitability | `docs/knowledge/06_determine_habitability.md` | ✅ Synced |
| World Position (AU) | Ch. 7 — Determine Position | `docs/knowledge/07_determine_position.md` | ✅ Synced |
| Population / Government / Law | Ch. 8 — Determine Inhabitants | `docs/knowledge/08_determine_inhabitants.md` | ✅ Synced |
| Tech Level / Starport / PVS | Ch. 8 — Determine Inhabitants | `docs/knowledge/08_determine_inhabitants.md` | ✅ Synced |
| Gas Giants / Belts / Orbits | Ch. 9 — Determine Planetary System | `docs/knowledge/09_determine_planetary_system.md` | ✅ Synced |
| Orbital Mechanics (Hill stability) | Supplemental S3 — Logic Spec v2.1 | `docs/knowledge/S3_logic_spec_260222.md` | ✅ Synced |
| Economy / TL / Asteroid Types | Ch. 10 — Appendix | `docs/knowledge/10_appendix.md` | ✅ Synced |

> **Note:** Knowledge base is fully synced as of 2026-03-04. All generation rules reference `docs/knowledge/` files — see `Mneme_World_Generator_Wiki_Sync.md` for re-sync instructions. Tables must be extracted from these files into JSON in `data/` before implementation.

---

## 5. MILESTONES

| Milestone | Scope | Status |
|-----------|-------|--------|
| **M1: Preparation** | Project setup, tech stack, initial structure | ✅ Complete |
| **M2: UI Stage** | Layout, routing, theme toggle, landing page, shadcn/ui | ✅ Complete |
| **M3: Star Generation** | Star type, luminosity, companion stars, export | 🔄 In Progress |
| **M3.1: Star Generation Phase** | Generation rules per wiki Chapter 2 | 🔄 In Progress |
| **M3.2: Persistence** | Export only (JSON) | 🔄 In Progress |
| **M4: Primary World Generation** | Full UWP, trade codes, starport, export | ⏳ Pending |
| **M5: Save/Load & Library** | IndexedDB, search, filter, import/export | ⏳ Pending |
| **M6: Disks & Full System** | Gas giants, belts, planetary orbits, moons | ⏳ Pending |
| **M7: UI Alignment** | Align to GI7B UI Standard — tile system, settings sections, layout/theme toggle | ⏳ Pending |

---

## 6. TECHNICAL ARCHITECTURE

**Stack:** React 19 + TypeScript + Vite 7 + Tailwind CSS v4 + shadcn/ui + React Router v7

**Routing (target — GI7B Standard):**
```
/                  Startup screen
/generate          Main generation flow
/library           Saved worlds
/settings          → redirects to /settings/tables
/settings/tables   JSON Tables editor
/settings/mechanics  Rule variant toggles
/settings/options  Generation presets
/settings/other    Misc settings
```

**Data Flow:**
1. User lands on `/` — sees Generate / Library / Settings
2. Generate → tiles guide through star → world → system steps
3. Each step reads from active JSON table (via Tables In Play)
4. Result auto-saved to Library (IndexedDB)
5. Settings → swap tables, toggle mechanics

**Knowledge Base:** All rules from `docs/knowledge/` (synced from wiki via `Mneme_World_Generator_Wiki_Sync.md`).
