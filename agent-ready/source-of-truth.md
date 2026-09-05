---
title: "Source of Truth: a local doc graph for your AI agent"
description: "Give an agent a structured graph of every page, section and link in your docs, built on its own machine by markdown-lsp — no hosted index, no quota, no upload."
tldr: "Source of Truth is a document graph an agent builds locally with the open-source markdown-lsp package: pages, headings, sections and resolved links, queried through CLI subcommands or an LSP server. There is no hosted index, no reindex quota and nothing drawn from your Docsbook balance — the structural commands work entirely offline."
---

# Source of Truth

Source of Truth is a structured graph of your entire documentation — pages, headings, sections, and cross-links — built locally by AI agents like Claude Code via [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp). The agent runs the parser on your repository, holds the graph in memory, and queries it — as commands, or as LSP requests — while it works on your docs.

> **Note.** Server-side Source of Truth indexing and the hosted MCP graph tools (`get_doc_graph`, `read_doc_sections`, `reindex_doc_graph` and the `doc_*` LSP-style tools) were removed in **v0.22.0**. The graph now lives entirely on the agent's machine: there is no hosted index, no reindex quota, and nothing about it draws on your project balance.

## How do I give an agent the Source of Truth graph?

Run `markdown-lsp` in the repository you want the agent to query, and the graph is available to it for as long as it works there. Nothing needs to be enabled in Docsbook, and you do not need a Docsbook account.

The graph is built by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source Markdown language server, published on npm as `markdown-lsp` and requiring Node 20 or newer. There are two ways an agent reaches it, and they are genuinely different interfaces rather than two names for one thing:

```bash
# 1. As commands the agent runs. Every subcommand prints JSON to stdout.
npx markdown-lsp workspace-outline ./docs
npx markdown-lsp links-to ./docs quick-start.md

# 2. As a language server, for an editor or a structural indexer.
npx markdown-lsp lsp --stdio
```

For Claude Code the package ships a skill that sets the first path up in conversation:

```bash
npx skills add Docsbook-io/markdown-lsp
```

