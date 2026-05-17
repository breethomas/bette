# Prompt Engineering for Product Managers

**Category:** AI-Era Practices
**Anchor sources:** Anthropic prompt engineering docs; Aakash Gupta (Product Growth, Reforge); Aman Khan (Arize); Hamel Husain (independent, on evals)
**Last Updated:** May 2026

## Headline

Prompt engineering is product design expressed as text. PMs own it because the choices encoded in a prompt are product decisions, not engineering decisions. What to optimize for, how to handle edge cases, what voice the product speaks in.

The field has shifted. **Modern prompt engineering is half prompt-writing and half eval-running.** The prompt is the artifact you ship. The eval suite tells you whether it's working. Engineering a prompt without engineering the eval is optimizing in the dark.

## Why PMs own prompts

Four reasons, in order of leverage:

1. **User understanding.** You talked to users. You know which outputs land. The prompt encodes that judgment.
2. **Product strategy.** Every prompt is opinionated about what the product values. Helpfulness vs accuracy. Brevity vs completeness. Agency vs caution. PM territory.
3. **Iteration speed.** A PM who can write and revise the prompt ships 10× faster than one waiting for an engineer.
4. **Pattern recognition.** User feedback exposes failure modes. The PM who triages it is best-placed to update the prompt.

This doesn't mean PMs ship prompts unsupervised. PMs draft, iterate, own the spec. Engineering owns the wiring (caching, fallbacks, retries, monitoring).

## The eval loop is the unit, not the prompt

2024 model: write a prompt, eyeball outputs, ship. 2026 model: write a prompt, run it against a labeled eval set, fix the failures, ship the prompt + the eval suite together.

Aman Khan and Hamel Husain have crystallized this. A prompt that performs well on five hand-picked examples isn't a working prompt. It's a working illusion. You need:

1. **A labeled eval set** (start with 20, grow to 50-100+ as failures surface)
2. **A failure taxonomy** that emerges from real outputs, not theory
3. **An iteration cadence** where each prompt change is graded against the eval set
4. **A shipping bar** that says "we don't ship if eval pass rate is below X"

Iterating on a prompt without an eval suite? Stop. Build the eval first. Bette's `/start-evals` and `/upgrade-evals` walk through this.

## Anthropic-specific guidance

How Claude reads prompts most reliably.

**Structure with XML tags.** Claude is trained to recognize XML-style structure. Use `<instructions>`, `<context>`, `<examples>`, `<format>` to separate sections. Big reliability lift vs prose-only.

**Be clear and direct.** "Summarize this in 3 bullet points" beats "Could you maybe condense this a bit?" Ambiguous polite phrasing leaks ambiguity into the output.

**Use prompt caching for production.** Static prompt prefixes get cached at the API level and cost a fraction to re-use. Put static parts (system instructions, examples, persistent context) at the top. Variable parts (user input) at the bottom. Caching cuts production costs without changing quality.

**Show, don't just tell.** Examples in `<examples>` blocks teach the output shape better than describing it in prose. 2-4 examples usually beats 0 or 10.

**Give the model an out.** Tell it what to do when it doesn't know. "If the user's question is unclear, ask one clarifying question instead of guessing." Prevents hallucination.

## Quality first, cost second (Aakash's hill-climb)

Aakash Gupta's framing: optimize for output quality first, cost second.

**Phase 1: climb quality.**
- Add structure (XML tags, role definition)
- Add examples (few-shot)
- Add reasoning scaffolds (chain-of-thought for complex tasks)
- Specify output format precisely
- Add edge case guidance based on observed failures

This phase adds tokens. Fine. Get the prompt working first.

**Phase 2: descend cost.**
- Remove redundant examples once the pattern is locked
- Compress role definitions to essentials
- Cache static prefixes
- Move per-request context to the variable section
- Consider a smaller model for sub-tasks (orchestrator-worker)

Reversing this order is the most common waste. Teams optimize cost on a prompt that doesn't work yet.

## Core patterns worth knowing

