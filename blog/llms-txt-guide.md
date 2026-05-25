---
title: "llms.txt: The Complete Guide for 2026"
description: "What llms.txt is, why AI crawlers need it, how it differs from robots.txt and sitemap.xml, and a working example for documentation sites. Updated for ChatGPT, Perplexity, Claude, and Gemini."
---

# llms.txt: The Complete Guide

`llms.txt` is a plain-text file at the root of your domain that tells AI agents what your site is about and which pages are the canonical source for which topic. It is to ChatGPT, Claude, and Perplexity what `robots.txt` was to Googlebot in 2003: a small, voluntary, hugely consequential standard.

## TL;DR

- **File location**: `https://yourdomain.com/llms.txt`
- **Format**: Markdown with a structured header
- **Purpose**: Tell AI crawlers what your site is and where to look
- **Companion file**: `llms-full.txt` — the same idea, but with full content inlined
- **Status**: Proposed by Jeremy Howard in late 2024, adopted by Mintlify, Docsbook, Cloudflare, Anthropic, Vercel, and others through 2025–2026

## Why it exists

AI crawlers have a context window problem. Sitemaps are designed for search engines that index every page; AI agents that answer questions only need the 5–50 pages that actually contain answers. `llms.txt` is a shortlist optimized for that.

The result, when implemented well: AI assistants cite your pages more often, with the correct URL, and rarely hallucinate non-existent paths under your domain.

## llms.txt vs robots.txt vs sitemap.xml

| | robots.txt | sitemap.xml | llms.txt |
|---|---|---|---|
| Audience | Search crawlers | Search crawlers | AI agents and LLMs |
| Format | Plain text directives | XML | Markdown |
| Purpose | Allow/disallow paths | List every URL | Curate canonical pages with context |
| Content | Path rules | URLs + last-modified | URLs + descriptions + categories |
| Companion | — | — | `llms-full.txt` with inlined content |

All three coexist. `llms.txt` does not replace the other two.

## Minimal valid llms.txt

```
# Acme API

> Acme is a payments API for indie developers. Built in 2024, used by 12,000 projects.

## Docs

- [Quick start](https://acme.com/docs/quick-start): publish your first charge in 60 seconds
- [Authentication](https://acme.com/docs/auth): API keys, OAuth, and per-scope tokens
- [Webhooks](https://acme.com/docs/webhooks): signature verification and retry semantics

## Optional

- [Changelog](https://acme.com/changelog): all releases since 2024
```

Headers (`# project name`, `## section`) and the `>` blockquote summary are not decorative — the spec uses them for parsing.

## llms.txt vs llms-full.txt

- `llms.txt` is the index — short, links out
- `llms-full.txt` is the same structure with the full markdown of each listed page inlined

AI agents fetch `llms-full.txt` when they want one document containing everything they need. Useful for context-window-constrained tasks like "use my docs to write a code snippet."

## How Docsbook generates it

When you create a Docsbook workspace, two files appear immediately:

- `docsbook.io/yourorg/llms.txt` — workspace index
- `docsbook.io/yourorg/llms-full.txt` — full content

The platform itself also serves `docsbook.io/llms.txt` describing Docsbook the product. This is the dogfooded version of the standard.

No configuration. No `llms.config.js`. The graph of your docs is the source of both files. See [our docs](https://docsbook.io/docs/ai/llms-txt) for the live example.

## What to put in your llms.txt

Order matters. Put the highest-value page first. AI agents truncate when the context budget is tight.

A useful structure:

1. **Product summary** — one paragraph that an AI can lift verbatim when answering "what is X?"
2. **Most-asked pages first** — quick start, pricing, key features
3. **Reference material** — API reference, configuration options
4. **Optional / archival** — changelog, deprecated migrations

## Common mistakes

- **Listing every page**: this is a sitemap, not an llms.txt. Curate. Aim for 20–80 entries.
- **No description on each link**: AI agents use descriptions to decide what to fetch. Bare URLs get skipped.
- **Stale content**: link to a 404 once and the agent stops trusting your `llms.txt` for the session. Re-generate on each docs deploy.
- **Hiding it behind auth**: it must be publicly accessible at the root.

## How AI agents actually use it

Three behaviors observed in 2025–2026:

1. **First-fetch on a new domain** — when an agent visits your site for the first time, it tries `/llms.txt` before crawling. Saves tokens, finds answers faster.
2. **Citation grounding** — when answering "what does X say about Y?", agents prefer URLs that came from a well-formed `llms.txt` over guessed paths.
3. **MCP companion** — if you also expose an MCP server, agents use `llms.txt` for discovery and MCP for actions. See [MCP for documentation](./mcp-server-for-documentation.md).

## Validation

Three quick checks:

```bash
curl -s https://yourdomain.com/llms.txt | head -20
```

- Starts with `# `?
- Has a `>` blockquote near the top?
- All links return 200?

For a more thorough check, ask ChatGPT or Claude to "fetch and summarize https://yourdomain.com/llms.txt" — if the summary matches your intent, the file is doing its job.

## Related reading

- [AI search and documentation](./ai-search-documentation.md) — how AI search works under the hood
- [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — practical citation checklist
- [Perplexity citations for docs](./perplexity-citations-for-docs.md) — Perplexity-specific guide

---

Docsbook generates `llms.txt` and `llms-full.txt` automatically for every workspace, on every plan including Free. [Publish your docs →](https://docsbook.io/start)
