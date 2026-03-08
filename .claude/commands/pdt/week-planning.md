Create the weekly planning file for the current week.

## Steps

1. **Load active context**: Read `20-work/_active-context.md` to load working memory from previous sessions — current priorities, open blockers, and recent decisions.

2. **Find the current OKR**: Read the active OKR file in `20-work/20.01-okr/` (or the relevant workspace). Identify the current quarter's objectives and key results.

3. **Check last week**: Look for the most recent weekly file in `20-work/20.02-weekly/`. Summarize any carry-over items or unfinished priorities.

4. **Create new weekly file**: Use the template from `00-system/00.01-templates/tpl-weekly.md`. Name it `YYYY-wWW-weekly.md` (e.g., `2026-w09-weekly.md`) and place it in `20-work/20.02-weekly/`.

5. **Set the 1Thing**: Ask the user: "What is your ONE most important thing this week?" This goes in the `one-thing` frontmatter field and the 1Thing section.

6. **Set priorities**: Ask the user to list their top 3-5 priorities for the week. These should connect to OKR key results where possible.

7. **Link to OKR**: Set the `linked-okr` field to the current OKR file.

8. **Update active context**: Update `20-work/_active-context.md` with the new week's priorities, key dates, and any changes to active projects.

9. **Summary**: Present the completed weekly plan and suggest checking it at the start of each day.

Adopt the **Chief of Staff** agent persona from `00-system/00.02-agents/chief-of-staff.md` during this interaction.
