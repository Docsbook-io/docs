---
title: "Free documentation hosting compared: six real options"
description: "GitHub Pages, Vercel, Netlify, Cloudflare Pages, Read the Docs and Docsbook compared as of September 2026: free-tier limits, commercial use and what you add."
---

# Free documentation hosting compared

Every free host below puts your docs online; they differ in their limits, in whether a business may use them, and in how much of a documentation site you still have to build.

Figures come from each vendor's own pricing and documentation pages, as of September 2026. Check them again before you commit: free tiers change.

## The six options at a glance

| Option | Free tier | Limits worth knowing | You still add |
|---|---|---|---|
| GitHub Pages | Free; on GitHub Free the repository must be public | 1 GB per site, 100 GB a month soft bandwidth, 10 builds an hour; not for sites mainly about commercial transactions or SaaS | A docs theme, search, analytics |
| Vercel Hobby | $0 | Non-commercial, personal use only; 100 GB of Fast Data Transfer, 100 deployments a day | Docs framework, search |
| Netlify Free | $0 | 300 credits a month, hard limit: 15 credits per production deploy, 20 per GB of bandwidth | Docs framework, search |
| Cloudflare Pages | $0 | Static requests free and unlimited; 500 builds a month, one at a time | Docs framework, search |
| Read the Docs | Community plan, free for open-source projects | Ad-supported; paid Business plans start at $50 a month | The docs tool it builds: Sphinx, MkDocs, Docusaurus and others |
| Docsbook | 14-day Pro trial with $5 of AI credit, no card | After the trial the site stays published; AI features need [Pro](../pricing/plans.md), $20 a month per project | Nothing to build or deploy |

## What does "free" leave to you?

A static host serves files. Everything that makes those files a documentation site is yours to choose, wire up and maintain:

- **A docs framework** — Jekyll, Docusaurus or another generator, and its upgrades.
- **Search** — a hosted service or a plugin.
- **Answers** — an AI chat is a separate service with its own bill.
- **Being found** — sitemaps, structured data, `llms.txt`, and the ongoing work of fixing pages that nobody finds.

## What does Docsbook include for free?

Docsbook hosts the site and generates the parts a static host leaves out. After the 14-day trial, a project without a plan stays published as static pages:

- **The site** — every Markdown file in your repository, with `README.md` as the home page and folders as the sidebar.
- **Search** — a search box on every page.
- **For search engines and AI** — a sitemap, JSON-LD, [`llms.txt`](../geo/llms-txt.md) and a Markdown copy of each page.
- **Your domain** — attached in **Settings ▸ Domain & API** once the trial has ended or you subscribe.

What switches off without a plan: the [AI chat](../ai-chat/README.md), the agents, [translations](../site/translations.md) and the analytics views. Every Docsbook site shows a small Powered by Docsbook badge.

## Which free option should you pick?

<!-- widget:cards plain cols=2 -->

- **GitHub Pages or Cloudflare Pages** — You want zero cost and you enjoy owning the stack. {server}
- **Read the Docs** — Your project is open source and you are fine with ads. {book-open}
- **Check the terms first** — GitHub Pages and Vercel Hobby both restrict commercial use, so a company's product docs may not fit. {scale}
- **Docsbook** — You want a docs site that answers readers and gets found, with nothing to build. {rocket}

<!-- /widget -->

Free hosting solves serving; it does not tell you which page readers searched for and never found, or why ChatGPT cites a competitor instead of you. Docsbook's agents work on exactly that: [Find wins fast](../find-wins-fast.md).

## FAQ

<!-- widget:accordion -->

### Can I use Vercel's free plan for company docs?

Vercel's docs restrict the Hobby plan to non-commercial, personal use, as of September 2026. A Pro developer seat is $20 per user a month.

### What happens when Netlify's free credits run out?

The Free plan has a 300-credit monthly hard limit with no automatic recharge. More usage means a paid plan: Personal at $9 a month or Pro from $20 a month.

### Is Docsbook free after the trial?

The site stays published as static pages, with search, for as long as you like. The AI chat, agents, translations and analytics views need Pro at $20 a month per project.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Quickstart](../quickstart.md) — From a repository to a live site {rocket}
- [How to host docs from GitHub](./how-to-host-docs-from-github.md) — GitHub Pages, Docusaurus and Docsbook, step by step {git-branch}
- [Plans and pricing](../pricing/plans.md) — What Pro adds and what AI usage costs {credit-card}
- [Find wins fast](../find-wins-fast.md) — What the agent fixes first on a new site {zap}

<!-- /widget -->
