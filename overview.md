---
title: "How Docsbook publishes documentation machines can cite"
description: "Docsbook publishes the documentation you already have to a site people and AI assistants can read, and reports what those readers did next."
---

# How Docsbook publishes documentation machines can cite

Docsbook is a documentation platform that publishes Markdown — from a GitHub repository, a website scan, or a written brief — as a live site at `docsbook.io/{owner}/{repo}`. After this page you can decide whether Docsbook fits your product, and which of its three jobs you need first: reaching people who search, giving AI assistants facts they can quote about you, and measuring what the pages earned.

Most companies with a product, customers and an ad budget still cannot be recommended by Google or by an AI assistant, because there is nothing to read: what exists is out of date, hidden behind a login, or disagrees with the product. Docsbook publishes what is already written to where machines read it, and shows how many readers it brought.

## What happens between your repository and a published page

| Stage | What Docsbook does | What you get |
|---|---|---|
| 1. Connect a source | Reads a GitHub repository, scans a website, or drafts from a sentence about your product | A draft site you can open before you sign in |
| 2. Index | Parses Markdown and frontmatter, extracts headings, links and metadata, builds a navigable graph | Full-text search, a per-page outline, links between files resolved |
| 3. Publish | Serves the site at `docsbook.io/{owner}/{repo}`, rendered on the server | A public URL with sitemap, OpenGraph and JSON-LD |
| 4. Expose to machines | Serves `llms.txt` and an MCP server with 309 tools | Assistants and agents can read your docs, and agents can edit them |
| 5. Sync | Re-checks GitHub when the site is visited and re-indexes what changed | Pages match the repository with no build step and no CI pipeline |
| 6. Measure | Records page views, searches, events, feedback and AI usage | Reports on which pages are read and where readers stop |

## Reach: a page for each question your customers ask

A documentation page that answers one narrow question costs less to write than a landing page and keeps earning search traffic for years, because the question does not go out of fashion. Docsbook gives each page its own URL, its own title and description, its own entry in `sitemap.xml`, and its own JSON-LD — so a page about one question competes on that question rather than being buried inside a marketing site.

Docsbook generates the machine-readable surfaces for this automatically: meta tags, `sitemap.xml`, OpenGraph, canonical URLs, and JSON-LD for FAQ and HowTo content. See [SEO](./content/features/seo.md) for the search-engine surface and [GEO](./content/features/geo.md) for the generative-engine one.

## Machine-readable facts: what an assistant quotes about you

An AI assistant recommending a product quotes what it can read and verify cheaply: prices, limits, what the product does not do, and who the company is. Where your documentation says nothing, the assistant fills the gap with a competitor's page. Docsbook's job here is to make those facts readable — as HTML rendered on the server, as `llms.txt`, and as an MCP server.

Three surfaces do this work:

- **`llms.txt`** — a plain-text index of your documentation at the site root, for AI agents that look for one. See [llms.txt](./ai/llms-txt.md).
- **MCP server** — 309 tools over the Model Context Protocol, so Claude Code, Cursor or ChatGPT can read your pages, search them, and commit changes back. See [MCP server](./ai/mcp.md).
- **AEO markup** — FAQPage, HowTo and speakable JSON-LD generated from your Markdown, for answer boxes and voice assistants. See [AEO](./content/features/aeo.md).

## Analytics: which pages are read and where readers stop

Docsbook records every page view, search query, feedback vote and tracked event on your documentation, and reports them per page. That answers the questions a marketer asks about a docs site: which pages nobody reaches, which searches return nothing, how far a reader gets before leaving, and which countries and languages they arrive from.

Events, goals and funnels let you mark a path through the docs and count how many readers finish it. See [Tracking overview](./analytics/tracking/overview.md) for what is measured and [Events](./analytics/tracking/events.md) for the event catalogue.

## Who Docsbook is for

| Reader | What they are buying |
|---|---|
| Founder | Their product appears in ChatGPT, Perplexity and Google answers to their customers' questions |
| Marketer | Documentation as a channel: conversion visible before the button, goals and funnels, dead-end pages named |
| Engineer or product manager | Repository to site in seconds, source of truth in GitHub, MCP from Claude Code, export in one click |

## What Docsbook does not do

Docsbook does not offer SAML SSO, team accounts with role-based access control, a SOC 2 Type II report, or a Data Processing Agreement — all four are on the compliance roadmap, not shipped. There is no WYSIWYG editor aimed at a non-technical author: pages are Markdown files, edited in the web editor, in GitHub, or by an agent over MCP. See [MCP security](./ai/mcp-security.md) for the current compliance position.

## What Docsbook runs on

Docsbook is a Next.js 16 and React 19 application on Vercel, with Postgres (Neon) and Redis behind it, Drizzle as the ORM, and Paddle as the merchant of record. Markdown is parsed with unified, remark and rehype, highlighted with Shiki, and navigated with [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp), Docsbook's open-source documentation parser. AI calls are routed through OpenRouter, or through your own provider key.

## What it costs

Docsbook meters four things against each project's own balance, and nothing else:

- **Readers (AI Chat)** — an AI answer given to a reader of your documentation.
- **Admin & AI Agent** — an agent run you or a connected agent started.
- **AI Translations** — translating a page into another language.
- **Semantic Index** — building the embeddings the AI chat retrieves from.

Hosting, a custom domain and its TLS certificate, readers, editors, GitHub sync, full-text search, branding and analytics are unmetered. Every new project starts with **$1.00** of balance and can claim **$5.00** more once it is 3 minutes old; top-ups after that run from $20.00 to $5,000.00. See [Pricing](./pricing.md) for the mechanism and [docsbook.io/pricing](https://docsbook.io/pricing) for current figures.

## Next steps

- [Quick start](./quick-start.md) — publish a documentation site, from source to public URL
- [Concepts](./basics.md) — workspace, project balance, indexing and the other terms used here
- [Use cases](./use-cases.md) — the jobs teams hire documentation for
- [FAQ](./faq.md) — sync, privacy, data ownership and billing questions

<!-- widget:cta -->

## Publish a site and look at it

The draft is generated before you sign in, so you can judge the result before committing to anything.

[Start free — no credit card](https://docsbook.io/start)

<!-- /widget -->
