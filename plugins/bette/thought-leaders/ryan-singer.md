# Ryan Singer

**Focus:** Product shaping, cycle planning, fixed time/variable scope development

**Known For:** Creating Shape Up methodology at Basecamp, author of "Shape Up: Stop Running in Circles and Ship Work that Matters"

## Core Philosophy

Ryan Singer believes the traditional approach to product development—writing detailed specs upfront or letting teams figure everything out—sets projects up for failure. Shape Up is a third way: work is shaped at the right level of abstraction before betting on it.

The key insight: **appetite drives scope, not the reverse.** Instead of estimating how long something will take, decide how much time it's worth and shape the work to fit.

## Key Framework: Shape Up

### The Problem with Traditional Approaches

**Waterfall approach:**
- ❌ Detailed specs written upfront
- ❌ Estimates become commitments
- ❌ No room for discovery during building
- ❌ Scope creep is inevitable

**"Agile" theater:**
- ❌ No shaping, just "the team will figure it out"
- ❌ Infinite backlogs of unvetted ideas
- ❌ Two-week sprints with no end in sight
- ❌ Projects drag on indefinitely

### The Shape Up Solution

**Three properties of shaped work:**

```
┌────────────────────────────────────┐
│  ROUGH                             │
│  - Not fully specified             │
│  - Leaves room for team creativity │
│  - Main elements defined           │
└────────────────────────────────────┘

┌────────────────────────────────────┐
│  SOLVED                            │
│  - Main elements connected         │
│  - Direction is clear              │
│  - Not just a problem statement    │
└────────────────────────────────────┘

┌────────────────────────────────────┐
│  BOUNDED                           │
│  - Explicit appetite (time budget) │
│  - Clear no-gos (what's out)       │
│  - Risks identified                │
└────────────────────────────────────┘
```

**See full framework:** `skills/shape-up/references/methodology.md`

### The Four Shaping Steps

**Step 1: Set Boundaries**
- Choose an appetite (Small Batch: 1-2 weeks, Big Batch: 6 weeks)
- Narrow the problem (dig past surface requests)
- Answer: "How much is this worth?" not "How long will it take?"

**Step 2: Find the Elements**
- Breadboard the solution (places, affordances, connections)
- Fat marker sketches if visual arrangement matters
- Keep it rough but solved

**Step 3: Address Risks**
- Walk through use cases slowly
- Identify rabbit holes (hidden complexity)
- Patch or cut risky parts
- Declare explicit no-gos

**Step 4: Write the Pitch**
- Five ingredients: Problem, Appetite, Solution, Rabbit Holes, No-Gos
- Ready for the betting table

**See techniques:** `skills/shape-up/references/techniques.md`

### The Pitch Format

Every pitch needs all five components:

```markdown
# [Feature Name]

## Problem
[Specific situation that doesn't work. Story or scenario. Show the friction.]

## Appetite
[Small Batch (1-2 weeks) or Big Batch (6 weeks)]

## Solution
[Breadboards and/or fat marker sketches. Main elements and how they connect.]

## Rabbit Holes
[Technical unknowns, integration challenges, scope creep risks]

## No-Gos
[Features we won't include, use cases we won't handle, platforms we won't support]
```

**See template:** `skills/shape-up/references/pitch-template.md`

### Betting Table vs. Backlog

**Traditional backlog:**
- ❌ Infinite list of ideas
- ❌ Items sit forever, get stale
- ❌ No real prioritization
- ❌ Guilt about not building everything

**Shape Up betting table:**
- ✅ Pitches compete each cycle
- ✅ Fresh look every time
- ✅ Items not bet on are discarded (can be re-pitched later)
- ✅ No backlog guilt

**Key principle:** If it matters, it will come back. If it doesn't come back, it didn't matter.

### Circuit Breaker

**The rule:** If it doesn't ship in the appetite, it doesn't ship.

**Why this works:**
- Forces scope discipline during building
- Prevents projects from dragging on
- Teams learn to make trade-offs
- No "just one more week" syndrome

**If a project gets cut:**
- It's not automatic continuation
- Goes back to shaping (what went wrong?)
- May or may not get re-bet

## Core Principles

### 1. Fixed Time, Variable Scope

"Instead of asking 'how long will this take?', ask 'how much time is this worth?'"

The appetite is a constraint, not an estimate. Scope flexes to fit the time, not the other way around.

### 2. Appetite Over Estimates

"Estimates assume perfect knowledge. Appetite accepts uncertainty."

Small Batch (1-2 weeks):
- Well-understood problems
- Limited scope
- Quick wins

Big Batch (6 weeks):
- Larger features
- More unknowns
- New capabilities

### 3. Shaped Work is Rough but Solved

"If it's too vague, the team won't know where to start. If it's too detailed, the team can't use their judgment."

The sweet spot: main elements are connected, but room for creativity remains.

### 4. Teams Get Full Responsibility

"Don't manage tasks, define appetite and boundaries. Let the team figure out how."

After betting:
- Pitch provides boundaries, not instructions
- Team owns execution
- Daily check-ins, not daily standups

### 5. De-risk Before Building

"Find the rabbit holes during shaping, not during building."

Questions to ask:
- Does this require unprecedented technical work?
- Are we assuming things fit together without validation?
- Is a hard decision deferred to the team?

## Two Product Modes

### Established Product Mode

**When to use:** Existing product with users, revenue, and reputation at stake

