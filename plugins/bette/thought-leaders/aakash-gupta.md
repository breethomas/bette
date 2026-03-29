# Aakash Gupta

**Focus:** PM frameworks, visual communication, stakeholder management, AI prototyping

**Known For:** Visual frameworks on LinkedIn, "One Minute PM" newsletter, making PM concepts accessible

## Core Philosophy

Aakash Gupta believes complex PM concepts should be simple to understand and immediately actionable. Through visual frameworks and clear communication, he makes product management accessible to PMs at all levels.

His approach combines framework thinking with practical application - showing not just WHAT to do, but HOW to do it, with templates and examples you can use immediately.

## Key Contributions

### The Three Gulfs (with Hamel Husain)

A diagnostic framework for why LLM pipelines fail. Three gaps between developer intent and pipeline behavior:

1. **Gulf of Comprehension** (Developer → Data): At scale, you can't inspect every input or output. The challenge is understanding your data distribution and failure patterns without examining every example.
2. **Gulf of Specification** (Developer → LLM Pipeline): Your intent is only loosely captured by your prompts. Unanswered questions (how detailed? what format? implicit vs explicit?) create ambiguity the model resolves on its own.
3. **Gulf of Generalization** (Data → LLM Pipeline): The model applies instructions incorrectly across diverse inputs. Even perfect prompts can't prevent this — no model generalizes perfectly.

**The fix:** Structured evaluation. Analyze → Measure → Improve, cycling continuously. Evals are to AI products what analytics are to traditional products.

### PM's Guide to Autoresearch

Adapted Karpathy's autoresearch pattern for PM work. The core insight: you define what "better" means, the agent runs 50+ rounds of optimization overnight.

Three requirements: (1) a clear metric — binary yes/no questions, not vibes, (2) automated measurement — an eval that runs without you, (3) one mutable file — the agent changes this and nothing else.

Works on any PM artifact: prompts, copy, email templates, skill files. "This is a new way to optimize anything."

### Ralph Wiggum Technique

A bash loop that runs Claude Code repeatedly, each iteration starting fresh (no context rot). Memory lives in three files: git commits (the code), progress.txt (learnings), prd.json (what's done, what's next). The agent picks a task, implements it, commits if tests pass, logs learnings, loops again. ~12 experiments per hour, ~100 overnight.

### Visual Frameworks Library

**The approach:** Turn complex PM concepts into clear, visual frameworks that are:
- Easy to understand at a glance
- Shareable (LinkedIn carousels, Twitter threads)
- Immediately applicable
- Template-ready

**Popular frameworks:**
- Product strategy canvases
- Prioritization matrices
- Stakeholder mapping
- Communication frameworks
- Roadmapping approaches

**Why it works:** Visual > Text for understanding and retention. A good framework diagram beats a 10-page doc.

### Stakeholder Communication

**Core insight:** Most PM work is communication and influence, not just building products.

**Frameworks cover:**
- How to communicate up (executives)
- How to communicate across (peers, other functions)
- How to communicate down (team)
- Presentation structures
- Meeting frameworks
- Update formats

**Key principle:** Match communication style to audience. What executives need is different from what engineers need.

### AI Prototyping Tutorial

**Recent contribution:** Comprehensive guide to AI prototyping tools for PMs.

**Compared four major tools:**
- **v0 (Vercel):** Beautiful UI, pre-built components
- **Bolt:** Fastest iteration, browser-based
- **Replit:** Full-stack with DB and auth
- **Lovable:** Most accessible for non-technical PMs

**Key insight:** The modern PM workflow now includes prototyping at EVERY stage (ideation, design, scoping, handoff) - not just during one phase.

**See framework:** `/frameworks/ai-era-practices/prototype-first.md`

### Product Sense Development

**Focus:** Help PMs develop better product intuition.

**Content areas:**
- Product teardowns (analyzing successful products)
- Decision frameworks (how to make better product calls)
- Pattern recognition (what works in different contexts)
- Case studies (real examples with analysis)

