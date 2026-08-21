---
title: "SEO Features in Docsbook"
description: "Automatic classical SEO for documentation — static HTML, fast Core Web Vitals, meta tags, OpenGraph, sitemaps, canonical URLs and per-language indexing without any configuration."
tldr: "Docsbook generates static HTML with meta tags, Open Graph, canonical URLs, sitemap.xml, robots.txt and JSON-LD on every page. Toggle SEO on in the admin SEO / GEO tab — no configuration needed."
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

Docsbook generates a sitemap automatically at `your-site/sitemap.xml`, and links it from `robots.txt` so crawlers find it without you submitting anything. Every page declares a canonical URL, which is what stops the same content from competing with itself when it is reachable by more than one path.

If you have translations turned on, the sitemap lists a language's URL only for pages that language has actually been translated into. An enabled language does not by itself translate anything, and advertising a URL that would just serve your original text spends crawl budget on a page that points search engines straight back to the original.

Renaming a page changes its URL, and the old one stops resolving. Docsbook does not create a redirect for you, so treat a rename of a page that already ranks as a deliberate act: keep the old path, or accept that the ranking restarts at the new one.

### Keeping a Page Out of Search

Some pages are not meant to rank. A changelog thousands of lines long, internal notes you publish for your team, a placeholder you have not finished — each of these spends crawl budget that your reference pages need.

Add `noindex` to a page's frontmatter and search engines are told to leave it out:

```markdown
---
title: "Internal Notes"
noindex: true
---
```

The page stays published and readable by anyone with the link; it simply asks not to be indexed. The `robots: noindex` spelling works too, if that is what you are used to from another tool.

This is per page. The `SEO` toggle in the admin panel is the whole-site switch — turning that off hides everything, which is not what you want when the problem is a single page.

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

See also: [GEO — Generative Engine Optimization →](./geo) · [AEO — Answer Engine Optimization →](./aeo) · [AI Translations →](../../translation/ai-translations) · [Search Options →](./search)
