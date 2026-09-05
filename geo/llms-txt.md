---
title: "llms.txt: what Docsbook generates, and what the file is worth"
description: "Docsbook generates llms.txt and llms-full.txt for every workspace — what goes in them, how they refresh, how they differ from sitemap.xml, and who measurably reads them."
tldr: "Docsbook generates llms.txt and llms-full.txt for every workspace automatically, cached one hour, listing every published page at its canonical URL. The evidence that AI crawlers read the file is weak: Ahrefs found 97% of llms.txt files got zero requests in May 2026, and Google says no new machine-readable file is needed."
---

# llms.txt

`llms.txt` is a plain-text index of a site written for models rather than browsers: a title, a one-line summary, and a linked list of the pages worth reading. Docsbook generates `llms.txt` and `llms-full.txt` for every workspace automatically — no configuration, no build step, nothing to keep in sync by hand.

This page says exactly what Docsbook puts in those files, and then — because the page is about honest machine-readable claims — how strong the evidence for `llms.txt` actually is. The short version of the second half: publish it, cost is zero, attribute no outcome to it.

## Where does Docsbook serve these files?

| File | URL | What it contains |
|---|---|---|
| Platform index | `https://docsbook.io/llms.txt` | Docsbook itself: what the product is, its plans, its MCP server and its skills catalog |
| Platform full text | `https://docsbook.io/llms-full.txt` | The body of Docsbook's own documentation pages |
| Workspace index | `https://<your-workspace>/llms.txt` | Every published Markdown page of that workspace, as links |
| Workspace full text | `https://<your-workspace>/llms-full.txt` | The full Markdown of every one of those pages |

All four are served as `text/plain; charset=utf-8` and need no authentication. A workspace published on a path of the apex domain — a showcase demo included, since a demo is a workspace — gets the same pair on that path, scoped to the one project named in the URL, so a crawler fetching one product's index is never handed another product's pages.

Every page is listed at its **canonical** URL. A workspace whose pages are canonical on the apex domain is never advertised on its mirror subdomain, because that host redirects and answers `Disallow: /` in `robots.txt`. Handing a crawler a list of URLs it is told not to fetch is worse than handing it no list.

## What exactly goes into the workspace llms.txt?

Markdown, in this order: an H1 with the workspace or product name, a blockquote summarising what the documentation is and where it lives, one H2 per connected repository, and under each H2 a bullet list of `[page title](canonical URL)` for every published Markdown page. Then an **About this workspace** section — the part written for agents rather than crawlers:

```markdown
## About this workspace

- Hosted by: [Docsbook](https://docsbook.io) — AI-native documentation platform
- MCP server (manage this workspace via AI agent): https://docsbook.io/api/mcp/server
- Skills catalog (AI agent instructions for docs tasks): https://docsbook.io/skills
- Last generated: 2026-09-05T09:14:22.104Z

> To connect an AI agent to this workspace: `claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server`
```

Three behaviours are worth knowing:

- **The H1 names the product, not the account.** A file scoped to one repository is titled with that workspace's display name; only an account-wide file is titled with the account login. The H1 is the first thing an assistant quotes when asked what a product is, and the account login is usually the wrong answer.
- **An empty workspace still returns a valid file** — the H1, a line saying no public docs are indexed yet, and a link home. An empty index is a fact; a 404 is a mystery.
- **A page that fails to fetch is skipped, not fatal.** `llms-full.txt` is assembled page by page; a single unreachable file logs an error and leaves that page out, rather than failing the whole request.

In `llms-full.txt` each page arrives under its own H2 with a `Source:` line carrying its canonical URL, and its YAML frontmatter stripped. The source line is what lets an assistant cite the page a sentence came from instead of citing the bundle.

## llms.txt or llms-full.txt — which does an agent want?

```
llms.txt       — compact index: page titles and links, one line each
llms-full.txt  — the full Markdown body of every page, concatenated
```

Use the index when the agent needs a map and will fetch pages on demand; use the full file when it wants the whole knowledge base in one request and has the context window for it. There is a third surface for the middle case: any single page is available as raw Markdown at `/api/md/<owner>/<repo>/<page path>`, and the same route without a page path returns every Markdown file of the repository concatenated. That is the route behind the **View as Markdown** item in the page menu.

## How is llms.txt different from sitemap.xml?

They answer different questions and neither replaces the other.

