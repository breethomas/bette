# The Orchestrator Context Prompt Template

This template structures context for LLMs in a way that reduces hallucinations by 70%+ in real systems. Use it as a reference when designing how context flows into your AI features.

## The Template

```
[System Instructions]
You are an AI assistant operating inside a structured context engine.
Follow all business rules, domain constraints, and formatting
instructions exactly.
Do not invent facts outside the provided context.

[User Intent]
{inferred_intent}
{explicit_prompt}

[Relevant Entities]
{structured_entities}

[Relationships]
{entity_relationships}

[Session State]
{recent_messages}
{recent_selections}

[User Profile]
{role}
{tone_preferences}
{writing_style}
{prior_examples}

[Domain Context]
{retrieved_docs}
{summaries}
{attached_metadata}

[Rules & Constraints]
{business_rules}
{policies}
{formatting_requirements}
{prohibited_actions}

[Environment Signals]
{calendar_events}
{deadlines}
{system_status}
{device_context}

[Task Instructions]
Clear, step-by-step instructions for what the model must produce.

[Output Schema]
{json_schema_or_output_structure}
```

---

## Section-by-Section Guide

### [System Instructions]

Set the operating mode. Key elements:
- Role definition
- Operating constraints
- What the model must NOT do (no inventing facts)

### [User Intent]

Two parts:
- **Inferred intent:** What the system understands the user wants (may differ from literal request)
- **Explicit prompt:** What the user actually typed

### [Relevant Entities]

Structured data about the objects involved:
- Use consistent schema (YAML, JSON)
- Include IDs, names, statuses, owners, dates
- Only include entities relevant to this request

### [Relationships]

How entities connect:
- "X depends on Y"
- "A is related to B"
- "C was caused by D"

### [Session State]

Recent context from this session:
- Last few messages in conversation
- What user recently selected, clicked, or highlighted
- Actions taken in the last few minutes

### [User Profile]

Personalization data:
- Role and responsibilities
- Communication preferences (tone, length, style)
- Examples of previous outputs they liked

### [Domain Context]

Retrieved knowledge:
- Relevant documents (with summaries, not full text unless needed)
- Metadata about freshness, source, confidence
- Definitions and rules from your knowledge base

### [Rules & Constraints]

