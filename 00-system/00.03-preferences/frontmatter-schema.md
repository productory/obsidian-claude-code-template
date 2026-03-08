# Frontmatter Schema Reference

All notes in this vault use YAML frontmatter for structured metadata.

---

## Universal Fields (required on all notes)

```yaml
type: meeting | project | okr | weekly | journal | blog-draft | insight | book | capture | profile | active-context
status: draft | active | completed | archived
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
```

---

## Type-Specific Fields

### Meeting

```yaml
participants: []
meeting-type: standup | 1on1 | planning | retro | ad-hoc
linked-project: ""
linked-weekly: ""
```

### Project

```yaml
pic: ""
priority: high | medium | low
linked-okr: ""
```

### OKR

```yaml
year: YYYY
quarters: [Q1, Q2, Q3, Q4]
```

### Weekly

```yaml
week: YYYY-wWW
one-thing: ""
linked-okr: ""
```

### Journal

```yaml
mood: ""
energy: high | medium | low
```

### Blog Draft

```yaml
substack-status: idea | drafting | review | published
target-date: YYYY-MM-DD
```

### Insight

```yaml
source: ""
source-type: book | article | conversation | experience
```

### Book

```yaml
author: ""
book-status: reading | completed | abandoned
rating: 1-5
```

### Capture

```yaml
suggested-location: ""
```

### Profile

```yaml
# No additional fields — content is freeform sections
```

### Active Context

```yaml
# No additional fields — content is structured sections maintained by Claude
```

---

## Conventions

- Dates always use `YYYY-MM-DD` format
- Tags use kebab-case: `#project-management`, `#deep-work`
- Links use wiki-link format: `[[note-name]]`
- Empty fields use `""` (not null or omitted)
- List fields use `[]` when empty
