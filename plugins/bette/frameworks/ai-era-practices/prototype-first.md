# Prototype-First Development

**Category:** AI-Era Practices
**Last Updated:** January 2025

## Overview

The AI era has fundamentally changed product development. You can now build working prototypes in hours, not weeks. This shifts the optimal strategy from "document first, build later" to "prototype first, decide with evidence."

**The core shift:**
- **Old:** Write comprehensive specs → Wait for eng → Build → Learn (weeks/months)
- **New:** Prototype in hours → Gather feedback → Learn → Decide → Build for real (days)

## Why Prototype First

### 1. Speed Compresses Decision Cycles

When you can build a prototype in an afternoon, the economics of validation completely change:

**Traditional approach:**
- Week 1-2: Write verbose PRD, gather requirements
- Week 3-4: Get eng feedback, refine specs
- Week 5-8: Build
- Week 9+: Learn it's not what was needed

**Prototype-first approach:**
- Day 1: Build prototype (2-4 hours)
- Day 2-3: Gather feedback (internal team, stakeholders, and when appropriate, users)
- Day 4: Decide if this is worth building for real
- Week 2+: Build production version (if validated)

**The difference:** Learn in days instead of weeks.

### 2. Prototypes Are Better Communication

**What works better:**
- Showing stakeholders a working prototype
- Aligning team on interaction patterns
- Engineers seeing the intended experience
- Designers exploring feasibility of concepts

**vs.**
- Lengthy PRD that gets skimmed
- Mockups that leave interaction unclear
- Spec documents with edge cases missed
- Abstract discussions without shared understanding

**As one engineer noted:** "Code you generated in an afternoon? You haven't invested your ego in it" - making it easier to objectively evaluate and pivot.

### 3. Throwaway Code Is an Asset, Not Debt

With AI refactoring code instantly:
- Technical debt is cheap to fix
- "Doing it messy first" has minimal cost
- The real scarce resource is learning what to build, not development time

**Old thinking:** "We can't afford to build it wrong"
**New reality:** "We can't afford NOT to prototype and learn"

### 4. The "Work Behind the Work" Is Dead

AI can now:
- Sync changes across tools automatically
- Generate documentation from prototypes
- Create Linear issues from working code
- Keep specs in sync with reality

No more manual coordination overhead.

## Types of Prototyping

### Concept Prototypes
**Purpose:** Explore ideas, align stakeholders, validate direction with team
**Tools:** v0, Bolt, Replit, Lovable, Claude Artifacts
**Characteristics:**
- Standalone (not connected to your codebase)
- Built in hours
- Disposable by design
- Focus on interaction and experience

**When to use:**
- **Internal alignment:** Stakeholders, designers, engineers
- **Problem exploration:** What should this even look like?
- **Design validation:** Does this interaction pattern work?
- **0-to-1 products:** When you're building something new

**Important context:**
- **Existing products:** Testing concept prototypes with users can be problematic if it doesn't match current UX
- **Better for alignment:** Most valuable for getting internal teams on the same page about the problem and solution
- **User testing:** More feasible for greenfield/new products than iterating existing ones

### Implementation Prototypes
**Purpose:** Scope feasibility, work with engineers, understand complexity
**Tools:** Cursor, Claude Code, Windsurf, Warp (terminal-based development)
**Characteristics:**
- Connected to real codebase
- Understands existing architecture
- Realistic technical constraints
- May become production code

**When to use:**
- Scoping with engineering team
- Understanding what's possible in your system
- Exploring technical approaches
- Planning implementation

## The Prototyping Tool Landscape

### Standalone Prototyping Tools

**v0 (Vercel)**
- Strength: Beautiful UI by default, pre-built components
- Best for: Stakeholder demos that need polish
- Limitation: No built-in backend/database

**Bolt**
- Strength: Fastest iteration, browser-based
- Best for: Rapid exploration of interaction patterns
- Limitation: No data persistence

**Replit**
- Strength: Full-stack with built-in DB and auth
- Best for: Prototypes that might scale to production
- Limitation: Slower than Bolt

**Lovable**
- Strength: Most accessible for non-technical PMs
- Best for: PMs who aren't comfortable coding
- Limitation: Less polished output

**Claude Artifacts / ChatGPT Canvas**
- Strength: Free, quick one-off prototypes
- Best for: Personal exploration, simple demos
- Limitation: Limited interactivity

### Codebase-Aware Tools

**Cursor**
- Understands your entire codebase
- Best for: Implementation planning with eng team

**Claude Code**
- Deep codebase context
- Best for: Scoping and feasibility exploration

**Windsurf**
- Similar to Cursor
- Best for: Developers building production features

