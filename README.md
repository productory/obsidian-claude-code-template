# Productory — A Claude Code-Native Obsidian Vault

An Obsidian vault template engineered for AI-assisted productivity. It merges personal knowledge management (PARA), work planning (OKR + weekly rhythms), and Claude Code context engineering into a single system.

This isn't a typical Obsidian starter vault. It's designed so that Claude Code understands your vault's structure, remembers context across sessions, and operates as specialized agents depending on what you're doing.

---

## 1. What's Inside

### 1.1 Vault Structure

```
00-system/          Infrastructure — templates, agents, preferences, workspace blueprint
01-shared-space/    Cross-workspace knowledge base — insights, books, reads, resources
10-personal/        Personal workspace — PARA, journal, blog
20-work/            Work workspace — OKR, weekly plans, meetings, projects
```

Folders use numbered prefixes (`XX.YY-name`) for consistent ordering. The tens digit defines the category: `00` = system, `01` = shared, `10` = personal, `20` = work. New workspaces slot in at `1x`, `2x`, etc. without renumbering.

### 1.2 Agent Personas

Six AI personas activate based on context — you don't invoke them manually, they engage when relevant.

| Agent                | When It Activates                              | What It Does                                                                   |
| -------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------ |
| **Chief of Staff**   | Working in `20-work/`, weekly planning/review  | Orchestrates priorities, surfaces blockers, manages weekly rhythms             |
| **Decision Advisor** | Asking for decision help or trade-off analysis | Applies frameworks (DACI, pre-mortem, weighted scoring), structures pros/cons  |
| **Original Thinker** | Brainstorming or challenging assumptions       | Inverts problems, draws cross-domain analogies, removes artificial constraints |
| **PARA Guide**       | Working in `10-personal/`, classifying notes   | Guides PARA organization, helps with periodic reviews                          |
| **Content Writer**   | Working in `10-personal/10.06-blog/`           | Writing partner for Substack — drafting, editing, voice calibration            |
| **Vault Builder**    | Working in `00-system/`, extending the vault   | Scaffolds new agents, commands, templates, workspaces; keeps registries in sync |

Agent definitions live in `00-system/00.02-agents/`. Each specifies a role, capabilities, and constraints.

### 1.3 Slash Commands

Nine commands drive the core workflows:

| Command               | Purpose                                                                            |
| --------------------- | ---------------------------------------------------------------------------------- |
| `/pdt:set-up-vault`   | Interactive setup wizard — configure PARA depth, preferences, profile              |
| `/pdt:week-planning`  | Create a weekly plan with 1Thing focus and priorities linked to OKRs               |
| `/pdt:week-reviewing` | Review the week, capture learnings, update OKR progress, suggest archiving         |
| `/pdt:daily-updates`  | Quick daily status (done/blocked/next) appended to current weekly file             |
| `/pdt:capture`        | Auto-classify any content and route it to the right folder with the right template |
| `/pdt:create-project` | Scaffold a new project linked to OKRs                                              |
| `/pdt:create-okr`     | Initialize or update yearly OKR file                                               |
| `/pdt:migrate-notes`  | Import existing notes from another location with a mapping plan                    |
| `/pdt:vault-build`    | Create or modify agents, commands, templates, workspaces, and vault config         |

### 1.4 Templates

Nine templates in `00-system/00.01-templates/` cover every note type:

`tpl-meeting` · `tpl-project` · `tpl-okr-yearly` · `tpl-weekly` · `tpl-journal` · `tpl-blog-draft` · `tpl-capture` · `tpl-insight` · `tpl-book`

Each template defines YAML frontmatter fields and content sections. When you use `/pdt:capture` or creation commands, the right template is applied automatically.

### 1.5 Active Context System

Each workspace has an `_active-context.md` file that serves as Claude's working memory across sessions. It tracks current priorities, recent decisions, open blockers, and active projects.

Claude reads it when entering a workspace and updates it at the end of meaningful interactions. During weekly reviews, old entries are pruned. This means Claude picks up where you left off without you having to re-explain context.

### 1.6 Shared Knowledge Base

`01-shared-space/` is a cross-workspace knowledge layer:

- **Insights** — key takeaways from any source
- **Books** — reading notes with application ideas
- **Reads** — articles and papers
- **Resources** — frameworks, tools, references

When Claude answers questions or helps create content, it searches here first. This means your accumulated knowledge actually gets reused.

---

## 2. Principles

This vault is built on the idea that an Obsidian vault can be more than a note store — it can be a **context-engineered environment** where an AI assistant operates with deep understanding of your system.

### 2.1 Context Engineering, Not Prompting

`CLAUDE.md` at the root isn't a prompt — it's a behavior specification. It defines frontmatter schemas, routing rules, linking conventions, workspace detection, and agent activation conditions. Claude doesn't just follow instructions; it understands the system's architecture.

