---
name: context-engineering
description: "[ARCHIVED] Full 4D Context Canvas reference. For new AI features, use /spec --ai. For debugging, use /ai-debug. For quality checks, use /context-check."
---

# Context Engineering for AI Products

> **ARCHIVED SKILL**
>
> This skill has been integrated into the unified spec system:
> - **New AI features:** Use `/spec --ai` or `/spec --deep context`
> - **Diagnose issues:** Use `/ai-debug`
> - **Quality checks:** Use `/context-check`
>
> This file remains as a **reference** for the full 4D Context Canvas framework.

---

## Core Philosophy

**Context engineering is the art of giving AI exactly the right information to do its job.**

Models are commodities—your context is your moat.

Most AI features fail before they reach the model. They fail because:
- Nobody defined the model's actual job
- Nobody mapped what context it needs
- Nobody figured out how to get that context at runtime
- Nobody designed what happens when it breaks

This skill prevents those failures.

## The 90/10 Mismatch

Teams spend 90% of their time on model selection and prompts.
But 90% of AI quality comes from context quality.

When AI fails, teams blame the model. But the real causes:
- System doesn't know what file the user is working on
- System doesn't see the user's preferences
- System isn't aware of entities or relationships in the workspace
- System cannot recognize the user's role
- System retrieves irrelevant documents
- System misses crucial logs or state

**Fix the context, fix the AI.**

## PM's Role in Context Engineering

Context engineering is NOT an engineering problem. It sits at the intersection of product strategy, user understanding, and system design.

**PMs own three critical layers:**

1. **Defining "intelligence"** - What should the AI know? What's essential vs nice-to-have? What level of personalization without feeling creepy?

2. **Mapping context requirements to user value** - Translating "users want better suggestions" into "system needs access to past rejections, current workspace state, and team preferences"

3. **Designing degradation strategy** - When context is missing, stale, or incomplete: Block the feature? Show partial answer? Ask clarifying questions? Fall back to non-personalized?

**Engineers own the implementation:** Retrieval architecture, vector databases, embedding pipelines, API integrations, performance optimization.

**But they need you to define the what and why before they can build the how.**

---

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CONTEXT ENGINEERING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What are you working on?

  1. Spec a new AI feature
     → Define what context it needs before engineering starts

  2. Diagnose an existing AI feature
     → Figure out why it's underperforming or hallucinating

  3. Quick quality check
     → Validate context before shipping or during review

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Route to the appropriate path based on user selection.

---

## Path 1: Spec New Feature (4D Context Canvas)

### Purpose
Walk through four dimensions that determine whether an AI feature ships successfully or dies in production. Use BEFORE engineering starts.

### Starting Point

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SPEC NEW FEATURE — 4D Context Canvas
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

We'll walk through 4 dimensions. Most AI features fail before
they reach the model—this prevents that.

