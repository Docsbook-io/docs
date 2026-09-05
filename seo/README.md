---
title: "SEO for docs: every signal generated, one switch to flip"
description: "Docsbook writes the title, description, canonical URL, hreflang set, cards, JSON-LD, robots.txt and sitemap for every page. You flip one switch and write good headings."
tldr: "Docsbook generates every classical search signal for every documentation page — title, meta description, canonical URL, hreflang, OpenGraph and X cards, JSON-LD, robots.txt and sitemap.xml — with no configuration. The one thing you must do is turn the site-wide SEO switch on in the admin panel: it is off by default, and until it is on every page ships noindex, nofollow."
---

# SEO

Docsbook builds the machine-readable half of your documentation for you. Every page
it hosts is server-rendered HTML carrying a resolved `<title>`, a cleaned meta
description, one canonical URL, an `hreflang` set that contains only languages you
have really translated into, OpenGraph and X cards with a generated image, a JSON-LD
graph, and an entry in a sitemap that `robots.txt` points at. You write Markdown; the
head is a consequence.

This section covers search results — what Google and Bing crawl, index and rank. Two
neighbours cover the other machine surfaces and do not overlap with it:
[AEO](../aeo/README.md) is the answer box above the results, and
[GEO](../geo/README.md) is being cited by an AI assistant instead of ranked.

## What it costs you

Three things, and one of them is not optional.

1. **Turn the SEO switch on.** In the admin panel, **Settings ▸ SEO & GEO**, the
   `SEO` toggle. It is **off on a new project**, and while it is off every page is
   served `noindex, nofollow` — the markup is all generated, and all of it says "do
   not index me". This is the single most common reason a Docsbook site is not in
   Google. It is free on every plan.
2. **Write one clear `# H1` and an opening paragraph that answers the page's
   question.** They become the title and the description unless you override them.
3. **Nothing else.** Canonical URLs, the sitemap, `robots.txt`, cards, JSON-LD and
   the language cluster are managed, and there is no configuration surface for them.

To override the generated line for one page, put it in frontmatter:

```markdown
---
title: "Configure a webhook"
description: "Register a Docsbook webhook, choose its events, and verify the first delivery."
---
```

To keep one page out of the index while leaving it published and readable:

```markdown
---
noindex: true
---
```

`robots: noindex`, `noindex: yes` and `noindex: 1` are accepted too. Use it on pages
that spend crawl budget without ever earning a click — a 90,000-character changelog,
internal working notes, an unfinished placeholder. The site-wide switch is the wrong
instrument for that: turning it off hides everything.

## The signals, and where each one is decided

