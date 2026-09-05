---
title: "Docsbook use cases: the jobs teams hire documentation for"
description: "Six situations teams bring to Docsbook — being recommended by AI assistants, proving docs convert, keeping pages current, and shipping other languages."
---

# Docsbook use cases: the jobs teams hire documentation for

Six situations teams arrive with, and what Docsbook does about each. Every one ends with the guide that carries out the work, so you can start from the situation rather than from a feature list.

## "I want ChatGPT to recommend us when a customer asks"

**The situation.** You have a product, customers and an ad budget. Someone asks an AI assistant which tool does the thing you do, and your company is not in the answer.

**What blocks it.** An assistant recommends what it can read and check cheaply: what the product does, what it costs, where its limits are, who is behind it. If that is not written anywhere it can fetch, it quotes a competitor who did write it.

**What Docsbook does.** Docsbook publishes your pages as server-rendered HTML, so a crawler sees the text without running JavaScript, and adds the surfaces assistants look for: `sitemap.xml`, canonical URLs, JSON-LD, a visible last-modified date, and `llms.txt` at the site root. Each page gets its own URL and its own title, so a page about one narrow question competes on that question.

**Start with:** [GEO — generative engine optimization](./geo/README.md), then [llms.txt](./geo/llms-txt.md).

## "Our docs get traffic and I cannot tell if it sells anything"

**The situation.** Analytics says the documentation is read. Nobody can say whether reading it made anyone sign up, or which pages waste the visit.

**What blocks it.** Page views do not describe a path. Without events and a defined goal, a docs site reports popularity, not progress.

**What Docsbook does.** Docsbook records page views, searches, read time, feedback votes and tracked events on every page, then reports them as paths: which pages nobody reaches, which searches return nothing, how far a reader gets before leaving, and which countries and languages they arrive from. Mark a page as a funnel step and count how many readers finish.

**Start with:** [Tracking overview](./analytics/tracking/overview.md), then [Events](./analytics/tracking/events.md).

## "Our documentation is three months behind the product"

**The situation.** The product shipped changes. The documentation still describes the old behaviour, and everyone knows it.

**What blocks it.** Documentation that lives outside the repository needs a separate act of remembering. A build-and-deploy step between writing and publishing turns a five-minute correction into a task nobody starts.

**What Docsbook does.** Docsbook serves the Markdown that is in your repository. It re-checks GitHub when the site is visited and re-indexes what changed, so a push is the publish — there is no build step, no CI pipeline and no deploy to wait for. Edits can also come from the web editor or from an agent over MCP, and all three land as commits in the same repository.

**Start with:** [Connect a GitHub repository](./content/setup/github-integration.md), then [Manage your documentation](./guides/getting-started/managing-docs.md).

## "Our customers do not read English"

**The situation.** You sell in markets where your documentation's language is not the one your customers search in. Translating by hand means the translations rot the moment the English changes.

**What blocks it.** A translation is only worth publishing if it stays level with the original and is indexed as its own page. A copy pasted into a folder is neither.

**What Docsbook does.** Docsbook translates your pages into 15 languages — English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish and Dutch. Each language is served on its own route with the right `hreflang` tags, so search engines index it separately, and readers land on their browser's language. Translation is AI work, so it draws on the project balance.

**Start with:** [Turn on translation](./translation/settings.md), then [AI translations](./translation/ai-translations.md).

## "Support answers the same five questions every week"

**The situation.** The answers exist in the documentation. Readers still open a ticket, because they did not find the page.

**What blocks it.** Search that matches literal keywords misses the way people actually ask. A reader who phrases a question differently from your heading gets nothing and asks a human instead.

**What Docsbook does.** Docsbook's AI assistant answers from your indexed pages and cites the page it answered from, so a reader who would have opened a ticket gets the answer where they are. What it could not answer is recorded: unanswered questions and searches that returned nothing are listed for you, which tells you which page to write next. Assistant answers are AI work and draw on the project balance.

**Start with:** [AI chat](./ai-chat/chat.md), then [Page feedback](./ai-chat/feedback.md).

## "We have a README and nobody has time to build a docs site"

**The situation.** The project's documentation is a long `README.md`, plus a `docs/` folder nobody has rendered. Setting up a static site generator is a week of work you will not get.

**What blocks it.** A generator needs a config, a theme, a build pipeline and a hosting decision before it renders one page — and then someone has to maintain all four.

**What Docsbook does.** Docsbook reads the repository as it is. Folder structure becomes the navigation tree, headings become the outline, relative `.md` links resolve to real URLs, and the site is live at `docsbook.io/{owner}/{repo}` with full-text search and a public URL. There is no config file to write. Your Markdown never leaves your GitHub repository, so pointing another tool at the same repo later costs nothing.

**Start with:** [Quick start](./quick-start.md), then [Create your first site](./guides/getting-started/creating-docs.md).

## Next steps

- [Overview](./overview.md) — what Docsbook does with your repository, end to end
- [Concepts](./basics.md) — the terms used above, defined once each
- [Pricing](./pricing.md) — what is metered, and what a project balance pays for
- [FAQ](./faq.md) — cancellation, privacy, sync and data ownership

<!-- widget:cta -->

## Start with the setup that matches your situation

Paste a repository, a website URL, or a sentence about your product, and read the draft before you sign in.

[Start with your own source](https://docsbook.io/start)

<!-- /widget -->
