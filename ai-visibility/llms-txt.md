---
title: "llms.txt: the machine-readable index of your docs site"
description: "Docsbook generates llms.txt and llms-full.txt for every workspace: what goes in them, where they are served, how often they refresh, and what they are worth."
---

# llms.txt

`llms.txt` is a plain-text index of a site, written for models rather than for browsers: a title, a one-line summary, and a linked list of the pages worth reading. Docsbook generates `llms.txt` and `llms-full.txt` for every workspace automatically, with no configuration and nothing to maintain by hand.

This page says exactly what Docsbook puts in those files, where they are served, and — because this page is about honest machine-readable claims — how strong the evidence for `llms.txt` actually is.

## Where does Docsbook serve llms.txt?

Docsbook serves an index and a full-text file at the platform level, and the same pair for every workspace published on a path of the apex domain — a showcase demo included, since a demo is a workspace. All of them are `text/plain; charset=utf-8` and need no authentication.

| File | URL | What it contains |
|---|---|---|
| Platform index | `https://docsbook.io/llms.txt` | Docsbook itself and its main navigation |
| Platform full text | `https://docsbook.io/llms-full.txt` | The body of those pages, concatenated |
| Workspace index | `https://docsbook.io/<workspace>/llms.txt` | Every public page of that workspace, as links |
| Workspace full text | `https://docsbook.io/<workspace>/llms-full.txt` | The full Markdown of every one of those pages |
| Showcase demo | `https://docsbook.io/<demo>/llms.txt` | The same list scoped to that one demo, with `llms-full.txt` beside it |

Each workspace form is scoped to the one project named in the URL, so a crawler fetching one product's index is never handed another product's pages.

Every one of these files lists each page at its **canonical** URL. A workspace whose pages are canonical on the apex domain is never advertised on its mirror subdomain, because that host redirects and answers `Disallow: /` in `robots.txt` — a list of URLs a crawler is told not to fetch is worse than no list.

## What exactly does Docsbook put in llms.txt?

The workspace `llms.txt` is Markdown, in this order: an H1 with the workspace or product name, a blockquote summarising what the documentation is and where it lives, one H2 per connected repository, and under each H2 a bullet list of `[page title](canonical URL)` for every published Markdown page.

After the page lists comes an **About this workspace** section, which is the part written for agents rather than for crawlers:

```markdown
## About this workspace

- Hosted by: [Docsbook](https://docsbook.io) — AI-native documentation platform
- MCP server (manage this workspace via AI agent): https://docsbook.io/api/mcp/server
- Skills catalog (AI agent instructions for docs tasks): https://docsbook.io/skills
- Last generated: 2026-09-03T09:14:22.104Z

> To connect an AI agent to this workspace: `claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server`
```

A workspace with nothing indexed yet still returns a valid file: the H1, a line saying no public docs are indexed, and a link home. An empty index is a fact; a 404 is a mystery.

## llms.txt or llms-full.txt — which does an agent want?

Use `llms.txt` when the agent needs a map and will fetch pages on demand. Use `llms-full.txt` when the agent wants the whole knowledge base in one request and has the context window for it.

```markdown
llms.txt       — compact index: page titles and links, one line each
llms-full.txt  — the full Markdown body of every page, concatenated
```

In `llms-full.txt` each page arrives under its own H2, with a `Source:` line carrying the canonical URL, and its YAML frontmatter stripped. The source line matters: it is what lets an assistant cite the page it lifted a sentence from instead of citing the bundle.

## How often does llms.txt refresh?

Docsbook regenerates `llms.txt` from your published pages on request and caches the result for **one hour** (`Cache-Control: public, s-maxage=3600, stale-while-revalidate=86400`). A page you push to GitHub appears in the file within an hour of the next fetch. There is no build step to run, no file to commit, and no quota — an agent may fetch it as often as it likes.

## What should I do as the owner of the docs?

Three things, and only three, change what an agent sees:

1. **Name your files well.** The link text in `llms.txt` comes from the **file path**, not from the page's frontmatter `title`. `api-rate-limits.md` becomes "Api Rate Limits"; a repository-root `README.md` becomes "Overview". A file called `page2.md` is listed as "Page2" and no model will pick it.
2. **Publish the page.** Only committed, published Markdown is listed. Drafts and unpushed edits are absent from both files.
3. **Write the first paragraph as an answer.** `llms-full.txt` carries the body verbatim, so whatever opens the page is what an assistant reads first.

Nothing else is configurable, which is the point: there is no separate machine-readable copy of your docs to keep in sync with the human one.

## How much is llms.txt actually worth?

Honestly: it is a **weak signal**, and Docsbook does not claim otherwise. Adoption is concentrated in developer-tool documentation. Some assistant vendors say they read `llms.txt`; at least one search vendor has said it will not. There is no published, replicated evidence that having the file changes how often a site is cited.

It costs an hour to support and Docsbook generates it for you, so there is no reason not to have it — but attribute no outcome to it. If you want to know whether assistants read your docs at all, measure the thing that leaves a trace: crawler hits from assistant user agents in your analytics, and referral traffic arriving from assistant domains. Both are visible in your Docsbook analytics; a file at a URL is not evidence of anything on its own.

The work that does move retrieval is on the page: self-contained sections, the answer in the first paragraph, the subject named in full, and a concrete number where you honestly have one. See [GEO](./geo.md) for what Docsbook adds to the page for citation, and [AEO](./aeo.md) for answer and voice markup.

## Related

- [GEO — citation by AI assistants](./geo.md) — TL;DR block, visible dates, author attribution.
- [AEO — answer boxes and voice](./aeo.md) — FAQPage, HowTo and speakable JSON-LD.
- [SEO — classical search](./seo.md) — sitemap, canonical URLs, `noindex`.
- [MCP Server](./mcp.md) — the other machine surface, for agents that write as well as read.
- [Source of Truth](./source-of-truth.md) — the local doc graph, for an agent with your repository on disk.
