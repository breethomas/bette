# Prioritize Enablers and Blockers

**Source:** Linear Method
**Category:** Planning & Prioritization
**Best for:** Deciding what to build next, balancing growth vs adoption, timing decisions

---

## Core Principle

**Distinguish between Enablers (add new functionality) and Blockers (gaps preventing adoption).**

Build blockers when they prevent usage. Build enablers when they move the needle on growth.

## Why This Matters

**The Problem:**
- Teams treat all feature requests equally
- "Nice to haves" get built before "must haves"
- Adoption stalls because critical gaps aren't addressed
- Growth slows because team is fixing paper cuts

**The Solution:**
Categorize work by **whether it blocks adoption or enables new value**, then prioritize based on timing.

## The Framework

### 1. Categorize Every Issue

**Blocker:**
A gap that **prevents someone from adopting or using your product.**

**Enabler:**
A feature that **adds new functionality or improves the experience** for existing users.

**Examples:**

| Issue | Type | Why |
|-------|------|-----|
| SSO login support | Blocker | Enterprise customers can't adopt without it |
| Dark mode | Enabler | Users can already use the product |
| Mobile app | Blocker (for mobile users) | Can't use product on mobile at all |
| Export to PDF | Enabler | Users can already access their data |
| Critical bug fix | Blocker | Prevents core workflow from working |
| Performance optimization | Enabler (usually) | Product works, just slower |

### 2. Apply the Decision Matrix

**For Blockers:**
Ask: **"Does this prevent a meaningful segment from adopting?"**

- ✅ **Yes** → High priority (removes adoption friction)
- ❌ **No** → It's actually an enabler

**For Enablers:**
Ask: **"Will this move the needle on our current goals?"**

- ✅ **Yes** → Build it (drives growth/engagement)
- ❌ **No** → Defer it (nice to have)

### 3. Timing Considerations

**Build blockers when:**
- They prevent adoption of a target segment
- The segment is strategically important NOW
- Cost of not building exceeds cost of building

**Defer blockers when:**
- The affected segment isn't a near-term priority
- Workarounds exist
- You haven't validated the segment's value yet

**Build enablers when:**
- They directly support current growth goals
- You've validated demand with existing users
- The impact is measurable and significant

**Defer enablers when:**
- They're speculative improvements
- You haven't validated the problem
- They don't move current metrics

## Real Example: Linear's Auth Strategy

**Linear launched with Google Logins only.**

**Why?**
- Google auth was sufficient for early adopter segment (startups, tech companies)
- Building SAML, Microsoft, etc. upfront would've delayed launch by months
- They could validate product-market fit without enterprise auth

**Later, they added:**
- SAML (blocker for enterprise customers)
- Microsoft auth (blocker for Microsoft shops)
- Email/password (blocker for some users)

**Each was added when:**
- The target segment became strategically important
- Demand was validated
- The blocker was preventing meaningful adoption

## How to Apply This

### Step 1: Audit Your Backlog

**Categorize each item:**
- Is this a blocker or enabler?
- If blocker: For whom? How many users/revenue?
- If enabler: What metric does it improve? By how much?

### Step 2: Stack Rank Blockers

**High priority blockers:**
- Prevent adoption of strategic segment
- Affect significant portion of target market
- No viable workaround exists

**Low priority blockers:**
- Affect small/non-strategic segment
- Workarounds exist
- Can be solved with customer success support

### Step 3: Stack Rank Enablers

**High priority enablers:**
- Directly tied to current OKRs/goals
- Validated demand from existing users
- Measurable impact on key metrics

**Low priority enablers:**
- Speculative improvements
- Affects small user subset
- Unclear impact

### Step 4: Balance Your Roadmap

**Don't just build blockers.** You need enablers to grow existing usage.

**Typical healthy mix:**
- 40% Blockers (remove adoption friction)
- 40% Enablers (grow existing users)
- 20% Exploratory/Bets (learn new things)

**Adjust based on context:**
- Early stage? More enablers (nail core value)
- Scaling stage? More blockers (expand addressable market)
- Mature product? Balance both

## Common Mistakes

### Mistake 1: Building All Blockers First

**Problem:** Product gets wider but not deeper. You can acquire users but not retain them.

**Fix:** Balance blockers (breadth) with enablers (depth).

### Mistake 2: Treating Everything as a Blocker

**Problem:** "Users can't adopt without [feature]" becomes excuse for every request.

**Fix:** Validate with data. Are you actually losing customers/deals over this?

### Mistake 3: Ignoring Strategic Timing

**Problem:** Building blockers for segments you're not targeting yet.

**Fix:** Align blockers with go-to-market strategy. Don't build enterprise features before you're selling to enterprise.

### Mistake 4: Building Enablers Users Don't Want

**Problem:** Spending months on "improvements" no one asked for.

**Fix:** Validate demand. Run surveys, interviews, prototypes before building.

## AI-Era Adaptation

**AI changes the blocker/enabler calculus:**

**Blockers you can now defer:**
- Custom integrations (AI can handle API calls)
- Complex workflows (AI can script them)
- Documentation (AI can answer questions)

**Enablers that matter more:**
- AI-powered core features (competitive moat)
- Data quality (AI needs clean inputs)
- Clear product structure (AI needs to understand it)

**New category: AI Enablers**
- Features that unlock AI capabilities
- API access for LLM integrations
- Structured data exports

---

## Key Takeaways

✅ **Blockers prevent adoption. Enablers enhance usage.**
✅ **Build blockers when they prevent meaningful adoption of strategic segments.**
✅ **Build enablers when they move the needle on current goals.**
✅ **Balance your roadmap—don't just remove friction, also add value.**
✅ **Validate demand before building, especially for enablers.**

**Bottom line:** Not everything that users "can't do" is a blocker. Not everything that "would be nice" is worth building. Prioritize based on strategic timing and measurable impact.

---

## Related Frameworks

- **[LNO Prioritization](lno-prioritization.md)** - Identify 10x impact work vs overhead
- **[Scope Projects Down](scope-projects-down.md)** - Ship blockers and enablers in small batches
- **[Four Risks](../discovery/four-risks.md)** - Validate that enablers have real value
- **[Jobs to be Done](../discovery/jobs-to-be-done.md)** - Understand what's actually blocking adoption
