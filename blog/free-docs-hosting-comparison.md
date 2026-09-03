---
title: "Free documentation hosting compared: six real options"
description: "Six ways to host documentation for nothing — GitHub Pages, Vercel, Netlify, Cloudflare Pages, ReadTheDocs and Docsbook — and what each one costs in time."
---

# Free documentation hosting compared: six real options

"Free" rarely means free. Every free docs hosting option has a real cost in setup time, missing features, or eventual upgrade. This is the comparison that tells you which "free" is closest to actually free.

We make Docsbook. We list our limitations honestly.

## TL;DR

| Option | Setup time | Custom domain | AI chat | Search | Analytics | Real cost |
|---|---|---|---|---|---|---|
| **Docsbook** | 5 sec | Included, with SSL | Included, metered per project | Included | Included | AI usage draws on a per-project balance |
| **GitHub Pages** | 1–4 hours | Free + DNS | None | None | None | Your hosting time |
| **Vercel free** | 1–2 hours | 50/account | None | None | Limited | Build minutes after free tier |
| **Netlify free** | 1–2 hours | Free | None | None | Limited | Bandwidth caps |
| **ReadTheDocs free** | 30 min | Paid only | None | Basic | None | Sphinx complexity |
| **Cloudflare Pages** | 1 hour | Free | None | None | None | Build minutes |

If your priority is "live today with good defaults," Docsbook wins. If your priority is "I want to own every layer," GitHub Pages + a static generator wins. Everything in between is a tradeoff.

## Docsbook

What you get, without paying anything to publish:

- 5-second setup from a GitHub repository
- Custom brand colours (light and dark), logo, icon, font
- Search, breadcrumbs, copy-code, theme toggle
- Header links and social links (GitHub, Discord, X)
- Analytics — pageviews, top pages, referrers, countries
- `llms.txt` and `llms-full.txt` for AI discoverability
- An MCP server, so Claude Code and Cursor can read and edit the docs
- AI chat trained on your content

What it costs, and what it does not:

- **Publishing, hosting, the custom domain and every page a reader opens cost nothing.** They do not draw on any balance.
- **AI usage is metered.** Each project carries its own balance, and questions to the assistant and translation runs spend it. Current numbers are on [docsbook.io/pricing](https://docsbook.io/pricing), generated from the live pricing constants on every request.
- **The footer credit is permanent.** Every Docsbook site renders a small "Powered by Docsbook" link in the page footer. There is no setting and no plan that removes it.

Best for: OSS projects, indie products, MVPs, and anyone who wants a real docs site without managing hosting.

## GitHub Pages

What you get:

- Free hosting for static sites
- Custom domain free
- Jekyll built-in or any static generator via Actions
- Decent uptime, CDN included

What you do not get:

- Out-of-the-box search (you add Algolia or build your own)
- AI chat (no integrations)
- Analytics (you add Google Analytics or similar)
- Automatic builds without writing GitHub Actions
- Anything beyond what your static generator produces

Real cost:

- 1–4 hours initial setup including DNS
- Recurring hours when your static generator has breaking updates
- Algolia DocSearch approval (weeks of wait, denial possible)

Best for: OSS engineers who enjoy owning the stack and want zero recurring cost.

## Vercel free tier

What you get:

- Generous free tier for static and serverless sites
- Custom domains, automatic SSL
- Excellent build performance and global CDN
- Preview deployments for every PR

What you do not get:

- A docs-aware setup (you bring your own framework)
- AI chat, search, analytics — all your problem
- Free is hobbyist tier; commercial use requires Pro

Real cost:

- Setup time depends entirely on the framework you pick (Next.js, Astro, Vite, etc.)
- Build minutes after free tier
- The "Pro" upgrade at $20/user/month when you commercialize

Best for: teams that already use Vercel for the rest of their stack and have a docs framework picked.

## Netlify free tier

Similar to Vercel — strong free tier for static sites, custom domains, CDN.

Same caveats: you bring the framework, the search, the AI, the analytics.

Bandwidth caps (100GB/month on free) can bite if your docs go viral.

Best for: same audience as Vercel.

## ReadTheDocs free

What you get:

- Free for OSS projects (paid for commercial)
- Sphinx and MkDocs supported
- Versioned docs out of the box
- Some search

What you do not get:

- Custom domain on free
- AI chat
- Modern theming (Sphinx themes are functional, not pretty)
- Frontmatter-driven workflow

Real cost:

- Sphinx complexity if you do not already use it
- RST format if you use Sphinx defaults
- $50/month for commercial use with custom domain

Best for: Python OSS projects with existing Sphinx setup.

## Cloudflare Pages

What you get:

- Generous free tier
- Custom domain free with Cloudflare DNS
- CDN performance
- Build minutes included

What you do not get:

- Docs-aware features
- Anything pre-built for documentation

Same caveats as Vercel and Netlify — you bring everything above the hosting layer.

Best for: teams already on Cloudflare with strong DevOps capacity.

## The hidden cost: time

The cheapest dollar-cost option is rarely the cheapest total-cost option.

Do this arithmetic with your own numbers rather than with ours: take the hourly cost of the person who would do the setup, multiply by the hours in the table above, and compare that against the alternative. We publish no dollar figure for it, because an hourly rate we invented for you would be a made-up number dressed as a calculation.

What Docsbook trades for those hours is concrete and small: every site carries a "Powered by Docsbook" link in its footer, on every site, with no way to remove it.

## The hidden cost: feature creep

Most teams that pick a self-hosted free option eventually add:

- Algolia DocSearch ($60+/month after approval)
- A chatbot SaaS ($30–100/month)
- Analytics ($0–50/month)
- Translation pipeline (weeks of engineering)

Price that stack against Docsbook on [docsbook.io/pricing](https://docsbook.io/pricing) rather than against a number quoted here. The shape of the comparison is what matters: the self-hosted stack accumulates several fixed monthly subscriptions plus the engineering time to wire them together, while Docsbook charges for AI usage and nothing for the site.

## How to pick

- **Will you spend more than two hours setting up docs hosting?** → Docsbook
- **Are you a Python OSS team already on Sphinx?** → ReadTheDocs
- **Do you want to own every layer, and enjoy owning it?** → GitHub Pages or Cloudflare Pages
- **Do you need `docs.yourcompany.com` on day one?** → Docsbook, Netlify or Cloudflare Pages
- **Will you publish in several languages?** → Docsbook, which indexes each locale at its own URL

## Why does this page not quote our own price?

Because a price copied into a blog post goes stale without telling anyone, and a stale price is the single most damaging thing a comparison page can carry: it is exactly the sentence a reader — or an AI assistant summarising this page six months from now — will repeat to a buyer.

[docsbook.io/pricing](https://docsbook.io/pricing) is generated from the live pricing constants on every request. It has no "last updated" date because there is nothing on it that can go stale. Read the number there; treat any Docsbook price you find anywhere else, including here, as a rumour.

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [Best documentation platforms for startups in 2026](./best-docs-platforms-for-startups-2026.md) — the same field ranked by company stage
- [How to host documentation from GitHub](./how-to-host-docs-from-github.md) — the step-by-step for the three main paths
- [Turn your README.md into a documentation site](./readme-md-to-docs-site.md) — the shortest path if your docs are one file
- [Custom domain for documentation](./custom-domain-for-docs-howto.md) — DNS, SSL and redirects for `docs.yourcompany.com`
