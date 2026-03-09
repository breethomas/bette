---
name: prep-review
description: Prepare a performance review draft for a direct report. Use when user says "prep [name]'s review", "draft review for [name]", "performance review for [name]", or similar. Gathers shipped work from Linear, project context from Notion, and synthesizes into review format.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."

# Prep Performance Review

Prepare a draft performance review for a direct report. Takes a person name as argument.

## Argument

`$ARGUMENTS` = person name (e.g., "chris", "Chris Johnson", "taylor")

Normalize the name to find the right file:
- Check `{People Directory}/` for matching filename (lowercase)
- If full name given, match against `{Home Directory}/reference/people.md` to find the right person

## Workflow

### 1. Load person context

Read `{People Directory}/[name].md` completely. Pay attention to:
- Background and role
- Previous review notes or feedback
- Coaching notes and development areas
- Meeting history (patterns, recurring themes)
- Wins and accomplishments already captured

### 2. Query shipped work (Linear)

Search Linear for work shipped during the review period:
```
mcp__linear__list_issues --query "[person name]" --limit 25
```

Look for: completed issues, project contributions, scope of work, complexity.

### 3. Query project context (Notion)

Search Notion for project context and meeting notes:
```
mcp__notion__notion-search --query "[person name] project" --query_type "internal"
```

Look for: project outcomes, cross-functional collaboration, leadership moments.

### 4. Synthesize review draft and write to file

**Write the full review draft to:** `{Home Directory}/drafts/prep-review-[name]-[YYYY-MM-DD].md`

Use this format:

```
# Performance Review Draft: [Full Name]
**Period:** [review period]
**Role:** [from people file]
**Prepared by:** {PM Name}

## Accomplishments
- [What shipped, with impact]
- [Projects delivered]
- [Scope and complexity of contributions]

## Strengths Demonstrated
- [Strength + specific example]
- [Strength + specific example]

## Development Progress
- [Growth area from previous review/coaching + evidence of progress]
- [New skills or capabilities developed]

## Areas for Growth
- [Growth area + specific example + suggestion]
- [Growth area + specific example + suggestion]

## Goals for Next Period
- [Suggested goal tied to team/company priorities]
- [Suggested goal tied to personal development]

## Documentation Gaps
- [Any missing context or areas where more evidence is needed]
```

### 5. Return file path

Your final message MUST include:
```
REVIEW_FILE: {Home Directory}/drafts/prep-review-[name]-[YYYY-MM-DD].md
```

## Output Guidelines

- Write full review draft to the file (this is the primary output)
- Be specific — every point should have a concrete example
- Distinguish between accomplishments (what shipped) and strengths (how they work)
- Flag documentation gaps honestly — better to note what's missing than fabricate
- Be thorough in the file — it will be read back by the main agent and presented to {PM Name}
- This is a draft for {PM Name} to edit, not a final review
