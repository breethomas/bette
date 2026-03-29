# Example: Domains Reference File

An annotated example of a product domains reference file. Generalized from a real implementation.

---

```markdown
# Product Domains Reference

Quick lookup for Claude.

**Last updated:** 2026-03-01

---

## Domain Map
                                          # ← Table format. Scannable.
                                          #   AI uses this to map conversations
                                          #   to the right domain context.

| Domain | PM Owner | Eng Lead | Scope |
|--------|----------|----------|-------|
| Platform | Carol | Frank (Grace) | Auth, billing, API, integrations |
| Growth | Eve | Hank | Onboarding, activation, self-service |
| Intelligence | [interim] | Iris | Signals, rules, data foundation |
| Messaging | — | Leo | Email, SMS, push delivery |

                                          # ← "(Grace)" = principal engineer.
                                          #   "[interim]" = no permanent owner.
                                          #   "—" = no PM (eng-only domain).

## Acronyms & Product Terms
                                          # ← Every acronym the AI will
                                          #   encounter in conversations,
                                          #   Slack, Linear, or docs.

- **CEP** — Customer Experience Portal. Main user-facing dashboard.
- **HBN** — Network product. Auto-matching partners with clients.
- **GOTS** — Get On The System. Client loading/engagement metric.
- **DBO** — Database Optimization. "Load them all" initiative.

## Architecture Layers
                                          # ← Numbered = sequential/layered.
                                          #   Helps the AI understand how
                                          #   data flows through the system.

1. **Data ingestion** — imports, API, integrations
2. **Intelligence** — signals, rules, partner logic
3. **Surfaces** — dashboards, AI chat, reports
4. **Delivery** — email, SMS, push notifications

## Segments
                                          # ← Customer segments affect
                                          #   how features are built and
                                          #   rolled out.

- **SMB** — Self-service. Quick onboarding, simple needs.
- **Enterprise** — ~50% of revenue. Feature flags, longer rollouts.

## Key Customers
                                          # ← Only include customers the AI
                                          #   will encounter in conversations.

- **Acme Corp** — Largest customer, $1.3M ARR. Loudest on feature requests.
- **GlobalCo** — Enterprise. Custom SSO + API work. ~$20k/mo.
```

---

## Design Choices

**Table for domain map.** The most information-dense format. Domain → owner → eng lead → scope in one scannable view. The AI uses this constantly to understand "who owns this?" and "what team does this belong to?"

**Bullet points for terminology.** Quick definitions. The AI encounters these acronyms in transcripts and Slack — it needs instant lookup, not detailed explanations.

**Numbered list for architecture.** Sequence matters. Data flows from ingestion → intelligence → surfaces → delivery. Numbering communicates this.

**Segments and key customers are operational context.** When someone says "this is an enterprise request" or "Acme wants this," the AI needs to know what that implies (feature flags, careful rollout, high revenue risk).

**This file does NOT include:**
- Implementation details (database names, repo structure)
- Engineering architecture (microservices, APIs, infrastructure)
- Historical decisions or rationale

Those belong in separate docs, loaded on demand. The domains reference is for day-to-day conversational context.