**Warp**
- Modern terminal (founded by Zach Lloyd, former Google Sheets lead)
- Best for: Developer-focused workflows, AI-native terminal experience
- Note: Reflects modern dev tooling philosophy - reimagining foundational tools

## How to Choose a Tool

**Don't overthink it.** Pick one and start. Your context matters more than the perfect tool choice.

### Consider your context:

**1. "Am I exploring a concept or planning implementation?"**
- Concept → Standalone tools (v0, Bolt, Replit, Lovable)
- Implementation → Codebase-aware (Cursor, Claude Code)

**2. "Who needs to see this?"**
- Stakeholders/execs → v0 (polish matters)
- Internal team (alignment) → Bolt (speed matters)
- Engineers → Cursor/Claude Code (reality matters)

**3. "Do I need a backend?"**
- No (UI/UX only) → v0 or Bolt
- Yes (simple) → Replit or Bolt + Supabase
- Yes (complex/existing systems) → Cursor/Claude Code

**4. "How technical am I?"**
- Not technical → Lovable or Claude Artifacts
- Somewhat technical → Bolt or Replit
- Very technical → Cursor or Windsurf

**5. "What's my budget?"**
- Free → Claude Artifacts, ChatGPT
- Paid → Pick one tool that fits your workflow

**6. "Is this a new product or existing?"**
- 0-to-1 / greenfield → More flexibility in testing
- Existing product → Focus on internal alignment first

## The Modern PM Workflow

From Aakash Gupta's research, prototyping now happens at EVERY stage:

```
IDEATION
├─ Old: <5% prototyping (mostly docs)
└─ New: Prototype to think, not just document

DESIGN EXPLORATION
├─ Old: ~75% prototyping (Figma mockups)
└─ New: Working prototypes, not static mocks

SCOPING
├─ Old: Specs and estimates
└─ New: Build in codebase to understand complexity

ENGINEERING HANDOFF
├─ Old: PRD + mockups
└─ New: Working prototype + implementation plan
```

**The shift:** Continuous prototyping throughout, not a single phase.

## The Hybrid Workflow

Emerging best practice: **Start standalone, migrate to codebase if validated**

**Example flow:**
1. **Day 1-2:** Build concept prototype in Bolt (2 hours)
2. **Day 3-4:** Review internally with stakeholders, designers, eng
3. **Week 2:** If aligned, work with eng in Cursor to scope implementation
4. **Week 3+:** Eng builds production version (proper testing, architecture)

**Why this works:**
- Align fast with standalone tools
- Only invest in production if direction is validated
- Engineers see working example, not just specs

## When to Throw Away vs. Scale

### Throw away when:
- ✅ Prototype was for alignment/exploration
- ✅ Production needs proper architecture
- ✅ Security/performance critical
- ✅ Needs to integrate with complex systems

### Consider scaling when:
- ✅ Simple CRUD or workflow tool
- ✅ Internal tool, lower quality bar
- ✅ Built in Replit with proper DB/auth
- ✅ Prototype validated and eng comfortable with code

**Default stance:** Prototypes are disposable. That's their power.

## Integration with Discovery Frameworks

### Teresa Torres' Continuous Discovery
- **Traditional:** Weekly interviews → Document insights → Plan features
- **Prototype-first:** Weekly interviews → Prototype solutions → Gather feedback → Decide

**Opportunity Solution Trees with prototyping:**
```
Outcome: Increase activation 40% → 60%
    |
Opportunity: "Users don't know what to do first"
    |
Solutions to prototype:
├─ Interactive tour → Prototype in Bolt (2 hrs)
├─ Checklist widget → Prototype in v0 (2 hrs)
└─ AI setup assistant → Prototype in Replit (4 hrs)
    |
Review with team → Pick direction based on feasibility & alignment
```

### Marty Cagan's Four Risks

Use prototypes to address each risk:

**Value Risk:**
- Prototype the concept
- Share with stakeholders/team
- For new products: Test with target users
- For existing products: Align internally first

**Usability Risk:**
- Build clickable prototype
- Review interaction patterns with team
- Iterate in hours based on feedback

**Feasibility Risk:**
- Build in Cursor/Claude Code
- Understand complexity in real codebase
- Get eng estimate based on working example

**Business Viability Risk:**
- Prototype business model implications
- Show to stakeholders
- Explore pricing/positioning concepts

## Context Matters: 0-to-1 vs. Existing Products

### Building Something New (0-to-1)
**More flexibility:**
- Can test prototypes with potential users
- No existing UX to conflict with
- Faster validation cycles possible

**Approach:**
- Build concept prototype
- Test with target users (when appropriate)
- Iterate based on feedback
- Build production version

