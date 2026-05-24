---
title: "Source of Truth — Doc Graph for AI Agents"
description: "A structured graph of every page, section, and link in your docs. Exposed to AI agents via MCP in TOON or JSON format."
---

# Source of Truth

Source of Truth is a structured graph of your entire documentation — pages, headings, sections, and cross-links — kept in sync with the GitHub repository. AI agents read it through the Docsbook MCP server and use it to answer questions or trigger workflows.

## What the graph contains

For each page the graph stores:

- Canonical reference (`owner/repo/path#section`)
- Title and frontmatter
- Heading tree with stable anchors
- Section bodies (markdown)
- Outbound and inbound links

This is the same structure that powers `llms-full.txt`, but exposed as a queryable API rather than a flat file.

## Formats

Request the graph in either format:

```json
{ "format": "toon" }
```

```json
{ "format": "json" }
```

`toon` is a compact, token-efficient representation designed to fit large graphs into an LLM context window. `json` is the canonical structured form for programmatic use.

## How the graph is built

The graph is parsed by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source Language Server Protocol implementation for Markdown, published on npm as `markdown-lsp`. It uses unified + remark AST instead of regex, so:

- Relative paths like `../guide.md#section` resolve correctly
- Wiki-style links `[[note]]` are supported
- Broken links are detected up-front and surfaced as `unresolved` items
- Inline, reference, and autolink styles are handled uniformly

The same parser powers the standalone LSP server (any editor) and Docsbook's Source of Truth, so the indexing behavior is consistent between local authoring and the hosted product.

## MCP tools

### Base graph (3 tools)

| Tool | Purpose |
|---|---|
| `get_doc_graph` | Return the full graph in the requested format (`toon` / `json`) |
| `read_doc_sections` | Read specific sections by canonical reference |
| `reindex_doc_graph` | Force a rebuild from the latest GitHub state |

### LSP-style read & search (17 tools)

These give an agent cheap, targeted access to the docs instead of dumping the whole graph. All operate on the same `richGraph` payload built by `markdown-lsp`.

**Structure**

| Tool | What it returns |
|---|---|
| `doc_outline` | Heading tree of one page, no bodies |
| `doc_breadcrumbs` | Ancestor headings for a section |
| `doc_neighbors` | parent / prev / next / children sections |
| `doc_list_pages` | Pages in workspace, optionally filtered by path prefix |

**Search**

| Tool | What it returns |
|---|---|
| `doc_search_symbols` | Fuzzy subsequence over headings (LSP `workspace/symbol`); query `oaf` matches `OAuth flow` |
| `doc_search_text` | Full-text search with surrounding-context snippets + line/col |
| `doc_grep` | Regex search |
| `doc_search_paths` | Glob filter on page paths (`docs/*.md`, `**/auth.md`) |
| `doc_search_by_anchor` | Find every section with a given heading slug |

**Link graph**

| Tool | What it returns |
|---|---|
| `doc_search_links_to` | All incoming links to a page (LSP `references`) |
| `doc_search_links_from` | All outgoing links from a page |
| `doc_search_unresolved` | Broken internal links in the workspace |
| `doc_search_orphans` | Pages with no incoming references |

**Resolve**

| Tool | What it returns |
|---|---|
| `doc_resolve_link` | Convert a relative or wiki link found in a page into an absolute `https://github.com/owner/repo/blob/branch/path#anchor` URL |
| `doc_definition` | Resolve a `page#anchor` ref to its declaring location + line/col |
| `doc_hover` | Title + first sentence of a ref — quick summary without reading the body |
| `doc_canonical_ref` | Normalize a free-form reference into a canonical page path |

> Workspaces indexed before the `markdown-lsp@0.2.0` integration must be reindexed once (`reindex_doc_graph`) before the LSP-style tools become available. Until then they return `GRAPH_NEEDS_REINDEX`.

## Freshness

If the graph has not been rebuilt for more than **7 days**, responses include a `stale` warning. Reindexing is rate-limited to **100 rebuilds per month** per workspace — enough for hourly cron jobs without abuse.

## Pricing

Source of Truth is a **PRO+** feature ($59/month). The underlying GitHub indexing runs on every plan, but graph access through the MCP API is gated to PRO+.

## Related

- [MCP Server](./mcp.md) — How agents authenticate and call the graph tools.
- [Webhooks](../webhooks.md) — Subscribe to `content.indexed` and `content.outdated` events.