**Approach:** Learn by studying what works, then apply patterns to your context.

## Core Principles

### 1. Make it Visual

"A framework people can see is more powerful than one they have to read."

Visual communication:
- Faster to understand
- Easier to remember
- More shareable
- Creates common language

### 2. Stakeholder Management is Core PM Work

"You don't build products alone. You build them through influence and communication."

Most PM work is actually:
- Aligning stakeholders
- Communicating strategy
- Managing expectations
- Building consensus

Product skills matter, but communication skills determine success.

### 3. Frameworks Enable Speed

"Good frameworks help you make better decisions faster."

Don't reinvent the wheel. Use proven frameworks, adapt to your context, execute.

### 4. Learn from the Best

"Study successful products. Extract patterns. Apply to your work."

Product sense isn't innate. It's pattern recognition developed through study and practice.

### 5. Make it Actionable

"Understanding is useless without application."

Every framework should answer: "What do I do with this tomorrow?"

## Key Frameworks

### Stakeholder Communication Matrix

**Framework:** Map stakeholders by:
- Power (high/low influence)
- Interest (high/low engagement)

**Action:**
- High power, high interest → Manage closely
- High power, low interest → Keep satisfied
- Low power, high interest → Keep informed
- Low power, low interest → Monitor

**Application:** Determines communication frequency and format for each stakeholder.

### Product Strategy Canvas

**Framework:** One-page strategy that covers:
- Problem you're solving
- Target users
- Value proposition
- Competitive positioning
- Success metrics
- Key initiatives

**Why it works:** Forces clarity and creates alignment on one page.

### Prioritization Framework

