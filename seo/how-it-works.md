---
title: "How Docsbook builds the head, canonical and sitemap of a page"
description: "The resolution orders behind every SEO signal Docsbook emits: title, description, canonical, hreflang, cards, robots, sitemap, structured data and render mode."
tldr: "Every doc page gets a title (frontmatter → H1 → filename, brand appended once), a description (frontmatter → cleaned first paragraphs, 160 and 400 characters), one canonical URL, an hreflang set containing only genuinely translated locales, an OpenGraph and X card with a generated 1200×630 image, robots directives, a JSON-LD graph, and a sitemap entry with a real commit date as lastmod."
---

# How Docsbook builds the head of a page

This page is the mechanism: what Docsbook puts in the `<head>` and in `sitemap.xml`
for every page it hosts, in the order the code resolves it, so you can predict the
output instead of curling it. For what it is worth to you and what you have to switch
on, start at the [SEO index](./README.md).

## What is the title on the page, and where does it come from?

The `<title>` of a Docsbook page is resolved in three steps, first match wins:

| Order | Source | Why it is first |
|---|---|---|
| 1 | Frontmatter `title:` | The only one of the three you can edit without changing what a reader sees on the page. |
| 2 | The body `# H1` | A real heading, already written for a human. |
| 3 | A title derived from the file name | Never empty; a page always has a SERP line. |

The workspace name is then appended **exactly once**, as `Page title — Workspace`,
and skipped when the title already says it as a standalone word. "Docs" inside
"Docsbook" does not count — both neighbours of the match must be non-word characters,
tested against Unicode letters and digits rather than ASCII ones, so a Cyrillic or
CJK workspace name matches the same way a Latin one does. A page whose title is only
the workspace name (the site root) becomes `Workspace — Documentation`. The finished
string is emitted as an absolute title, which stops the site-wide `%s | Docsbook`
template from appending a second brand copy.

On a translated page the title comes from the cached translated metadata, and
otherwise from the first `<h1>` of the stored translated HTML — so a Chinese page
ships a Chinese title. The description is deliberately left in the source language
there: Docsbook does not invent a translation for it.

## What is the meta description, and what is stripped out of it?

Order: frontmatter `description:` first, then the page's own opening paragraphs.

Before body text can become a description it is cleaned: HTML comments (which is what
widget markers are), `{icon-name}` markers, headings, images, fenced and inline code,
emphasis characters, raw HTML tags, list bullets and blockquote markers are removed,
and a markdown link collapses to its link text rather than dragging its URL into the
sentence. Paragraphs of 20 characters or fewer are dropped as fragments.

Two lengths are built from the same source in one pass: **160 characters** for
`<meta name="description">` and **400** for `og:description` and the JSON-LD
`description`. An authored frontmatter description fills both. Truncation lands on a
word boundary, and prefers the end of a sentence when one falls in the back half of
the budget; otherwise the text ends in an ellipsis.

## Which URL does the page call canonical?

One page, one canonical URL, resolved in this order:

1. **Your custom domain**, when the workspace has one. The `*.docsbook.io` mirror
   then serves `Disallow: /` rather than standing as a second copy.
2. **A product-owned apex path**, for Docsbook's own documentation.
3. **The apex short path** for showcase workspaces, because that is the URL that
   answers `200` — the subdomain form redirects to it.
4. **`https://<owner>.docsbook.io/<repo>/<path>`** for everything else.

Translated pages take the same four branches with the locale inserted where the
router actually serves it. `en` is special-cased back to the unprefixed URL, since
`/en/page` and `/page` serve byte-identical content, and a locale URL for a page that
is **not** actually translated renders the source text, so it canonicals to the
source URL instead of claiming to be authoritative.

## Which languages are advertised as alternates?

The `hreflang` set contains `x-default` and `en` at the source URL, plus one entry
per enabled language **that this page has actually been translated into**. Enabling a
language does not add it: an untranslated locale URL canonicals away from itself, and
one such member is enough to void the whole cluster. A page carrying `noindex` gets
no set at all, rather than a dangling one.

The sitemap emits **no** page-level alternates, on purpose: it cannot afford the
per-page translation check, so any set it built would list every enabled locale and
reintroduce exactly the contradiction the page-level set exists to avoid.

