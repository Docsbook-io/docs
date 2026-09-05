---
title: "Get cited by AI and found by search"
description: "The Docsbook surfaces that make your product readable and quotable by Google, ChatGPT, Perplexity and any coding agent: SEO, GEO, AEO, llms.txt, the MCP server and the source-of-truth graph."
---

# Get cited by AI and found by search

This is the job from ["I want ChatGPT to recommend us when a customer asks"](../use-cases.md#i-want-chatgpt-to-recommend-us-when-a-customer-asks): an assistant or a search engine recommends what it can read and check cheaply. If nothing is readable, it quotes a competitor instead.

Every page below is part of the same retrieval side of the product, and they do not overlap:

| Surface | What it does | Who reads it | Page |
|---|---|---|---|
| SEO | Meta tags, sitemap.xml, OpenGraph, canonical URLs | Google, Bing and every classical crawler | [SEO](./seo.md) |
| GEO | TL;DR block, visible last-modified date, author attribution | Perplexity, ChatGPT Search, AI Overviews | [GEO](./geo.md) |
| AEO | FAQPage, HowTo and speakable JSON-LD generated from your Markdown | Answer boxes and voice assistants | [AEO](./aeo.md) |
| `llms.txt` | A plain-text index of your docs, served at the site root | AI crawlers and assistants that look for one | [llms.txt](./llms-txt.md) |
| MCP server | 309 tools over the Model Context Protocol | Claude Code, Cursor, Codex, and any MCP client | [MCP server](./mcp.md) |
| Source of Truth | A document graph an agent navigates on its own machine | An agent working on your checked-out repository | [Source of truth](./source-of-truth.md) |

None of this costs anything to serve — `llms.txt`, SEO and AEO markup and the Source of Truth graph are generated from content you have already published. The MCP server draws on your project balance per metered call; see [MCP security](./mcp-security.md) for the current compliance position and [Docsbook pricing](https://docsbook.io/pricing) for current figures.

## Where should I start?

Start with [llms.txt](./llms-txt.md) if assistants describe your product wrongly, or not at all. Start with [SEO](./seo.md) if the problem is that Google does not rank you. Start with the [MCP server](./mcp.md) if you want your own agent doing the writing.

## Related

- [Answer readers with AI chat](../ai-chat/README.md) — the other half of the AI layer: an assistant that answers ON your own site
- [Use cases](../use-cases.md) — the situations teams bring to Docsbook
- [Overview](../overview.md) — how these pieces fit together, end to end