What the model must and must not do:
- Business rules (don't share internal IDs externally)
- Policies (no forward-looking commitments)
- Formatting requirements (use specific structure)
- Prohibited actions (don't fabricate metrics)

### [Environment Signals]

Current situational context:
- Calendar events and deadlines
- System status (all systems operational, errors present)
- Device context (desktop, mobile, inside specific tool)

### [Task Instructions]

Clear, numbered steps for what to produce:
1. Do X
2. Follow Y format
3. Include Z
4. Avoid W

### [Output Schema]

Exact structure for the response:
- JSON schema
- Required fields
- Expected format

---

## Example: Weekly Product Update Generator

```
[System Instructions]
You are an AI assistant operating inside a structured context engine for
a product team.

You write weekly product updates for senior stakeholders (VP Product,
CTO, CEO) based strictly on the context provided below.

You must:
- Follow all business rules, domain constraints, and formatting
  instructions exactly.
- Never invent projects, metrics, incidents, or timelines that are not
  explicitly present in Domain Context, Relevant Entities, Relationships,
  or Session State.
- Treat the Domain Context and Rules & Constraints sections as the
  single source of truth.
- If critical information is missing, you must clearly state what is
  missing instead of guessing.

[User Intent]
{inferred_intent}:
"Summarize the most important product changes, progress, risks, and next
steps for the past week into an executive-ready weekly update."

{explicit_prompt}:
"Can you draft this week's product update for leadership based on what
changed since last Monday?"

[Relevant Entities]
{structured_entities}:
- project_roadmap_item:
    id: "PRJ-142"
    title: "Onboarding Funnel Revamp"
    owner: "Sara"
    status: "In Progress"
    target_release: "2025-12-01"
- project_roadmap_item:
    id: "PRJ-087"
    title: "AI Assistant v2"
    owner: "Imran"
    status: "Shipped"
    target_release: "2025-11-15"
- metric:
    id: "MTR-DAU"
    name: "Daily Active Users"
    current_value: 18240
    previous_value: 17680
    unit: "users"
- incident:
    id: "INC-221"
    title: "Checkout Latency Spike"
    status: "Resolved"
    severity: "High"

[Relationships]
{entity_relationships}:
- "PRJ-142" depends_on "PRJ-087"
- "INC-221" impacted "checkout_conversion"
- "MTR-DAU" improved_after "AI Assistant v2" release
- "PRJ-087" linked_to_release "2025.11.15-prod"

[Session State]
{recent_messages}:
- 2025-11-17T09:03Z - User: "Last week's update is in the doc; I want
  something similar but shorter."
- 2025-11-17T09:04Z - Assistant: "Understood, I will keep a similar
  structure but be more concise."
- 2025-11-17T09:06Z - User: "Don't oversell wins; keep it realistic."

{recent_selections}:
- User highlighted last week's "Risks & Blockers" section.
- User opened the "AI Assistant v2 - Launch Notes" document.
- User clicked on metrics dashboard filtered to "Last 7 days".

[User Profile]
{role}:
- "Director of Product, responsible for AI & Growth initiatives."

{tone_preferences}:
- Confident but not hype.
- Data-informed, not overly narrative.
- Clear separation of "What happened", "Why it matters", and "What's next".

{writing_style}:
- Short paragraphs.
- Uses headers and subheaders.
- Uses occasional bullet points for clarity, but avoids long bullet lists.
- Avoids exclamation marks and marketing language.

{prior_examples}:
- Example snippet of previous accepted update:
  "This week we completed the rollout of the new onboarding experiment
  to 50% of new users. Early results show a +3.2% lift in activation.
  Next week we'll either scale this to 100% or roll back depending on
  retention impact."

[Domain Context]
{retrieved_docs}:
- "Weekly Update - 2025-11-10" (last week's product update)
- "AI Assistant v2 - Launch Notes"
- "Onboarding Funnel - Experiment Spec v3"
- "Incident Report - INC-221 Checkout Latency"

{summaries}:
- Last Week's Update Summary:
  "Focused on preparing AI Assistant v2 launch, mitigating checkout
  latency incidents, and kicking off onboarding experiment planning."
- AI Assistant v2 Launch Notes Summary:
  "Shipped on 2025-11-15 to 100% of users, goals: improve task
  completion speed and increase DAUs among power users."

{attached_metadata}:
- current_week_range: "2025-11-10 to 2025-11-17"
- timezone: "America/Los_Angeles"
- environment: "Production"
- product_area_focus: ["Onboarding", "AI Assistant", "Checkout"]

[Rules & Constraints]
{business_rules}:
- Do not share internal incident IDs in the update; describe incidents
  in business terms instead.
- Do not reference customers by name; aggregate or anonymize.
- Always tie product work back to business outcomes (activation,
  retention, revenue, support volume).

{policies}:
- No forward-looking commitments beyond what exists in the roadmap.
- Do not mention unannounced features by name.
- Maintain consistency with metric definitions (use official metric
  names only).

{formatting_requirements}:
- Structure the update into sections: Highlights, Metrics & Impact,
  Risks & Blockers, Next Week
- Use Markdown headings: H2 for main sections, bold for key terms.
- Keep total length under 600 words.

{prohibited_actions}:
- Do not fabricate metrics, dates, or launches.
- Do not mention any feature that is not explicitly referenced in
  Domain Context.
- Do not change the interpretation of metric names (e.g., DAU vs MAU).

[Environment Signals]
{calendar_events}:
- Today is Monday, 2025-11-17.
- The "Exec Product Sync" is scheduled for 2025-11-17 at 15:30 local time.
- This update is intended to be pasted into the agenda doc before that
  meeting.

{deadlines}:
- Q4 goals lock on 2025-12-01.
- Onboarding Funnel Revamp milestone review on 2025-11-25.

{system_status}:
- All systems operational.
- No open P0 incidents.
- Analytics data is fresh as of 2025-11-17T08:00Z.

{device_context}:
- User is currently on desktop web.
- Editing inside an internal docs tool with Markdown support.

[Task Instructions]
Using only the information provided above:
1. Draft a weekly product update that is realistic, grounded, and
   aligned with the user's tone and prior examples.
2. Follow the required structure exactly: Highlights, Metrics & Impact,
   Risks & Blockers, Next Week.
3. Emphasize what actually changed this week compared to last week.
4. Connect product work to business outcomes using the metric context.
5. Avoid exaggerating wins; if results are early or inconclusive,
   state that explicitly.
6. If there are known gaps in the context, note them transparently.

[Output Schema]
{json_schema_or_output_structure}:

Return the final result as a JSON object:

{
  "highlights_markdown": "string",
  "metrics_and_impact_markdown": "string",
  "risks_and_blockers_markdown": "string",
  "next_week_markdown": "string",
  "notes_for_user": "string - caveats, missing data, assumptions"
}
```

---

## Why This Works

1. **Clear sections** - Model knows exactly where to look for each type of information
2. **Explicit constraints** - No ambiguity about what's allowed
3. **Grounding** - All facts come from provided context, not model's training data
4. **Structured output** - Predictable format for downstream processing
5. **Transparency** - Model acknowledges gaps rather than filling them with hallucinations

---

## Adapting for Your Use Case

1. **Start with the template** - Don't reinvent the structure
2. **Add sections you need** - Some use cases need more user profile, less environment
3. **Remove sections you don't** - Simpler is better if you don't need everything
4. **Test with real data** - Fill in actual values and see how the model behaves
5. **Iterate on constraints** - The Rules section is where most tuning happens

---

## Attribution

**Source:** Aakash Gupta & Miqdad Jaffer, "The Ultimate Guide to Context Engineering for PMs"
