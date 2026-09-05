---
title: "Publish your documentation in another language and keep it current"
description: "What opening a language actually gets you: a separate indexable URL set, translated on-site search, and pages that follow your commits — and what it costs in effort and money."
tldr: "Switch a language on and Docsbook translates every page, publishes each language on its own URL path, and re-translates a page when the commit that changed it lands. Translating spends your project's AI balance; serving a translated page does not. Automatic translation is a paid capability."
---

# Translation

Docsbook publishes your documentation in fifteen language codes. You do not write, store or maintain translation files: you switch a language on, and Docsbook translates the pages straight from the Markdown already in your repository, publishes each language on its own URL path, and re-translates a page when a commit changes it.

Machine-translated documentation is usually a liability — mangled code identifiers, terminology that drifts between pages, translations that quietly rot when the source moves on, and locale URLs that damage your search presence instead of extending it. The rest of this section is about how Docsbook's pipeline handles each of those specifically, and where it still does not.

## What opening a language gets you

Three concrete things, all of which you can check yourself.

**A separate set of URLs that a query in that language can match at all.** Each language is a distinct URL path, rendered as static HTML, listed in your sitemap and given its own `hreflang` entry. An English-only page cannot match a Spanish query however well it ranks; a Spanish page can. Google's own guidance is that translated pages are how you become eligible for that audience — not a duplicate-content problem — and Docsbook builds the `hreflang` cluster per page rather than per site so the cluster it publishes is one Google will accept. The mechanism, and the way it fails when done carelessly, is on [Translation quality and SEO](./quality.md).

**On-site search that works in the reader's language.** When a page is translated, the translated text is indexed for full-text search under that language code, not just the English original. A reader searching in German matches German pages.

**Documentation an assistant can quote in that language.** The same static HTML that a crawler reads is what an AI assistant retrieves. Translation extends [GEO](../geo/README.md) coverage to the languages you open, because there is now a page in that language to cite.

## What it costs

**Effort.** Enabling a language is a checkbox and a confirmation dialog. There is no export step, no `.po` files, no keys, no vendor account. Correcting a specific sentence afterwards is an edit in the Translations panel or an `upload_translation` call — see [the correction flow](./quality.md#can-i-correct-a-translation-and-will-the-correction-survive).

**Money.** Translating spends your project's AI balance; serving an already-translated page to a reader spends nothing. A page is split into sections keyed by content hash, so editing one paragraph re-translates that section and reuses the rest from cache. Docsbook quotes the run before you confirm it, and stops rather than overspending when the balance runs out. Automatic translation and the translation workflow tools are part of the paid plan — see [Pricing](https://docsbook.io/pricing).

**Attention.** This is the cost most teams underestimate. Machine translation of technical prose is good enough to publish and not good enough to ignore: terminology drift and over-translated domain terms are the documented failure modes, and Google's spam policies treat unreviewed machine translation as a risk to your site, not a neutral act. [Translation quality and SEO](./quality.md) states what Docsbook measures, what it does not, and what you should review.

## In this section

<!-- widget:cards -->

- [AI translations](./ai-translations.md) — what triggers a pass, how a page is chunked, exactly what is protected from the model, and what happens when a run fails halfway
- [Translation settings](./settings.md) — enabling languages, the source language, the language switcher, and the URL shape of every locale
- [Translation quality and SEO](./quality.md) — coverage and freshness metrics, correcting a translation, `hreflang` and canonical handling, and the honest limits

<!-- /widget -->

## Limits and open questions

- **Fifteen language codes, and only these.** `en`, `es`, `fr`, `de`, `pt`, `it`, `ru`, `zh`, `ja`, `ko`, `ar`, `hi`, `tr`, `pl`, `nl`. One of them is your project's own source language, which is never a translation target — so an English-language project has fourteen targets. Regional variants (`pt-BR` against `pt-PT`, `zh-Hans` against `zh-Hant`) are not separate options.
- **Docsbook publishes no translation quality score.** There is no BLEU, COMET or human-rating figure for your pages, and this documentation does not claim one. What the product measures is coverage and freshness — how many pages exist in each language and how many were translated from the current version of the source. Treat "the translation is good" as your judgement to make, on the evidence in [Translation quality and SEO](./quality.md).
- **Automatic translation is a paid capability, and so is the language configuration around it.** A free project sees the settings and gets its source language auto-detected when it connects, but cannot change the enabled languages or the source language, cannot set the translation mode, and cannot run a pass. See [Pricing](https://docsbook.io/pricing).
- **The pipeline translates Markdown pages from your repository.** It is not a UI-string localisation system, and it does not translate an OpenAPI specification's field descriptions.

## Related

- [SEO](../seo/README.md) — what Docsbook emits for search engines on every page, translated or not
- [GEO](../geo/README.md) — being quoted by an AI assistant rather than ranked
- [Visitor countries report](../analytics/reports/countries.md) — which regions arrive that you do not translate for yet
- [Content & Setup](../content/README.md) — how pages get into Docsbook in the first place
