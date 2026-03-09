# Reference File Design

How to structure persistent knowledge files that AI can consume efficiently.

---

## The Principle

Reference files are the AI's long-term memory. They hold stable context that doesn't change session to session — who people are, what domains exist, how systems work. Well-designed reference files mean the AI starts every session already knowing what matters.

The design philosophy: **one line per entry, deep context lives elsewhere.**

## File Types

### People Reference

Who's who. Roles, relationships, disambiguation. The AI uses this to understand context in conversations, meeting notes, and Slack messages.

**Pattern:**
```markdown
# People Reference

Quick lookup. One line per person.

## Leadership
- **Alice** — CEO. Sets vision. Your boss.
- **Bob** — VP Engineering. Closest peer.

## Your Direct Reports
- **Carol** — PM, Platform domain. See `people/carol.md`.
- **Dan** — Designer. Junior, first design role. See `people/dan.md`.

## Engineering
- **Eve** — Principal Engineer. Auth, billing, SSO.
- **Frank** — Engineer. API work, integrations.
```

**Design rules:**
- One line per person: name, role, one distinguishing detail
- Group by relationship to you (reports, peers, leadership, cross-functional)
- Link to deep files for direct reports (`people/name.md`)
- Include disambiguation when names collide ("Not Sean the designer")
- Update when people join, leave, or change roles

### Domains Reference

Product areas, terminology, architecture. The AI uses this to understand what teams own, what acronyms mean, and how the product is structured.

**Pattern:**
```markdown
# Product Domains Reference

## Domain Map

| Domain | Owner | Eng Lead | Scope |
|--------|-------|----------|-------|
| Platform | Carol | Eve | Auth, billing, API |
| Growth | Dan | Frank | Onboarding, activation |

## Acronyms & Product Terms
- **CEP** — Customer Experience Portal. Main dashboard.
- **HBN** — Homebot Network. Partner matching.

## Architecture Layers
1. Data ingestion (imports, API, integrations)
2. Intelligence (signals, rules, logic)
3. Surfaces (dashboards, AI chat, reports)
4. Delivery (email, SMS, push)
```

**Design rules:**
- Tables for structured relationships (domain → owner → scope)
- Bullet points for terminology definitions
- Numbered lists for sequential/layered concepts
- Include what the AI needs to parse conversations, not implementation details

### Systems Reference

Technical systems, meeting cadences, methodology, compliance. The operational context the AI needs to understand how your company works.

**Pattern:**
```markdown
# Company & Systems Reference

## Technical Systems
- **Mikasa** — Billing backend. Manages subscriptions.
- **Recurly** — External billing platform.
- **Maestra** — AI orchestration layer.

## Methodology
- **Shape Up** — 6-week development cycles.
- **Speedboat** — Small team, next-gen work.
- **Ocean Liner** — Maintains current revenue systems.

## Meeting Cadences
- **Exec meeting** — Tuesdays. Status update format.
- **All-Hands** — 2nd Thursday monthly.
- **MBRs** — Monthly. Goals tracking.
```

---

## Design Principles

### 1. One Line Per Entry

Every entry should be scannable in a single line. If it takes a paragraph to explain, it belongs in a linked deep file, not the reference.

**Good:** `- **Eve** — Principal Engineer. Auth, billing, SSO.`

**Bad:** `- **Eve** — Eve is a principal engineer who has been at the company for 3 years. She originally joined as a senior engineer and was promoted last year. She owns the authentication system, billing integration with Recurly, and SSO implementation. She's also involved in...`

### 2. Deep Context Lives Elsewhere

Reference files are indexes, not encyclopedias. For people you work with closely (direct reports, key partners), create dedicated files with full context.

```
reference/
  people.md          ← One line per person (loaded every session)
people/
  carol.md           ← Full context: background, coaching notes, 1:1 logs
  dan.md             ← Full context: goals, performance tracking, wins
```

The reference file gets loaded every session. The deep files get loaded on demand (for 1:1 prep, reviews, etc.).

### 3. Group by Relationship, Not Org Chart

The AI doesn't need your company's org chart. It needs to understand how people relate to YOUR work.

**Good groupings:**
- Leadership / Your directs / Engineering / Cross-functional / External
- By how often you interact with them

**Bad groupings:**
- By department (Engineering, Marketing, Sales, Support)
- By seniority (VP, Director, Manager, IC)

### 4. Include Disambiguation

When names are ambiguous, resolve it explicitly. The AI will encounter these names in transcripts, Slack messages, and meeting notes.

```markdown
- **Sean** — Designer, your direct report. (Not Sean D. or Sean O.)
- **Sean Doran** — Engineer, messaging team.
- **Sean O'Neill** — Engineer, UI/interactions.
```

### 5. Flag What Changes

Add a "Last updated" date to each reference file. This signals to both you and the AI how fresh the context is.

```markdown
# People Reference
**Last updated:** 2026-03-01
```

---

## Maintenance

### When to Update

- **Immediately:** Someone joins, leaves, or changes roles
- **Weekly:** After digesting meeting transcripts, flag new names/terms
- **Monthly:** Review for stale entries, remove departed people

### How to Update

The AI should flag updates proactively:

> "I noticed the transcript mentions 'Rachel' who isn't in people.md. She appears to be a new designer. Want me to add her?"

Build this expectation into your CLAUDE.md:

```markdown
When processing transcripts or meetings, flag new people, terms,
or systems not in reference files. Suggest additions. Keep entries
concise — one line per item.
```

---

*Reference files are the AI's cheat sheet. Make them scannable, keep them current, and link to depth when needed.*