| | `sitemap.xml` | `llms.txt` |
|---|---|---|
| Written for | Search-engine crawlers | Models and agents reading a site cold |
| Format | XML, URLs plus metadata | Markdown: H1, summary, titled link lists |
| Carries meaning | No — a URL and a timestamp | Yes — a project summary and a title per link |
| Standardised by | [sitemaps.org](https://www.sitemaps.org/protocol.html), supported by search engines | [llmstxt.org](https://llmstxt.org/), a proposal |
| Consumed in production by | Search engines, demonstrably | See below |

Docsbook generates both, and `audit_geo` checks for both.

## How often does it refresh?

Docsbook regenerates the file from your published pages on request and caches the result for **one hour** (`Cache-Control: public, s-maxage=3600, stale-while-revalidate=86400`). A page you push to GitHub appears within an hour of the next fetch. There is no build step, no file to commit and no quota — an agent may fetch it as often as it likes.

## What can I change about what an agent sees?

Three things, and only three:

1. **Name your files well.** Link text in `llms.txt` comes from the **file path**, not from the page's frontmatter `title`. `api-rate-limits.md` becomes "Api Rate Limits"; a repository-root `README.md` becomes "Overview"; `page2.md` becomes "Page2", and no model will pick it.
2. **Publish the page.** Only committed Markdown on the default branch is listed. Drafts and unpushed edits are in neither file.
3. **Write the first paragraph as an answer.** `llms-full.txt` carries the body verbatim, so whatever opens the page is what an assistant reads first.

## How strong is the evidence for llms.txt?

Weak, and Docsbook will not pretend otherwise. Here is the whole case, both directions.

| Question | What is actually established | Source |
|---|---|---|
| Is there a spec? | Yes — a proposal by Jeremy Howard, published 3 September 2024 and revised since; the page now reads "The /llms.txt file, v2", modified 10 August 2026. Only the H1 is required: "An H1 with the name of the project or site. This is the only required section" | [llmstxt.org](https://llmstxt.org/) |
| Is `llms-full.txt` in that spec? | **No.** Checked against the page as it stands: the string does not occur in it once. It is a community convention, which Docsbook follows because agents ask for it | [llmstxt.org](https://llmstxt.org/) |
| Does Google use it? | No. John Mueller, 17 June 2025: "FWIW no AI system currently uses llms.txt". Google's own AI-features documentation says "You don't need to create new machine readable files, AI text files, or markup to appear in these features" | [Search Engine Roundtable](https://www.seroundtable.com/google-ai-llms-txt-39607.html), [Google AI features](https://developers.google.com/search/docs/appearance/ai-features) |
| Do OpenAI, Anthropic and Perplexity read it? | Unproven either way. They *publish* their own — [developers.openai.com/llms.txt](https://developers.openai.com/llms.txt) and [docs.perplexity.ai/llms.txt](https://docs.perplexity.ai/llms.txt) both answer `200 text/plain` — but publishing a file is not consuming one, and none of the three vendors' crawler documentation describes fetching yours | [OpenAI bots](https://developers.openai.com/api/docs/bots), [Perplexity bots](https://docs.perplexity.ai/guides/bots) |
| Is it requested in practice? | Measured by Ahrefs across 137,000 domains: 28% published a valid `llms.txt`, and of those, "97% received zero requests for it" in May 2026 | [Ahrefs, updated 15 June 2026](https://ahrefs.com/blog/what-is-llms-txt/) |
| Does having it raise citations? | No published, replicated study shows it does | — |

**What the file still buys you.** An agent you hand the URL to — in a prompt, in an MCP client, in a support workflow — gets a complete, current map of your documentation in one fetch instead of crawling. Your MCP server and skills catalog are discoverable from it. It is diffable, so it is a cheap inventory of what is actually published. And it costs you nothing, because Docsbook generates it.

**What it does not buy you.** Any claim about assistant traffic. If you want to know whether assistants read your docs, measure the thing that leaves a trace: crawler hits from assistant user agents, and referral traffic from assistant domains. Both are visible in your [analytics](../analytics/README.md); a file at a URL is not evidence of anything on its own.

## Limits and open questions

- **The link text ignores your frontmatter `title`.** A page titled "Rate limits and quotas" in frontmatter is listed as "Api Rate Limits" if that is the filename. Rename the file, or accept the derived title.
- **`llms-full.txt` has no size ceiling.** A large workspace produces a file that may exceed an agent's context window; there is no pagination and no truncation. Prefer `llms.txt` plus per-page fetches above a few dozen pages.
- **Docsbook does not serve the spec's `.md` page variants.** The proposal asks for "a clean markdown version of those pages at the same URL as the original page … with `.md` appended". Docsbook serves raw Markdown at `/api/md/…` instead, which is the same content at a different address, and is not what a spec-following client would probe for.
- **The one-hour cache is not configurable**, and neither is the file's content. That is deliberate — there is no second, machine-readable copy of your docs to drift out of sync — but it means you cannot curate what an agent sees.
- **Under question: is any of this read by the assistants that matter?** The vendor bot documentation describes crawlers that fetch *pages*; none of it describes fetching `llms.txt`. Until a vendor documents consumption, or someone publishes server-log evidence that contradicts the Ahrefs measurement above, treat the file as free hygiene rather than a channel.

## Related

- [GEO](./README.md) — the page-level signals: TL;DR block, visible dates, author attribution.
- [Citation signals](./citation-signals.md) — the writing rules that decide whether a retrieved passage gets quoted.
- [SEO](../seo/README.md) — sitemap, canonical URLs, `noindex`.
- [MCP server](../agent-ready/mcp.md) — the machine surface for agents that write as well as read.
- [Source of truth](../agent-ready/source-of-truth.md) — the local doc graph, for an agent with your repository on disk.