**Full rigor applies:**
- Strict appetites (1-2 weeks or 6 weeks exactly)
- Circuit breaker enforced (auto-cancel at deadline)
- Pitches compete at betting table
- Output ready for production

### New Product Mode

**When to use:** New product, exploration phase, validating direction

**Looser constraints:**
- Flexible appetite (whatever makes sense)
- Goal is learning, not shipping
- Circuit breaker less strict
- Pitch as working document, not contract

**Key insight:** Shape Up was designed for established products. New products need more iteration room.

## How AI Changes Shaping

### Faster Prototyping

**Traditional shaping:**
- Breadboards and sketches only
- Can't test assumptions easily
- Risk assessment is theoretical

**AI-era shaping:**
- Prototype competing solutions quickly
- Validate technical feasibility before betting
- De-risk with working code, not speculation

### Shaping Still Matters

**Why AI doesn't replace shaping:**
- AI can build fast, but building the wrong thing fast is worse
- Appetite and boundaries still essential
- Rabbit holes still need identification
- No-gos still need to be explicit

"The faster you can build, the more important it is to know what to build."

## When to Use Shape Up

### Use this framework when:
- Planning multi-week product work
- Need to ship with deadlines
- Want to avoid scope creep
- Teams capable of autonomous execution
- Leadership willing to let teams own execution

### Works especially well for:
- Product teams at established companies
- Cycle-based planning (6-8 week cycles)
- Teams with clear ownership
- Organizations tired of Agile theater

### Less suitable for:
- Brand new products (use New Product Mode)
- Maintenance/bug work (use kanban)
- Agency/client work with fixed requirements
- Teams not empowered to make scope decisions

## Integration with Other Frameworks

**Combines well with:**

**Now-Next-Later (Janna Bastow):**
- LATER items → shaping candidates
- Shaped pitches → NEXT items
- Bet pitches → NOW items
- Shipped work → Done

**Four Risks (Marty Cagan):**
- Use Four Risks during shaping (Step 3: Address Risks)
- Rabbit holes map to feasibility and viability risks
- No-gos clarify what value/usability trade-offs you're making

**Continuous Discovery (Teresa Torres):**
- Discovery identifies problems worth solving
- Shaping takes validated problems and designs solutions
- Pitches are shaped solutions to validated problems

**Prototype-First Development:**
- Prototype during shaping to de-risk
- Prototype during building for quick vertical slices
- Working software beats documentation

## Common Objections Answered

### "Six weeks is too long/short"

**Answer:** Adjust for your context, but keep the principle. The point is:
- Fixed, meaningful time boxes
- Not infinite sprints
- Enough time for significant work

### "We can't just cut projects"

**Answer:** The circuit breaker prevents worse outcomes:
- Projects that drag on forever
- Teams demoralized by endless work
- Opportunity cost of not moving on

### "Leadership wants estimates"

**Answer:** Give them appetite + confidence:
- "This is a Big Batch (6 weeks) with high confidence"
- "This is a Small Batch (1-2 weeks) with some technical risk"

Better than false precision.

### "What about bugs and maintenance?"

**Answer:** Shape Up is for feature work. Use kanban for:
- Bug fixes
- Maintenance tasks
- Support escalations

Cool-down (time between cycles) handles small stuff.

## Quotes to Remember

> "Appetite drives scope, not the reverse."

> "If it doesn't ship in the appetite, it doesn't ship."

> "Shaped work is rough but solved."

> "The best work happens when teams have clear boundaries and full responsibility."

> "Backlogs are where ideas go to die. Pitches compete for cycles."

> "Fixed time, variable scope. Not fixed scope, variable time."

## Further Learning

### Essential Reading
- **"Shape Up"** - Free online book: [basecamp.com/shapeup](https://basecamp.com/shapeup)
- **"New Product Mode"** - Brian Bailey's synthesis: [world.hey.com/bb/new-product-mode](https://world.hey.com/bb/new-product-mode-48a43806)
- **Felt Presence Blog** - Ryan's writing: [feltpresence.com](https://feltpresence.com)

### Background
- 17 years at Basecamp (formerly 37signals)
- Led strategy and product development
- Shape Up emerged from real practice, not theory

### Where to Follow
- Twitter/X: [@rjs](https://twitter.com/rjs)
- Felt Presence: [feltpresence.com](https://feltpresence.com)
- Shape Up book (free): [basecamp.com/shapeup](https://basecamp.com/shapeup)

## Key Takeaways

1. **Appetite over estimates** - Decide time budget first, shape to fit
2. **Rough but solved** - Main elements connected, room for creativity
3. **De-risk before building** - Find rabbit holes during shaping
4. **Fixed time, variable scope** - Trade scope for time, not the reverse
5. **Circuit breaker** - If it doesn't ship in appetite, it doesn't ship
6. **Betting table, not backlog** - Pitches compete, no infinite lists
7. **Full team responsibility** - Boundaries, not instructions

---

**In the context of this PM Thought Partner:**

Ryan's framework helps you ship meaningful work without scope creep.

Use it to:
- Shape work at the right level of abstraction (rough but solved)
- Set clear boundaries (appetite, no-gos, rabbit holes)
- Avoid estimate theater (appetite accepts uncertainty)
- Empower teams (boundaries, not instructions)
- Ship on time (circuit breaker forces trade-offs)

Combined with discovery (Teresa), roadmapping (Janna), and AI prototyping, you have: validated problems → shaped solutions → focused execution → shipped work.
