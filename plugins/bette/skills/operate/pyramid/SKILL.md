---
name: pyramid
description: Apply the Pyramid Principle (Minto/McKinsey) to structure communication. Use when user says "structure this", "pyramid this", "make this executive-ready", "SCQA", "restructure for clarity", or when drafting any exec-facing document. Enforces answer-first structure, SCQA framing, MECE logic, and action titles.
---

# Pyramid Principle — Communication Framework

Structure any communication so the audience gets the answer first, supported by logically ordered, MECE arguments, each backed by evidence.

**Core rule:** Think bottom-up (gather, group, synthesize). Communicate top-down (lead with the answer).

---

## When to Apply

- Executive summaries, stakeholder updates, strategy memos
- PRD sections (problem statements, recommendations, trade-off analyses)
- Slack messages and emails to leadership
- Any document where the reader is time-constrained and decision-oriented
- When composing with other skills (exec-update, prep-1on1, synthesize)

## When NOT to Apply

- Exploratory brainstorms or brain dumps (structure kills divergent thinking)
- 1:1 coaching conversations (relational, not transactional)
- Raw meeting notes or transcripts (capture first, structure later)
- Creative writing or narrative storytelling

---

## The Pyramid Structure

```
           ┌─────────────────┐
           │   MAIN POINT    │  ← Answer/recommendation (one sentence)
           │  (the "so what") │
           └────────┬────────┘
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
   ┌─────────┐ ┌─────────┐ ┌─────────┐
   │ Arg 1   │ │ Arg 2   │ │ Arg 3   │  ← 2-5 MECE supporting arguments
   │         │ │         │ │         │     (each answers "why?" or "how?")
   └────┬────┘ └────┬────┘ └────┬────┘
        │           │           │
      ┌─┴─┐      ┌─┴─┐      ┌─┴─┐
      │ E │      │ E │      │ E │       ← Evidence, data, examples
      └───┘      └───┘      └───┘
```

### Rules

1. **Answer first.** The main point goes at the top. Not at the end. Not "after context." First.
2. **2-5 supporting arguments.** Each argument directly answers the question raised by the level above.
3. **MECE at every level.** Arguments at the same level must be Mutually Exclusive (no overlap) and Collectively Exhaustive (no gaps).
4. **Vertical logic (Q&A).** Each point raises a question in the reader's mind. The level below answers it.
5. **Horizontal logic.** Ideas at the same level connect by either:
   - **Deductive:** Major premise → Minor premise → Conclusion
   - **Inductive:** Similar items grouped to support a single insight
6. **Action titles.** Every heading states the point as a complete sentence, not a topic label.

---

## SCQA Introduction Framework

Use SCQA to frame the opening of any structured communication. Four variants depending on context:

### Standard SCQA
| Element | What it does | Example |
|---------|-------------|---------|
| **Situation** | Shared context the reader agrees with | "Acme is our largest customer at $1.3M ARR" |
| **Complication** | What changed or went wrong | "Their satisfaction scores have dropped — users got burned by false positives" |
| **Question** | The question this raises | "How do we restore credibility before the leadership summit?" |
| **Answer** | The recommendation | "Run a root cause analysis and present accuracy data" |

### Variant: Direct (skip to CA when S is obvious)
For audiences with full context — exec updates, follow-up Slacks.
> "The scoring algorithm is drifting (C). We need a root cause analysis before the customer summit (A)."

### Variant: Concern (when delivering bad news)
S → C → reframe the Q to focus on the path forward → A.
> "We committed to mid-Feb for SSO (S). The team is behind by a week (C). What's the minimum viable path to keep the customer's trust? (Q) Ship SSO auth by Feb 21, defer admin features to March (A)."

### Variant: Action Request (when you need something from the reader)
S → C → Q → A, where A is the specific ask.
> "The monthly board report is due Tuesday (S). I don't have last month's shipped features from engineering (C). Can you send me the release notes from January? (Q+A)"

---

## SCQA Templates by Document Type

### Executive Summary / Stakeholder Update
```
**[Action title stating the recommendation]**

[Situation: 1 sentence — shared context]
[Complication: 1-2 sentences — what changed]
[Question: implicit or explicit]

**Recommendation:** [1 sentence answer]

**Why:**
1. [Argument 1 — action title] — [evidence]
2. [Argument 2 — action title] — [evidence]
3. [Argument 3 — action title] — [evidence]

**Next steps:** [specific actions, owners, dates]
```

### PRD Problem Statement
```
**[Action title: the problem in one sentence]**

[Situation: how the system works today]
[Complication: what's breaking, what changed, what users are experiencing]
[Question: what should we build / change / fix?]

**Recommendation:** [the proposed solution]

**Supporting arguments:**
1. [User impact — action title] — [data/quotes]
2. [Business impact — action title] — [metrics]
3. [Technical feasibility — action title] — [eng assessment]
```