### 2.2 Convention-Driven Navigation

Numbered folders (`XX.YY`), kebab-case filenames, date prefixes (`YYYY-MM-DD`), and wiki-links (`[[note-name]]`) create predictable patterns. Claude can navigate, create, and link notes reliably because the conventions are explicit and consistent.

### 2.3 Agents Over Modes

Instead of manually switching Claude's behavior, agent personas activate based on where you're working. Enter `20-work/` and Chief of Staff thinking kicks in. Start editing a blog draft and the Content Writer engages. The vault's folder structure _is_ the context switch.

### 2.4 Structured Metadata Everywhere

Every note has YAML frontmatter with `type`, `status`, `created`, `updated`, and `tags` at minimum. Type-specific fields (like `participants` for meetings or `pic` for projects) enable Claude to reason about relationships, filter by status, and maintain consistency.

### 2.5 Session Continuity Without Replay

`_active-context.md` files give Claude persistent working memory. Instead of re-reading entire workspaces each session, Claude loads a compact summary of what matters now — priorities, blockers, recent decisions, project states. This is updated incrementally, not rebuilt.

### 2.6 Workflows as Commands

Slash commands aren't shortcuts — they're multi-step procedures. `/pdt:week-planning` reads the active context, checks last week's carryovers, creates a new weekly file, asks for your 1Thing, links to OKRs, and updates the active context. The vault's structure enables these workflows to be reliable and repeatable.

### 2.7 Knowledge Compounds

The shared knowledge base (`01-shared-space/`) is designed so insights from reading, conversations, and experience accumulate and get surfaced when relevant. Cross-workspace linking means a work project can reference a book note, and a blog draft can build on captured insights.

### 2.8 Lightweight by Design

No heavy project management. Projects track with just an objective, tasks, a PIC (Person In Charge), and a priority level. Journals are ad-hoc, not daily obligations. Meetings are dynamic notes, not rigid structures. The system supports without imposing.

---

## 3. How to Use

### 3.1 Getting Started

1. **Download** this vault — click **Code → Download ZIP** on GitHub and unzip it
2. **Open it in Obsidian** as a vault
3. **Run `/pdt:set-up-vault`** in Claude Code — it walks you through configuring PARA depth, note-taking style, and your profile
4. **Fill in your profile** at `00-system/00.03-preferences/profile.md` — this personalizes Claude's tone and recommendations
5. **Create your first OKR** with `/pdt:create-okr` to establish goals

### 3.2 Weekly Rhythm

| When    | What                                          | Command               |
| ------- | --------------------------------------------- | --------------------- |
| Monday  | Plan the week — set 1Thing, top priorities    | `/pdt:week-planning`  |
| Daily   | Quick status update — done, blocked, next     | `/pdt:daily-updates`  |
| Anytime | Capture a meeting, idea, insight, or note     | `/pdt:capture`        |
| Friday  | Review the week, log learnings, prep for next | `/pdt:week-reviewing` |

### 3.3 Capturing Notes

Use `/pdt:capture` for everything. Describe what you have and Claude will:

- Classify the content type (meeting, insight, project idea, blog draft, etc.)
- Pick the right template
- Route it to the correct folder
- Name it with the proper date prefix and kebab-case convention
- Link it to relevant projects, weeklies, or OKRs

### 3.4 Building Knowledge

As you capture insights, book notes, and reads into `01-shared-space/`, Claude starts referencing them in future interactions. When you plan a week, write a blog post, or make a decision, relevant prior knowledge gets surfaced automatically.

### 3.5 Scaling to New Workspaces

The workspace template at `00-system/00.04-workspace-template/` is a clonable blueprint. To add a new workspace (e.g., a side project or second job):

1. Copy the workspace template folder
2. Rename with a new prefix (e.g., `30-side-project/`)
3. Rename subfolders accordingly (`30.01-okr/`, `30.02-weekly/`, etc.)
4. Add the workspace to `CLAUDE.md`

The system scales horizontally without restructuring.

### 3.6 Agent Activation

To activate agents, You don't need to name the agent. Claude detects the context — which folder you're in, what kind of question you're asking — and activates the matching persona. If the context is ambiguous, Claude asks which workspace applies.

Try these prompts in Claude Code while working in the vault:

