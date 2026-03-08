Analyze existing notes from another location and build a migration plan into the vault.

## Step 1: Ask for Source Locations

Ask the user:
- **Where are your existing notes?** (e.g., another Obsidian vault, a folder of markdown files, Apple Notes export, Notion export, etc.)
- Accept one or more paths/locations to analyze
- Ask about the format: markdown, plain text, HTML, or mixed

## Step 2: Analyze the Source

For each source location:
1. Scan the directory structure and list top-level folders
2. Count total files by type (`.md`, `.txt`, etc.)
3. Sample 10-15 representative files to understand content patterns
4. Check for existing frontmatter, tags, or metadata
5. Identify common note types present (meetings, journals, projects, todos, references, etc.)

Present a summary:
```
Source: /path/to/old-vault
Files: 342 markdown files across 12 folders
Detected types:
  - ~45 meeting notes (contain "attendees", "action items")
  - ~80 daily journals (date-named files)
  - ~30 project docs (contain task lists)
  - ~50 book/article notes
  - ~137 uncategorized
Existing metadata: 60% have YAML frontmatter
```

## Step 3: Build Migration Mapping

Map source content to destinations using the capture routing rules from `CLAUDE.md` Section 7:

| Source Pattern | Count | Destination | Template |
|---------------|-------|-------------|----------|
| Meeting notes | ~45 | `20-work/20.03-meetings/` | `tpl-meeting` |
| Daily journals | ~80 | `10-personal/10.05-journal/` | `tpl-journal` |
| Project docs | ~30 | `20-work/20.04-projects/` or `10-personal/10.01-projects/` | `tpl-project` |
| Book notes | ~50 | `01-shared-space/01.02-books/` | `tpl-book` |
| Uncategorized | ~137 | Needs manual triage | `tpl-capture` |

Ask the user to confirm or adjust the mapping before proceeding.

## Step 4: Plan the Migration

For each mapped group, outline the migration steps:
1. **Rename** files to kebab-case with date prefix (`YYYY-MM-DD-topic.md`)
2. **Add/update frontmatter** to match the vault schema (see `00-system/00.03-preferences/frontmatter-schema.md`)
3. **Update internal links** to wiki-link format `[[note-name]]`
4. **Move** files to their destination folders
5. **Flag** notes that need manual review (ambiguous type, broken links, duplicates)

Present the full plan as a checklist and ask the user:
- Migrate all at once or group by group?
- What to do with uncategorized notes — triage now or dump into a staging folder?
- Preserve original files (copy) or move them?

## Step 5: Execute (only after user approval)

For each note being migrated:
1. Read the original file
2. Apply the appropriate template structure where possible (don't force content into sections that don't fit)
3. Add/normalize frontmatter fields
4. Rename to vault conventions
5. Write to the destination folder
6. Log the migration (source path → destination path)

After completion, present a migration report:
- Files migrated successfully
- Files flagged for manual review
- Any broken links detected
- Suggested next steps (review flagged items, run `/capture` for stragglers)

## Constraints

- **Never delete source files** — always copy unless the user explicitly says to move
- **Never overwrite** existing vault files — if a name conflict exists, append a suffix
- **Preserve content** — migration adds structure, it should not remove or rewrite the user's words
- Flag anything ambiguous rather than guessing wrong
