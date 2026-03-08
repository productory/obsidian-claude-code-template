Scaffold a new project from template.

## Input

The user may provide a project name: $ARGUMENTS

If no arguments, ask for the project name.

## Steps

1. **Gather details**: Ask the user for:
   - **Project name** (if not provided)
   - **Objective**: What is this project trying to achieve?
   - **PIC** (Person In Charge): Who owns this?
   - **Priority**: High, medium, or low
   - **Workspace**: Which workspace (default: `20-work/`)
   - **Linked OKR**: Which OKR key result does this support? (Search active OKR files to suggest options)

2. **Create project file**:
   - Read the template from `00-system/00.01-templates/tpl-project.md`
   - Generate filename: `YYYY-MM-DD-project-name.md` (kebab-case)
   - Place in `{workspace}/projects/` (e.g., `20-work/20.04-projects/`)
   - Fill in frontmatter and objective section

3. **Link to OKR**: If an OKR key result was specified, add a wiki-link in both the project and the OKR file.

4. **Update active context**: Add the new project to the Active Projects Summary in `{workspace}/_active-context.md`.

5. **Confirm**: Show the created project file and its location. Suggest next steps (add tasks, set timeline).
