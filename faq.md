---
title: "Docsbook FAQ: agents, SEO, AI answers and pricing"
description: "Straight answers about Docsbook: what the AI agent does on its own, how docs get found on Google and cited by ChatGPT, what it costs, and who owns your content."
---

# FAQ

Short answers to what people ask before and after they publish, each linking to the page that covers it in full.

## Getting started

<!-- widget:accordion -->

### What is Docsbook?

Docsbook publishes your documentation and puts AI agents to work on it: they check the pages against 299 published rules, read what search engines, AI assistants and readers do, and ship improvements as pull requests. Start with the [quickstart](./quickstart.md).

### Do I need a GitHub account?

No. Start from a template and Docsbook creates and hosts the repository for you; you need GitHub only to import a repository you already have. See [edit and publish](./site/editing.md).

### Can I bring the docs I already have?

Yes. Connect the GitHub repository your Markdown lives in and its pages become the site as they stand, or upload PDF, Word and Markdown files as [sources](./brain/sources.md), each of which becomes a page. Guides for [GitBook](./blog/migrating-from-gitbook-to-docsbook.md) and [Docusaurus](./blog/migrating-from-docusaurus-to-docsbook.md) cover the details.

### Does Docsbook support versioned docs?

Not as a version switcher: a project publishes one branch of one repository. Keep each version you need live as its own project.

<!-- /widget -->

## The agent

<!-- widget:accordion -->

### What does the agent do without being asked?

It runs the [triggers](./agent/triggers.md) you switch on — 49 ready-made workflows that wake on a schedule or on an event, such as a search that found nothing or a question the chat could not answer. [Find wins fast](./find-wins-fast.md) explains how it picks what to fix.

### Will it change my docs without my approval?

Every change is a git commit delivered as a pull request, and **Settings ▸ General ▸ When a change goes live** decides whether it merges itself or waits for you. A write never marks a page approved. See [review and publish](./agent/review.md).

### Which AI tools can I give it work from?

Claude Code, Cursor, Codex, VS Code, Windsurf, Gemini CLI, ChatGPT and Claude connectors — any MCP client — plus the chat in the panel. See [tell your agent, get discovered](./get-discovered.md).

### How much does an agent run cost?

$0.10 per run plus three times what its model tokens cost, capped at $50 a run, paid from your balance. See [pricing](./plans-and-pricing.md).

<!-- /widget -->

## Search and AI engines

<!-- widget:accordion -->

### Is SEO set up automatically?

Yes, on every plan. Every page ships server-rendered with its title, description, canonical URL, social card and structured data, and sites on a `docsbook.io` address also get a sitemap and `hreflang`. See [search engines see you](./seo/README.md).

### Does `llms.txt` get my docs cited by ChatGPT?

Not on its own: Google says its AI features need no AI text file, and no major AI crawler documents reading one. Docsbook still publishes `llms.txt` and a Markdown copy of every page, because they cost nothing; what earns citations is sections that answer one question clearly, which is what the agent works on. See [AI engines read and cite you](./geo/README.md).

### How do I know whether AI assistants cite my docs?

**Analytics ▸ GEO** shows which AI crawlers read each page, and which of the questions you watch name you in Google's AI Overviews; checks you run in ChatGPT, Claude or Perplexity can be added through the API. See [AI visibility](./geo/ai-visibility.md).

<!-- /widget -->

## Your readers

<!-- widget:accordion -->

### Does the AI chat make things up?

It answers from the pages it found for the question and shows them as sources. When the docs don't cover a question, the answer says so and sends the reader to support — your support email, if you set one. See [AI chat](./ai-chat/README.md).

### Do reader analytics use cookies?

No. A visitor is counted by a salted hash of their IP address and your project, and history is kept for 30 days. See [you hear every reader](./analytics/README.md).

<!-- /widget -->

## Plans and your content

<!-- widget:accordion -->

### How much does Docsbook cost?

Publishing is free. Pro is $20 a month with $20 of AI usage credited every month, and every account starts with a 14-day Pro trial with $5 of AI credit. See [pricing](./plans-and-pricing.md).

### What happens when the trial ends?

The site, its search, your domain, the editor and GitHub sync keep working. AI chat, agents and translations switch off, and analytics are hidden until you subscribe or top up.

### Can I use my own domain or make the docs private?

Yes to both, on every plan — only during the free trial can a custom domain not be set until the plan is paid. See [custom domain](./site/custom-domain.md) and [private docs](./site/private-docs.md).

### Who owns the content?

You do. Pages are plain Markdown in a Git repository — yours, or one Docsbook hosts for you and can move to your GitHub — so nothing is locked in.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Quickstart](./quickstart.md) — Publish a site and start the trial {rocket}
- [Tell your agent, get discovered](./get-discovered.md) — Connect your agent and give it a goal {megaphone}

<!-- /widget -->
