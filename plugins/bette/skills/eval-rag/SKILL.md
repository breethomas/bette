---
name: eval-rag
description: >
  Evaluate RAG pipeline retrieval and generation quality separately. Measure
  Recall@k, Precision@k, MRR, NDCG@k for retrieval. Assess faithfulness and
  relevance for generation. Use when the AI feature uses retrieval (search,
  knowledge base, document QA). Do NOT use for non-RAG AI features.
---

# Eval RAG

Evaluate RAG pipelines by separating retrieval quality from generation quality. Fix retrieval first.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 EVAL RAG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Retrieval and generation fail differently. Measure them separately.

What RAG feature are we evaluating?
What does it retrieve from? (knowledge base, docs, database)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Prerequisites

Complete error analysis (`/upgrade-evals`) on RAG pipeline traces before selecting metrics. Inspect what was retrieved vs. what the model needed. Determine whether the problem is retrieval, generation, or both. Fix retrieval first — the LLM can ignore irrelevant context but cannot generate from missing context.

## Core Process

### Step 1: Separate Retrieval from Generation

Ask the PM: "When the AI gives a wrong answer, is it because it found the wrong documents, or because it had the right documents but said the wrong thing?"

This determines where to focus:

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| AI says "I don't know" or gives generic answer | Retrieval: relevant docs not found | Improve chunking, embeddings, or query |
| AI confidently states something not in any doc | Generation: hallucination | Improve prompt, add grounding |
| AI answers a different question than asked | Could be either | Check retrieved docs first |

### Step 2: Build a Retrieval Evaluation Dataset

Queries paired with ground-truth relevant document chunks.

**Manual curation (highest quality, PM-driven):**
Ask the PM: "For each of these test queries, which document(s) actually contain the answer?"

The PM maps queries to chunks. This is domain knowledge work — the PM knows the content better than any automated system.

**Synthetic QA generation (scalable):**

Claude Code executes: For each document chunk, extract a fact and generate a question answerable only from that fact.

```
Given a chunk of text, extract a specific, self-contained fact from it.
Then write a question that is directly and unambiguously answered
by that fact alone.

Return output in JSON format:
{ "fact": "...", "question": "..." }

Chunk: "{text_chunk}"
```

**Adversarial questions (stress-testing):**

Claude Code executes: Create queries that resemble content in multiple chunks but are only answered by one. Find similar chunks via embedding search, then generate a question that only the target chunk answers.

### Step 3: Measure Retrieval Quality

Claude Code executes all metric computations. The PM interprets results.

**Recall@k** — Did we find the right documents?
```
Recall@k = (relevant docs in top k) / (total relevant docs for query)
```
Prioritize for first-pass retrieval. High recall = the right docs are in the candidate set.

**Precision@k** — How much noise in the results?
```
Precision@k = (relevant docs in top k) / k
```
Prioritize for reranking evaluation.

**MRR (Mean Reciprocal Rank)** — How quickly do we find the first right document?
```
MRR = (1/N) * sum(1/rank_of_first_relevant_doc)
```
Best for single-fact lookups.

**NDCG@k** — Are the most relevant results ranked highest?
```
DCG@k  = sum over i=1..k of: rel_i / log2(i+1)
IDCG@k = DCG@k with documents sorted by decreasing relevance
NDCG@k = DCG@k / IDCG@k
```
Use when documents have varying utility.

**Which metric to use:**

| Your Query Type | Primary Metric | Why |
|----------------|---------------|-----|
| Single-fact lookups ("What's our refund policy?") | MRR | One key chunk needed, want it ranked first |
| Broad coverage ("Summarize market trends") | Recall@k | Need all relevant docs, even at cost of noise |
| Ranked results matter | NDCG@k or Precision@k | Quality of ranking matters for the answer |

**Choosing k:** Factual lookup uses k=1-2. Synthesis query uses k=5-10. Ask the PM: "How many documents does your pipeline pass to the LLM?"

### Step 4: Optimize Chunking (if retrieval is the bottleneck)

Treat chunking as a tunable hyperparameter. Claude Code executes a grid search.