### Strategy Memo
```
**[Action title: the strategic recommendation]**

[Situation: market context, current position]
[Complication: threat, opportunity, or shift]
[Question: how should we respond?]

**Recommendation:** [1-2 sentences]

**The case:**
1. [Argument 1 — action title]
   - [Evidence]
   - [Evidence]
2. [Argument 2 — action title]
   - [Evidence]
   - [Evidence]
3. [Argument 3 — action title]
   - [Evidence]
   - [Evidence]

**Risks and mitigations:**
- [Risk] → [Mitigation]

**Timeline:** [key milestones]
```

### Slack Message to Leadership
```
[One sentence: the point / ask / update]

Context: [1-2 sentences if needed — S+C compressed]

[Supporting detail as bullets if needed]

[Specific ask or next step]
```

---

## MECE Validation Checklist

When reviewing arguments at any level of the pyramid, test:

**Mutually Exclusive (no overlap):**
- [ ] Can I read any two arguments side by side without thinking "these are basically the same point"?
- [ ] If I removed one argument, would the others still make distinct points?
- [ ] Are there clear boundaries between each argument's scope?

**Collectively Exhaustive (no gaps):**
- [ ] If the reader only read these arguments, would they have the complete picture?
- [ ] Is there an obvious objection or angle that isn't addressed?
- [ ] Does the set of arguments fully support the main point above them?

**Logical ordering (are they in the right sequence?):**
- [ ] Chronological — if time matters (project phases, historical analysis)
- [ ] Structural — if describing components (teams, systems, segments)
- [ ] Comparative — if evaluating options (importance ranking, impact order)
- [ ] Deductive — if building a logical case (premise → premise → conclusion)

**Common MECE failures to catch:**
- Two arguments that are really one argument split artificially
- A "catch-all" bucket that hides unstructured thinking (e.g., "Other considerations")
- Missing the stakeholder/user perspective when all arguments are internal
- Arguments at different levels of abstraction (mixing strategic and tactical)

---

## Action Title Transformation

**The test:** If someone only reads the headings, do they get the full argument?

### Weak (topic labels) → Strong (action titles)

| Weak | Strong |
|------|--------|
| "Background" | "Customer satisfaction scores have drifted since the pricing change" |
| "Pricing" | "Usage-based pricing aligns revenue with the value we deliver" |
| "Timeline" | "SSO must ship by mid-Feb to hold the enterprise customer's trust" |
| "AI Strategy" | "AI replaces the dashboard — the conversational interface becomes the product" |
| "Risks" | "Algorithm drift could undermine the entire intelligence layer" |
| "Team" | "Two new PMs close the segment coverage gap" |
| "Next Steps" | "Three actions this week unblock the customer analysis" |
| "Customer Feedback" | "Users want fewer signals, not more — precision over volume" |

### Transformation rules
1. **Add a verb.** "Pricing" → "Engagement pricing aligns..."
2. **Add the "so what."** "AI Strategy" → "AI replaces the dashboard..."
3. **Make it falsifiable.** A good action title can be disagreed with. If it can't, it's too vague.
4. **Keep it to one line.** If the title needs two sentences, the argument needs splitting.

---

## Composing with Other Skills

### With exec-update
Apply SCQA to the Insight section. Use action titles for all Top 3 bullets. Run MECE check on the Top 3 to ensure no overlap and full coverage of what moved.

### With prep-meeting
Structure each talk track topic as a mini-pyramid: open with the point (what you want to communicate or learn), support with 2-3 specific items, have evidence ready. Use SCQA for difficult conversations.

### With synthesize
After extracting decisions and insights from transcripts, apply MECE validation to the output categories. Ensure the synthesis doesn't have overlapping buckets or missing angles.

### With any Slack/email draft
Default to the Slack template above. Answer first, context second, ask last. Cut everything that doesn't support the point.

---

## Quality Checks

Before finalizing any pyramid-structured output:

- [ ] **Answer is first.** The main point appears before any context or reasoning.
- [ ] **SCQA is clean.** Situation is agreed-upon (not controversial), Complication is specific (not vague), Answer directly addresses the Question.
- [ ] **Arguments are MECE.** No overlap, no gaps, logically ordered.
- [ ] **Vertical logic holds.** Each level answers the "why?" or "how?" from the level above.
- [ ] **Action titles throughout.** Every heading states the point, not the topic. Passes the "titles-only" test.
- [ ] **Evidence is concrete.** Data points, quotes, or specific examples — not "studies show" or "feedback suggests."
- [ ] **No orphan arguments.** Every point at a level has at least one sibling (if you only have one sub-point, it should merge with the parent).