## What do the social cards contain?

Every page emits OpenGraph (`og:title`, `og:description` at the 400-character length,
`og:url` = the canonical URL, `og:site_name`, `og:type: article`, `og:locale`) and an
X card of type `summary_large_image` carrying the 160-character description. The
image is generated per page at **1200×630**, cached for 24 hours, and renders the
workspace lockup, the section as an eyebrow, the page title (cut at 64 characters,
set smaller above 30) and the description cut at 130, in the workspace's colours. On a
custom domain the card is the same image, requested by absolute URL from the apex — but
`og:description` there carries the 160-character string, not the 400-character one.

## What robots directives does a page carry?

Four rules, in strict precedence:

| Condition | Emitted |
|---|---|
| Admin preview (`?preview=true`) | `noindex, follow` |
| Site-wide SEO switch off | `noindex, nofollow` |
| Page frontmatter `noindex` | `noindex, follow` |
| Otherwise | `index, follow` |

`noindex: true`, `noindex: yes`, `noindex: 1` and the `robots: noindex` spelling all
count. Anything else — absent, `false`, `index` — means index.

`robots.txt` differs by host. The apex serves a permissive wildcard rule with
`Crawl-delay: 10`, disallows the app's own non-content paths, names **eighteen** AI
and search crawlers explicitly at `Crawl-delay: 5`, blocks **thirteen** high-volume
low-citation-value crawlers outright, and lists one `Sitemap:` line per discoverable site. A
workspace subdomain serves the same bot policy plus its own `Sitemap:` line. A custom
domain serves the bot policy with **no** `Sitemap:` line — it has no sitemap of its
own yet, and pointing crawlers at the mirror's sitemap would advertise a second host
for every page. Crawl-delay is a courtesy, not a standard: [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html)
defines only `user-agent`, `allow` and `disallow`, and
[Google](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt)
adds `sitemap` and nothing else — "other fields such as `crawl-delay` aren't supported".

## What goes into sitemap.xml?

One sitemap per owner, rebuilt at most hourly. For each indexed repository it lists
every Markdown file, mapping a repository-root `README` to the site root and every
other file to its own path. Each entry carries:

- **`lastmod`** — the date of the last commit that touched that file, from the
  source repository. Render time is used only when the commit history cannot be read.
- **`changefreq`** — `weekly`.
- **`priority`** — `0.9` for a landing page, `0.7` for an inner page, and `0.8` /
  `0.6` for their translations.

Translated URLs are listed **only** where a translation genuinely exists, and
duplicate URLs are collapsed before the file is emitted. A repository whose tree
cannot be read is dropped silently and the rest of the sitemap is still served: a
sitemap that 500s costs more than one that is a site short.

Pages carrying `noindex` **are** still listed. Recognising the flag means reading
every page's content, which building the sitemap deliberately does not do; the page's
own directive is honoured on arrival, so the cost is one crawl visit.

## What structured data is emitted?

On a Docsbook-hosted host, every page emits a JSON-LD `@graph` with three nodes:

- **`Organization`** — the workspace, its URL, its GitHub profile, its logo if set.
- **`TechArticle`** — headline, description, canonical URL, `inLanguage`,
  `datePublished` and `dateModified` from the source repository's commit history,
  author, publisher, `mainEntityOfPage`.
- **`BreadcrumbList`** — owner → site → each path segment, built from the same
  canonical builder the `<link rel="canonical">` uses, so no crumb can name a host
  the canonical tag disagrees with.

With [AEO](../aeo/README.md) on, `speakable` is added, and `FAQPage` / `HowTo` nodes
appear only when the page genuinely contains that shape. With
[GEO](../geo/README.md) on, a `Person` author is added from frontmatter or from the
last commit's author.

## Anchors, render mode and hosts

**Anchors.** Heading ids come from the renderer's own slugger, and every deep link
Docsbook hands out — search results, AI citations — is computed by calling that same
library rather than re-deriving the string. Duplicate headings resolve to the first
occurrence.

**Render mode.** An anonymous request for a public page is served from a cached
server-rendered route (24-hour window); signed-in and preview requests fall through
to a dynamic render and are never CDN-cached. Either way the crawler receives
complete HTML — no client-side render step stands between a bot and your text.

