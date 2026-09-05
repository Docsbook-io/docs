---
title: "Docsbook concepts: workspace, project balance, indexing"
description: "Definitions of the terms Docsbook uses — workspace, project balance, indexing, source of truth, draft, sync, and the surfaces machines read your docs through."
---

# Docsbook concepts: workspace, project balance, indexing

Every term Docsbook's interface and documentation use, defined once. Each entry gives a one-sentence definition, then says where you meet the term and what it affects. Terms are grouped, and the groups are alphabetical inside themselves.

## The site and its content

### Workspace

A **workspace** is one documentation site and its settings, backed by a repository of Markdown files. The repository is either your own on GitHub, or one Docsbook hosts for you when you started from a website scan or a written brief.

A workspace owns its address, its appearance, its language settings, its analytics and its balance. Docsbook's admin panel and billing screens call the same object a **project**; the two words mean one thing.

### Draft

A **draft** is a generated documentation site that has not been published yet. Docsbook creates one from your source before you have an account.

A draft from a website scan or a written brief lives in your browser until you publish it. A draft opens on the same admin panel a published workspace gets, so branding, layout and SEO can be set before signing in.

### Page

A **page** is one Markdown file in the workspace repository, served at its own URL. File and folder names decide the URL and the position in the navigation tree.

Both `.md` and `.markdown` extensions are read. Files in other formats — `.txt`, `.rst` — are not turned into pages.

### Navigation tree

The **navigation tree** is the sidebar Docsbook builds from the folder structure of your repository. A folder becomes a group; a file becomes an entry under it.

`README.md` at the root of a folder becomes that folder's landing page. You do not write a navigation file: moving a file in the repository moves it in the sidebar.

### Outline

The **outline** is the per-page table of contents Docsbook builds from that page's headings, shown to the right of the content. Clicking a heading scrolls the page to it.

The outline is generated from H2 and lower headings, so skipping a heading level leaves a gap in it.

### Content widget

A **content widget** is a region of a Markdown page that Docsbook renders as a rich block — a card grid, an accordion, numbered steps, or a call-to-action — marked with two HTML comments.

The comments are invisible in every other Markdown reader, so the same file still reads correctly on GitHub. An unknown widget name degrades to ordinary Markdown; nothing is ever hidden. See [Content widgets](./content/features/widgets.md).

## How content gets in and stays current

### Indexing

**Indexing** is the pass Docsbook runs over your Markdown to build everything the site needs: the search index, the navigation tree, the per-page outline, the link graph, and the embeddings the AI chat retrieves from.

Indexing runs when a workspace is created and again when Docsbook sees changed content. A page that is not indexed cannot be found by search or quoted by the chat.

### GitHub sync

**GitHub sync** is how a Docsbook site stays level with its repository: Docsbook checks GitHub for new commits when the site is visited, and re-indexes what changed. There is no webhook to configure and no build step to wait for.

Synced: new `.md` files, text edits, deletions, renames, new folders. Not synced: commit history, branch information, code comments, and files in other formats.

### Source of truth

A **source of truth** is a repository or website you have connected to a workspace so that an agent writing your documentation reads facts from it instead of recalling them. Each connected source carries the owner's own note about why it is connected.

Sources are read-only inputs. They are separate from the repository the site is built from. See [Connected sources](./ai/sources.md).

### Web editor

The **web editor** is Docsbook's in-browser editor for the workspace's Markdown files. Saving commits to the repository the site is built from.

Edits made in the web editor, in GitHub, and by an agent over MCP all land in the same repository, so there is one history rather than two.

## Money and metering

### Project balance

A **project balance** is the money attached to one workspace, spent on the AI work done for that workspace. Every new project is created with **$1.00** of balance, plus **$5.00** the owner can claim once the project is **3 minutes old**, and is topped up after that from the billing screen.

Balances are per project, not per account: one project running out does not stop another. See [Pricing](./pricing.md).

### Top-up

A **top-up** is a payment onto one project's balance, at an amount you name. The smallest single top-up is **$20.00** and the largest is **$5,000.00**.

Top-ups do not expire, and no balance is refilled on a schedule. A recurring monthly payment can be set up on the billing screen; it tops up the same balance each month.

### Metered work

**Metered work** is the work that draws on a project balance. There are exactly four kinds, and each is a row in **Spend by source** on the project's Limits card:

- **Readers (AI Chat)** — an AI answer given to a reader of the published documentation.
- **Admin & AI Agent** — an agent run, including metered MCP tool calls.
- **AI Translations** — translating a page into another language.
- **Semantic Index** — building the embeddings the AI chat retrieves from.

Nothing else is metered: hosting, a custom domain and its TLS certificate, readers, editors, GitHub sync, full-text search, branding, analytics and MCP read calls all cost nothing per use. Any one of the four sources can be capped for the cycle from the Limits card, and a cap of $0 switches that source off.

### Markup

**Markup** is the percentage Docsbook adds to the AI provider's real price for the model that answered — currently **900%**. The model, its per-1M-token rate and the markup are all shown in the dashboard.

Bringing your own provider API key removes it: you pay the provider directly and Docsbook bills you nothing for that usage.

## Who can read the site

### Public site

A **public site** is the default: anyone with the link reads it, including people without a GitHub account and search-engine crawlers. The repository's own visibility does not change this — Docsbook reads the repository, then serves the pages it built.

Public is what makes the site indexable by Google and quotable by AI assistants.

### Private site

A **private site** shows an unlock screen instead of your content to everyone but the owner, gated by a shared password or by your own SSO identity provider. Structure, pages and the search index stay hidden until a reader unlocks it.

The owner always has full access regardless of visibility. See [Private docs: password and SSO](./guides/advanced/sso.md).

### Custom domain

A **custom domain** is your own hostname — `docs.yourcompany.com` — serving the workspace instead of `docsbook.io/{owner}/{repo}`. You add one CNAME record and Docsbook provisions the TLS certificate.

The `docsbook.io` address keeps working after a custom domain is attached. See [Custom domain setup](./guides/advanced/custom-domain.md).

## Surfaces machines read

### llms.txt

**`llms.txt`** is a plain-text index of a Docsbook site, served at the site root for AI agents that look for one. It lists the pages and what each one covers.

Docsbook generates it from the indexed content, so it does not go stale separately from the site. See [llms.txt](./ai/llms-txt.md).

### MCP server

The **MCP server** is Docsbook's Model Context Protocol endpoint at `https://docsbook.io/api/mcp/server`, exposing 309 tools that let an AI agent read your documentation, search it, change settings, and commit pages back. Authentication is Bearer over OAuth 2.0 with PKCE.

Discovery calls are never metered; other calls draw on the project balance. See [MCP server](./ai/mcp.md) and the [MCP tools reference](./reference/mcp-tools.md).

### Float widget

The **float widget** is the control menu in the bottom-right corner of your own published documentation, visible only to you while signed in. Readers never see it.

It switches chat, repository and mode, opens settings, and signs you out.

## Related

- [Overview](./overview.md) — how these pieces fit together, end to end
- [Quick start](./quick-start.md) — the tutorial that uses these terms in order
- [MCP tools reference](./reference/mcp-tools.md) — every tool, its parameters and its price class
- [Pricing](./pricing.md) — what is metered and what a project balance pays for
