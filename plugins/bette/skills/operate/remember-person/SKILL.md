---
name: remember-person
description: Save context about a person so Claude remembers them in future sessions. Use when user says "remember that [name] is...", "save notes about [name]", "add [name] to my people", or after any interaction where context about a person should persist.
---

# Remember Person

Save or update context about a person so Claude has it in future workflows. This is Claude's memory of who people are and what they work on.

## Argument

`$ARGUMENTS` = person name and/or context about them.

Examples:
- "remember that Nina is on the data team and owns attribution"
- "save notes about Dan from today's meeting"
- "add Rachel — new designer, started Jan 27, working on opportunity lists"

## Workflow

### 1. Check if person file exists

Look in `{People Directory}/` for a matching filename (lowercase, e.g., `nina.md`).

- **If exists:** Read the file, then update with the new context.
- **If doesn't exist:** Create a new file.

### 2. Extract context

From `$ARGUMENTS` and conversation, capture whatever is relevant:
- **Who they are** — name, role, team
- **What they work on** — domain, projects, focus areas
- **How you interact** — peer, stakeholder, eng partner, customer contact
- **Notes** — anything worth remembering for future interactions

Don't force structure. If {PM Name} just says "remember that Nina owns attribution," save that one line. Don't pad with empty sections.

### 3. Write or update the file

**New person — create `{People Directory}/[firstname].md`:**

```
# [Person Name]

**Role:** [if known]
**Team/Domain:** [if known]
**Relationship:** [if known]

## Notes
- [YYYY-MM-DD] — [what was shared]
```

**Existing person — append to Notes section:**

```
- [YYYY-MM-DD] — [new context]
```

If the new information updates something structural (role changed, moved teams), update the header fields too.

### 4. Confirm

Tell {PM Name} what was saved: "[Name]'s file updated — added [brief summary]."

## How This Gets Used

Other skills read person files automatically:
- `prep-meeting` reads the file to build a talk track
- `digest` checks for person files when routing meeting topics
- `slack-find` uses people for name resolution

The more context here, the smarter those workflows get.

## Output Style

- Fast — this should take 5 seconds
- Don't over-structure. One line of context is fine.
- Only ask questions if the person's name is ambiguous
