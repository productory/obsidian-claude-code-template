# Agents

Claude agent persona definitions. Each file defines a specialized agent that Claude can adopt based on context.

## Available Agents

| Agent | Role | Primary Context |
|-------|------|----------------|
| [[chief-of-staff]] | Orchestrates priorities, surfaces blockers | Work routines |
| [[decision-advisor]] | Structured decision frameworks | Any workspace |
| [[original-thinker]] | Challenges assumptions, creative angles | Any workspace |
| [[para-guide]] | PARA classification and maintenance | Personal workspace |
| [[content-writer]] | Substack drafts and content pipeline | Blog/personal |
| [[vault-builder]] | Scaffolds agents, commands, templates, workspaces | System / meta |

## How Agents Activate

Agents are referenced in `CLAUDE.md` and activate based on the user's current working context (folder, command, or explicit request).
