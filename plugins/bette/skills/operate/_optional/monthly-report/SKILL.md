---
name: monthly-report
description: Draft a monthly stakeholder report. Use when user says "draft monthly report", "prep stakeholder update", "monthly report", or similar. Reads from a queue file, groups by product area, and outputs a draft section ready for editing.
---

# Draft Monthly Report

Draft a monthly product section for stakeholder reporting.

## Context

Customize these for your reporting cadence:
- **What:** Monthly reporting for [stakeholder / board / parent company]
- **Who:** [Recipient name and role]
- **When:** [Due date each month]
- **Doc:** [Link to shared document if applicable]

## Workflow

### 1. Read queue

Read `{Home Directory}/mdna-queue.md` (or equivalent queue file) — all raw captures for the current period.

If no queue file exists, ask {PM Name} what shipped this month or pull from recent backlog completed items.

### 2. Group by product area

Organize captures by product area, domain, or team — whatever grouping matches the report format.

### 3. Transform to report format

For each capture:
- Format: `[Area]: [What shipped] -- [context/timing if relevant]`
- Keep bullets concise (1-2 lines max)
- Focus on what shipped, not activity
- Check against previous month to avoid redundancy (if available)

### 4. Output draft

```
## Product — [Month Year]

### [Product Area]
- [What shipped] -- [context]
- [What shipped] -- [context]

### [Product Area]
- [What shipped] -- [context]
```

### 5. After submission

After {PM Name} confirms the report has been submitted:
- Clear the raw captures section in the queue file
- Update the period header to next month

## Output Style

- Concise — this is a summary for stakeholders, not internal detail
- Focus on shipped outcomes, not work-in-progress
- Every bullet should communicate value delivered
