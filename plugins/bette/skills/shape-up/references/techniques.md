# Shape Up Techniques

**Author:** Ryan Singer (Basecamp)
**Source:** [Shape Up](https://basecamp.com/shapeup)
**Category:** Shaping / Planning
**Last Updated:** January 2026

---

## The Four Shaping Steps

1. **Set Boundaries** - Define appetite and problem
2. **Find the Elements** - Sketch the solution
3. **Address Risks** - Identify and patch rabbit holes
4. **Write the Pitch** - Package for betting

---

## Step 1: Set Boundaries

### Choosing an Appetite

**Small Batch (1-2 weeks):**
- Well-understood problems
- Limited scope
- Quick wins
- Bug fixes with clear solutions

**Big Batch (6 weeks):**
- Larger features
- More unknowns to uncover
- New capabilities
- Meaningful user value

**The question to ask:** "How much is this problem worth solving?"

Not: "How long will this take?"

### Narrowing the Problem

Surface-level requests hide the real problem:

**Bad:** "Customers want a calendar"
**Better:** "Customers can't see upcoming events at a glance"
**Best:** "Customers miss appointments because they don't check the Events page"

**Technique:** Ask "why" until you hit the real friction:
- Why do they want a calendar? → To see upcoming events
- Why can't they see them now? → Events page requires navigation
- Why don't they navigate? → Too many clicks, forget to check

**Now you can shape:** Maybe it's not a calendar. Maybe it's a dashboard widget.

---

## Step 2: Find the Elements

### Breadboarding

Borrowed from electrical engineering - design at the right abstraction level.

**Three components:**
- **Places** - Screens, dialogs, menus (where users go)
- **Affordances** - Buttons, fields, links (what users can do)
- **Connection lines** - How affordances move users between places

**Example: Invoice Autopay**
```
[Invoice Screen]
    |
    └── "Enable Autopay" link
            |
            ↓
[Autopay Setup Dialog]
    |
    ├── Account dropdown (select payment method)
    ├── "Save" button → [Invoice Screen] (with autopay badge)
    └── "Cancel" button → [Invoice Screen]
```

**Key principle:** Use words for everything instead of pictures. The important things are the components and their connections.

### Fat Marker Sketches

When visual arrangement matters, sketch deliberately rough:

**Rules:**
- Use thick markers (Sharpie, not fine-tip)
- Or large brush size on iPad (20+ pt)
- Can't add detail = won't add detail
- Focus on relationships, not refinement

**When to use:**
- Layout decisions matter to the solution
- Need to communicate spatial relationships
- Breadboard isn't capturing the key idea

**When NOT to use:**
- Solution is about workflow, not visuals
- Breadboard captures it fine
- You're tempted to make it pretty

### Moving at the Right Speed

**Requirements for good shaping sessions:**
1. Right people in the room (or solo)
2. Shared context (no lengthy explanations needed)
3. Whiteboard or paper ready
4. No distractions

**What to focus on:**
- Where does this fit in the current system?
- How do users access it?
- What are the key components?
- Where does it lead?

**What to avoid:**
- Pixel-perfect layouts
- Exact copy/labels
- Color, typography, visual style
- Edge cases (save those for de-risking)

---

## Step 3: Address Risks (De-risking)

### What Are Rabbit Holes?

Hidden complexities that could derail a project:
- Technical unknowns
- Unresolved design challenges
- Misunderstood interdependencies
- Scope that looks simple but isn't

**The danger:** Fat-tailed probability distributions. Projects can take 3x+ longer if rabbit holes aren't identified.

### De-risking Techniques

**1. Walk through use cases slowly**

Play out the user journey step by step:
- User lands here...
- Clicks this...
- Sees what?
- Then what?

**Look for:**
- Missing screens/states
- Unclear transitions
- Assumed functionality that doesn't exist
- Edge cases that break the flow

**2. Question your assumptions**

Ask yourself:
- Does this require unprecedented technical work?
- Are parts assumed to fit together without validation?
- Does a design solution exist that we couldn't develop ourselves?
- Are hard decisions deferred to the team?

If any answer is "yes" → dig deeper or patch it.

**3. Patch problems proactively**

Make trade-offs during shaping, not during building:

**Example:** Completed items in to-do groups
- Ideal solution: Elegant collapsible sections
- Rabbit hole: Complex interaction design
- Patch: Just append completed items at bottom with strikethrough
- Result: Simpler to build, still solves the problem

**4. Declare explicit boundaries**

Mark use cases as "out of bounds":
- "This won't handle bulk operations"
- "Mobile is out of scope"
- "We're not building the admin view"

Write these down. They become no-gos in the pitch.

**5. Cut nice-to-haves early**

Remove before you start, not when you're running out of time:
- Color-coding? Cut it.
- Drag-and-drop? Cut it.
- Undo? Cut it (maybe).

**The test:** Could we ship without this and still solve the problem?

**6. Consult technical experts**

Frame it as a potential bet:
- "We're thinking about betting on X..."
- "Is this possible in 6 weeks?"
- "What's the riskiest part?"

Emphasize the appetite constraint. You're not asking "is it possible?" - you're asking "is it possible in this timeframe?"

---

## Step 4: Write the Pitch

See [pitch-template.md](pitch-template.md) for the five ingredients and examples.

---

## Building Techniques

These techniques are used by teams during the cycle, but shapers should understand them:

### Vertical Slices

Integrate one small piece end-to-end first:
- Something clickable within the first week
- Proves the concept works
- Front-end AND back-end connected
- "Done-done" = functions end-to-end

**Why it matters:** Prevents the situation where designers have screens and programmers have logic but nothing works together.

### Scopes (Not Tasks)

Organize work into integrated slices:
- Combine frontend + backend
- Completable independently in a few days
- Organize by structure, not by person
- Emerge through hands-on work

**Example scopes for "Invoice Autopay":**
- Enable autopay on a single invoice
- Handle failed payments
- Show autopay status on invoice list
- Send autopay confirmation email

Each scope has design AND programming work. Each can ship independently.

### Hill Charts

Visualize progress without estimates:

```
        ▲
       /|\        Figuring      Executing
      / | \       things out    the plan
     /  |  \
    /   |   \
   /    |    \
  /     |     \
 /      |      \
────────┼────────
     UPHILL   DOWNHILL
```

- **Uphill:** Uncertainty, unknowns, problem-solving
- **Downhill:** Certainty, confidence, clear path

**How to use:**
- Plot each scope as a dot on the hill
- Move dots as work progresses
- Stuck scopes (not moving) signal problems
- Riskier work should go uphill first

### Scope Hammering

When time runs short, cut scope aggressively:

**Questions to ask:**
- "Is this a must-have?"
- "Could we ship without this?"
- "What's the baseline? (what customers have today)"

**Compare down, not up:**
- Don't compare to the ideal you imagined
- Compare to what customers have now
- Even imperfect improvement > no improvement

---

## Common Shaping Mistakes

### Too Abstract
- "We need better reporting"
- "Customers want more flexibility"
- "Make it faster"

**Fix:** Dig into specific friction, specific users, specific scenarios.

### Too Concrete
- Full wireframes
- Detailed specs
- Every edge case covered

**Fix:** Step back to breadboards and fat markers. Leave room for the team.

### Skipping De-risking
- "The team will figure it out"
- "It's probably fine"
- "We don't have time to dig deeper"

**Fix:** Slow down. Walk through use cases. Consult experts. Patch or cut.

### Wrong Appetite
- Forcing big ideas into small batches
- Giving 6 weeks to 2-week problems
- Not questioning whether the problem is worth solving

**Fix:** Start with appetite as constraint. Shape to fit, or don't shape at all.

---

## Resources

- [Shape Up - Chapter 4: Find the Elements](https://basecamp.com/shapeup/1.3-chapter-04)
- [Shape Up - Chapter 5: Risks and Rabbit Holes](https://basecamp.com/shapeup/1.4-chapter-05)
- [Shape Up - Chapter 12: Map the Scopes](https://basecamp.com/shapeup/3.3-chapter-12)
- [Shape Up - Chapter 13: Show Progress](https://basecamp.com/shapeup/3.4-chapter-13)