**Custom domain versus the shared domain.** On a custom domain the canonical URL,
title, description, cards and a `TechArticle` node are all present, and the bot
policy is enforced. Five things are not: the site-wide SEO switch and per-page `noindex`
(pages are served `index, follow` unconditionally), the `hreflang` set, the
`BreadcrumbList` and `Organization` nodes, moved-page redirects, and the
[GEO](../geo/README.md) signals — no TL;DR block, no visible Updated line, and a
`TechArticle` author that is always a `Person` named after the repository owner. See
[Limits](#limits-and-open-questions).

## Why these rules (evidence)

| Rule | Why it works on the consumer | Source |
|---|---|---|
| A `<title>` on every page, brand appended once | Google lists `<title>` first among title-link sources, and warns against "repeated or boilerplate text in `<title>` elements" | [Title links](https://developers.google.com/search/docs/appearance/title-link) |
| Per-page descriptions, never one site-wide string | "Identical or similar descriptions on every page of a site aren't helpful" | [Snippets](https://developers.google.com/search/docs/appearance/snippet) |
| Canonical points at a URL that answers 200, never a redirect | `rel="canonical"` is "a strong signal", and Google recommends a self-referential canonical on the canonical page | [Consolidate duplicate URLs](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) |
| Only genuinely translated locales in `hreflang` | "If page X links to page Y, page Y must link back to page X… those annotations may be ignored" | [Localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions) |
| Real commit dates as `lastmod` | Google uses `<lastmod>` "if it's consistently and verifiably… accurate" | [Build a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) |
| Structured data only for content the page has | "don't add structured data about information that is not visible to the user" | [Intro to structured data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) |
| Server-rendered HTML rather than client-side | Google renders JS in a queue where a page "may stay… for a few seconds, but it can take longer", and "not all bots can run JavaScript" | [JavaScript SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics) |
| 1200×630 card image | "Use images that are at least 1200 x 630 pixels", close to a 1.91:1 ratio | [Sharing images](https://developers.facebook.com/docs/sharing/webmasters/images/) |

## Limits and open questions

- **`priority` and `changefreq` are decoration.** Docsbook emits them, and Google
  states plainly: "Google ignores `<priority>` and `<changefreq>` values." The
  sitemaps.org protocol adds that priority "is not likely to influence the position
  of your URLs". They cost nothing and buy nothing from Google; other engines vary.
- **`TechArticle` is not on Google's Article rich-result list.** It is a real
  schema.org type (`Thing > CreativeWork > Article > TechArticle`) and describes the
  content honestly, but Google's Article documentation says objects "must be based on
  one of the following schema.org types: `Article`, `NewsArticle`, `BlogPosting`".
  Treat the node as accurate description, not rich-result eligibility. Nor is
  structured data documented as a ranking factor: Google's introduction describes it
  as making a page *eligible* for enhanced appearance and says nothing about rank.
- **Under question: what the 400-character `og:description` buys.** Docsbook builds
  it because the tag has room where `<meta description>` does not. No source we
  fetched documents how any specific consumer truncates `og:description`, and the
  OpenGraph protocol specifies no length. Treat 400 as a house choice, not a measured
  optimum.
- **Custom-domain pages ignore your indexing switches.** The site-wide SEO switch and
  per-page `noindex` are honoured only on Docsbook-hosted hosts; on a custom domain
  the page is served `index, follow` regardless. `/sitemap.xml` does not resolve
  there either, so its `robots.txt` carries no `Sitemap:` line, and a page renamed
  through Docsbook keeps its redirect only on the shared domain. To keep a page out
  of the index on a custom domain today, keep it out of the published repository.
- **A single sitemap caps at 50,000 URLs / 50 MB** per the sitemaps.org protocol and
  Google's own limit. Docsbook emits one sitemap per owner and does not shard; an
  owner past that ceiling is not handled today.

## Related

- [SEO — what Docsbook does for search visibility](./README.md)
- [Indexing — how a change reaches Google](./indexing.md)
- [AEO — answer engines and rich results](../aeo/README.md)
- [GEO — being cited by AI assistants](../geo/README.md)
- [AI translations](../translation/ai-translations.md)
