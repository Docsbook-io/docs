---
title: "GEO for docs: get cited by ChatGPT, Perplexity and Claude"
description: "How Docsbook makes docs citable by AI answer engines: llms.txt, Markdown copies, open AI crawlers, answer-first pages, and an agent that checks the answers."
---

# AI engines read and cite you

Every Docsbook site can be read by ChatGPT, Claude, Perplexity and Gemini from day one, and the [Docsbook agent](../agent/README.md) checks what answer engines say about your product and fixes the pages behind wrong answers.

## What's on from day one

Nothing to switch on: every page on a `docsbook.io` address gets all of this, on every plan.

- **[`llms.txt` and `llms-full.txt`](./llms-txt.md)** — every page with its Markdown address, plus the languages the site is published in
- **A Markdown copy of every page** — the page as plain text, a fraction of the weight of its HTML
- **Text in the HTML** — pages are server-rendered, so a crawler that runs no JavaScript still reads every word
- **AI crawlers welcome** — the crawlers of OpenAI, Anthropic, Perplexity, Google and Apple may read every page
- **An answer-first summary** — the first paragraph becomes a summary block under the title, up to 280 characters, marked `speakable` in JSON-LD; frontmatter `tldr:` replaces it
- **Dates and authors** — a visible **Updated** date from the last commit, plus `datePublished`, `dateModified` and a `Person` author in JSON-LD
- **Buttons that hand a page to AI** — **Copy page** as Markdown, **Open in ChatGPT**, **Open in Claude** and **Connect MCP**
- **An MCP server for your readers' agents** — each page names it in a `mcp-server` meta tag; see [MCP server](../brain/mcp-server.md)

A few high-volume crawlers are refused by default, on every site:

| Crawler | Why it is refused |
|---|---|
| `Meta-ExternalAgent`, `Meta-ExternalFetcher` | Meta's AI crawlers, very high volume |
| `Bytespider` | ByteDance's crawler, very high volume |
| `Amazonbot`, `PetalBot` | Amazon's and Huawei's crawlers, very high volume |
| `GoogleOther` (and its image and video variants) | Google's generic research crawler, separate from Search and Gemini |
| `AhrefsBot`, `SemrushBot`, `DataForSeoBot`, `MJ12bot`, `DotBot` | SEO-tool crawlers that build backlink indexes, not readers |

To close your site to AI engines, switch off **Readable and quotable by AI engines** on **Settings ▸ Access ▸ AI engines**: the project leaves `llms.txt` and `llms-full.txt`, and the named AI crawlers are refused in `robots.txt`. Search engines are unaffected.

<!-- widget:callout type=note -->

On a [custom domain](../site/custom-domain.md), `llms.txt`, the summary block, the **Updated** date and most of the JSON-LD currently appear on `docsbook.io` addresses only. The Markdown copy of each page works on every address.

<!-- /widget -->

## What the agent does on its own

On [Pro](../plans-and-pricing.md), the agent works toward the goal every project has: be found on Google and in AI answers. For AI answers it runs two weekly [triggers](../agent/triggers.md) and a citability check, judged against the GEO axes of the [expertise catalog](../agent/expertise.md): Eligibility, AI crawlers, llms.txt, Passages, Content moves and Measurement.

<!-- widget:cards cols=2 icons=inline -->

- [Find out what AI engines say](../agent/triggers.md) — **Do AI engines cite you**, weekly {message-square-quote}

  - **Watches** — Google's AI Overview for the questions a buyer asks, with the sources it cites, and Bing's results, which Copilot draws on
  - **Changes** — the pages behind wrong answers: an outdated claim repeated, a feature said not to exist, a competitor named instead
  - **Measures** — how many watched questions come back naming the page, read again on the check date
  - **Axes** — Measurement, Passages

