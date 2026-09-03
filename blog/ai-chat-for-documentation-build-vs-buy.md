---
title: "AI chat for documentation: should you build or buy?"
description: "The real cost of building retrieval-based AI chat for your docs versus buying it — engineering weeks, model spend, and where each option breaks."
---

# AI chat for documentation: should you build or buy?

You decided your docs need AI chat. The next decision matters more than people expect — it determines 3–6 weeks of engineering and the next 18 months of model-cost optimization.

This is the honest cost breakdown in 2026.

## TL;DR

| | Build it | Buy it |
|---|---|---|
| Initial cost | 3–6 engineer weeks of build | Setup time, measured in hours |
| Monthly cost | Vector store, embeddings, model calls, and the person who owns it | A subscription or metered usage, depending on the vendor |
| Time to live | Weeks to months | Hours |
| Customization | Full | Hooks, system prompt, provider |
| Maintenance | Continuous — retrieval quality decays as docs change | The vendor's problem |
| Best for | Specific RAG needs, non-docs use cases | Documentation specifically |

For documentation specifically, buy it. Build it only if your AI chat needs extend beyond docs — knowledge base + product help + support deflection across multiple surfaces.

## What "build it" actually requires

A production RAG (Retrieval-Augmented Generation) pipeline for docs has six components:

### 1. Content ingestion

- Watch your docs source (GitHub, MDX folder, CMS)
- Parse into chunks (typically 500–1500 tokens)
- Handle Markdown, code blocks, tables, frontmatter
- Re-index on every change without rebuilding everything

Engineering: 1 week if you have done it before, 2 weeks if not.

### 2. Embedding

- Pick an embedding model (OpenAI text-embedding-3-small, Cohere, or open source)
- Embed every chunk
- Re-embed when the source changes
- Handle rate limits and batching

Engineering: 3–5 days.

### 3. Vector store

- Pick storage (Pinecone, Weaviate, pgvector, Qdrant, Turbopuffer)
- Schema design (metadata, namespaces per workspace)
- Querying performance
- Backup and migration plan

Engineering: 1 week. Ongoing infrastructure: $50–300/month.

### 4. Query pipeline

- Embed the user query
- Retrieve top-K chunks
- Rerank (often a second model call)
- Format into prompt with context
- Call the LLM
- Parse and return the answer

Engineering: 1–2 weeks.

### 5. Frontend

- Chat UI component
- Streaming response handling
- Citations linking back to source pages
- Conversation memory
- Feedback widget (thumbs up/down)

Engineering: 1 week.

### 6. Observability and analytics

- Log every query and answer
- Track unanswered queries (your future content gaps)
- Track negative feedback
- Cost per query
- Latency P50/P95/P99

Engineering: 1 week.

**Total**: 6 engineer-weeks minimum, often 10+ once edge cases land.

## Recurring costs of "build it"

Per month at moderate usage (1,000 queries):

| | Cost |
|---|---|
| Vector store | $50–300 |
| Embedding API | $10–50 |
| LLM API (GPT-4 class) | $100–400 |
| Logging/observability | $20–100 |
| Engineering maintenance (2 hours/week × $100/hr) | $800 |
| **Total** | **$980–1,650/mo** |

At 10,000 queries the model cost dominates. At 100,000 queries you need caching, rate limiting, and possibly a smaller model for cheap queries.

## What "buy it" looks like

Three categories of "buy it" exist:

### Standalone docs chat product

Bring your docs URL, get a chat widget. Examples: kapa.ai, intercom Fin, custom GPTs.

- **Cost**: $30–500/month depending on volume
- **Pros**: independent of your docs platform
- **Cons**: separate dashboard, separate billing, separate analytics, often does not have read access to your source files

### Docs platform with AI included

Docsbook, Mintlify, GitBook ship AI chat as a feature. The chat is trained on your content and integrated into the docs UI.

- **Cost**: a subscription on Mintlify and GitBook, metered AI usage on Docsbook — read each vendor's own pricing page
- **Pros**: one platform, one bill, native integration, one analytics view
- **Cons**: your choice of provider is the platform's choice

### Self-hosted open-source RAG

Examples: Anything LLM, Chainlit, custom LangChain stack. You self-host and integrate.

- **Cost**: hosting only + your time
- **Pros**: full control
- **Cons**: same engineering load as "build it" minus the prompt engineering

## When to actually build

Build only when one or more of these apply:

1. **Multi-source RAG** — you want one chat that pulls from docs + your CRM + your knowledge base + Slack history
2. **Strict residency requirements** — every byte must stay in your VPC and your DPA
3. **Custom retrieval logic** — your content has structure (graph, hierarchy) that off-the-shelf retrieval cannot exploit
4. **Already-existing platform** — you have a customer-facing AI surface that needs to extend to docs

If documentation is the only surface, buy.

## What you can customize on Docsbook AI chat

Docsbook gives you more control than most managed options:

- **Provider** — OpenAI, Anthropic, Gemini, OpenRouter. Bring your own API key, pick your model.
- **System prompt** — full text replacement
- **Pre/post hooks** — intercept a query before the model call, post-process the answer
- **Usage** — metered in dollars against the project's balance; when the balance runs out the assistant stops answering rather than billing further

If you outgrow these knobs, the "build it" math changes — but most teams do not.

## The actual decision

Three questions, in order:

1. **Are docs the only AI surface you need?** Yes → buy. No → consider building, because the pipeline is then shared across several surfaces.
2. **Do you have someone who will own retrieval quality for the next eighteen months?** No → buy. The pipeline is not the hard part; keeping its answers good as the docs change is.
3. **Is the subscription cost material against an engineer's time?** Compare a month of the platform against a day of the person who would otherwise maintain it, using your own numbers.

Buying is the right answer for most teams for one structural reason: docs AI is a maintenance commitment, not a build. The teams that should build are the ones building a broader AI product where documentation is one surface among several.

## Related reading

- [AI documentation platforms compared (2026)](./ai-docs-platform-comparison.md)
- [Documentation analytics: what to track in 2026](./documentation-analytics-what-to-track.md)
- [API documentation best practices in 2026](./api-documentation-best-practices-2026.md)

---

Docsbook AI chat: bring your own provider, set your own system prompt, and hook the request before and after the model call. Cost is metered in dollars against the project's balance rather than sold as a tier — current numbers on [docsbook.io/pricing](https://docsbook.io/pricing).

[Start free — no credit card](https://docsbook.io/start)