**Common approaches Aakash shares:**
- RICE (Reach, Impact, Confidence, Effort)
- Value vs. Effort matrix
- MoSCoW (Must have, Should have, Could have, Won't have)
- Kano model

**Key insight:** No single framework is always right. Choose based on your context, stage, and needs.

### The PM Meeting Framework

**Structure for effective meetings:**
1. **Context** (why we're here)
2. **Objective** (what we need to decide/align on)
3. **Discussion** (explore options)
4. **Decision** (what we're committing to)
5. **Next steps** (who does what by when)

**Why it works:** Meetings have clear outcomes, not just discussion.

## How AI Changes Aakash's Contributions

### AI Prototyping as Core PM Skill

**Insight:** Prototyping moved from "nice to have" to "essential PM skill."

**Old PM workflow:**
- Write specs → Wait for eng → Review implementation

**New PM workflow:**
- Prototype concept → Align team → Eng builds production version

**Impact:** PMs who can prototype gain:
- Faster stakeholder alignment
- Better eng communication
- Clearer requirements
- Validated ideas before building

### Tool Comparison Framework

Aakash's AI prototyping guide helps PMs navigate:
- Which tool for which situation
- Pros/cons of each platform
- When to use standalone vs. codebase-aware tools
- Cost considerations

**Value:** Saves PMs from analysis paralysis. Pick one, start building.

### Visual Frameworks in AI Era

**New frameworks needed:**
- AI product strategy canvas (includes evals, costs)
- AI feature prioritization (value + quality + cost)
- Stakeholder communication for AI uncertainty

## When to Use Aakash's Resources

### Use visual frameworks when:
- Communicating complex concepts
- Creating alignment across teams
- Need quick understanding at-a-glance
- Building shared vocabulary

### Use stakeholder frameworks when:
- Managing up to executives
- Navigating cross-functional relationships
- Planning communication strategy
- Building influence without authority

### Use prototyping guides when:
- Learning AI prototyping tools
- Deciding which tool to use
- Teaching team about modern PM workflow

### Study product teardowns when:
- Developing product sense
- Understanding what works
- Analyzing competition
- Learning from successful products

## Integration with Other Frameworks

**Aakash synthesizes and visualizes other thought leaders:**

**Teresa Torres' Opportunity Solution Tree:**
- Aakash creates visual templates
- Makes it easier to adopt
- Shows real examples

**Marty Cagan's Four Risks:**
- Visual framework for assessing risks
- Template for risk mitigation planning

**Brian Balfour's Four Fits:**
- Canvas for mapping fits
- Visual diagnostic tool

**Janna's Now-Next-Later:**
- Visual roadmap templates
- Stakeholder communication formats

**Role:** Makes other frameworks more accessible through visualization and templates.

## Common Themes in Aakash's Work

### 1. Clarity Over Complexity

Strip away jargon. Make it simple. If you can't explain it clearly, you don't understand it.

### 2. Templates Accelerate Work

Don't start from scratch. Use templates, adapt to your context, ship faster.

### 3. Communication is a PM Superpower

Technical skills get you in the door. Communication skills determine how far you go.

### 4. Learn in Public

Share what you're learning. Teaching others reinforces your understanding.

### 5. Prototypes > Specs (AI Era)

Show, don't tell. A working prototype communicates better than a written spec.

## Practical Applications

### For New PMs:
- Study Aakash's visual frameworks to learn core concepts quickly
- Use templates to avoid starting from scratch
- Follow stakeholder communication guides

### For Experienced PMs:
- Use visual frameworks to communicate with teams
- Adapt templates to your context
- Study product teardowns for continuous learning

### For Teams:
- Adopt common frameworks for shared vocabulary
- Use visual canvases in planning sessions
- Implement communication frameworks

## Quotes to Remember

> "A framework people can see is more powerful than one they have to read."

> "Most PM work is actually stakeholder management and communication."

> "Product sense isn't innate. It's pattern recognition from studying what works."

> "Prototyping is now a core PM skill, not a bonus."

> "The best PMs make complex things simple, not simple things complex."

## Further Learning

### Essential Resources
- **Newsletter:** "One Minute PM" (Product, Persuasion, Profit)
  - Weekly frameworks and insights
  - Visual breakdowns of PM concepts
  - Actionable templates

- **Website:** [news.aakashg.com](https://www.news.aakashg.com)
  - Deep dives on PM topics
  - Framework libraries
  - Product teardowns

- **LinkedIn:** Regular visual frameworks and carousels
  - Follow for daily PM insights
  - Engaging, shareable content

- **YouTube:** Video explanations of frameworks
  - Visual learning
  - Step-by-step guides

### Key Content
- **"AI Prototyping Tutorial"** - Tool comparison and workflow
- **Marty Cagan Podcast Episode** - Product management fundamentals
- **Visual framework library** - Dozens of PM frameworks visualized
- **Stakeholder management guides** - Communication templates

### Where to Follow
- Newsletter: [news.aakashg.com](https://www.news.aakashg.com)
- LinkedIn: Active daily with frameworks
- YouTube: Video content
- Twitter/X: Quick insights

## Key Takeaways

1. **Make it visual** - Frameworks beat paragraphs for understanding
2. **Communication is core** - Stakeholder management determines PM success
3. **Use templates** - Don't reinvent, adapt and execute
4. **Develop product sense** - Study successful products, extract patterns
5. **Prototype now matters** - AI makes prototyping essential PM skill
6. **Simplify complexity** - Best PMs make hard things easy to understand
7. **Learn in public** - Teaching others accelerates your learning

---

**In the context of this PM Thought Partner:**

Aakash's contribution is accessibility and application.

Use his work to:
- Communicate frameworks visually (stakeholder alignment)
- Navigate AI prototyping tools (choose and start building)
- Manage stakeholders effectively (influence without authority)
- Develop product sense (study and pattern match)
- Make complex PM work simple (clarity beats complexity)

He's the bridge between framework theory and daily PM practice - showing how to actually use these concepts through visual templates, clear communication, and modern tools like AI prototyping.