- [Win the questions rivals own](../agent/triggers.md) — **Where competitors get named**, weekly {swords}

  - **Watches** — who results pages and AI answers name for the questions this product should own
  - **Changes** — reads up to 50 pages of a rival's docs, records which catalog rules their winning pages follow, and writes the page you are missing
  - **Measures** — which questions name a competitor instead of you
  - **Axes** — Content moves, Passages

- [Keep the doors open](../agent/expertise.md) — citability check {door-open}

  - **Watches** — `robots.txt` against 7 named AI agents, each page fetched both as a browser and as `OAI-SearchBot`, and at least 200 words readable without JavaScript
  - **Changes** — whatever blocks a fetch or leaves a page with nothing to quote
  - **Measures** — five scores out of 100, computed from the fetches rather than written by a model
  - **Axes** — Eligibility, AI crawlers, llms.txt

<!-- /widget -->

Answer engines score passages, not whole pages, so the agent holds each section to these catalog rules:

- **One question per section** — the section answers it fully on its own
- **A named subject** — the section says what it is about instead of "it" or "this"
- **Numbers in place** — every claim's supporting number sits in the same paragraph as the claim
- **No keyword stuffing** — the catalog records that repeating a phrase performs worse than leaving the page alone

A GEO change states its bet like any other: the watched questions it expects to name the page, today's count, the predicted one and a check date. Docsbook computes the verdict from the before and after readings.

## See it working

**Analytics ▸ GEO** is one list with a **View** switch. The [AI visibility](./ai-visibility.md) page explains each reading and its limits.

| View | What it shows |
|---|---|
| **Pages** | Which pages AI crawlers read, split into **AI Answers**, **Indexing** and **Training**, and how many checked questions cite each |
| **Crawlers** | Each AI crawler by company, with requests, distinct visitors and how often its engine names you |
| **Prompt mentions** | The questions checked against answer engines, and which ones named you |
| **Prompt demand** | The search demand behind a question your buyers ask |
| **Competitors**, **Competitor prompts** | Who the engines name for your questions, and where they name them instead of you |
| **Competitor tactics** | Which catalog rules the pages engines cite apply |

**Analytics ▸ Audit** shows where your pages stand against the two GEO families: What answer engines require, and Being quoted by models.

## Tell your agent

Say it in a sentence, from [Claude Code, Cursor, Codex or the panel chat](../get-discovered.md):

```text
What does Google's AI Overview say about our product? Fix what it gets wrong.
Which questions name a competitor instead of us? Write the pages we're missing.
Can AI crawlers read our docs? Check and fix whatever blocks them.
Watch these questions every day: "best API docs tool", "host docs from GitHub".
Run the weekly check of what AI engines say about us.
```

## FAQ

<!-- widget:accordion -->

### Does llms.txt get my docs cited?

There is no evidence that it does. Google says its AI features need no AI text file, and none of OpenAI's, Anthropic's or Perplexity's crawler documentation says they read a site's `llms.txt`. Docsbook generates it because it costs you nothing and gives an agent you point at it a map of your docs.

### Which AI crawlers can read my docs?

All of them by default, except the high-volume crawlers in the table above. Switching off **AI engines** refuses the rest by name.

### Can I stay in Google but out of AI answers?

Partly. Switching off **AI engines** refuses the named AI crawlers and drops the project from `llms.txt`, but Google's AI Overviews are built from Google's search index, so a page listed in Google can still be quoted there. `robots.txt` is also a request, not a lock: anything already quoted stays quoted until it is crawled again.

### Do I need a special writing style for AI engines?

No. Google says its AI features need no special writing style or markup, only a page that is indexed and allowed a snippet. What helps is sections that answer one question on their own.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [llms.txt and Markdown](./llms-txt.md) — The machine-readable files and the page buttons for AI tools {file-text}
- [Track AI citations](./ai-visibility.md) — What the GEO numbers measure, and what they cannot {radar}
- [Search engines see you](../seo/README.md) — Being indexed comes first; here is what Docsbook does for it {search}
- [MCP server](../brain/mcp-server.md) — Let your readers' agents search and read your docs {plug}

<!-- /widget -->