| Signal | What Docsbook does | Where |
|---|---|---|
| `<title>` | Frontmatter `title` → body `H1` → file name; workspace name appended exactly once | [How it works](./how-it-works.md#what-is-the-title-on-the-page-and-where-does-it-come-from) |
| `<meta description>` | Frontmatter `description` → opening paragraphs, stripped of markup, at 160 characters | [How it works](./how-it-works.md#what-is-the-meta-description-and-what-is-stripped-out-of-it) |
| Canonical URL | Custom domain → product path → apex short path → owner subdomain; never a URL that redirects | [How it works](./how-it-works.md#which-url-does-the-page-call-canonical) |
| `hreflang` | Only locales this page is genuinely translated into, plus `x-default` | [How it works](./how-it-works.md#which-languages-are-advertised-as-alternates) |
| OpenGraph / X card | `summary_large_image` with a generated 1200×630 image per page | [How it works](./how-it-works.md#what-do-the-social-cards-contain) |
| Robots directives | Preview → site switch → page `noindex`, in that precedence | [How it works](./how-it-works.md#what-robots-directives-does-a-page-carry) |
| `sitemap.xml` | Every page plus real translations, `lastmod` from the source commit | [How it works](./how-it-works.md#what-goes-into-sitemapxml) |
| JSON-LD | `Organization` + `TechArticle` + `BreadcrumbList` on every page | [How it works](./how-it-works.md#what-structured-data-is-emitted) |
| Discovery and re-crawl | Sitemap, `robots.txt`, IndexNow push, cache timers | [Indexing](./indexing.md) |
| Google positions | Search Console read into the admin panel, free on every plan | [Indexing](./indexing.md#what-does-the-search-console-integration-actually-do) |

## Why this is the right way (evidence)

| What Docsbook does | Why it works on the crawler | Source |
|---|---|---|
| Serves complete server-rendered HTML | Google renders JavaScript in a queue where a page "may stay… for a few seconds, but it can take longer", and "not all bots can run JavaScript" | [JavaScript SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics) |
| Gives every page its own title and description | Google's title-link sources begin with "Content in `<title>` elements"; and "Identical or similar descriptions on every page of a site aren't helpful" | [Title links](https://developers.google.com/search/docs/appearance/title-link), [Snippets](https://developers.google.com/search/docs/appearance/snippet) |
| Points canonical at the URL that answers 200 | `rel="canonical"` is "a strong signal that the specified URL should become canonical" — a signal Google can only follow if the target resolves | [Consolidate duplicate URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) |
| Lists only real translations in `hreflang` | "If page X links to page Y, page Y must link back to page X. If this is not the case… those annotations may be ignored" | [Localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions) |
| Uses real commit dates for `lastmod` | Google uses `<lastmod>` "if it's consistently and verifiably… accurate" | [Build a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) |
| Emits `FAQPage` / `HowTo` only when the page has that content | "don't add structured data about information that is not visible to the user, even if the information is accurate" | [Intro to structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) |
| Renders the sidebar as HTML links on every page | Crawl budget is spent on what is reachable; "If many of these URLs are duplicates… this wastes a lot of Google crawling time on your site" | [Crawl budget](https://developers.google.com/search/docs/crawling-indexing/large-site-managing-crawl-budget) |
| Serves a 308 when a page moves | A temporary redirect would leave the dead URL as the canonical one | [Consolidate duplicate URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) |

## What Docsbook will not claim

- **None of this makes a page rank.** Every mechanism above makes a page
  *crawlable*, *unambiguous* and *correctly presented*. Google's page-experience
  FAQ answers "Is there a single 'page experience signal'…?" with "There is no
  single signal", and answers how much page experience matters to ranking with
  "Google Search always seeks to show the most relevant content, even if the page
  experience is sub-par" ([Page experience](https://developers.google.com/search/docs/appearance/page-experience)).
  Markup is the floor, not the lever.
- **Structured data is documented as an eligibility signal, not a ranking one.**
  Google's own introduction talks about rich results and says nothing about rank.
- **`priority` and `changefreq` in the sitemap do nothing for Google.** "Google
  ignores `<priority>` and `<changefreq>` values." Docsbook emits them for the
  engines that do read them.
- **Crawl budget is probably not your problem.** Google's crawl-budget guide is
  addressed to "Large sites (1 million+ unique pages) with content that changes
  moderately often (once a week)" and "Medium or larger sites (10,000+ unique
  pages) with very rapidly changing content (daily)" — and says in the same breath
  that these "are a rough estimate to help you classify your site. These are not
  exact thresholds." `noindex` on a huge changelog is still worth doing; treating a
  60-page docs site as a crawl budget emergency is not.
- **No multiplier.** Traffic depends on your topic, your competition and your
  domain. Any platform quoting you a percentage is quoting you someone else's site.

## Limits

- **The site-wide switch defaults to off**, and it is workspace-wide. There is no
  "index this section, not that one" control above the per-page `noindex` flag.
- **On a custom domain, the SEO switch and per-page `noindex` are not honoured** —
  pages are served `index, follow` unconditionally — and there is no `hreflang`
  cluster, no `BreadcrumbList`, no sitemap, no moved-page redirect and none of the
  [GEO](../geo/README.md) page-level signals. The canonical URL, title, description,
  cards and `TechArticle` node are all correct there. See
  [How it works](./how-it-works.md#limits-and-open-questions).
- **Search Console positions cover Docsbook-hosted hosts only.** A site on your own
  domain is outside the property Docsbook reads. See
  [Indexing](./indexing.md#limits-and-open-questions).
- **A rename outside Docsbook leaves no redirect.** Moves made through Docsbook
  write one automatically; a `git mv` does not.

## Checklist

- [ ] The `SEO` toggle is on in **Settings ▸ SEO & GEO**.
- [ ] Every page has one clear `# H1`, or a frontmatter `title`.
- [ ] The opening paragraph answers the page's question in one or two sentences.
- [ ] Every page is reachable from the sidebar; no orphans.
- [ ] Pages that should never rank carry `noindex: true`.
- [ ] For multilingual docs, [translations are enabled](../translation/settings.md)
      so each language earns its own indexable URL.

## Related

- [How Docsbook builds the head of a page](./how-it-works.md) — the resolution orders.
- [Indexing](./indexing.md) — discovery, re-crawl and Search Console.
- [AEO — answer engines and rich results](../aeo/README.md)
- [GEO — citation by AI assistants](../geo/README.md)
- [llms.txt](../geo/llms-txt.md)
- [AI translations](../translation/ai-translations.md)
- [Search options](../ai-chat/search.md) — the on-site search readers use once they arrive.
