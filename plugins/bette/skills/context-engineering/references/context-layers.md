# The 6 Layers of Context

Every world-class AI product's intelligence comes from a carefully engineered hierarchy of context—not clever prompts or bigger models.

## The Context Pyramid

From bottom (foundation) to top (final output):

---

## Layer 1: Intent Context

**What it is:** Understanding what the user *actually means*, not what they literally typed.

**Why it matters:** Almost every catastrophic AI failure traces back to misunderstood intent. Users speak imprecisely—they request one thing while meaning another, highlight text instead of explaining the problem, click and hesitate and rephrase.

**The Triple-I Intent Framework:**

1. **Interpret** - Translate explicit text into a structured task objective
2. **Infer** - Use recent user behavior (selections, hovers, edits, recent failures) to uncover hidden meaning
3. **Identify Gaps** - Detect missing information the system must retrieve before reasoning

**Examples of intent signals:**
- User highlighted text (implies "do something with this")
- User is in a specific part of the app (implies relevant context)
- User's recent actions (just created X, just deleted Y)
- Time of day, deadline proximity

---

## Layer 2: User Context

**What it is:** A continuously updated portrait of the individual—their patterns, preferences, behaviors, and cognitive style.

**Why it matters:** Even the most correct output can feel wrong if it's not personalized. A senior engineer expects surgical diff; a beginner wants detailed walkthrough. A founder wants executive-level brevity; a student wants scaffolding and structure.

**The 5-P Personalization Matrix:**

1. **Preferences** - Tone (concise, formal, friendly), depth, writing voice
2. **Patterns** - Common edits, recurring corrections, formatting habits
3. **Proficiency** - Beginner, intermediate, expert (auto-adjust complexity)
4. **Pacing** - How fast the user consumes or expects answers
5. **Purpose** - Their role-specific motivations and workflows

**What to capture:**
- Writing style samples from past interactions
- Common corrections they make to AI output
- Their role and responsibilities
- How they've configured their preferences

---

## Layer 3: Domain Context

**What it is:** Everything the system must treat as law—your entities, metadata, relationships, processes, codebase, documents, metrics, business rules, historical decisions, and institutional memory.

**Why it matters:** Without domain grounding, an AI system is a hallucination machine covered in UX polish. Domain context turns it from a generative toy into a factual expert.

**Five Structural Pillars:**

1. **Entities** - Objects in your world (tasks, metrics, PRs, dashboards, users, components)
2. **Attributes** - Metadata fields that describe them (owners, timestamps, tags, versions)
3. **Relationships** - Connections between entities ("depends on," "caused by," "related to," "belongs to")
4. **Definitions & Rules** - Canonical metric definitions, formulas, business logic
5. **Lineage** - Version history and provenance of every object

**Critical:** Domain knowledge cannot live as blobs of text. It must be structured.

---

## Layer 4: Rule Context

**What it is:** The boundaries, constraints, permissions, policies, and formats that govern what the AI may or may not do.

**Why it matters:** Even the smartest system becomes dangerous without rules. Rule context is the judicial system of your AI—determining what's allowed, forbidden, enforced, and precisely formatted.

**The Two-Wall Constraint Framework:**

1. **Soft Wall** - Advisory constraints that shape behavior
   - Tone and brand voice
   - Style preferences
   - Communication guidelines

2. **Hard Wall** - Mandatory constraints that enforce correctness
   - Output schemas and validation
   - Permission boundaries
   - Safety and compliance rules
   - Data handling requirements

**Key insight:** Soft walls shape behavior. Hard walls enforce correctness. Together, they transform your AI from a probabilistic improviser into a deterministic operator.

---

## Layer 5: Environment Context

**What it is:** The real-time conditions shaping the user's world in this exact moment.

**Why it matters:** Nearly all user tasks depend on the *present situation*, not static knowledge. A code assistant must know which file is open. A writing assistant must know which paragraph is selected. A dashboard assistant must know which metric failed in the last hour.

**The N.O.W. Awareness Model:**

1. **Nearby Activity** - What the user is interacting with right now (highlighted text, cursor position, open file)
2. **Operational Conditions** - Logs, recent errors, system state, device context
3. **Window of Time** - Deadlines, timestamps, recency signals

**What to capture:**
- Current document/file/screen
- Recent actions in the last few minutes
- System state (errors, warnings, status)
- Calendar context (deadlines, meetings)
- Device and environment info

---

## Layer 6: Exposition Context

**What it is:** The final, distilled, structured, contradiction-free packet of meaning the model actually sees.

**Why it matters:** This is where intelligence becomes execution. It's the difference between giving the model the entire haystack and giving it exactly the right needle.

**The Context Distillation Loop:**

1. **Collect** - Gather all relevant intent, user, domain, rule, and environment signals
2. **Compress** - Remove noise, collapse redundancy, clean contradictions
3. **Construct** - Organize the final payload into labeled sections with clear boundaries
4. **Constrain** - Apply rules, schemas, safety boundaries, and formatting requirements
5. **Check** - Validate internal consistency and readiness for LLM reasoning

---

## Making the Layers Work Together

Most teams skip layers or implement them shallowly. The best teams treat each layer as essential infrastructure, not optional polish.

**Common failure patterns:**
- Intent layer missing → Model guesses what user wants
- User layer missing → Generic, impersonal outputs
- Domain layer missing → Hallucinations and made-up facts
- Rule layer missing → Inconsistent, sometimes dangerous outputs
- Environment layer missing → Outputs disconnected from current reality
- Exposition layer weak → Messy context confuses the model

**The goal:** When all six layers work together, the AI finally becomes intelligent—not because the model is smarter, but because the context is complete.

---

## Attribution

**Source:** Aakash Gupta & Miqdad Jaffer, "The Ultimate Guide to Context Engineering for PMs"
