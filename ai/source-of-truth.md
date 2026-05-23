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

## MCP tools

Three MCP tools operate on the graph:

| Tool | Purpose |
|---|---|
| `get_doc_graph` | Return the full graph in the requested format |
| `read_doc_sections` | Read specific sections by canonical reference |
| `reindex_doc_graph` | Force a rebuild from the latest GitHub state |

## Freshness

If the graph has not been rebuilt for more than **7 days**, responses include a `stale` warning. Reindexing is rate-limited to **100 rebuilds per month** per workspace — enough for hourly cron jobs without abuse.

## Pricing

Source of Truth is a **PRO+** feature ($59/month). The underlying GitHub indexing runs on every plan, but graph access through the MCP API is gated to PRO+.

## Related

- [MCP Server](./mcp.md) — How agents authenticate and call the graph tools.
- [Webhooks](../webhooks.md) — Subscribe to `content.indexed` and `content.outdated` events.
