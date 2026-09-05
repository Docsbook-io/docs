---
title: "What changed in Docsbook SEO and GEO, and in which release"
description: "Every release that touched SEO and GEO: how your pages rank in search engines, and how answer engines such as ChatGPT and Perplexity come to cite them."
---

# What changed in Docsbook SEO and GEO, and in which release

Everything that shipped in **SEO & GEO**. This is the SEO & GEO slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 05.09.2026

### Added

- A **Mentions in AI** card beside Sources answers whether Google's AI Overview and AI Mode actually name your docs for the questions you care about: save up to five queries and a daily check reports, per query, whether you were mentioned and whether you were cited. Search Console tells you where you rank, and this tells you whether the answer above the ranking is yours. `AEO`

## NEW - 03.09.2026

### Fixed

- Showcase demos served on the apex path (`docsbook.io/[demo]`) now answer `llms.txt` and `llms-full.txt`, named after the demo rather than the account, and their translated pages open at `docsbook.io/[demo]/[lang]/…` with a canonical that points at itself, so an AI assistant can read and cite every public demo and search engines index its translations instead of following 112 sitemap entries into a noindex 404. `SEO`
- A documentation page's own `title` and `description` now reach the HTML head. Both were being ignored: the `<title>` was built from the body's H1 and the meta description from the first paragraph of the page, which on an index page shipped the widget's `{compass}` icon markers into the Google result. The brand was appended twice on top of that (`— Docsbook | Docsbook`), spending 22 of the title's characters on a repeat, and the JSON-LD `headline` named the page a third way, from the filename. Every page's search result and AI-assistant citation now says what the author wrote, on the apex domain and on custom domains alike. `SEO`

## NEW - 30.08.2026

### Added

- The `SEO`, `GEO` and `AEO` cards each gained the same pair, and Analyze reads your live pages rather than the switch: a setting that is on while the markup never renders is exactly what a green Active pill cannot tell you. `SEO`

### Changed

- The button on `Search rankings` no longer switches SEO, GEO and AEO on for you. It walks you to them instead: the panel moves to `Settings` ▸ `SEO & GEO`, lights each of the three in turn and says what it does and who it is for — search engines, AI answer engines, or featured snippets and voice — and the last step brings you back to `Search rankings`. Each switch stays live under the light, so you can turn one on where you are standing or just press Next. `SEO`
- Nothing is switched on unless you switch it. If you turned one on along the way, the walkthrough ends pointing at **Load your Google positions**; if you turned none on, it says so and how to go back, rather than promising data that is not coming. `SEO`

### Fixed

- Custom-domain workspaces are no longer crawled twice. The same pages were reachable through the `docsbook.io` mirror as well as your own domain, so search engines indexed both and split the ranking between them; the mirror now points at your domain as the original. `SEO`

## NEW - 28.08.2026

### Fixed

- Each documentation page in your sitemap is now dated by its own last change instead of the moment the sitemap was requested, so search engines can tell what actually moved. `SEO`

## NEW - 26.08.2026

### Fixed

- Russian-language pages now emit the FAQ and how-to markup that makes them eligible for rich results and AI answers, and a procedure written as a `stepper` widget is picked up as steps. Widget markers no longer leak into that markup. `SEO`

## NEW - 22.08.2026

### Added

- `Search rankings` now opens with a one-click activation prompt when SEO, GEO and AEO are all off — showing what your rankings will look like and turning any of them on, free on every plan, instead of an empty tab. `SEO`

## NEW - 21.08.2026

### Added

- Keep a single page out of search with `noindex: true` in its frontmatter. Until now the only control was the site-wide `SEO` toggle, so a changelog or a page of internal notes could not be hidden without hiding everything. `SEO`

### Fixed

- Your sitemap now lists a language's URL only for pages actually translated into it. Enabling a language does not translate anything, so those URLs served your original text and asked search engines to crawl a page that points back to the original. `SEO`
- Translated pages of a site with several languages are now grouped correctly for search engines. One URL in the group that served untranslated content was enough for the whole group to be discarded, including the languages that were translated. `SEO`

### Changed

- The documented behaviour on renaming a page has been corrected: Docsbook does not create a redirect from the old URL. `SEO`

## NEW - 10.08.2026

### Fixed

- Showcase sites had a canonical URL that pointed in a loop and no sitemap of their own. `SEO`

## NEW - 07.08.2026

### Added

- `Search rankings` leads with four figures — impressions, clicks, average position and the queries you rank for — each with its own trend, and every query row carries the action to take on it. `SEO`

### Fixed

- Long URLs in `Search rankings` are shortened to fit the card instead of pushing the table sideways. `SEO`

## NEW - 01.08.2026

### Fixed

- The sitemap now lists each marketing page's real publication date instead of the time it was last crawled, so Google can trust which pages actually changed. `SEO`

## NEW - 31.07.2026

### Fixed

- The auto-generated TL;DR block now replaces the opening paragraph it was taken from, instead of repeating the same sentence directly below itself. `GEO`

## NEW - 29.07.2026

### Fixed

- The Search rankings card in a preview no longer claims Search Console is not connected. `SEO`

## NEW - 28.07.2026

### Added

- The SEO/GEO tab now shows your real Google Search Console positions, including which queries are worth improving, with no OAuth or domain verification needed on a `*.docsbook.io` subdomain. `SEO`
- Search rankings gained a Search Health Score, period-over-period comparison, rising and falling queries, and pages Google shows but nobody clicks. `SEO`

### Fixed

- Search rankings now report your full search volume instead of only the fraction Google exposes per query, and time windows are anchored to the date Google's data actually covers. `SEO`

## NEW - 24.07.2026

### Changed

- `/llms.txt` and the shared preview image now describe Docsbook's current positioning instead of an outdated tagline. `SEO`

### Fixed

- `/llms-full.txt` no longer silently serves a "Failed to generate" stub when the docs source is unavailable — it now falls back to the same content as `/llms.txt`. `SEO`

## NEW - 18.07.2026

### Changed

- SEO, GEO, and AEO optimization now apply to docs on every plan, no longer Pro-only. `SEO`

## NEW - 17.07.2026

### Improved

- Doc page titles are now derived from the page's own H1 heading instead of its filename. `SEO`
- Sitemap no longer collapses nested `README` pages onto the repo-root URL. `SEO`

### Fixed

- Internal links that pointed at a blocked documentation path now resolve to the canonical `/docs/*` URL. `SEO`
- A doc URL with different letter casing than the source file now redirects to the canonical URL instead of 404ing. `SEO`
- Decorative background animation on the homepage no longer leaves placeholder text in the page source. `SEO`

## NEW - 14.07.2026

### Fixed

- Workspace subdomain `sitemap.xml` crashing instead of listing pages. `SEO`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [SEO](../content/features/seo.md) — how your pages rank in search engines
- [GEO](../content/features/geo.md) — how answer engines come to cite you
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