### Iterating Existing Products
**More constraints:**
- Concept prototypes may confuse users if they don't match current product
- Better to align internally first (stakeholders, designers, eng)
- User testing often requires higher fidelity

**Approach:**
- Build concept prototype for internal alignment
- Get team consensus on direction
- Build higher-fidelity prototype (or use existing product) for user testing
- Then build production version

**Key insight:** The purpose of prototyping shifts based on your product maturity.

## Common Objections Answered

### "We don't have time to prototype"
**Response:** You don't have time NOT to. Building the wrong thing takes way longer than prototyping first.

**Math:**
- 2 hours to prototype + 2 days feedback = Learning before Week 1
- vs. 4 weeks building → Learning it's wrong → Rebuild = Months wasted

### "Our eng team doesn't like throwaway code"
**Response:** They'll like rebuilding the wrong thing even less.

**Better conversation:**
- "Here's a working prototype the team aligned on"
- "Can we scope building this properly?"
- vs. "Here's a lengthy spec, please estimate"

### "Prototypes won't have proper architecture"
**Response:** Correct. That's the point. Validate direction BEFORE investing in proper architecture.

Prototypes answer: "Should we build this?"
Production code answers: "How do we build this right?"

### "We need stakeholder buy-in first"
**Response:** Prototypes GET you stakeholder buy-in faster than decks.

Show > Tell

### "What if the prototype sets unrealistic expectations?"
**Response:** Better to learn constraints early than after commitments are made.

- Prototype reveals what's hard → Adjust approach
- Team aligns on feasibility → Realistic planning

## Key Questions to Ask

### Before prototyping:
- "What am I trying to learn?"
- "Who needs to see this?"
- "Is this about the concept or the implementation?"
- "Is this a new product or iterating an existing one?"
- "How much time do I have?" (Pick tool accordingly)

### During prototyping:
- "Is this realistic enough to get useful feedback?"
- "What assumptions am I testing?"
- "Who's the right audience for this fidelity?"

### After prototyping:
- "What did I learn?"
- "Does this validate the direction?"
- "Should we build this for real?"
- "What changed from my original assumptions?"
- "Who else needs to see this before we commit?"

## Best Practices

### 1. Start Small
- Don't prototype everything
- Focus on riskiest assumptions
- One core flow, not entire product

### 2. Timebox It
- Set a limit: 2-4 hours max
- If taking longer, you're overbuilding
- Remember: It's disposable

### 3. Know Your Audience
- Internal alignment: Lower fidelity is fine
- Stakeholders: Polish matters
- Engineers: Functionality matters more than polish
- Users (when appropriate): Context-dependent fidelity

### 4. Document Learnings, Not the Prototype
- Write down what you learned
- Capture feedback and reactions
- Note what to change
- Then throw away the prototype

### 5. Involve Engineers Early
- Show them the prototype
- "Is this feasible?"
- "How would you build this?"
- Get their input before committing

## Real-World Example

**Scenario:** SaaS onboarding is confusing, activation is 40%

**Old approach:**
- Week 1: Write PRD on new onboarding flow
- Week 2: Designer creates mockups
- Week 3-4: Eng feedback, revisions
- Week 5-8: Build
- Week 9: Launch, measure results
- Result: 6-8 weeks to learn if it works

**Prototype-first approach:**
- Monday AM: Build 3 different onboarding prototypes in Bolt (6 hours total)
  - Interactive tour
  - Checklist widget
  - AI assistant
- Tuesday: Review with design + eng team
- Wednesday: Tour approach wins consensus, scope implementation
- Thursday: Work with eng in Cursor to validate in codebase
- Week 2-3: Build production version of agreed approach
- Result: 2 weeks to aligned solution

**The difference:**
- Explored 3 approaches instead of guessing
- Got team alignment before building
- Eng builds with clear direction, not assumptions
- 4-6 weeks saved

## Resources

**Tools mentioned:**
- v0.dev
- Bolt.new
- Replit
- Lovable.dev
- Claude.ai (Artifacts)
- Cursor.sh
- Claude Code
- Windsurf
- Warp (modern terminal)

**Further reading:**
- Aakash Gupta: "AI Prototyping Tutorial" (tool comparison)
- Bret Horsting: "Claude Code is unreasonably good at building MVPs"
- Nikunj Kothari: "The work behind the work is dead"

**Grounded in:**
- Teresa Torres: Continuous Discovery (test assumptions fast)
- Marty Cagan: Four Risks (prototype to de-risk)
- Linear Method: Build with momentum, ship continuously

---

**Remember:** The goal isn't perfect prototypes. It's learning fast and building alignment.

Prototype in hours. Gather feedback. Learn from the right audience. Decide with evidence. Build the right thing.
