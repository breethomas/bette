---
name: eval-rag
description: >
  Evaluate RAG pipeline retrieval and generation quality separately. Measure
  Recall@k, Precision@k, MRR, NDCG@k for retrieval. Assess faithfulness and
  relevance for generation. Use when the AI feature uses retrieval (search,
  knowledge base, document QA). Do NOT use for non-RAG AI features.
---

# Eval RAG

Load these into context before responding:

- `../../frameworks/ai/ai-evals.md` — eval methodology overview
- `../../frameworks/ai/pm-friendly-evals-guide.md` — Aman Khan / Hamel Husain PM-friendly evals
- `../../thought-leaders/aman-khan.md` — Aman's perspective on PM-owned evals

Help the user evaluate a RAG pipeline. Separate retrieval quality (Recall@k, Precision@k, MRR, NDCG@k) from generation quality (faithfulness, relevance). The two failure modes are different — measure them separately so the fix lands on the right side of the pipeline.

## When this skill is the wrong fit

- The feature doesn't use retrieval — use general evals workflow instead
- The user wants overall quality only, not retrieval-vs-generation breakdown — those numbers will hide which side is broken

## Avoid

- Conflating retrieval and generation in one score — that's how teams ship hallucination fixes that don't fix anything
- Skipping a labeled retrieval set — without ground truth for relevant docs, retrieval metrics are guesses
