Vault infrastructure builder: create or modify agents, commands, templates, workspaces, and vault configuration.

## Input

The user may describe what they want to build or change: $ARGUMENTS

If no arguments, ask the user: "What would you like to build or change in the vault? I can help with: new agents, new commands/skills, new templates, new workspaces, frontmatter schema changes, or CLAUDE.md configuration updates."

## Steps

1. **Activate Vault Builder agent**: Read `00-system/00.02-agents/vault-builder.md` and adopt the Vault Builder persona for the duration of this interaction.

2. **Understand the request**: Classify what the user wants to build or modify:
   - New agent → agent scaffolding flow
   - New command/skill → command authoring flow
   - New template → template design flow
   - New workspace → workspace scaffolding flow
   - Schema change → frontmatter schema evolution flow
   - CLAUDE.md update → targeted configuration update
   - Multiple or unclear → ask the user to clarify scope

3. **Survey existing state**: Before creating anything, read the relevant current files:
   - For agents: read `00-system/00.02-agents/_index.md` and `CLAUDE.md` Section 3 to check for overlaps
   - For commands: list `.claude/commands/pdt/` to check for naming conflicts
   - For templates: list `00-system/00.01-templates/` and read `CLAUDE.md` Section 10
   - For workspaces: read `CLAUDE.md` Section 1 to determine the next available prefix number
   - For schema: read `00-system/00.03-preferences/frontmatter-schema.md`

4. **Design and preview**: Draft the complete artifact content and list all files that will be created or modified. Present this to the user for review before making any changes. For multi-file changes, show each file's planned modifications.

5. **Build**: After user approval, create or modify the files. Follow these conventions strictly:
   - All file and folder names use kebab-case
   - Agent files follow the exact format: frontmatter, Role, Activation Context, Capabilities, Constraints, Example Interactions
   - Command files follow the exact format: description line, Input section with `$ARGUMENTS`, numbered Steps
   - Templates include proper frontmatter with all required fields plus type-specific fields
   - Folder names use `XX.YY-name` numbering

6. **Register**: Update all relevant registries:
   - Agent created → update `00-system/00.02-agents/_index.md` AND `CLAUDE.md` Section 3
   - Template created → update `CLAUDE.md` Section 10 AND (if new type) Section 2 and `frontmatter-schema.md`
   - Workspace created → update `CLAUDE.md` Section 1 AND Section 4
   - Capture routing affected → update `CLAUDE.md` Section 7

7. **Validate**: After all changes are made, re-read the modified files to confirm:
   - Frontmatter is valid YAML
   - Table formatting is consistent with existing tables
   - Wiki-links resolve correctly
   - No naming conflicts were introduced
   - Kebab-case is used throughout

8. **Summarize**: Present a final summary of everything that was created or changed, with file paths and brief descriptions. Suggest any follow-up actions (e.g., "You can test the new command by running `/pdt:your-new-command`").
