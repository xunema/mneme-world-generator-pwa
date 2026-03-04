# Mneme World Generator — Wiki Sync

**Canonical Source:** https://wiki.gi7b.org/index.php/Mneme_World_Generator
**Last Synced:** _(update this date each sync)_
**Status:** ⚠️ Needs initial sync — run instructions below

---

## Purpose

This file instructs developers and AI assistants to keep the project's knowledge base in sync with the live Mneme World Generator wiki. The wiki is the authoritative source for rules, tables, and generation procedures. Local markdown copies in `docs/` are used as the in-repo reference for AI-assisted development.

---

## Wiki Structure

The Mneme World Generator wiki is organized into the following chapters. Each chapter should have a corresponding local markdown file in `docs/knowledge/`:

| Chapter | Wiki URL | Local File | Synced |
|---------|----------|------------|--------|
| Main Index | https://wiki.gi7b.org/index.php/Mneme_World_Generator | `docs/knowledge/00_index.md` | ⚠️ Pending |
| Chapter 1: Introduction | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Chapter_1 | `docs/knowledge/01_introduction.md` | ⚠️ Pending |
| Chapter 2: Star Generation | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Chapter_2 | `docs/knowledge/02_star_generation.md` | ⚠️ Pending |
| Chapter 3: World Generation | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Chapter_3 | `docs/knowledge/03_world_generation.md` | ⚠️ Pending |
| Chapter 4: System Details | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Chapter_4 | `docs/knowledge/04_system_details.md` | ⚠️ Pending |
| Chapter 5: Trade & Economy | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Chapter_5 | `docs/knowledge/05_trade_economy.md` | ⚠️ Pending |
| Change Notes | https://wiki.gi7b.org/index.php/Mneme_World_Generator_Change_Notes | `docs/knowledge/CHANGE_NOTES.md` | ⚠️ Pending |

> **Note:** Chapter URLs above are the expected pattern. Verify and correct against the actual wiki. Add any additional chapters found during sync.

---

## Sync Instructions

### Manual Sync (Human)

1. Visit each URL in the table above
2. Copy the page content (use the wiki's "Edit" view to get clean wikitext, or copy rendered text)
3. Convert to markdown and save in the corresponding `docs/knowledge/` file
4. Update the **Last Synced** date at the top of this file
5. Update the **Synced** column in the table above (✅ Done / ⚠️ Pending / 🔄 Outdated)
6. Commit with message: `docs: sync wiki — [chapter name] — [date]`

### AI-Assisted Sync

When asking an AI assistant to sync, provide this prompt:

```
Please sync the Mneme World Generator wiki into the local docs/knowledge/ folder.

For each chapter in WIKI_SYNC.md:
1. Fetch the wiki URL using WebFetch
2. Convert content to clean markdown
3. Save to the corresponding local file
4. Update the sync status and date in WIKI_SYNC.md

Start with the main index: https://wiki.gi7b.org/index.php/Mneme_World_Generator
```

### Checking for Changes

The wiki does not have an RSS feed. To check for updates:
1. Visit the wiki's Recent Changes: https://wiki.gi7b.org/index.php/Special:RecentChanges
2. Filter by "Mneme World Generator" pages
3. Compare against the **Last Synced** date in this file
4. Re-sync any changed chapters

---

## Change Notes Format

When the wiki is updated, record changes here:

```
### [DATE] — [Chapter]
- [Description of change]
- [Impact on implementation]
- Files updated: [list]
```

### Change Log

_(empty — populate on first sync)_

---

## Local Knowledge Base Structure

```
docs/
└── knowledge/
    ├── 00_index.md          # Wiki main index
    ├── 01_introduction.md   # Chapter 1
    ├── 02_star_generation.md
    ├── 03_world_generation.md
    ├── 04_system_details.md
    ├── 05_trade_economy.md
    └── CHANGE_NOTES.md      # Tracked changes from wiki
```

---

## For AI Assistants

When working on this project, **always check this file first** to understand the authoritative rules source. If a local `docs/knowledge/` file exists, use it as the reference. If it doesn't exist or is marked ⚠️ Pending, note that the knowledge base needs syncing before implementation can proceed.

**Never implement generation rules from memory.** Always reference the local knowledge base files or re-sync from the wiki.