| Agent                | Test Prompt                                                                              | Expected Behavior                                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Chief of Staff**   | Run `/pdt:week-planning`, or ask "what are my priorities this week?" while in `20-work/` | Reads `20-work/_active-context.md`, surfaces blockers, references OKRs, uses professional tone                 |
| **Decision Advisor** | "Help me decide between X and Y" or "run a pre-mortem on this plan"                      | Applies a structured framework (weighted scoring, DACI, pre-mortem), presents options without pushing a choice |
| **Original Thinker** | "Challenge my thinking on..." or "brainstorm creative angles for..."                     | Inverts the problem, offers cross-domain analogies, removes constraints to expand the solution space           |
| **PARA Guide**       | "Where should I file this note?" or work on any file in `10-personal/`                   | Asks clarifying questions about the note's purpose, suggests Project/Area/Resource/Archive placement           |
| **Content Writer**   | Edit a file in `10-personal/10.06-blog/` or ask "help me draft a Substack post about..." | Asks about target audience, offers hook options, provides structural feedback, matches your voice              |
| **Vault Builder**    | Run `/pdt:vault-build`, or ask "I want to add a new agent for retros"                    | Surveys existing state, designs the artifact, previews all file changes, builds after confirmation            |

**What to look for:**

- **Tone shift.** Chief of Staff is professional and action-oriented. PARA Guide is methodical. Content Writer is craft-focused. Each agent has a distinct voice.
- **Context loading.** The agent should read the relevant `_active-context.md` and reference current priorities, not start from scratch.
- **Constraints respected.** No agent should make decisions for you, auto-archive, or fabricate status. They surface options and ask for confirmation.
- **Profile awareness.** Agents that read `00-system/00.03-preferences/profile.md` should adapt tone and recommendations to your stated preferences.

### 3.7 Customizing the Vault

This vault is designed to be extended. The Vault Builder agent (via `/pdt:vault-build`) helps you adapt the system to your specific use cases without needing to understand every convention by hand.

Things you can ask it to build:

- **New agents** — "I want an agent that facilitates team retrospectives" → it scaffolds the agent file, registers it in `_index.md` and `CLAUDE.md`, and checks for activation overlap with existing agents
- **New commands** — "I need a monthly review command" → it creates the command file in `.claude/commands/pdt/` with the right step format and pairs it with the appropriate agent
- **New templates** — "I want to track decision records as a note type" → it creates the template, updates the frontmatter schema, and adds capture routing rules
- **New workspaces** — "Add a side-project workspace" → it clones the workspace template with the next available prefix and updates `CLAUDE.md`

The Vault Builder previews all changes before making them, so you can review what will be created or modified across multiple files. It enforces the vault's conventions (kebab-case naming, `XX.YY` folder numbering, frontmatter schema, wiki-links) so your extensions stay consistent with the rest of the system.

### 3.8 Tips

- **Let agents work for you** — don't try to manually structure everything. Use the commands and let Claude apply the templates and routing.
- **Keep the profile updated** — the more Claude knows about your preferences and context, the better it personalizes.
- **Link freely** — wiki-links across workspaces are encouraged. A work meeting can reference a personal insight.
- **Trust the weekly rhythm** — the planning/review cycle is where the system compounds. Blockers get tracked, OKRs get updated, and context carries forward.
- **Don't over-capture** — the journal and blog are optional. Use what serves you.

---

## 4. Structure Reference

```
productory/
├── CLAUDE.md                       # Behavior spec for Claude Code
├── .claude/commands/pdt/            # Slash command definitions (pdt namespace)
│
├── 00-system/
│   ├── 00.01-templates/           # 9 note templates
│   ├── 00.02-agents/              # 6 agent personas
│   ├── 00.03-preferences/         # Profile, vault settings, frontmatter schema
│   └── 00.04-workspace-template/  # Clonable workspace blueprint
│
├── 01-shared-space/
│   ├── 01.01-insights/            # Key takeaways
│   ├── 01.02-books/               # Book notes
│   ├── 01.03-reads/               # Article notes
│   └── 01.04-resources/           # Frameworks and references
│
├── 10-personal/
│   ├── 10.01-projects/            # Active personal projects
│   ├── 10.02-areas/               # Ongoing responsibilities (PARA)
│   ├── 10.03-resources/           # Personal reference material
│   ├── 10.04-archive/             # Completed/inactive items
│   ├── 10.05-journal/             # Ad-hoc journal entries
│   └── 10.06-blog/                # Substack content pipeline
│
└── 20-work/
    ├── 20.01-okr/                 # Yearly OKR with quarterly breakdown
    ├── 20.02-weekly/              # Weekly 1Thing plans and reviews
    ├── 20.03-meetings/            # Meeting notes (linked to projects/weeklies)
    ├── 20.04-projects/            # Lightweight PM with PIC
    └── 20.05-archive/             # Completed/inactive items
```

---

## 5. For Git Users

If you want version control and the ability to pull future template updates:

1. **Click "Use this template"** on GitHub → create a **private** repository
2. **Clone your new repo** into your Obsidian vault location
3. To pull future updates:

```bash
git remote add upstream https://github.com/productory/obsidian-claude-code-template.git
git fetch upstream
git merge upstream/main --allow-unrelated-histories
```

Since template repos start with fresh history, you'll need `--allow-unrelated-histories` on the first merge. Conflicts will mostly be in `00-system/` — your personal notes in other folders won't be affected.
