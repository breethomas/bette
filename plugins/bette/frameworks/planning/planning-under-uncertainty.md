# Planning Under Uncertainty

Most planning frameworks assume you know the direction. This one is for when you don't.

---

## Real Options Thinking

Every decision is a bet. Some bets buy information. Others buy commitment.

**Preserve optionality.** The cost of keeping an option open is usually lower than the cost of committing early and being wrong. Small, reversible investments that teach you something are almost always worth making.

The question is not "what should we build?" It is "what's the cheapest way to learn whether we should build it?"

- Run a spike before committing a team
- Ship a manual version before automating
- Test with 5 users before designing for 5,000
- Buy time with a workaround while the real answer emerges

**The trap:** optionality becomes indecision. Options have expiration dates. If you are paying to keep an option open and not learning anything new, you are just stalling.

---

## Reversible vs Irreversible Decisions

Bezos's one-way/two-way door framework.

**Two-way doors (most decisions):** Make them fast. Reverse if wrong. The cost of delay usually exceeds the cost of a bad call. Staffing a spike, choosing a technical approach for a prototype, running an experiment, setting a meeting cadence.

**One-way doors (few decisions):** Slow down. Get more input. These are hard or impossible to undo. Shutting down a product line, signing a multi-year contract, making a public commitment, changing pricing architecture.

The failure mode is treating two-way doors like one-way doors. This looks like extensive analysis, committee review, and months of deliberation on decisions that could be tested in a week.

---

## Scenario Planning

When the future depends on factors outside your control, map the possibility space.

1. Identify the two most critical uncertainties (things that matter AND that you cannot predict)
2. Build a 2x2 matrix
3. Name each quadrant -- make it memorable
4. For each quadrant: what would you do? What bets would you place?
5. Look across all four: what actions are good regardless of which scenario plays out?

**Robust strategies** work across multiple scenarios. **Contingent strategies** bet on one scenario being right. Prefer robust when uncertainty is high. Go contingent when you have strong signal.

Keep the matrix simple. If you need more than a whiteboard to explain it, you have overcomplicated it.

---

## Assumption Mapping

Every plan rests on assumptions. Most of them are invisible.

1. List what must be true for your plan to work
2. Rate each assumption on two axes:
   - **How critical** -- if this is wrong, does the plan fail or just get harder?
   - **How uncertain** -- do you have evidence, or is this a guess?
3. Plot them: critical + uncertain assumptions go in the top-right quadrant
4. Test those first

The top-right quadrant is where plans die. A beautifully executed plan built on a wrong critical assumption is worse than a rough plan built on validated ones.

**Common hidden assumptions:**
- "Customers will change their behavior"
- "The data exists and is clean enough"
- "Engineering can build this in the time we have"
- "Leadership will stay aligned on the direction"

---

## When to Commit

Exploration is not free. At some point you stop learning and start building.

**Signals it is time to commit:**
- New experiments are confirming what you already believe (diminishing information returns)
- The team is ready and losing energy waiting
- A market window is closing
- You have enough conviction to defend the direction, even if you cannot prove it

**Signals it is too early to commit:**
- Your critical assumptions are untested
- The team cannot articulate the strategy in one sentence
- Key stakeholders have fundamentally different mental models of the problem
- You are choosing between options you do not yet understand

**The commitment spectrum:** You do not have to go from "exploring" to "all in." Increase commitment gradually. Staff one person, then a pair, then a team. Ship to 10 users, then 100, then everyone. Each step is a chance to validate or course-correct.

---

## Putting It Together

When facing genuine uncertainty:

1. Map your assumptions -- find the critical unknowns
2. Design cheap experiments to test them (real options)
3. Make reversible decisions fast, irreversible ones slowly
4. Run scenarios on the factors you cannot control
5. Commit when information returns diminish and the cost of delay exceeds the cost of being wrong
