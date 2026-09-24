---
title: "llms.txt explained: the complete guide for docs sites"
description: "What llms.txt is, what the v2 spec requires, how it differs from robots.txt and sitemap.xml, what the evidence says it does, and what Docsbook generates."
layout: landing
---

<!-- widget:story share -->

[All posts](../README.md)

**Get found**

# llms.txt explained

[Start free](https://docsbook.io/?start=1)

**llms.txt** {bg:violet}

`llms.txt` is a Markdown file at the root of a site that lists its most useful pages for AI tools; it is an open proposal rather than a standard, and Docsbook generates one for every site.

The proposal is Jeremy Howard's, published at [llmstxt.org](https://llmstxt.org/): version 1 on September 3, 2024, version 2 on August 10, 2026.

- **Category** — Get found
- **Facts checked** — September 2026
- **Reading time** — 4 min

[Get discovered](../../get-discovered.md)

<!-- /widget -->

<!-- widget:quote -->

> We propose adding a /llms.txt markdown file to websites to provide LLM-friendly content.

**Jeremy Howard** — author of the llms.txt proposal, [llmstxt.org](https://llmstxt.org/)

<!-- /widget -->

## What goes in an llms.txt file?

Version 2 of the proposal describes the file in this order:

- **An H1 with the name of the project or site** — the only required section.
- **A blockquote summary** — the key facts needed to understand the rest of the file.
- **Optional prose** — paragraphs or lists, without headings.
- **H2 sections of links** — "file lists" pointing at the pages worth reading.
- **An `Optional` section** — secondary links an agent can skip when it needs a shorter context.

Here is a small file for a product called Acme API, after its opening `# Acme API` line:

```markdown
> Acme is a payments API. These are the pages an AI tool needs to answer questions about it.

## Docs

- [Quickstart](https://docs.acme.example/quickstart.md): make a first charge
- [Authentication](https://docs.acme.example/auth.md): API keys and scopes

## Optional

- [Changelog](https://docs.acme.example/changelog.md): every release
```

The proposal also asks for a clean Markdown version of each listed page, at the page's URL with `.md` appended or with the extension replaced by `.md`.

## How is llms.txt different from robots.txt and sitemap.xml?

The three files answer different questions, and a site usually wants all three.

| | `robots.txt` | `sitemap.xml` | `llms.txt` |
|---|---|---|---|
| Read by | Crawlers, before they fetch | Search engines | AI tools and agents, when asked about your product |
| Says | Which paths a crawler may fetch | Every URL you want indexed | Which pages matter, with a summary |
| Format | Plain-text rules | XML | Markdown |
| Status | Standard (RFC 9309) | Sitemaps protocol | Open proposal |

## Does llms.txt get your docs cited?

Not on its own. As of September 2026, none of Google, OpenAI, Anthropic or Perplexity says its crawlers read a third-party `llms.txt`:

- **Google** — its [AI features guide](https://developers.google.com/search/docs/appearance/ai-features) says you don't need new machine-readable files, AI text files or markup to appear in AI Overviews or AI Mode.
- **OpenAI, Anthropic and Perplexity** — each publishes an `llms.txt` for its own docs, but their crawler pages do not say their bots fetch yours.

Treat it as cheap help for an agent that a person points at your docs, such as a developer's coding assistant. What moves citations is covered in [How to get your docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md).

<!-- widget:callout type=note -->

The Docsbook agent audits against the same evidence: the `llms.txt` axis on **Analytics ▸ Audit** holds 9 rules, each tied to its published source. See [Expertise](../../agent/expertise.md).

<!-- /widget -->

## What does Docsbook generate?

Every Docsbook site gets these with nothing to switch on:

- **`llms.txt`** — every public page with its URL and a link to its Markdown copy, plus the languages the site is published in.
- **`llms-full.txt`** — the full text of the pages in one file, up to 1,000 pages or 3 MB.
- **A Markdown copy of every page** — the **View as Markdown** item in each page's **Copy page** menu.
- **An [MCP server](../../brain/mcp-server.md)** — for agents that would rather query your docs than read a file.

Both files live on the site's `docsbook.io` address, for example `https://<owner>.docsbook.io/llms.txt`, and follow the repository as it changes. Turning off **AI engines** in **Settings ▸ Access** removes the project from `llms.txt` and asks AI crawlers to stay away.

## How do I check my llms.txt?

Fetch it and read the top:

```bash
curl -s https://<owner>.docsbook.io/llms.txt | head -20
```

It should open with a `#` heading and a `>` summary, and every link should load. For the full picture of what AI engines do with your site, see [AI visibility](../../geo/ai-visibility.md).

## FAQ

<!-- widget:accordion -->

### Is llms.txt an official standard?

No. It is an open proposal, now in version 2, and the only section it requires is an H1 naming the project or site.

### What is llms-full.txt?

A companion file with the full text of the listed pages inlined; the v2 proposal itself does not define it. Docsbook generates one for every site.

### Does Google use llms.txt?

Google says you don't need AI text files to appear in AI Overviews or AI Mode. A page there must be indexed and eligible to show a snippet.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [llms.txt and Markdown for AI](../../geo/llms-txt.md) — Exactly what Docsbook publishes for AI tools {file-text}
- [How to get cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md) — What actually moves AI citations {quote}
- [AI engines read and cite you](../../geo/README.md) — The whole GEO side of Docsbook {sparkles}
- [Find wins fast](../../find-wins-fast.md) — How the agent picks the next change {zap}

<!-- /widget -->