There is no MCP server inside `markdown-lsp`. An agent uses it by running commands or by speaking LSP — which is why nothing here consumes an MCP token or a Docsbook balance. See the [markdown-lsp README](https://github.com/Docsbook-io/markdown-lsp) for the full flag list.

## What the graph contains

For each page the graph stores:

- Canonical reference (`path#section`)
- Title and frontmatter
- Heading tree with stable anchors
- Section bodies (markdown)
- Outbound and inbound links

Each command reads the working tree as it is when it runs, so what the agent gets always matches the files on disk — including edits it has not committed. There is no cache to invalidate on the structural path.

## How the graph is built

The graph is parsed by [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) — our open-source Language Server Protocol implementation for Markdown, published on npm as `markdown-lsp`. It parses to a `unified` + `remark` AST (with GitHub-flavoured Markdown) rather than matching regexes over the text, so:

- Relative paths like `../guide.md#section` resolve to a real page and a real anchor
- Inline, reference and autolink styles are all seen as links, not just the inline form
- A link that resolves to nothing is reported up front — the graph export carries an `unresolvedCount`, and each edge names the kind of link it came from

## What the agent can ask the graph

These are the `markdown-lsp` subcommands. They run against the in-memory graph built from disk, so they are instant, free, and make no call back to Docsbook. Every one takes the docs directory as its first argument and prints JSON; `--pretty` indents it.

**Structure**

| Subcommand | What it returns |
|---|---|
| `workspace-outline <dir>` | All pages with metadata — the cheapest orientation there is |
| `outline <dir> <page>` | Heading outline of a single page, no bodies |
| `get-section <dir> <page> <anchor>` | The body of one section, by anchor slug |

**Search**

| Subcommand | What it returns |
|---|---|
| `search-symbols <dir> <query>` | Fuzzy subsequence over headings; `oaf` matches `OAuth flow` |
| `search-text <dir> <query>` | Full-text search, `ranked` or `verbatim`, with `--regex`, `--case-sensitive` and `--context n` |
| `search-paths <dir> <glob>` | Pages matching a glob (`ai/*.md`, `**/auth.md`) |

**Link graph**

| Subcommand | What it returns |
|---|---|
| `links-to <dir> <page>` | Every page that links to this one — the LSP `references` question |
| `links-from <dir> <page>` | Every link leaving this page |
| `resolve-link <dir> <from-page> <link-text>` | The target page and anchor a link text actually resolves to |
| `graph <dir> --format json\|dot\|mermaid\|html` | The whole graph: nodes with section counts, edges with their kind, and `unresolvedCount` — the links that resolve to nothing |

Three more subcommands are the semantic layer, and they are the ones that are *not* purely local: `index` builds a persistent embedding index, `semantic-search` queries it, and `graph --semantic` adds similarity edges. Each needs an embedding provider key in the environment and sends page text to that provider. `index` is incremental — unchanged units are served from the local cache under `.markdown-lsp-cache/`, so re-running it after a one-page edit re-embeds one page.

## Why is the graph local instead of hosted?

Docsbook builds the Source of Truth graph on the agent's machine because the three things an agent needs from it — freshness, privacy and unlimited re-reads — are exactly the three a hosted index cannot give.

- **No quotas, and no cost.** Reindex as often as the agent needs; it is all on disk, and no call is metered.
- **Always fresh.** The graph reflects uncommitted edits the moment the agent saves them, which a hosted index built from pushed commits cannot do.
- **Private.** With the structural subcommands, unpublished drafts never leave the machine — no key is configured and no request is made.
- **Not tied to Docsbook.** `markdown-lsp` runs against any Markdown repository, including documentation that is not published here.

The trade-off is real and worth naming: an agent with no checkout of your repository gets nothing from this graph. That agent should use the hosted [`search_docs` and `get_doc_outline`](./mcp.md#how-do-i-search-and-edit-docs-content-from-an-agent) tools instead.

## Limits and open questions

- **"Nothing leaves the machine" holds for the structural half only.** `index`, `semantic-search` and `graph --semantic` send page text to an embedding provider, because that is what an embedding is. If your documentation is confidential, use the structural subcommands, which need no key at all, and decide about the semantic ones separately.
- **The LSP server is not the CLI.** The subcommands build their graph in memory and need no database; running the full language server for an editor requires Postgres for its incremental index. The commands in this page are the CLI path.
- **Freshness is a property of the run, not of a watcher.** Each command reads the working tree as it is when it runs, so the graph an agent gets is fresh at that moment; the semantic index is only as current as the last `index`. The package's own recommendation is a git hook, not a daemon.
- **The graph knows link structure, not correctness.** `unresolvedCount` tells you a link resolves to nothing. Nothing here tells you a page is wrong, out of date or contradicted by the product — that is what the [MCP server's](./mcp.md) analytics and change-history tools are for.
- **Version-dependent.** Subcommand names and flags belong to `markdown-lsp`, which versions on its own schedule. The package README is the authority; this page describes the interface as published today.
- **Under question: wiki-style `[[note]]` links.** An earlier version of this page said they are supported. The package documents neither wiki links nor a plugin that adds them, and its parser is `remark` with GitHub-flavoured Markdown, which does not resolve them by itself. Treat wiki links as unsupported until the package says otherwise; ordinary Markdown links in all three styles are covered above.

## Related

- [MCP Server](./mcp.md) — the hosted server for workspace, content, analytics and webhooks.
- [Docs Skills](./skills.md) — the skills catalog that builds on top of the graph.
- [llms.txt](../geo/llms-txt.md) — the machine-readable index of the *published* site, for agents with no checkout.
- [MCP server security](./mcp-security.md) — what the hosted half stores, and what a token can reach.
- [Webhooks](../reference/webhooks.md) — subscribe to `content.indexed` and `content.outdated` on the hosted side.
