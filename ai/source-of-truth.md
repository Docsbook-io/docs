---
title: "Source of Truth: a local doc graph for your AI agent"
description: "Give an agent a structured graph of every page, section and link in your docs, built on its own machine by markdown-lsp — no hosted index, no quota, no upload."
---

# Source of Truth

Source of Truth is a structured graph of your entire documentation — pages, headings, sections, and cross-links — built locally by AI agents like Claude Code via [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp). The agent runs the parser on your repository, holds the graph in memory, and queries it through LSP-style tools while it works on your docs.

> **Note.** Server-side Source of Truth indexing and the MCP graph tools (`get_doc_graph`, `read_doc_sections`, `reindex_doc_graph`, and the 17 `doc_*` tools) were removed in **v0.22.0**. The graph now lives entirely on the agent's machine: there is no hosted index, no reindex quota, and nothing about it draws on your project balance.

## How do I give an agent the Source of Truth graph?

Run `markdown-lsp` in the repository you want the agent to query, and the graph is available to it for as long as it works there. Nothing is uploaded and nothing needs to be enabled in Docsbook.

The graph search is powered by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source LSP implementation for Markdown, published on npm as `markdown-lsp`. Run it in any repo whose docs you want to query:

```bash
npx markdown-lsp <subcommand> ./docs
```

This makes the LSP-style tools available to the agent against your local working tree. See the [markdown-lsp README](https://github.com/Docsbook-io/markdown-lsp) for the full subcommand list and setup options.

## What the graph contains

For each page the graph stores:

- Canonical reference (`path#section`)
- Title and frontmatter
- Heading tree with stable anchors
- Section bodies (markdown)
- Outbound and inbound links

The graph is rebuilt incrementally from disk on every relevant edit, so it always matches the working tree the agent sees.

## How the graph is built

The graph is parsed by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source Language Server Protocol implementation for Markdown, published on npm as `markdown-lsp`. It uses unified + remark AST instead of regex, so:

- Relative paths like `../guide.md#section` resolve correctly
- Wiki-style links `[[note]]` are supported
- Broken links are detected up-front and surfaced as `unresolved` items
- Inline, reference, and autolink styles are handled uniformly

## LSP-style tools available to the agent

These are MCP tools the plugin exposes to Claude Code (or any MCP-compatible client). They run against the in-memory graph, so they are free and instant — no API calls back to Docsbook.

**Structure**

| Tool | What it returns |
|---|---|
| `doc_outline` | Heading tree of one page, no bodies |
| `doc_workspace_outline` | All pages with titles and heading counts |
| `doc_get_section` | Body of a specific section by anchor |

**Search**

| Tool | What it returns |
|---|---|
| `doc_search_symbols` | Fuzzy subsequence over headings; query `oaf` matches `OAuth flow` |
| `doc_search_text` | Full-text search with surrounding-context snippets + line/col |
| `doc_search_paths` | Glob filter on page paths (`docs/*.md`, `**/auth.md`) |

**Link graph**

| Tool | What it returns |
|---|---|
| `doc_search_links_to` | All incoming links to a page (LSP `references`) |
| `doc_search_links_from` | All outgoing links from a page |
| `doc_resolve_link` | Convert a relative or wiki link into a resolved target page + anchor |

## Why is the graph local instead of hosted?

Docsbook builds the Source of Truth graph on the agent's machine because the three things an agent needs from it — freshness, privacy and unlimited re-reads — are exactly the three a hosted index cannot give.

- **No quotas, and no cost.** Reindex as often as the agent needs; it is all on disk, and no call is metered.
- **Always fresh.** The graph reflects uncommitted edits the moment the agent saves them, which a hosted index built from pushed commits cannot do.
- **Private.** Unpublished drafts never leave the machine.
- **Not tied to Docsbook.** `markdown-lsp` runs against any Markdown repository, including documentation that is not published here.

The trade-off is real and worth naming: an agent with no checkout of your repository gets nothing from this graph. That agent should use the hosted [`search_docs` and `get_doc_outline`](./mcp.md#how-do-i-search-and-edit-docs-content-from-an-agent) tools instead.

## Related

- [MCP Server](./mcp.md) — the hosted server for workspace, content, analytics and webhooks.
- [Docs Skills](./skills.md) — the skills catalog that builds on top of the graph.
- [llms.txt](./llms-txt.md) — the machine-readable index of the *published* site, for agents with no checkout.
- [Webhooks](../webhooks.md) — subscribe to `content.indexed` and `content.outdated` on the hosted side.
