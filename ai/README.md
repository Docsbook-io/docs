---
title: "The Docsbook AI layer: every machine-readable surface"
description: "Index of the Docsbook surfaces an AI reads or writes — the docs assistant, the MCP server, llms.txt, connected sources, translations and the skills catalog."
---

# The Docsbook AI layer

Docsbook publishes your documentation twice. Once as pages a person reads, and once as surfaces a machine reads: an assistant trained on your pages, an MCP server your coding agent can call, `llms.txt` for AI crawlers, connected sources the assistant checks before it answers, and translations that give each language its own indexable URL.

This page is the index of those surfaces. Each one has its own page with the detail.

## Which Docsbook AI surface do I need?

Pick by what you are trying to make happen. Every surface below is part of the product; what separates them is who consumes them — your readers, your own agents, or someone else's crawler — and whether using them draws on your project's balance.

| Surface | Who consumes it | What it draws on | Page |
|---|---|---|---|
| AI chat trained on your docs | Your readers, on your docs site | Project balance, per answer | [AI Chat](./chat.md) |
| Translations into 15 languages | Readers in other markets, and search engines | Project balance, per translated page version | [Translations](./translations.md) |
| `llms.txt` and `llms-full.txt` | AI crawlers and assistants | Nothing — generated and served with the site | [llms.txt](./llms-txt.md) |
| Source of Truth doc graph | An agent working on your checked-out repository | Nothing — the graph is built on the agent's machine | [Source of Truth](./source-of-truth.md) |
| Connected sources | The admin assistant and your own MCP agents | Project balance when a source is fetched | [Sources](./sources.md) |
| MCP server | Claude Code, Cursor, Codex, and any MCP client | Project balance, per metered call | [MCP Server](./mcp.md) |
| Pre/post-LLM chat hooks | Your own HTTPS endpoint, inside the chat pipeline | Nothing extra beyond the answer itself | [Chat Hooks](./chat-hooks.md) |
| Docs Skills catalog | Any agent that can read a SKILL.md file | Nothing to install and run locally | [Skills](./skills.md) |

What each of those costs in money is on the [Docsbook pricing page](https://docsbook.io/pricing.md), which is generated from the live billing constants on every request.

## How does Docsbook decide which pages an assistant sees?

Docsbook builds every machine-readable surface from the same indexed content: the Markdown in your connected GitHub repository. The chat, the translations and the hooks sit on top of that index. The MCP server and `llms.txt` expose the same index outward, so a Claude Code session can read your docs, write a translation, or change your branding without leaving the editor.

Nothing is published to a machine surface that is not already published as a page. A page you have not committed is not in `llms.txt`, not in the chat's search, and not readable over MCP.

The Source of Truth doc graph is the exception, and deliberately so: it runs on the agent's own machine through [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) (`npx markdown-lsp <subcommand> ./docs`), against your working tree rather than against anything hosted. Unpublished drafts stay on the machine.

## Where should I start?

Start with [AI Chat](./chat.md) if readers already arrive and leave without an answer. Start with [llms.txt](./llms-txt.md) and [Sources](./sources.md) if the problem is that assistants describe your product wrongly, or not at all. Start with the [MCP Server](./mcp.md) if you want your own agent doing the work.

Whichever you start with, connect your [Sources](./sources.md) early. A connected source is what stops the assistant answering about your product from memory: with a repository or a site registered, "update the documentation" begins by reading it, rather than by guessing at a price or a version number.

## How your docs get found and cited

Three pages cover the retrieval side of the same layer, and they do not overlap:

- [SEO](../content/features/seo.md) — the classical search surface: static HTML, meta tags, sitemap, canonical URLs, `noindex`.
- [AEO](../content/features/aeo.md) — answer boxes and voice: `FAQPage`, `HowTo` and `speakable` JSON-LD generated from your Markdown.
- [GEO](../content/features/geo.md) — citation by assistants: TL;DR block, visible last-modified date, author attribution.

## Next steps

Create a workspace at [docsbook.io/start](https://docsbook.io/start) and connect a repository — every surface on this page reads from it.

## Related

- [Quick start](../quick-start.md)
- [Sources](./sources.md)
- [MCP tools reference](../reference/mcp-tools.md)
- [Webhooks](../webhooks.md)
- [Translation settings](../translation/settings.md)