Claude Code executes:

```
Test combinations of chunk size and overlap.
Re-index the corpus for each configuration.
Measure retrieval metrics on the evaluation dataset.
```

Example results:

| Chunk Size | Overlap | Recall@5 | NDCG@5 |
|-----------|---------|----------|--------|
| 128 tokens | 0 | 0.82 | 0.69 |
| 128 tokens | 64 | 0.88 | 0.75 |
| 256 tokens | 0 | 0.86 | 0.74 |
| 256 tokens | 128 | 0.89 | 0.77 |
| 512 tokens | 0 | 0.80 | 0.72 |

Present to PM: "256 tokens with 128 overlap gives the best recall. Want to go with that?"

**Content-aware chunking:** When fixed-size chunks split related information, use natural document boundaries (sections, paragraphs). Augment chunks with context: prepend document title and section headings before embedding.

### Step 5: Evaluate Generation Quality

After confirming retrieval works, evaluate what the LLM does with the retrieved context.

**Answer faithfulness** — Does the output accurately reflect the retrieved context?
- **Hallucinations:** Information absent from source documents. In RAG, even correct facts from the LLM's own knowledge count as hallucinations.
- **Omissions:** Relevant information from the context ignored in the output.
- **Misinterpretations:** Context information represented inaccurately.

**Answer relevance** — Does the output address the original query? An answer can be faithful to the context but fail to answer what the user asked.

Use `/upgrade-evals` to discover specific manifestations in your pipeline. Use `/build-judge` for failure modes that require subjective evaluation.

### Step 6: Diagnose with the Metric Pattern Table

Present this to the PM for root cause identification:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 RAG DIAGNOSTIC TABLE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

| Context Quality | Faithfulness | Relevance | Diagnosis |
|-----------------|-------------|-----------|-----------|
| Good            | Good        | Bad       | Generator attended to wrong section |
| Good            | Bad         | --        | Hallucination or misinterpretation |
| Bad             | --          | --        | Retrieval problem. Fix first. |

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**What to tell your engineer:**
- "Context quality is low" → Fix chunking, embeddings, or query preprocessing.
- "Faithful but not relevant" → Generator needs better instruction to address the actual question.
- "Not faithful" → Add grounding instructions, reduce temperature, or use citation enforcement.

## Multi-Hop Retrieval

For queries requiring information from multiple chunks:

**Two-hop Recall@k:** Fraction of 2-hop queries where both ground-truth chunks appear in top k results.

```
TwoHopRecall@k = (1/N) * sum(1 if {Chunk1, Chunk2} ⊆ top_k_results)
```

Diagnose: classify failures as hop 1 miss, hop 2 miss, or rank-out-of-top-k.

## Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 RAG EVALUATION RESULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Eval dataset: [N] queries with ground-truth mappings

RETRIEVAL:
| Metric | Score | Interpretation |
|--------|-------|---------------|
| Recall@5 | [X] | [good/needs work] |
| Precision@5 | [X] | [good/needs work] |
| MRR | [X] | [good/needs work] |

GENERATION:
| Dimension | Pass Rate | Top Failure Mode |
|-----------|-----------|-----------------|
| Faithfulness | [%] | [description] |
| Relevance | [%] | [description] |

DIAGNOSIS: [Retrieval problem / Generation problem / Both]

RECOMMENDED ACTIONS:
1. [highest-impact fix]
2. [second fix]
3. [third fix]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Anti-Patterns

- Using a single end-to-end correctness metric without separating retrieval and generation.
- Jumping directly to metrics without reading traces first.
- Overfitting to synthetic evaluation data. Validate against real user queries regularly.
- Using similarity metrics (ROUGE, BERTScore, cosine similarity) as primary generation evaluation. Use binary evaluators driven by error analysis.
- Evaluating generation without checking context grounding.
- Optimizing generation when retrieval is the bottleneck.

---

**Methodology:** Adapted from Hamel Husain's evaluate-rag skill (evals-skills, MIT license)
**PM adaptation:** Each metric gets plain-language explanation, Claude Code computes metrics, PM interprets diagnostic table
