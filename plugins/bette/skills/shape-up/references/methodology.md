# Shape Up Methodology

**Author:** Ryan Singer (Basecamp)
**Source:** [Shape Up: Stop Running in Circles and Ship Work that Matters](https://basecamp.com/shapeup)
**Category:** Planning / Execution
**Last Updated:** January 2026

---

## Core Philosophy

**Fixed time, variable scope.**

This is the fundamental inversion from traditional estimation:

| Traditional | Shape Up |
|-------------|----------|
| Estimates start with design, end with a number | Appetites start with a number, end with a design |
| Scope is fixed, time is variable | Time is fixed, scope is variable |
| "How long will this take?" | "What can we build in 6 weeks?" |

**Why this works:** Deadlines force necessary decisions about what truly matters. When time is fixed, teams make trade-offs instead of expanding scope indefinitely.

---

## The Three Phases

```
┌─────────────────────────────────────────────────────────────────┐
│  SHAPING (Senior staff, pre-cycle)                              │
│  Define work at right abstraction - rough, solved, bounded      │
│  Output: Pitch                                                  │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│  BETTING (Leadership, during cool-down)                         │
│  Review pitches, commit teams to cycle work                     │
│  Output: Cycle plan                                             │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│  BUILDING (Teams, during cycle)                                 │
│  Execute with autonomy, ship by end of cycle                    │
│  Output: Deployed feature                                       │
└─────────────────────────────────────────────────────────────────┘
```

---

## Properties of Shaped Work

Work is ready for betting when it has three properties:

### 1. Rough
- Visibly unfinished
- Leaves room for designer/developer creativity
- Not wireframes or detailed mockups
- Uses breadboards and fat marker sketches

### 2. Solved
- Main elements are connected
- Clear direction on approach
- Core interactions figured out
- But allows for surprises in execution

### 3. Bounded
- Indicates what NOT to do
- Explicit appetite (time constraint)
- Clear no-gos defined
- Scope is deliberately limited

**The abstraction problem:**
- **Wireframes are too concrete** - they constrain designers and hide complexity
- **Words are too abstract** - "add a calendar" leaves teams without direction
- **Shape Up lives in between** - concrete enough to guide, rough enough to allow creativity

---

## Appetite: The Time Budget

Appetite is NOT an estimate. It's a creative constraint.

| Batch Size | Duration | Team Size | Use When |
|------------|----------|-----------|----------|
| Small batch | 1-2 weeks | 1-2 people | Well-understood problems, quick wins |
| Big batch | 6 weeks | 1-2 people | Larger features, more unknowns |

**Key insight:** You don't estimate how long something will take, then ask for that time. You decide how much time something is worth, then shape to fit.

---

## The Circuit Breaker

Projects that don't ship within their cycle face **cancellation by default**.

**Why this matters:**
- Prevents runaway projects
- Forces better shaping upfront
- Motivates teams to make hard scope decisions
- Maximum downside is one cycle of investment

**If a project doesn't ship:**
1. It doesn't automatically continue
2. Must be re-pitched if still important
3. Gets re-shaped with learnings from failed attempt
4. Competes with fresh ideas at next betting table

---

## Why No Backlogs

Shape Up explicitly rejects backlogs:

**Problems with backlogs:**
- Create psychological burden (perpetually behind)
- Constant grooming wastes time
- Old ideas crowd out fresh thinking
- False sense of organization

**Instead:**
- Important ideas naturally resurface
- Decentralized lists per department (support tracks bugs, product tracks ideas)
- Pitches are created fresh when needed
- Rejected pitches released without tracking

**The test:** When's the last time you forgot a really great, inspiring idea?

---

## Bets, Not Plans

The betting table replaces traditional planning:

| Traditional Planning | Shape Up Betting |
|---------------------|------------------|
| Backlog grooming meetings | No backlog to groom |
| Sprint planning every 2 weeks | Betting table every 6 weeks |
| Committing to estimates | Committing to appetites |
| Features get "scheduled" | Features get "bet on" |

**A bet commits to:**
- **Payout:** Something meaningful ships within the cycle
- **Exclusivity:** Team gets uninterrupted time
- **Downside cap:** Maximum loss is the cycle duration

---

## Building: Teams Own Projects

**Assign projects, not tasks:**
- Teams receive entire shaped projects
- "Splitting the project into tasks up front is like putting the pitch through a paper shredder"
- Teams discover and define their own tasks
- Designers and programmers work together

**Done = Deployed:**
- Not just "finished" but actually shipped
- Testing and QA happen within the cycle
- No hand-off to another team

**The first 3 days:**
- Expect "radio silence" as teams get oriented
- Don't request status updates too early
- Teams discover "imagined vs discovered tasks"

---

## Two Product Modes

Shape Up adapts based on product maturity:

### Established Product Mode
- Fixed time, variable scope (full rigor)
- Clear appetites and betting tables
- Teams commit to shipping within defined cycles
- Circuit breaker enforced

### New Product Mode
- Variable time AND scope
- Optimize for optionality and speed
- Looser constraints, faster iteration
- Goal: validate concepts, not ship to customers yet

**Key insight:** New product mode only works with experienced practitioners who intuitively understand Shape Up principles and can self-regulate.

---

## Integration with Other Frameworks

**Complements:**
- **Now-Next-Later** - Betting table output maps to NOW, shaped pitches to NEXT
- **Four Risks** - Rabbit hole identification during shaping
- **Continuous Discovery** - Discovery informs what to shape

**Tension with:**
- **Sprint-based Scrum** - 6-week cycles vs 2-week sprints
- **Story points** - Appetites replace estimation
- **Centralized backlogs** - Shape Up rejects them

---

## When to Use Shape Up

**Good fit:**
- Teams that ship regularly
- Products with clear customer value
- Organizations that can protect team time
- Leadership willing to make bets (not just approve backlogs)

**Poor fit:**
- Heavy external dependencies
- Organizations that can't protect cycle time
- Teams without shaping capability
- Pure maintenance/support work

---

## Resources

- [Shape Up (free online book)](https://basecamp.com/shapeup)
- [New Product Mode - Brian Bailey](https://world.hey.com/bb/new-product-mode-48a43806)
- Ryan Singer on X/Twitter: [@rjs](https://twitter.com/rjs)
- Basecamp Blog: Product development insights
