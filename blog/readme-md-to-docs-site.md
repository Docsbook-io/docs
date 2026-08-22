---
title: "Turn Your README.md into a Documentation Site (2026)"
description: "Most open-source projects have docs hidden in README.md. This is how to turn that README into a real documentation site in 5 seconds — without rewriting anything."
---

# Turn Your README.md into a Documentation Site

Your project's docs live in `README.md`. You always meant to set up a real docs site. You looked at Docusaurus, opened the configuration guide, closed the tab.

This post is the 5-second alternative.

## TL;DR

- Most OSS projects publish docs as `README.md` only
- A README is fine, but it does not index in Google as well as a real docs site, has no AI chat, no analytics, no translations
- Docsbook turns a `README.md` (and optional `docs/`) into a site at `docsbook.io/yourorg/yourrepo` in 5 seconds
- Free plan covers public repos. No CI/CD, no config files.

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

## The free plan covers most OSS projects

Free includes:

- Any public GitHub repo
- Custom site name, icon, logo, accent colors (light + dark)
- Theme toggle, search, breadcrumbs, copy-code buttons
- Header links, social links (GitHub, Discord, Twitter)
- Last 24 hours of analytics
- `llms.txt` and `llms-full.txt` for AI discoverability
- AI chat backed by your README + `docs/`

What you do not get on Free:

- Custom domain (Business feature)
- AI translations to 15 languages
- The "Powered by Docsbook" credit stays in the footer — it isn't a paid removal, it's just how the product works
- Analytics beyond 24h
- MCP server for advanced workflows

For most OSS projects, Free is fine. Upgrade when you outgrow it.

## Custom domain (paid)

If you want `docs.yourproject.com` instead of `docsbook.io/yourorg/yourrepo`:

- Business ($159/month)
- Dashboard → Settings → Domain
- DNS: CNAME `docs` → `cname.vercel-dns.com`
- SSL is automatic and free

## What happens when you push

You push a commit to `main`. Docsbook indexes the change and updates the site. No GitHub Action, no build step. The new content is live within seconds.

## Common questions

### Does it work for private repos?

Yes, on paid plans. Docsbook authenticates through your GitHub OAuth scope.

### What about MDX or interactive demos?

Docsbook is markdown-first. For interactive demos, link out to a hosted demo. If your project needs deep React component embedding, see [Docusaurus vs Docsbook 2026](./docusaurus-vs-docsbook-2026.md) — Docusaurus is the better fit.

### Will it look like every other Docsbook site?

You control brand colors, fonts, layout, header, footer, sidebar, and can add a custom domain on Business — the one thing you can't remove is the small "Powered by Docsbook" credit in the footer, on any plan.

### Can I move away later?

Yes. Your files are in GitHub. Cancel the subscription, point DNS elsewhere, your content is untouched.

## Related reading

- [Why README-only projects need a docs site](./why-readme-only-projects-need-a-docs-site.md)
- [How to host documentation from GitHub](./how-to-host-docs-from-github.md)
- [Free docs hosting comparison](./free-docs-hosting-comparison.md)

---

Try it on your project: paste `github.com/yourorg/yourrepo` at [docsbook.io](https://docsbook.io). Site live in 5 seconds.
