# Productory Vault — Design Brainstorm

> Status: **In Progress — Identifying Blindspots**
> Started: 2026-03-01

---

## Vision

Design `/Documents/productory` as an Obsidian vault that:
- Serves both personal and work use cases
- Scales by cloning a workspace template
- Fully leverages Claude Code context engineering (agents, custom commands, skills)

---

## Decisions Log

| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| D1 | Numbered folders: `XX.YY` format (e.g., `01.01`) | Consistent ordering, multi-level hierarchy | 2026-03-01 |
| D2 | Single clonable workspace template | Scale by duplicating, one employer currently | 2026-03-01 |
| D3 | CLAUDE.md at vault root; .claude/ for commands/skills referencing `_system/` | Default Claude Code convention + centralized config | 2026-03-01 |
| D4 | Global Claude config, adapts per workspace context | Avoid duplication, context-aware behavior | 2026-03-01 |
| D5 | Reusable templates live in `_system/` | Single source of truth | 2026-03-01 |
| D6 | `/set-up-vault` command for guided initialization | Onboarding UX for new workspaces | 2026-03-01 |
| D7 | Note-taking framework: suggest Classical/Zettelkasten during setup | User chooses; CLAUDE.md references shared-space for discovery | 2026-03-01 |
| D8 | Simplified PARA (choice during `/set-up-vault`) | Reduce overhead; user picks depth | 2026-03-01 |
| D9 | Journal: ad-hoc, date-based naming | Not weekly-bound, lower friction | 2026-03-01 |
| D10 | Blog target: Substack | Affects content workflow/templates | 2026-03-01 |
| D11 | OKR: single file per year, quarterly/monthly breakdown | Less file sprawl, single source of truth | 2026-03-01 |
| D12 | 1Thing: 1 file per week | Clean separation, easy to review | 2026-03-01 |
| D13 | Meetings: dynamic, custom tags/fields, linked to projects & weekly | Flexible; no rigid folder-per-type | 2026-03-01 |
| D14 | Lightweight PM with PIC (Person In Charge) | Not full kanban; notes + ownership | 2026-03-01 |
| D15 | Obsidian plugins: compatible but not actively used now | Future-proof without dependency | 2026-03-01 |
| D16 | YAML frontmatter on all notes | Enables future querying, structured metadata | 2026-03-01 |
| D17 | kebab-case naming convention | Consistency across vault | 2026-03-01 |
| D18 | Gap-based numbering: `0X` infra, `1X` personal, `2X` work | Tens-digit = category prefix; avoids mixing infra and workspace folders; new workspaces (3X, 4X…) slot in without renumbering | 2026-03-02 |
| D19 | Remove `/create-meeting`; use `/capture` for meetings | Redundant — `/capture` already routes meeting notes with the right template | 2026-03-02 |
| D20 | `/migrate-notes` command for importing existing notes | Analyze source, build mapping plan, execute with user approval; never deletes originals | 2026-03-02 |
| D21 | `profile.md` in `00-system/00.03-preferences/` | Gives Claude persistent user context for personalized interactions | 2026-03-02 |
| D22 | `_active-context.md` per workspace, Claude-maintained | Working memory across sessions; loaded on agent activation, not every interaction | 2026-03-02 |

---

## Confirmed Structure

