# Example: People Reference File

An annotated example of a people reference file. Generalized from a real implementation.

---

```markdown
# People Reference

Quick lookup for Claude. One line per person.

**Last updated:** 2026-03-01
                                          # ← Date signals freshness.
                                          #   Review monthly.

---

## Leadership
                                          # ← Group by relationship to you,
                                          #   not org chart.

- **Alex** — CEO. Sets vision, strong POV on AI. Your boss.
- **Jordan** — Co-founder. Headcount, strategic direction.
- **Morgan** — Chief of Staff. MBRs, budget, reporting.
- **Sam** — VP Engineering. Closest peer. On leave (as of Feb 2026).
                                          # ← Temporary status notes are fine.
                                          #   Remove when no longer relevant.

## Your Direct Reports

- **Carol** — PM, Platform domain. See `people/carol.md`.
- **Dan** — Designer. Junior, first design role. See `people/dan.md`.
- **Eve** — PM, Growth domain. See `people/eve.md`.
                                          # ← Link to deep files.
                                          #   One-liners here, full context there.

## Engineering
                                          # ← People the AI will encounter
                                          #   in transcripts, Slack, Linear.

- **Frank** — Eng Lead. Frontend and API. Principal: Grace.
- **Grace** — Principal Engineer. Auth, billing, SSO.
- **Hank** — Engineer. Mobile team.
- **Iris** — Engineer. AI/ML work.

## Cross-Functional

- **Jack** — Customer Success lead. Escalation point.
- **Kate** — Marketing. Lifecycle and digital.
- **Leo** — Sales leadership. Enterprise deals.

## Name Disambiguation
                                          # ← Critical section. Without this,
                                          #   the AI WILL confuse people.

- **Sam** (VP Eng, leadership) vs **Sam K** (engineer, mobile).
- **Pat** (QA) vs **Pat M** (support).
- "Betty" (dictated) = "Bette" (correct spelling).
                                          # ← Voice-to-text disambiguation.

## External

- **Noah** — Enterprise customer contact.
- **Olivia** — Partner relationship manager.

## Former
                                          # ← Keep briefly. Useful for
                                          #   understanding old transcripts.

- **Quinn** — Designer, left. Dan picked up their work.
```

---

## Design Choices

**One line per person.** Name, role, one distinguishing fact. That's it. If the AI needs more, it loads the linked deep file.

**Grouped by relationship.** Leadership, directs, engineering, cross-functional, external, former. This mirrors how you encounter these people in your day.

**Disambiguation is explicit.** If two people share a name (or a dictation tool mangles a name), resolve it here. The AI will encounter these names in messy contexts — transcripts, Slack threads, meeting notes.

**"See people/name.md" pattern.** Direct reports and close collaborators get their own files with full context (background, coaching notes, 1:1 history). The reference file is the index; deep files are the content.

**Former section exists.** When you process old transcripts or reference past decisions, the AI needs to know who these people were. Keep entries minimal — remove after ~6 months.
