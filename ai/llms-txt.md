---
title: "llms.txt — AI Agent Discovery"
description: "Auto-generated llms.txt and llms-full.txt files make your docs discoverable by Perplexity, ChatGPT Search, Cursor, Cline, and other AI agents."
---

# llms.txt

`llms.txt` is an emerging standard that tells AI agents and AI search engines how your site is organized and which pages matter. Docsbook generates it for every workspace, on every plan, with no configuration.

## The standard

AI clients that read `llms.txt` include Perplexity, ChatGPT Search, Cursor, Cline, and a growing list of agentic tools. The file is a markdown index of titles, descriptions, and links — short enough for a model to load into context on a single request.

## Two levels

Docsbook serves `llms.txt` at two scopes.

| Scope | URL | Contents |
|---|---|---|
| Platform | `docsbook.io/llms.txt` | Description of Docsbook itself and its main navigation |
| Workspace | `docsbook.io/[user]/llms.txt` | Structured list of pages for that user's docs |
| Showcase demo on the apex path | `docsbook.io/[demo]/llms.txt` | The same list, scoped to that one demo and named after it (with `llms-full.txt` beside it) |

Each scope also has a `llms-full.txt` variant.

## llms.txt vs llms-full.txt

```markdown
# llms.txt        — compact index: titles, descriptions, links
# llms-full.txt   — full markdown body of every page, concatenated
```

Use `llms.txt` when the agent needs a map and will fetch pages on demand. Use `llms-full.txt` when the agent wants the entire knowledge base in one shot.

## Availability

Available on **all plans**, including Free. There is no quota — agents can fetch the files as often as they need.

## Customization

The files are generated server-side from your published documentation by a dedicated parser — independent of the local Source of Truth graph. There is no manual file to maintain. When you push new content to GitHub, the next index rebuild updates both `llms.txt` and `llms-full.txt`.

The relevant source files are:

```text
src/lib/generate-llms-txt.ts            # platform-level
src/lib/generate-workspace-llms-txt.ts  # workspace-level
```

## Related

- [Source of Truth](./source-of-truth.md) — Local doc graph for AI agents, indexed by the `docs-sync` Claude Code plugin.
- [MCP Server](./mcp.md) — Hosted MCP tools for querying your published docs.