```
productory/
├── CLAUDE.md                          # Root context for Claude Code
├── .claude/                           # Claude commands/skills (default location)
│   └── commands/                      # Slash commands referencing _system/
├── .obsidian/                         # Obsidian config (auto-generated)
│
├── 00-system/                         # Configs, templates, agent defs, preferences
│   ├── 00.01-templates/              # Reusable templates (meetings, projects, OKR, journal, etc.)
│   ├── 00.02-agents/                 # Agent definitions (chief-of-staff, decision-advisor, etc.)
│   ├── 00.03-preferences/           # User preferences, vault settings
│   └── 00.04-workspace-template/    # The clonable template
│
├── 01-shared-space/                   # Cross-workspace knowledge
│   ├── 01.01-insights/
│   ├── 01.02-books/
│   ├── 01.03-reads/
│   └── 01.04-resources/
│
├── 10-personal/                       # Personal workspace (simplified PARA)
│   ├── 10.01-projects/
│   ├── 10.02-areas/
│   ├── 10.03-resources/
│   ├── 10.04-archive/
│   ├── 10.05-journal/               # Ad-hoc, date-based entries
│   └── 10.06-blog/                  # Substack content pipeline
│
├── 20-work/                           # Work workspace
│   ├── 20.01-okr/                   # Yearly OKR file with Q/M breakdown
│   ├── 20.02-weekly/                # 1Thing per week + week plans/reviews
│   ├── 20.03-meetings/              # Dynamic, tagged, linked
│   ├── 20.04-projects/             # Lightweight PM with PIC
│   └── 20.05-archive/
│
└── _init-brainstorm.md               # This file (remove after setup)
```

---

## Claude Code Integration

### Agents (in `00-system/00.02-agents/`)
**Work agents:**
- Chief of Staff — orchestrates priorities, surfaces blockers, weekly prep
- Decision Advisor — structured decision frameworks, pros/cons, second opinions
- Original Thinker — challenges assumptions, reframes problems, creative angles

**Personal agents:**
- PARA Guide — helps classify, review, and maintain PARA structure
- Content Writer — Substack drafts, editing, content calendar
- Project-specific agents (created per side project)

### Slash Commands (in `.claude/commands/`)
**Setup:**
- `/set-up-vault` — guided vault initialization (asks about PARA depth, workspaces, preferences)

**Work routines:**
- `/week-planning` — create weekly 1Thing + priorities from OKR
- `/week-reviewing` — review week, capture learnings, update OKR progress
- `/daily-updates` — quick status capture (not a full daily note system)
- `/capture` — quick capture for notes, meeting notes, ideas (auto-routes to right folder)

**Creation:**
- `/create-project` — scaffold a new project from template
- `/create-okr` — initialize or update OKR file
- ~~/create-meeting~~ — removed; `/capture` handles meeting notes via routing rules

### CLAUDE.md Behavior
- References `00-system/` for agent definitions and templates
- Instructs Claude to search `01-shared-space/` for relevant knowledge
- Adapts behavior based on which workspace (personal vs work) the user is working in
- Defines frontmatter conventions and linking standards

---

## Frontmatter Convention (YAML)

```yaml
---
type: meeting | project | okr | weekly | journal | blog-draft | insight | book | note
status: draft | active | completed | archived
created: 2026-03-01
updated: 2026-03-01
tags: []
# Meeting-specific
participants: []
meeting-type: standup | 1on1 | planning | retro | ad-hoc
linked-project: ""
linked-weekly: ""
# Project-specific
pic: ""
priority: high | medium | low
# Blog-specific
substack-status: idea | drafting | review | published
---
```

---

## Blindspot Resolutions

| # | Question | Answer | Date |
|---|----------|--------|------|
| B1 | Git repo? | Git + iCloud hybrid. Needs careful .gitignore for Obsidian cache | 2026-03-01 |
| B2 | Capture workflow | Auto-classify immediately (Claude routes to right folder) | 2026-03-01 |
| B3 | MCP integration | Not now, but design for it. Keep structure compatible | 2026-03-01 |
| B4 | File naming | Date-first: `2026-03-01-topic.md`, `2026-w09-weekly.md` | 2026-03-01 |
| B5 | Cross-linking | Yes, link freely across all workspaces | 2026-03-01 |
| B6 | Archive strategy | Claude-assisted: suggests during /week-reviewing, user confirms | 2026-03-01 |
| B7 | Privacy | No concern, all together in single vault + git | 2026-03-01 |
| B8 | Link format | Wiki-links `[[note-name]]` (Obsidian default) | 2026-03-01 |
