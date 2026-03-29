---
name: build-judge
description: >
  Build an LLM-as-Judge evaluator for one specific failure mode. Binary pass/fail
  only. Use when a failure mode requires interpretation (tone, faithfulness,
  relevance, completeness) and cannot be checked with code. Do NOT use when the
  failure can be checked with regex, schema validation, or execution tests.
  Do NOT use before completing error analysis (/upgrade-evals).
---

# Build Judge

Design a binary Pass/Fail LLM-as-Judge evaluator for one specific failure mode. Each judge checks exactly one thing.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 BUILD JUDGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

One judge. One failure mode. Binary pass/fail.

What failure mode are you building a judge for?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Prerequisites

- Error analysis is complete (`/upgrade-evals`). The failure mode is identified from real traces.
- The PM has human-labeled traces for this failure mode (at least 20 Pass and 20 Fail examples).
- A code-based evaluator cannot check this failure mode.

## Prerequisite Gate: Can Code Check This?

Before building any judge, exhaust code-based options. Many failure modes that seem subjective reduce to keyword checks, regex, or API calls when you understand the domain.

Ask the PM:
- "Can you describe the failure in terms a simple rule could catch?"
- "Is there a keyword, format, or structural pattern that distinguishes pass from fail?"

Example: Detecting whether an AI interviewing coach suggests "general" questions (typical behavior vs. specific past event) seems to require semantic understanding, but a keyword check for "usually," "typical," and "normally" works well.

If code can check it → write the code check. Skip the judge.

Claude Code executes: Write and test code-based evaluators when applicable. Only proceed to judge building when code checks are insufficient.

## The Four Components

Every judge prompt requires exactly four components. Claude Code generates the prompt; the PM provides the domain-specific content.

### 1. Task and Evaluation Criterion

State what the judge evaluates. One failure mode per judge.

```
You are an evaluator assessing whether a real estate assistant's email
uses the appropriate tone for the client's persona.
```

Not: "Evaluate whether the email is good" or "Rate the email quality from 1-5."

### 2. Pass/Fail Definitions

Binary only. No Likert scales, no letter grades, no partial credit. Definitions come from the PM's error analysis.

```
## Definitions

PASS: The email matches the expected communication style for the client persona:
- Luxury Buyers: formal language, emphasis on exclusive features, premium
  market positioning, no casual slang
- First-Time Homebuyers: warm and encouraging tone, educational explanations,
  avoids jargon, patient and supportive
- Investors: data-driven language, ROI-focused, market analytics, concise
  and professional

FAIL: The email uses a tone mismatched to the client persona. Examples:
- Using casual slang ("hey, check out this pad!") for a luxury buyer
- Using heavy financial jargon for a first-time homebuyer
- Using overly emotional language for an investor
```

Ask the PM to describe what Pass and Fail look like in their domain. Use their language.

### 3. Few-Shot Examples

Include labeled Pass and Fail examples from the PM's human-labeled data.

```
## Examples

### Example 1: PASS
Client Persona: Luxury Buyer
Email: "Dear Mr. Harrington, I am pleased to present an exclusive listing
at 1200 Pacific Heights Drive. This distinguished property features..."
Critique: The email opens with a formal salutation and uses language
consistent with luxury positioning. No casual slang or informal phrasing.
Result: Pass

### Example 2: FAIL
Client Persona: Luxury Buyer
Email: "Hey! Just found this awesome place you might like. It's got a
pool and stuff, super cool neighborhood..."
Critique: "Hey!" is informal. "awesome place," "got a pool and stuff,"
and "super cool" are casual slang inappropriate for a luxury buyer.
Result: Fail

### Example 3: PASS (borderline)
Client Persona: First-Time Homebuyer
Email: "Hi Sarah, I found a property that might be a great fit for your
first home. The neighborhood has good schools nearby, and the monthly
payment would be similar to what you're currently paying in rent..."
Critique: Warm but not overly casual. Explains in relatable terms.
Avoids jargon. Matches the supportive tone expected for first-time buyers.
Result: Pass
```

**Rules for selecting examples:**
- Include at least one clear Pass, one clear Fail, and one borderline case. Borderline examples are the most valuable — they teach nuance.
- Draw examples from the training split (10-20% of labeled data set aside for this purpose).
- Examples used in the judge prompt must be excluded from dev and test sets. Using dev/test examples is data leakage.
- 2-4 examples is typical. Performance plateaus after 4-8.

Ask the PM: "Show me one output that clearly passes, one that clearly fails, and one that's a close call."

### 4. Structured Output Format

The output must include a critique before the verdict. Placing the critique first forces the judge to articulate its reasoning before committing to a decision.

```json
{
  "critique": "string — detailed assessment of the output against the criterion",
  "result": "Pass or Fail"
}
```

Claude Code executes: Generate the complete judge prompt, set up structured output enforcement (response_format or tool definitions depending on provider), and wire it into a test script the PM can run.

## Choosing What to Pass to the Judge

Feed only what the judge needs for an accurate decision:

| Failure Mode | What the Judge Needs |
|-------------|---------------------|
| Tone mismatch | Client persona + generated email |
| Answer faithfulness | Retrieved context + generated answer |
| SQL correctness | User query + generated SQL + schema |
| Instruction following | System prompt rules + generated response |
| Tool call justification | Conversation history + tool call + tool result |

For long documents, feed only the relevant snippet, not the entire document.

## Model Selection

Start with the most capable model available. The same model used for the main task works as judge (the judge performs a different, narrower task). Optimize for cost later once alignment with human labels is confirmed.

## Output

Claude Code produces:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 JUDGE PROMPT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Failure mode: [name]

[Complete judge prompt — copy-pasteable]

TEST RESULTS:
Ran against [N] labeled examples.
Agreement with human labels: [%]

NEXT STEPS:
- If agreement > 80%: Deploy judge in eval pipeline
- If agreement < 80%: Review disagreements, refine definitions
- Need more test data? → /generate-test-data

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## What to Tell Your Engineer

When handing off the judge prompt:
- The prompt is self-contained — paste it into whatever eval harness you use.
- It checks ONE failure mode. Build separate judges for separate failure modes.
- Run it against the test split (not training split) to validate.
- Track agreement with human labels over time. If it drifts, update the few-shot examples.

## Anti-Patterns

- Vague criteria like "is this helpful?" Target a specific failure mode from error analysis.
- One judge covering multiple dimensions. Produces unactionable verdicts.
- No few-shot examples. Without examples, the model won't know what counts as a failure in your application.
- Dev/test examples used as few-shot. This is data leakage.
- Likert scales (1-5, letter grades). Binary pass/fail only. Likert scales produce scores that sound precise but can't be calibrated.
- Skipping validation against human labels before trusting the judge.
- Building judges for failures you haven't observed in real traces.

---

**Methodology:** Adapted from Hamel Husain's write-judge-prompt skill (evals-skills, MIT license)
**PM adaptation:** PM defines failure mode and provides examples, Claude Code generates prompt and test harness
