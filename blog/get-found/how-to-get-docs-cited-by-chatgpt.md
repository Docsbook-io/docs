---
title: "How to get your documentation cited by ChatGPT in 2026"
description: "A checklist built on OpenAI, Google, Anthropic and Perplexity docs: let the right crawlers in, stay indexable, write quotable passages, and measure citations."
layout: landing
---

<!-- widget:story share -->

[All posts](../README.md)

**Get found**

# How to get your documentation cited by ChatGPT

[Start free](https://docsbook.io/?start=1)

**Cited by ChatGPT** {bg:green}

ChatGPT search only shows sites its search crawler may fetch, and it quotes pages that answer the question in a passage it can lift, so the work is crawler access first, then pages written to be quoted, then measuring what the engines say.

Crawler and eligibility facts below come from each vendor's own documentation as of September 2026.

- **Category** — Get found
- **Facts checked** — September 2026
- **Reading time** — 5 min

[Get discovered](../../get-discovered.md)

<!-- /widget -->

## Which crawlers need access?

Each AI vendor runs several crawlers with different jobs, and a `robots.txt` rule for one does not touch the others.

| Crawler | Vendor | What it does |
|---|---|---|
| `OAI-SearchBot` | [OpenAI](https://developers.openai.com/api/docs/bots) | Surfaces sites in ChatGPT search; sites that block it are not shown in ChatGPT search answers |
| `GPTBot` | [OpenAI](https://developers.openai.com/api/docs/bots) | Crawls content that may be used to train OpenAI's models |
| `ChatGPT-User` | [OpenAI](https://developers.openai.com/api/docs/bots) | Visits a page when a ChatGPT user's question needs it; robots.txt rules may not apply |
| `Claude-SearchBot` | [Anthropic](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) | Indexes content to improve Claude's search results |
| `Claude-User` | [Anthropic](https://support.claude.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler) | Fetches a page when someone asks Claude a question |
| `PerplexityBot` | [Perplexity](https://docs.perplexity.ai/guides/bots) | Surfaces and links sites in Perplexity's search results; not used for model training |
| `Google-Extended` | [Google](https://developers.google.com/search/docs/crawling-indexing/google-common-crawlers) | Controls use in Gemini training and grounding; no effect on Google Search inclusion or ranking |

OpenAI treats these settings as independent: you can allow `OAI-SearchBot` to appear in ChatGPT search and still disallow `GPTBot` to keep your pages out of training.

On Docsbook, the default `robots.txt` lets these crawlers in. The **AI engines** switch in **Settings ▸ Access** turns AI crawlers away as a group when you want your docs kept out of AI answers.

## Can the engines read your pages?

For Google's AI Overviews and AI Mode, a page must be indexed and eligible to show a snippet; Google says no special files or markup are needed ([AI features guide](https://developers.google.com/search/docs/appearance/ai-features)).

- **No `noindex` or `nosnippet`** on pages you want quoted.
- **Text in the HTML** — a crawler that does not run JavaScript sees only what the server sends. Docsbook renders every page on the server.
- **Public pages** — a site behind a password or SSO sign-in cannot be quoted.

## How do you write a passage an engine can quote?

Answer engines retrieve passages, not whole pages, so each section has to stand on its own:

- **Lead with the answer** — the first sentence under each heading says what is true or what to do.
- **Name the subject in every section** — "Rotate an API key", not "How to do it".
- **Use specifics** — names, numbers, limits and prices a reader can check.
- **Keep headings stable** — every heading on a Docsbook page gets its own anchor, which is the link an engine can cite.

These are rules from the Docsbook [expertise catalog](../../agent/expertise.md): 299 rules, each tied to a published source, grouped into axes such as **Passages** and **Eligibility** on **Analytics ▸ Audit**.

## How do you measure AI citations?

Ask the engines the questions your customers ask, and record whether they cite you and who they cite instead.

- **Analytics ▸ GEO** — for each prompt you track, whether the AI answer cited your docs, and in **GEO Competitors**, whose pages the engines returned.
- **Do AI engines cite you** — a weekly trigger that asks the answer engines about your product and fixes what makes them cite someone else.
- **Where competitors get named** — a weekly trigger that finds the questions you should own and someone else is answering.

## What should I tell my agent?

You don't have to run this checklist by hand. Tell the Docsbook agent in one sentence, from Claude Code, Cursor or the panel chat ([Get discovered](../../get-discovered.md)):

```text
Check whether ChatGPT and Perplexity cite our docs for our top five questions, and fix the pages that lose to competitors.
```

It works through [pull requests](../../agent/review.md), each with a reason and a date to check the result. [Find wins fast](../../find-wins-fast.md) explains how it picks what to fix first.

## FAQ

<!-- widget:accordion -->

### Does llms.txt get my docs cited by ChatGPT?

No vendor says so: OpenAI's crawler documentation does not mention reading a site's `llms.txt`, and Google says AI text files are not needed. More in [llms.txt explained](./llms-txt-guide.md).

### Can I allow ChatGPT search but block training?

With OpenAI, yes: allow `OAI-SearchBot` and disallow `GPTBot`. Docsbook's **AI engines** switch treats AI crawlers as one group, on or off.

### How do I know if ChatGPT already cites my docs?

Check the answers, not only your traffic. **Analytics ▸ GEO** records whether AI answers cite your docs for the prompts you track.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [AI visibility](../../geo/ai-visibility.md) — Track AI answers and citations for your docs {radar}
- [AI engines read and cite you](../../geo/README.md) — What Docsbook does for GEO {sparkles}
- [llms.txt explained](./llms-txt-guide.md) — What the file does, and what it doesn't {file-text}
- [Find wins fast](../../find-wins-fast.md) — How the agent picks the next change {zap}

<!-- /widget -->
