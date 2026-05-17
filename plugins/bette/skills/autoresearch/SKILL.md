---
name: autoresearch
description: "Automated improvement loop for any PM artifact. Define what 'better' means, then let the agent iterate. Uses Karpathy's autoresearch pattern. Say 'autoresearch my [thing]', 'optimize this automatically', 'run the improvement loop'."
user-invocable: true
---

# Autoresearch

Apply Karpathy's autoresearch pattern: define an evaluable "better" criterion, then iterate on the artifact in a loop, scoring each pass against the criterion until improvement plateaus or a stop condition is hit.

The pattern, succinctly:

1. **Define "better"** — what does an improvement look like? Specific, evaluable, ideally measurable.
2. **Generate a variant** — produce a candidate improvement.
3. **Score it** — against the criterion. Honestly.
4. **Decide** — keep, discard, or iterate further.
5. **Stop** — when scores plateau, when a budget is hit, or when the user calls it.

Apply this to whatever the user wants to improve — a PRD, a Slack message, a roadmap, a spec, a prompt, a meeting agenda. Adapt the criterion to the artifact.

## Avoid

- Iterating without a clear "better" criterion — that's just spinning
- Loop without a stop condition — be explicit about when to stop
- Treating subjective artifacts as if they have an objective score

## Source

Andrej Karpathy's autoresearch framing. No dedicated framework doc in the plugin yet — a TODO to add `thought-leaders/andrej-karpathy.md` and a proper framework writeup.
