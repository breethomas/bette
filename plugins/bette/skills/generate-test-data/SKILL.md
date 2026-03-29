---
name: generate-test-data
description: >
  Create diverse synthetic test inputs using dimension-based tuple generation.
  Use when bootstrapping an eval dataset, when real user data is sparse, or
  when stress-testing specific failure hypotheses. Do NOT use when you already
  have 100+ representative real traces (use stratified sampling instead).
---

# Generate Test Data

Generate diverse, realistic test inputs that cover the failure space of an LLM pipeline. Dimension-based tuples, not random generation.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GENERATE TEST DATA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Diverse inputs expose the failure space. Random generation doesn't.

What AI feature are we generating test data for?
What kinds of inputs does it take?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Prerequisites

Before generating synthetic data, identify where the pipeline is likely to fail. Ask the PM about known failure-prone areas, review existing user feedback, or form hypotheses from available traces. Dimensions (Step 1) must target anticipated failures, not arbitrary variation.

## Core Process

### Step 1: Define Dimensions

Dimensions are axes of variation specific to the application. The PM defines these — they know where failures happen.

```
Dimension 1: [Name] — [What it captures]
  Values: [value_a, value_b, value_c, ...]

Dimension 2: [Name] — [What it captures]
  Values: [value_a, value_b, value_c, ...]

Dimension 3: [Name] — [What it captures]
  Values: [value_a, value_b, value_c, ...]
```

Example for a customer support chatbot:

```
Query Type: what the user is asking about
  Values: [billing, technical issue, account access, feature request, cancellation]

User Expertise: how technical the user is
  Values: [non-technical, somewhat technical, power user]

Complexity: how many steps to resolve
  Values: [single-step, multi-step, requires escalation]
```

Start with 3 dimensions. Add more only if initial traces reveal failure patterns along new axes.

Ask the PM: "What are the 3 most important ways inputs vary for your feature? Think about what makes some inputs harder than others."

### Step 2: Draft 20 Tuples with the PM

A tuple is one combination of dimension values defining a specific test case. Present 20 draft tuples to the PM and iterate until they confirm the tuples reflect realistic scenarios.

```
(Query Type: Billing, User Expertise: Non-technical, Complexity: Multi-step)
(Query Type: Technical Issue, User Expertise: Power User, Complexity: Single-step)
(Query Type: Cancellation, User Expertise: Non-technical, Complexity: Requires Escalation)
```

The PM's domain knowledge is essential. They know which combinations actually occur and which are unrealistic.

Claude Code executes: Generate the initial 20 tuples ensuring coverage across dimension values. Present to PM for validation.

### Step 3: Expand Tuples with LLM

Claude Code executes: Generate additional tuples using the PM-validated set as examples.

```
Generate 10 random combinations of ({dim1}, {dim2}, {dim3})
for a {application description}.

The dimensions are:
{dim1}: {description}. Possible values: {values}
{dim2}: {description}. Possible values: {values}
{dim3}: {description}. Possible values: {values}

Output each tuple in the format: ({dim1}, {dim2}, {dim3})
Avoid duplicates. Vary values across dimensions.
```

### Step 4: Convert Tuples to Natural Language Queries

Separate step from tuple generation. Single-step generation (tuples + queries together) produces repetitive phrasing.

Claude Code executes: Convert each tuple to a realistic user query using a separate prompt per tuple.

```
We are generating synthetic user queries for a {application}.
{Brief description of what it does.}

Given:
{dim1}: {value}
{dim2}: {value}
{dim3}: {value}

Write a realistic query that a user might enter. The query should
reflect the specified characteristics.

Example: "{one of the PM-written examples}"

Now generate a new query.
```

### Step 5: Filter for Quality

Review generated queries with the PM. Discard and regenerate when:
- Phrasing is awkward or unrealistic.
- Content doesn't match the tuple's intent.
- Queries are too similar to each other.

Claude Code executes: Rate realism using an LLM, discard below threshold, regenerate replacements.

### Step 6: Run Through Pipeline

Execute all queries through the full LLM pipeline. Capture complete traces: input, all intermediate steps, tool calls, retrieved docs, final output.

**Target: ~100 high-quality, diverse traces.** This is a rough heuristic for reaching saturation.

Claude Code executes: Run the queries, capture traces, format for analysis. These traces feed directly into `/upgrade-evals` for error analysis.

## Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 TEST DATA GENERATED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Dimensions: [dim1], [dim2], [dim3]
Tuples generated: [count]
Queries generated: [count]
Queries after filtering: [count]

DIMENSION COVERAGE:
| Dimension | Values Covered | Gaps |
|-----------|---------------|------|
| [dim1]    | [X/Y]        | [any missing] |
| [dim2]    | [X/Y]        | [any missing] |
| [dim3]    | [X/Y]        | [any missing] |

NEXT STEPS:
- Run /upgrade-evals on these traces for error analysis
- Run /build-judge for failure modes that need automated evaluation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## When Real Data Exists

When you have real queries available, don't just sample randomly. Use stratified sampling:

1. **Identify high-variance dimensions** — read through queries and find ways they differ (length, topic, complexity, presence of constraints).
2. **Assign labels** — for small sets, with the PM; for large sets, use K-means clustering on query embeddings.
3. **Sample from each group** — ensures coverage across query types, not just the most common ones.

Use synthetic data to fill gaps in underrepresented query types.

## Anti-Patterns

- Unstructured generation. "Give me test queries" without dimensions produces generic, repetitive, happy-path examples.
- Single-step generation. Generating tuples and queries in one prompt produces less diverse results.
- Arbitrary dimensions. Dimensions that don't target failure-prone regions waste test budget.
- Skipping PM review of tuples. Without the PM validating tuples, you can't judge realism.
- Synthetic data when no one can judge realism. If no one can tell whether a synthetic trace is realistic, use real data.
- Synthetic data for complex domain-specific content (legal filings, medical records) where LLMs miss structural nuance.

---

**Methodology:** Adapted from Hamel Husain's generate-synthetic-data skill (evals-skills, MIT license)
**PM adaptation:** PM defines dimensions and validates realism, Claude Code handles generation and pipeline execution
