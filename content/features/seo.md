---
title: "SEO Features in Docsbook"
description: "Automatic SEO for documentation — static HTML, fast Core Web Vitals, meta tags, OpenGraph, sitemaps, and per-language indexing without any configuration."
---

# SEO Optimization

Docsbook handles technical SEO automatically so your documentation ranks on Google without configuration.

## What Docsbook Does for You

### Static Pages, No JavaScript Penalty

Most documentation platforms ship heavy JavaScript bundles. Google's Core Web Vitals penalize slow pages directly — a slow docs site loses rankings before anyone reads it.

Docsbook generates static HTML pages with minimal JavaScript. Every page scores **95+ on Google PageSpeed Insights** out of the box.

### Meta Tags on Every Page

Each page gets:
- A unique `<title>` derived from your page heading
- A `<meta description>` generated from your opening paragraph
- Open Graph tags for social sharing previews

You don't write these manually. If you want to override them per page, you can — but defaults are production-ready.

### Structured Data (JSON-LD)

Search engines understand your content better when you label it. Docsbook automatically adds JSON-LD structured data to every page so Google knows whether it's reading a how-to guide, a reference page, or a FAQ.

This structured markup is what earns rich results — the enhanced search listings with descriptions, breadcrumbs, and FAQ dropdowns.

### Sitemap and Canonical URLs

Docsbook generates and submits a sitemap automatically. Every page has a canonical URL set correctly, which prevents duplicate-content penalties when the same page is accessible via multiple paths.

When you rename a page, Docsbook handles the redirect so you don't lose the ranking the old URL had accumulated.

### Internal Linking via Sidebar

Google discovers pages by following links. Documentation buried behind a bad navigation structure doesn't get indexed — it simply doesn't exist from Google's perspective.

Docsbook's sidebar is rendered as real HTML links on every page, giving search engine crawlers a complete map of your content without any additional configuration.

## Why Documentation SEO Compounds

Documentation targets **high-intent queries** — searches by developers actively building products: "how to integrate X", "API reference for Y", "troubleshoot Z error". These readers have purchasing authority and influence tool decisions at their companies.

Unlike blog posts, which decay in relevance, a thorough reference page written once keeps ranking for years. A page explaining how to configure a webhook doesn't get stale just because it's old — it gets stronger as more sites link to it.

The typical trajectory:

| Timeline | What happens |
|---|---|
| Month 1–2 | Pages indexed, ranking for nothing |
| Month 3–6 | Long-tail queries start showing up in Search Console |
| Month 6–18 | Compounding — 10× more impressions than month 1 |
| Month 18+ | Organic signups from Google every week, for free |

## AI Search Discoverability

In 2025, developers get answers directly from ChatGPT, Perplexity, and Gemini — without clicking through to a website. To appear in these AI-generated answers, your docs need to be structured for AI crawlers.

Docsbook automatically generates an **`llms.txt`** file — a plain-text index of your documentation that AI crawlers use to understand your site. Think of it as `robots.txt` for LLMs.

Every Docsbook page is also structured with clear prose and direct answers — the format AI models prefer when sourcing citations.

## What You Control

| Setting | Where |
|---|---|
| Page title (overrides auto-generated) | Front matter: `title: "..."` |
| Meta description | Front matter: `description: "..."` |
| Canonical URL | Managed automatically |
| Sitemap | Generated automatically |

## Checklist: Getting the Most Out of Docsbook SEO

- [ ] Every page has a clear H1 heading — this becomes the `<title>`
- [ ] Opening paragraphs are 1–2 sentences that answer the page's topic directly
- [ ] Pages are linked from the sidebar (no orphan pages)
- [ ] You've submitted your sitemap to Google Search Console
- [ ] For multilingual docs: [translations enabled](../../translation/settings) — each language version is indexed separately

---

> **Your docs are already SEO-optimized the moment you publish.**
> [Connect your GitHub repo →](https://docsbook.io/connect)

See also: [AI Translations →](../../translation/ai-translations) · [Search Options →](./search)
