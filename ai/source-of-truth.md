---
title: "Source of Truth — Local Doc Graph for AI Agents"
description: "A structured graph of every page, section, and link in your docs, indexed locally by Claude Code via the docs-sync plugin. No server-side index, no PRO+ gating."
---

# Source of Truth

Source of Truth is a structured graph of your entire documentation — pages, headings, sections, and cross-links — built locally by AI agents like Claude Code via the [`docs-claude-plugins`](https://github.com/Docsbook-io/docs-claude-plugins) package. The agent runs the parser on your repository, holds the graph in memory, and queries it through LSP-style tools while it works on your docs.

> **Note.** Server-side Source of Truth indexing and the MCP graph tools (`get_doc_graph`, `read_doc_sections`, `reindex_doc_graph`, and the 17 `doc_*` tools) were removed in **v0.22.0**. The graph now lives entirely on the agent's machine — there is no hosted index, no reindex quota, and no PRO+ gating for it.

## Install

The graph search is shipped as a Claude Code plugin. Install it once in any repo whose docs you want to query:

```bash
/plugin install docs-sync@docs-claude-plugins
```

This registers the bundled `markdown-lsp` MCP server with your Claude Code session and makes the LSP-style tools available to the agent.

## What the graph contains

For each page the graph stores:

- Canonical reference (`path#section`)
- Title and frontmatter
- Heading tree with stable anchors
- Section bodies (markdown)
- Outbound and inbound links

The graph is rebuilt incrementally from disk on every relevant edit, so it always matches the working tree the agent sees.

## How the graph is built

The graph is parsed by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source Language Server Protocol implementation for Markdown, published on npm as `markdown-lsp` and bundled in the `docs-sync` plugin. It uses unified + remark AST instead of regex, so:

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

## Why local instead of server-side

- **No quotas.** Reindex as often as the agent needs — it's all on disk.
- **No PRO+ gating.** The graph is free and works on any Docsbook plan, including non-Docsbook docs.
- **Always fresh.** The graph reflects uncommitted edits the moment the agent saves them.
- **Private.** Your unpublished drafts never leave the machine.

## Related

- [MCP Server](./mcp.md) — The hosted MCP server for workspace, branding, analytics, and webhooks.
- [docs-skills](./skills.md) — AI skills catalogue that builds on top of the graph.
- [Webhooks](../webhooks.md) — Subscribe to `content.indexed` and `content.outdated` events on the hosted side.
