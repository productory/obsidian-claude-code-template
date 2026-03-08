Interactive vault setup wizard for the Obsidian vault.

Walk the user through initial configuration by asking these questions in order:

1. **PARA Depth**: Ask whether they want simplified PARA (Projects, Areas, Resources, Archive — fewer subfolders) or full PARA (with more granular categorization). Default: simplified.

2. **Note-Taking Framework**: Ask their preference:
   - Classical (hierarchical folders, straightforward)
   - Zettelkasten (atomic notes, heavy linking)
   - Hybrid (folders for structure, atomic notes for ideas)
     Default: classical.

3. **Workspaces**: Confirm the current workspace setup (personal = 10, work = 20). Ask if they want to create additional workspaces. If yes, use the workspace template from `00-system/00.04-workspace-template/` to scaffold it.

4. **Default Workspace**: Ask which workspace should be the default context when ambiguous.

5. **Date Preferences**: Confirm date format (YYYY-MM-DD) and week start day (Monday).

6. **User Profile**: Walk the user through filling out `00-system/00.03-preferences/profile.md`. Ask about:
   - Name, role, and organization
   - Communication preferences (tone, detail level, feedback style)
   - Working style (planning approach, energy patterns)
   - Current goals and focus areas

   Fill in only what the user provides — leave sections empty if they prefer not to share.

After collecting answers:

- Update `00-system/00.03-preferences/vault-settings.md` with their choices
- Update `00-system/00.03-preferences/profile.md` with their profile information
- Confirm the setup summary
- Suggest running `/week-planning` to get started
