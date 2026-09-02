---
title: "AI Features"
description: "Overview of Docsbook's AI capabilities — chat, translations, llms.txt, doc graph, MCP server, hooks, and the skills catalog."
---

# AI Features

Docsbook ships a full AI layer on top of your documentation: a chatbot trained on your content, automatic translations into 15 languages, machine-readable surfaces for AI agents, and an MCP server that lets Claude Code or Cursor manage your workspace.

## What's included

Every AI surface in Docsbook is documented on its own page. Use this index to jump to the area you care about.

| Feature | Plan | Page |
|---|---|---|
| AI Chat trained on your docs | Free | [AI Chat](./chat.md) |
| Translations into 15 languages | PRO | [Translations](./translations.md) |
| `llms.txt` for AI agent discovery | Free | [llms.txt](./llms-txt.md) |
| Source of Truth doc graph | Free (local) | [Source of Truth](./source-of-truth.md) |
| Connected sources your agent reads | Free | [Sources](./sources.md) |
| MCP server with 244 tools | Free | [MCP Server](./mcp.md) |
| Pre/post LLM chat hooks | PRO | [Chat Hooks](./chat-hooks.md) |
| Docs Skills catalog | Free | [Skills](./skills.md) |

## How the pieces fit together

The chat, translations, and hooks sit on top of your indexed content. The hosted MCP server and `llms.txt` expose that same content to external AI agents — so a Claude Code session can read your docs, write a translation, or update branding without leaving the editor. The Source of Truth doc graph runs locally instead: use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) (`npx markdown-lsp <subcommand> ./docs`) to index your repo on your own machine — no hosted endpoint, no PRO+ plan required.

If you are setting up AI for the first time, start with [AI Chat](./chat.md), then enable [Translations](./translations.md) when you have a multi-language audience. Teams running AI agents against their docs should read [llms.txt](./llms-txt.md) and [Source of Truth](./source-of-truth.md) next.

Whichever you start with, connect your [Sources](./sources.md) early. That is what stops the assistant answering about your product from memory: with a repository or a site registered, "update the documentation" begins by reading it.

## Related

- [Quick start](../quick-start.md)
- [Webhooks](../webhooks.md)
- [Translation settings](../translation/settings.md)