How do you want to start?

  1. From a Linear issue (I'll pull the details)
  2. Describe it manually

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**If Linear:** Use Linear MCP to pull issue details. Pre-populate what's available.

**If Manual:** Ask user to describe the AI feature in 1-2 sentences.

### D1 — DEMAND: What's the Model's Job?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 D1: DEMAND — What's the model's job?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 If you can't articulate the job precisely, the model can't do it.
   "Make it smart" is not a spec. Neither is "personalized."
```

**Questions to ask:**

1. **What should the model produce?**
   - Push for specificity: Not "recommendations" → "3 ranked options with rationale"
   - Not "a summary" → "2-paragraph executive summary with key metrics"

2. **For whom?** (User segment, role, context)

3. **Under what assumptions?** (What must be true for this to work?)

4. **What constraints apply?** (Tone, format, length, boundaries, prohibited content)

5. **What defines success?** (Measurable outcome, not "users like it")

**The transformation to model:**

```
VAGUE: "Draft a status update"

PRECISE: "Summarize the key changes in project X since the last report,
structured for stakeholder Y, using the user's preferred tone,
adhering to the product's reporting format, in under 200 words."
```

**Education moment:**
```
💡 PM vs Engineer: You own the what and why. Engineers own the how.
   Without this spec, they build impressive systems that feel hollow.
```

**Capture and display D1 summary before moving on.**

### D2 — DATA: What Context Is Required?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 D2: DATA — What context does the model need?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Every piece of context costs tokens. More tokens = higher cost +
   slower responses. Include only what's essential for the job.
```

**Build a Context Requirements Table together:**

For each piece of context needed:

1. **Data Needed** - The entity, document, metric, or signal
2. **Source** - Where it lives (DB, API, user input, cache, logs)
3. **Availability**:
   - Always (can fetch 100% of the time)
   - Sometimes (depends on user actions or data freshness)
   - Never (must be requested explicitly or cannot be assumed)
4. **Sensitivity** - PII, internal-only, restricted, public

**Example output:**

```
| Data Needed          | Source      | Availability | Sensitivity |
|---------------------|-------------|--------------|-------------|
| User equity estimate | Internal DB | Always       | PII         |
| Browsing history    | Analytics   | Always       | Internal    |
| Stated goals        | User input  | Sometimes    | Internal    |
| Local market trends | API         | Always       | Public      |
```

**Flag problems immediately:**
- "Sometimes" availability needs a decision: What happens when it's missing?
- "Never" availability is a blocker: Can't build without resolving this

**Education moment:**
```
💡 Hidden dependencies live here. When you map honestly, you discover
   critical data that doesn't exist, sources that are unreliable, or
   assumptions that will break at scale.
```

### D3 — DISCOVERY: How Will You Get Context at Runtime?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 D3: DISCOVERY — How will you get the context at runtime?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Knowing what data you need ≠ knowing how to get it at runtime.
   This is where "it worked in the demo" dies in production.
```

For each piece of context from D2:

1. **How will the system fetch this?**
   - Real-time query
   - Pre-computed/cached
   - User provides it
   - Inferred from behavior

2. **What's the latency budget?**

3. **What if the source is slow or unavailable?**

**Discovery strategies to consider:**

- **Search-Based:** Vector search (semantic), keyword search (precision), hybrid
- **Graph-Based:** Follow relationships through knowledge graph
- **Precomputed:** Daily/weekly jobs, materialized views, caches

**Education moment:**
```
💡 Trade-off: Real-time = fresh but slow. Cached = fast but stale.
   Know which context needs which strategy.
```

### D4 — DEFENSE: What Happens When It Fails?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 D4: DEFENSE — What happens when it fails?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 AI will fail. Context will be missing. Data will be stale. The
   model will hallucinate confidently. Design for failure first.
```

**Four defense mechanisms to define:**

**1. Pre-Checks (before calling model):**
- What must be true before calling the model?
- Enough context present?
- Data fresh enough?
- Required entities available?
- If checks fail → block generation or ask clarifying questions

**2. Post-Checks (after generation):**
- Did output follow constraints?
- Does it match required schema?
- Is it logically consistent?
- Does it violate any rules?

**3. Fallback Paths (when things break):**
- Partial answer with caveats?
- Clarifying questions to user?
- Conservative defaults?
- Non-AI fallback experience?

**4. Feedback Loops (how to improve):**
- Explicit ratings (thumbs up/down)
- Implicit behavior (edits, corrections, abandonment)
- Pattern detection across failures

**Education moment:**
```
💡 The best AI features degrade gracefully. Users trust systems
   that know their limits.
```

### Path 1 Output

After completing all four dimensions, generate summary:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 4D CONTEXT CANVAS COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [Name]

  D1 Demand:      [CLEAR / NEEDS WORK / BLOCKED]
  D2 Data:        [CLEAR / NEEDS WORK / BLOCKED]
  D3 Discovery:   [CLEAR / NEEDS WORK / BLOCKED]
  D4 Defense:     [CLEAR / NEEDS WORK / BLOCKED]

Overall: [READY FOR ENGINEERING / NEEDS WORK / BLOCKED]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If blocked or needs work, list specific items to resolve.

**Output options:**
1. Add to Linear issue as comment
2. Create new Linear story with spec
3. Export as markdown
4. Export Context Requirements Table as spreadsheet format
5. Just show the summary

---

## Path 2: Diagnose Existing Feature (Context Audit)

### Purpose
Figure out why an existing AI feature is underperforming, hallucinating, or behaving inconsistently. Work backwards from symptoms to root cause.

### Starting Point

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 DIAGNOSE EXISTING FEATURE — Context Audit
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 When AI features fail, teams blame the model. But 90% of failures
   are context failures—wrong data, missing data, stale data, or
   poorly structured data.

Let's find the root cause.

How do you want to start?

  1. From a Linear issue (I'll pull the details)
  2. Describe the feature and symptoms manually

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**⚠️ TOKEN MANAGEMENT (for Claude):**
When pulling from Linear, use `get_issue` for a single issue ID—don't search
broadly. If searching, always use `limit: 10` and get titles first before
fetching full details.

### Scope Check (for multi-issue features)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SCOPE — What are we diagnosing?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 AI features often span multiple issues—a parent spec plus
   implementation tasks and bug reports. Diagnosing without the
   full picture leads to incomplete answers.

What's the scope?

  1. Single issue — One specific problem to diagnose
  2. Entire feature — A feature that spans multiple issues

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**If "Entire feature":**

Ask for parent/overview issue ID, then use Linear MCP to find related issues.

**⚠️ IMPLEMENTATION NOTE FOR CLAUDE:**
Linear queries can return massive amounts of data that exceed token limits.
ALWAYS follow this pattern:

1. **First query: titles only** — Use `list_issues` with `limit: 20` max
2. **Count results** — Report how many issues were found
3. **Ask user preference** — Before fetching full details
4. **Selective fetch** — Only `get_issue` on specifically selected issues

NEVER try to read all issue details in one query. This will fail.

```
Found 12 related issues:
  • 3 sub-issues
  • 2 blocked-by relations
  • 4 bugs referencing this feature
  • 3 other relations

⚠️  Loading all of them may be slow and increase cost.

How do you want to proceed?

  1. Smart summary — Pull titles + key details, summarize each
     (faster, cheaper, usually sufficient)

  2. Full context — Pull everything including comments
     (slower, more expensive, use for deep dives)

  3. Let me pick — Show me the list, I'll select what's relevant
```

**Education moment:**
```
💡 This is context engineering in action—we're deciding what's
   relevant vs. what's noise. Same trade-off you'll make for
   your AI features.
```

### Symptoms Collection

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SYMPTOMS — What's going wrong?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What are you seeing? (Select all that apply)

  □ Hallucinations — Confidently wrong facts, made-up data
  □ Inconsistency — Different outputs for similar inputs
  □ Generic outputs — Feels like it doesn't know the user/context
  □ Wrong tone/format — Output doesn't match expectations
  □ Slow responses — Taking too long
  □ High costs — Token usage is out of control
  □ Works in demo, fails in prod — Different behavior in real conditions
  □ Other: ___

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Symptom-to-cause mapping:**

| Symptom | Likely Root Cause | Focus Area |
|---------|------------------|------------|
| Hallucinations | Missing domain context, no grounding | D2, D4 |
| Inconsistency | Vague job definition, missing rules | D1, D4 |
| Generic outputs | Missing user/environment context | D2 |
| Wrong tone/format | Missing constraints, no examples | D1, D4 |
| Slow responses | Too much context, bad discovery | D2, D3 |
| High costs | Dumping everything in prompt | D2, D3 |
| Demo vs prod | Discovery strategy broken | D3, D4 |

### Audit D1 — Was the Job Defined?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AUDIT D1: Was the model's job clearly defined?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Vague jobs cause vague outputs. "Make it personalized" is not
   a spec—it's a wish.
```

**Diagnostic questions:**

1. Can you articulate exactly what the model should produce?
   - Hesitation = 🚨 **Gap: Job never properly defined**

2. Is there a written spec for inputs, outputs, constraints, success criteria?
   - No = 🚨 **Gap: No spec exists**

3. Do engineers and PMs agree on what "good" looks like?
   - No = 🚨 **Gap: Misaligned expectations**

```
D1 Assessment: [CLEAR / GAP FOUND / CRITICAL GAP]
```

### Audit D2 — Is the Model Getting the Right Context?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AUDIT D2: Is the model getting the right context?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Most hallucinations are context failures, not model failures.
   The model can only reason about what it sees.
```

**Diagnostic questions:**

1. What context is the model actually receiving today?

2. Walk through the 6 layers—what's present vs missing?

| Layer | What It Is | Present? |
|-------|-----------|----------|
| Intent | What user actually wants (not just what they typed) | ? |
| User | Preferences, patterns, history, proficiency | ? |
| Domain | Entities, rules, relationships, definitions | ? |
| Rules | Constraints, policies, formats, permissions | ? |
| Environment | Current state, time, location, recent actions | ? |
| Exposition | Structured, labeled, clean final payload | ? |

3. Is context structured or dumped as raw text?
   - Dumped = 🚨 **Gap: Unstructured context confuses models**

4. Is there too much context? (Token bloat)
   - Yes = 🚨 **Gap: Over-stuffed prompt, model loses focus**

**Education moment:**
```
💡 Common failure: Teams dump everything into the prompt hoping the
   model will "figure it out." It won't. Curate ruthlessly.
```

```
D2 Assessment: [CLEAR / GAP FOUND / CRITICAL GAP]
```

### Audit D3 — Is Context Being Fetched Reliably?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AUDIT D3: Is context being fetched reliably at runtime?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 This is where "it worked in the demo" dies. Demo uses hardcoded
   context. Production must fetch it live—and things break.
```

**Diagnostic questions:**

1. How is each piece of context being fetched?
   - Hardcoded? = 🚨 **Gap: Won't work at scale**
   - API that times out? = 🚨 **Gap: Latency/reliability issue**
   - Cache that goes stale? = 🚨 **Gap: Freshness issue**

2. What happens when a data source is unavailable?
   - Feature crashes? = 🚨 **Gap: No fallback**
   - Silent failure? = 🚨 **Gap: Model hallucinates to fill gap**

3. Is there visibility into what context is being used per request?
   - No = 🚨 **Gap: Can't debug failures**

```
D3 Assessment: [CLEAR / GAP FOUND / CRITICAL GAP]
```

### Audit D4 — Are Failures Being Caught?

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AUDIT D4: Are failures being caught and handled?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 AI will fail. The question is whether users see raw failures or
   graceful degradation. Trust comes from knowing your limits.
```

**Diagnostic questions:**

1. Are there pre-checks before calling the model?
   - No = 🚨 **Gap: No validation before generation**

2. Are there post-checks validating output?
   - No = 🚨 **Gap: No output validation**

3. What's the fallback UX when things break?
   - None designed = 🚨 **Gap: Users see raw failures**

4. Is there a feedback loop capturing failures?
   - No = 🚨 **Gap: Same failures repeat**

```
D4 Assessment: [CLEAR / GAP FOUND / CRITICAL GAP]
```

### Path 2 Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CONTEXT AUDIT COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [Name]
Symptoms: [What was reported]

  D1 Demand:      [CLEAR / GAP / CRITICAL]
  D2 Data:        [CLEAR / GAP / CRITICAL]
  D3 Discovery:   [CLEAR / GAP / CRITICAL]
  D4 Defense:     [CLEAR / GAP / CRITICAL]

Primary Issue: [e.g., "Missing user context (D2) + no fallback (D4)"]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

RECOMMENDED FIXES (prioritized):

1. [Highest impact fix]
2. [Second fix]
3. [Third fix]

Quick Win: [Smallest change that would improve things]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Output options:**
1. Add to Linear issue as comment
2. Create fix stories in Linear
3. Export as markdown
4. Just show the summary

---

## Path 3: Quick Quality Check

### Purpose
Fast 5-check validation of context quality. Use before shipping, during code review, or when reviewing a prompt/payload.

### Starting Point

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 QUICK QUALITY CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 All hallucinations are context failures before they're model
   failures. This checklist catches problems before users do.

5 checks. 5 minutes. Use before shipping or during review.

What are you checking?

  1. A prompt/context payload (paste it)
  2. A feature spec (describe it)
  3. A Linear issue (I'll pull it)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Check 1: RELEVANCE

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CHECK 1: RELEVANCE — Is everything here necessary?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 More context ≠ better. Irrelevant context confuses the model,
   increases cost, and slows responses.
```

- Does every piece of context directly contribute to the task?
- Is there anything "kind of related" that could be cut?
- Is there decorative metadata that doesn't help reasoning?

```
Relevance: [PASS / NEEDS WORK]
```

### Check 2: FRESHNESS

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CHECK 2: FRESHNESS — Is the data current enough?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Stale context = stale outputs. A model reasoning about yesterday's
   data will give yesterday's answers.
```

- Are timestamps recent enough for this task?
- Are metrics, dashboards, logs up to date?
- Could cached data be invalid for this request?

```
Freshness: [PASS / NEEDS WORK]
```

### Check 3: SUFFICIENCY

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CHECK 3: SUFFICIENCY — Does the model have enough to reason?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Missing context forces the model to guess. Guessing = hallucinating.
   If the model needs it to reason, it must be provided.
```

- Are all required entities present?
- Are dependencies, relationships, history included?
- Could the model answer correctly without guessing?

```
Sufficiency: [PASS / NEEDS WORK]
```

### Check 4: STRUCTURE

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CHECK 4: STRUCTURE — Is context organized clearly?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Dumping raw text forces the model to parse meaning. Structured,
   labeled sections reduce ambiguity and improve accuracy.
```

- Is context broken into labeled sections?
- Are relationships explicitly described (not implied)?
- Is domain knowledge structured (not prose blobs)?

```
Structure: [PASS / NEEDS WORK]
```

### Check 5: CONSTRAINTS

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CHECK 5: CONSTRAINTS — Are the rules explicit?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Prompts are suggestions. The model will eventually ignore them.
   Hard rules must be enforced outside the prompt or stated as
   non-negotiable constraints.
```

- Are business rules explicitly stated?
- Are tone, formatting, domain rules included?
- Is permission logic represented accurately?
- Are prohibited actions clearly listed?

```
Constraints: [PASS / NEEDS WORK]
```

### Path 3 Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CONTEXT QUALITY CHECK COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  ┌─────────────┬────────────┐
  │ Check       │ Result     │
  ├─────────────┼────────────┤
  │ Relevance   │ ✓ PASS     │
  │ Freshness   │ ✓ PASS     │
  │ Sufficiency │ ⚠ NEEDS WORK │
  │ Structure   │ ✓ PASS     │
  │ Constraints │ ⚠ NEEDS WORK │
  └─────────────┴────────────┘

  Overall: 3/5 PASSING — Fix issues before shipping

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ISSUES TO FIX:

[List specific issues found with concrete recommendations]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Pro tip: Run this check again after fixes to confirm resolution.
```

**Output options:**
1. Add to Linear issue as comment
2. Export as markdown
3. Just show the summary

---

## Linear Integration

When Linear MCP is available:

**Pulling issues:**
- Use `mcp__plugin_hb-tools_linear__get_issue` to fetch issue details
- Use `mcp__plugin_hb-tools_linear__list_issues` with parent filter to find related issues
- Check for blocking/blocked-by relations

**Creating output:**
- Use `mcp__plugin_hb-tools_linear__create_comment` to add canvas/audit as comment
- Use `mcp__plugin_hb-tools_linear__create_issue` to create new stories from specs
- Apply appropriate labels: `context-engineering`, `ai-feature`

---

## Integration with Other Commands

**Before `/context-engineering`:**
- `/four-risks` - Validate the feature is worth building at all

**After `/context-engineering`:**
- `/ai-cost-check` - Model the unit economics
- `/ai-health-check` - Pre-launch validation

**The sequence:**
1. Is this worth building? (`/four-risks`)
2. How do we spec it correctly? (`/context-engineering`)
3. Can we afford it? (`/ai-cost-check`)
4. Is it ready to ship? (`/ai-health-check`)

---

## Key Concepts Reference

### The 6 Layers of Context

Every AI system needs these layers (bottom to top):

1. **Intent** - What user actually means, not what they typed
2. **User** - Preferences, patterns, history, proficiency
3. **Domain** - Entities, rules, relationships, definitions
4. **Rules** - Constraints, policies, formats, permissions
5. **Environment** - Current state, time, location, recent actions
6. **Exposition** - Final structured, clean payload the model sees

### The 4D Canvas Summary

- **Demand** - What the model must do (precise job spec)
- **Data** - What context is required (requirements table)
- **Discovery** - How to get context at runtime (fetch strategy)
- **Defense** - What happens when it fails (guardrails)

### Context Quality Checklist

1. **Relevance** - Only what's necessary
2. **Freshness** - Current enough for the task
3. **Sufficiency** - Everything needed to reason
4. **Structure** - Organized with clear labels
5. **Constraints** - Rules explicitly stated

---

## Attribution

**Source framework:** 4D Context Canvas, 6 Layers of Context, C.E.O. Framework
**Authors:** Aakash Gupta & Miqdad Jaffer (OpenAI)
**Publication:** "The Ultimate Guide to Context Engineering for PMs" - Product Growth Newsletter, 2025

---

## Remember

- Context engineering > prompt engineering
- 90% of AI quality comes from context quality
- PMs own the what and why; engineers own the how
- Design for failure first
- Context is your only durable moat
