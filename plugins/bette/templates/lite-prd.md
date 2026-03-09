# Lite PRD Template

**Philosophy:** Use what you need. Skip what you don't. Focus on shared understanding, not completeness.

**The point:** Help your team understand what problem you're solving, why it matters, and what success looks like. Everything else is optional.

---

## The Essentials (Always answer these)

### What problem are we solving?
[2-3 sentences. Customer pain or opportunity.]

### For whom?
[Specific user segment]

### How do we know this matters?
[Evidence: research, data, feedback]

### What are we building?
[High-level solution. Link to prototype if you have one - you should!]

### How will we know it worked?
[1-2 key metrics with targets]

---

## The Rest (Use what's helpful)

Pick the sections that help create shared understanding with your team. Skip the rest.

---

### 📋 Scope & Decisions
**Use when:** Team needs clarity on boundaries

**In scope:**
- [What we're building]

**Out of scope:**
- [What we're explicitly NOT doing]

**Open questions:**
- [Unresolved decisions]

---

### ⚠️ Risks
**Use when:** You need to address concerns or validate assumptions

**Biggest assumption:**
[What must be true for this to work?]

**How we'll validate:**
[Prototype test, user interviews, beta]

**Four Risks quick check:**
- Value (will customers use it?): ⬜ Low ⬜ Med ⬜ High
- Usability (can users figure it out?): ⬜ Low ⬜ Med ⬜ High
- Feasibility (can we build it?): ⬜ Low ⬜ Med ⬜ High
- Viability (does it work for business?): ⬜ Low ⬜ Med ⬜ High

---

### 🔍 Discovery Insights
**Use when:** Research informed your direction

**Customer research:**
[Key learnings]

**Data insights:**
[Relevant metrics or trends]

---

### 🛠️ Technical Notes
**Use when:** Engineering needs context

**Estimate:** [Small / Medium / Large]

**Key challenges:**
[Any complexity engineering flagged]

**Dependencies:**
[Other teams/systems this relies on]

---

### 🤖 AI Product Considerations
**Use when:** Building AI features

**Model/approach:**
[Which model, RAG, agent, etc.]

**Eval strategy:**
[How you're testing quality]

**Cost model:**
[Cost per query, projected at scale]

**Failure handling:**
[What happens when AI is wrong?]

---

### 🚀 Launch Notes
**Use when:** Go-to-market needs planning

**Launch strategy:**
[Beta, rollout, full launch]

**User communication:**
[How you'll announce/educate]

---

### 📅 Timeline
**Use when:** Team needs sequencing clarity

Use Now-Next-Later format:
- **Now:** [Currently working on]
- **Next:** [After this succeeds]
- **Later:** [Future considerations]

---

### 🔗 Links
[Prototype] • [Design] • [Research] • [Related issues]

---

## How to Use This Template

### Start Simple
Begin with just "The Essentials" - that might be all you need.

Add other sections only if they help create shared understanding.

### Prototype > Spec
If you have a working prototype, lead with that. A demo + 3 paragraphs beats a 5-page doc.

### Keep It Conversational
Write like you're explaining to a teammate, not writing a legal document.

### Link, Don't Duplicate
Reference other docs, designs, prototypes. Don't copy-paste everything here.

### When to Use This vs. Issues
- **PRD:** For larger features needing alignment across team/stakeholders
- **Issue:** For specific, clear tasks ("Add export button to dashboard")

If your entire "PRD" is one sentence, just write an issue instead.

### Update as You Learn
This isn't a static contract. Update when you learn new information.

---

## Real Examples

### Example 1: Minimal (This might be enough!)

**What problem:** Users can't export their dashboard data for offline analysis.

**For whom:** Data analysts who need to work in Excel/Google Sheets.

**Evidence:** Top 3 feature request in feedback (40+ mentions), competitive gap.

**What we're building:** CSV export button on analytics dashboard. [Link to prototype]

**Success:** 30% of active users export at least once in first month.

**Scope:** V1 exports visible data only (respects filters). Future: custom columns, scheduled exports.

**Next steps:** Design review Monday, eng estimate by Wed, target 2-week build.

---

### Example 2: More Context Needed

**What problem:** New users don't know what to do first - activation rate is 40%, should be 60%+.

**For whom:** New signups in their first session.

**Evidence:**
- User interviews (8/10 said "I was confused where to start")
- Analytics: 60% bounce without completing any action
- Session recordings show users clicking around aimlessly

**What we're building:** Interactive product tour that guides users through first 3 key actions. [Prototype link]

**Success:** Increase activation (complete core action) from 40% → 55% within 30 days of launch.

**Scope:**
- In: 3-step tour, dismissible, shows on first login only
- Out: Advanced features, custom tours per use case, video content

**Risks:**
- Usability: Medium - need to test that tour doesn't annoy users
- Value: Low - user research strongly validates need
- Validation: Testing prototype with 10 users next week

**Technical:** Medium complexity (2-3 weeks). Needs tooltip library and user state tracking.

**Launch:** Beta with 20% of new users, measure for 2 weeks, then roll out to all.

---

### Example 3: AI Feature

**What problem:** Users spend too much time writing email subject lines - often end up with low open rates.

**For whom:** Sales and marketing teams sending cold outreach emails.

**Evidence:**
- User interviews: "I rewrite subject lines 5+ times"
- Data: Emails with AI-suggested subjects in prototype had 23% higher open rates

**What we're building:** AI suggests 3 subject lines based on email body. User can click to use or ignore. [Prototype link]

**Success:**
- 40% of users try the feature in first week
- 60% positive feedback (thumbs up)
- 20% improvement in average open rates

**AI specifics:**
- Model: GPT-4o (fast, cost-effective)
- Cost: ~$0.01 per generation, ~$800/month at 10K users
- Evals: 50-case test dataset, 70%+ rated "good" by humans
- Failure handling: If API fails, feature gracefully hidden

**Risks:**
- Value: Low - prototype tested well
- Cost: Medium - need to monitor usage patterns
- Quality: Medium - evals in place, user can always ignore

**Timeline:**
- Now: Finalize eval dataset, eng building v1
- Next: Internal dogfooding (1 week), beta (20% of users, 2 weeks)
- Later: Multi-language support, learn from user feedback

---

## Remember

The goal isn't to fill out every section.

The goal is to create shared understanding so your team can build the right thing.

Write what's needed. Skip what's not. Move fast.

---

**Pro tip:** If you're spending more time on the PRD than you did prototyping, you're doing it backwards.