Four patterns. Apply when warranted. Don't run a checklist.

1. **Role and audience definition.** "You are a [role] writing for [audience] who needs [outcome]." Anchors voice, vocabulary, and depth in one line.
2. **Chain-of-thought for complex reasoning.** "Think step by step before giving your final answer." Improves accuracy on multi-step tasks. Skip for simple classification.
3. **Few-shot examples.** Two or three input → output examples showing the desired shape. Crucial when the format is unusual or the judgment call is subtle.
4. **Output format specification.** "Respond in JSON with keys: `summary`, `next_steps`, `confidence`." If you need structure, name it. Don't make the model infer.

## Production prompts vs one-off prompts

Different problems. PMs often confuse them.

**One-off prompts** (using Claude to think through something now): minimal structure, no examples needed, no eval suite. Just talk.

**Production prompts** (will run thousands of times, ship in a product): full structure, examples, evals, caching, version control, A/B-testable, monitoring. The discipline isn't optional. It's what separates "the demo worked" from "the feature ships."

Users will hit it? Production. Drafting an email? One-off.

## Prompts for agentic workflows

When the prompt is for an agent, priorities shift. Load `frameworks/ai-era-practices/agent-workflow-design.md` for the full picture. Briefly:

- **System prompt** describes the agent's persistent identity, tools, operating rules
- **Sub-agent prompts** need objective, output format, tool guidance, boundaries (the "sub-agent spec" pattern)
- **Memory and context budgets** matter more than for single-shot. See `pm-memory-architecture.md`.
- **Evals shift** from "does the output match expected" to "did the agent take a sensible trajectory." Hamel Husain and Aman Khan's evals work is essential here.

## Common mistakes

- **Iterating without evals.** Prompt feels better. Can't prove it. Next failure is a surprise.
- **Optimizing cost before quality.** Strips load-bearing structure, breaks the prompt.
- **No examples.** Especially in production. The single biggest reliability win in most cases.
- **Long polite ramble.** "Could you please consider, if it's not too much trouble..." Claude absorbs the ambiguity.
- **Treating the system prompt as a one-time write.** Production prompts iterate on production failure data. The launch prompt should not be the six-month prompt.
- **No version control on prompts.** Product surface deserves git history.
- **Prompting for the demo, not the user.** Optimizing on five examples you picked. Real users hit edge cases you didn't.

## When to use this framework

- Designing a new AI feature's prompt(s)
- Diagnosing why a production prompt is inconsistent or low-quality
- Onboarding a PM to prompt engineering as a craft
- Pushing back on "make it cheaper" before the prompt has been measured

## See also

- `frameworks/ai/pm-friendly-evals-guide.md` — Aman Khan's PM-readable evals framework
- `frameworks/ai/ai-evals.md` — broader evals methodology
- `frameworks/ai-era-practices/agent-workflow-design.md` — when the prompt is for an agent
- `frameworks/ai-era-practices/pm-memory-architecture.md` — context and memory in production prompts
- `thought-leaders/aakash-gupta.md` — quality-then-cost hill-climb
- `thought-leaders/aman-khan.md` — evals-first prompt iteration
- `frameworks/ai-era-practices/continuous-calibration.md` — how production prompts evolve post-launch

## Resources

- Anthropic prompt engineering docs: [docs.claude.com](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering)
- Anthropic prompt caching: [docs.claude.com/en/docs/build-with-claude/prompt-caching](https://docs.claude.com/en/docs/build-with-claude/prompt-caching)
- Aman Khan — "Beginner's Guide to AI Evals (Walkthrough)" ([Substack](https://amankhan1.substack.com/p/beginners-guide-to-ai-evals-walkthrough))
- Aman Khan — "AI PM Crash Course 2026: Prototyping → Observability → Evals" ([podcast](https://www.news.aakashg.com/p/aman-khan-podcast))
- Hamel Husain — independent writing on evals
- Aakash Gupta — "Quality First, Cost Second" prompt engineering framing ([Product Growth](https://www.news.aakashg.com/))
