Quick capture: auto-classify and route content to the right folder.

## Input

The user will provide: $ARGUMENTS

If no arguments, ask the user: "What would you like to capture?"

## Steps

1. **Analyze content**: Determine the type of content from the user's input:
   - Meeting note → `meeting`
   - Project idea → `project`
   - Insight/takeaway → `insight`
   - Book note → `book`
   - Article/read → `capture` (routed to reads)
   - Blog idea → `blog-draft`
   - Journal entry → `journal`
   - General/unclear → `capture`

2. **Determine routing**: Use the routing rules from `CLAUDE.md` Section 7 to pick the destination folder.

3. **Select template**: Read the appropriate template from `00-system/00.01-templates/`.

4. **Create the note**:
   - Generate a kebab-case filename (date-prefixed: `YYYY-MM-DD-topic.md`)
   - Fill in frontmatter from context
   - Place content in the appropriate template sections
   - Add relevant wiki-links

5. **Update active context**: If the capture is significant (new project, key decision, blocker, or deadline), update the relevant workspace's `_active-context.md` to reflect it.

6. **Confirm**: Show the user where the note was created and what type was assigned. Ask if they want to reclassify.

If the content type is ambiguous, ask the user to clarify before creating the note.
