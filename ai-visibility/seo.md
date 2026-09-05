---
title: "SEO for docs: rank in search without configuring anything"
description: "Docsbook ships static HTML, meta tags, Open Graph, JSON-LD, a sitemap and canonical URLs on every page, and keeps single pages out of the index on request."
tldr: "Docsbook generates static HTML with meta tags, Open Graph, canonical URLs, sitemap.xml, robots.txt and JSON-LD on every page. Turn SEO on in the admin SEO / GEO tab; per-page opt-out is `noindex: true` in frontmatter."
---

# SEO Optimization

Docsbook SEO is the classical search surface of your documentation: what Google and Bing crawl, index and rank. Docsbook generates it for every page automatically — static HTML, a unique title and description, Open Graph tags, JSON-LD, a sitemap and a canonical URL — so a new page is indexable the moment it is published.

This page covers search results. Two neighbours cover the other two machine surfaces, and they do not overlap with this one:

- [AEO](./aeo.md) — the answer boxes above the results: `FAQPage`, `HowTo` and `speakable` markup.
- [GEO](./geo.md) — being cited by an AI assistant rather than ranked by a search engine.

## What does Docsbook do for SEO without being asked?

Docsbook renders every documentation page as static HTML with a unique `<title>`, a `<meta description>`, Open Graph tags, JSON-LD structured data and a canonical URL, and lists it in `sitemap.xml`. You configure none of that. The `SEO` toggle in the admin **SEO / GEO** tab is the whole-site switch, and it is the only control most sites ever touch.

### Static pages, no JavaScript penalty

Docsbook serves documentation as server-rendered HTML with minimal JavaScript. This matters more for crawling than for speed scores: a crawler that has to execute a bundle to see your text often does not, and content that appears only after client-side rendering is content some assistant crawlers never read at all. Fetch any page of your docs with `curl` and grep for a sentence from the body — if it is there, every crawler can see it.

### Meta tags on every page

Each page gets:

- A unique `<title>` derived from the page's own heading.
- A `<meta description>` generated from the opening paragraph.
- Open Graph tags for social sharing previews.

You do not write these by hand. Override either per page from frontmatter — `title:` and `description:` — when the generated one is not the sentence you want a searcher to read.

### Structured data (JSON-LD)

Docsbook adds JSON-LD to every page, so a search engine is told what it is reading rather than left to infer it. Each page carries a `TechArticle` object with its headline, description, canonical URL, language and publisher, plus a `BreadcrumbList` describing where the page sits in your navigation.

Two more objects appear only when [AEO](./aeo.md) is enabled and the page actually contains the matching content: `FAQPage` and `HowTo`. Docsbook never emits markup for content a page does not have — invented structured data is a manual-action risk, not an optimisation.

### Sitemap and canonical URLs

Docsbook generates `your-site/sitemap.xml` automatically and links it from `robots.txt`, so crawlers find it without you submitting anything. Every page declares a canonical URL, which is what stops the same content competing with itself when more than one path reaches it.

With translations turned on, the sitemap lists a language's URL only for the pages that language has actually been translated into. An enabled language does not by itself translate anything, and advertising a URL that would serve your original English text spends crawl budget on a page that points search engines straight back to the original. The same rule governs the `hreflang` cluster on the page itself: a locale that is not genuinely translated is dropped from it.

### Renaming a page breaks its ranking

Renaming a page changes its URL, and the old URL stops resolving. **Docsbook does not create a redirect for you.** Treat renaming a page that already ranks as a deliberate act: keep the old path, or accept that the ranking restarts at the new one.

## How do I keep one page out of Google?

Add `noindex: true` to that page's frontmatter. The page stays published and readable by anyone with the link; it asks search engines not to index it.

```markdown
---
title: "Internal Notes"
noindex: true
---
```

The `robots: noindex` spelling other documentation tools use works too, as do `noindex: yes` and `noindex: 1`. Anything else — absent, `false`, `index` — means index.

Use it on the pages that spend crawl budget without ever earning a click: a changelog thousands of lines long, internal working notes you publish for your team, a placeholder you have not finished. The site-wide `SEO` toggle is the wrong instrument for this; turning it off hides everything.

### Internal linking via the sidebar

Google discovers pages by following links, and documentation buried behind bad navigation does not get indexed — from a crawler's point of view it does not exist. Docsbook renders the sidebar as real HTML links on every page, so every crawl of any page is also a crawl of the map of your content.

A page nothing links to is an orphan. Docsbook's own analytics can show you which pages readers never reach; the sidebar is the cheapest fix.

## Why does documentation SEO compound?

Documentation targets **high-intent queries** — the searches of people who are already building something: "how to integrate X", "API reference for Y", "troubleshoot Z error". A reader searching that is much closer to a decision than a reader who found a blog post.

Unlike a blog post, a reference page does not decay. A page explaining how to configure a webhook does not become less true because it is eighteen months old, and it keeps matching the same query for as long as the feature exists. Each new page adds another entry point rather than replacing the last one, which is why a documentation site's search traffic tends to build slowly and then keep building — and why a rename that silently drops a ranking page is expensive.

What Docsbook will not tell you is how much or how fast. Traffic depends on your topic, your competition and your domain, and any platform quoting you a multiple is quoting you someone else's site.

## What you control

| Setting | Where |
|---|---|
| Page title (overrides the generated one) | Frontmatter: `title: "..."` |
| Meta description | Frontmatter: `description: "..."` |
| Keep one page out of the index | Frontmatter: `noindex: true` |
| Site-wide SEO markup | Admin panel → **SEO / GEO** tab → `SEO` |
| Canonical URL | Managed automatically |
| Sitemap and `robots.txt` | Generated automatically |
| Which language URLs are advertised | Follows what is actually translated |

## Checklist: getting the most out of Docsbook SEO

- [ ] Every page has one clear H1 — it becomes the `<title>`.
- [ ] The opening paragraph answers the page's question in one or two sentences.
- [ ] Every page is reachable from the sidebar; no orphans.
- [ ] Pages that should not rank carry `noindex: true`.
- [ ] Your sitemap is submitted to Google Search Console.
- [ ] For multilingual docs, [translations are enabled](../../translation/settings.md) so each language is indexed separately.

## Next steps

Turn `SEO` on in the admin **SEO / GEO** tab — it applies to every page on the next render, and costs nothing to run.

## Related

- [AEO — answer engines and voice](./aeo.md) — FAQ, HowTo and speakable markup.
- [GEO — citation by AI assistants](./geo.md) — TL;DR blocks, dates and attribution.
- [llms.txt](./llms-txt.md) — the machine-readable index of your site.
- [AI translations](../translation/ai-translations.md) — one indexable URL per language.
- [Search options](../ai-chat/search.md) — the on-site search readers use once they arrive.
