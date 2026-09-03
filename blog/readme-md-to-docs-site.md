---
title: "Turn your README.md into a real documentation site"
description: "Most open-source projects hide their docs in README.md. Here is how to publish that file as a real documentation site without rewriting anything."
---

# Turn your README.md into a real documentation site

Your project's docs live in `README.md`. You always meant to set up a real docs site. You looked at Docusaurus, opened the configuration guide, closed the tab.

This post is the 5-second alternative.

## TL;DR

- Most OSS projects publish docs as `README.md` only
- A README is fine, but it does not index in Google as well as a real docs site, has no AI chat, no analytics, no translations
- Docsbook turns a `README.md` (and optional `docs/`) into a site at `docsbook.io/yourorg/yourrepo` in 5 seconds
- Publishing a public repository costs nothing. No CI/CD, no config files.

## Why a README is not enough

Three losses for README-only projects:

### 1. SEO

A GitHub README is indexed, but Google ranks `github.com/user/repo` for the repo name, not for technical queries. A user searching "how to authenticate with X library" rarely lands on the README, even when the answer is there.

A real docs site at `docs.yourproject.com` (or `docsbook.io/yourorg/yourrepo`) ranks for the long-tail queries your README covers but cannot surface.

### 2. AI distribution

ChatGPT and Perplexity do cite GitHub READMEs, but inconsistently. A clean docs site with `llms.txt`, structured headings, and JSON-LD gets cited far more often.

If your project depends on developer discovery, AI citations are now a real channel — see [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md).

### 3. UX

A 1,500-line README is a single scroll wall. A docs site gives you a sidebar, search, headings as anchor links, breadcrumbs, copy-code buttons. Same content, much better discoverability.

## The 5-second setup

Three steps:

1. Go to [docsbook.io](https://docsbook.io)
2. Sign in with GitHub
3. Paste `github.com/yourorg/yourrepo`

Site live at `docsbook.io/yourorg/yourrepo`. Your README appears as the home page. If you have a `docs/` folder, those pages become the sidebar.

No configuration. No `docsbook.config.js`. No CI/CD pipeline. No deployment.

## What gets indexed

Docsbook reads:

- `README.md` at the repo root → home page
- `docs/` folder (recursively) → site pages
- `docs/README.md` → docs landing page
- YAML frontmatter (`title`, `description`) → page metadata

If you have nothing but a README, you get a one-page docs site. If you have `docs/getting-started.md`, `docs/api.md`, etc., you get a multi-page site with a sidebar built from the folder structure.

## Frontmatter (optional)

Add YAML at the top of any markdown file:

```markdown
---
title: "Quick Start"
description: "Get up and running in 60 seconds"
---

# Quick Start
...
```

`title` becomes the page title in search engines. `description` becomes the meta description. If you skip both, Docsbook uses the first H1 as title and the first paragraph as description.

## What does publishing an OSS project cost?

Publishing the site costs nothing, and neither does anyone reading it. What is metered is AI usage: each project carries its own balance, and questions to the assistant and translation runs spend it. Current numbers live on [docsbook.io/pricing](https://docsbook.io/pricing), generated from the live pricing constants on every request.

Publishing a repository gives you:

- Any public GitHub repository, rendered as a site
- Custom site name, icon, logo, accent colours for light and dark
- Theme toggle, search, breadcrumbs, copy-code buttons
- Header links and social links (GitHub, Discord, X)
- Analytics — pageviews, top pages, referrers, countries
- `llms.txt` and `llms-full.txt` for AI discoverability
- An MCP server, so Claude Code and Cursor can read and edit the docs
- AI chat backed by your `README.md` and `docs/`
- `docs.yourproject.com` with automatic SSL

The one thing you cannot switch off is the small "Powered by Docsbook" link in the page footer. It renders on every Docsbook site, unconditionally — that is the trade for not running the hosting yourself.

## How do I use my own domain instead of docsbook.io?

Point a subdomain at Docsbook and it serves your docs there with SSL provisioned automatically.

- Dashboard → Settings → Domain
- DNS: CNAME `docs` → `cname.vercel-dns.com`
- SSL is automatic

Full walkthrough, including apex domains and redirects: [Custom domain for documentation](./custom-domain-for-docs-howto.md).

## What happens when you push

You push a commit to `main`. Docsbook indexes the change and updates the site. No GitHub Action, no build step. The new content is live within seconds.

## Common questions

### Does it work for private repositories?

Yes. Docsbook authenticates through your GitHub OAuth scope, and the published site can itself be public or private.

### What about MDX or interactive demos?

Docsbook is Markdown-first. For interactive demos, host the demo elsewhere and link to it. If your project needs React components embedded inside docs pages, see [Should you move off Docusaurus in 2026?](./docusaurus-vs-docsbook-2026.md) — Docusaurus is the better fit for that.

### Will it look like every other Docsbook site?

You control brand colours, fonts, layout, header, footer, sidebar and your own domain. The one thing you cannot remove is the small "Powered by Docsbook" link in the footer — it renders on every Docsbook site.

### Can I move away later?

Yes. Your files are in GitHub. Cancel the subscription, point DNS elsewhere, your content is untouched.

Paste `github.com/yourorg/yourrepo` and the site is live in five seconds. Nothing is copied out of your repository, so the README stays the source of truth.

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [Why README-only projects need a documentation site](./why-readme-only-projects-need-a-docs-site.md) — the case for doing this at all
- [How to host documentation from a GitHub repository](./how-to-host-docs-from-github.md) — the other two routes, with tradeoffs
- [Free documentation hosting compared](./free-docs-hosting-comparison.md) — six options against each other
- [Custom domain for docs](./custom-domain-for-docs-howto.md) — moving the result to your own domain
