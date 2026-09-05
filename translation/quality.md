---
title: "How good are Docsbook's translations, and what does Google do with them?"
description: "What Docsbook measures about translation quality, how to correct a translation, how hreflang and canonicals are built per page, and what machine translation still gets wrong in technical docs."
tldr: "Docsbook publishes no translation quality score. It measures coverage and freshness — how many pages exist per language and how many were translated from the current source — and builds a per-page hreflang cluster that lists only locales this page is genuinely translated into, because Google discards a cluster containing one member that contradicts its own canonical."
---

# Translation quality and SEO

This is the page where the claim gets checked. It covers what Docsbook actually measures about a translation, how you correct one, what search engines and AI assistants do with translated documentation, and — at the end — what machine translation still gets wrong in technical prose, with a source.

## What Docsbook measures, and what it does not

**Docsbook publishes no translation quality score.** There is no BLEU, COMET, TER or human-rating figure for your pages, and this documentation will not invent one. What the product measures instead is *coverage* and *freshness*: whether a page exists in a language, and whether it was made from the version of the source that is live right now.

That is a narrower claim than "our translations are good", and it is the one that can be checked.

### Coverage and freshness

Every stored translation keeps the **git blob SHA of the source file it was made from**. Coverage is computed by reading your repository tree at HEAD and comparing per path:

| State | Meaning | What it costs your reader |
|---|---|---|
| `current` | Translated from the file's SHA at HEAD | Nothing |
| `behind` | Translated from an older version of the page | The page tells them something your docs no longer say |
| `missing` | In the repository, never translated into this language | They fall back to the original language |
| `manual` | Hand-written or uploaded — freshness is the author's call | Nothing; never counted as behind |
| `orphaned` | Translated page whose source file no longer exists at HEAD | A page for content you deleted |

Coverage is `(current + manual) / total`. A language is **in sync** when `behind` and `missing` are both zero. When your repository cannot be read, coverage is `null` — never a confident zero — so a rate-limited GitHub read can never paint a healthy language red.

### Reading it

- **In the panel.** Each language has its own page: one coverage percentage over a bar split by the *kind* of gap, the commit your docs are currently at, a live progress bar naming who started the running pass, the last dozen runs coloured by how each ended, and — when a run stopped short — the reason in words. Below that, your commits newest first, each with a verdict on how its pages stand in this language, so "the pricing rewrite went out on Tuesday" is a thing you can check rather than a filename you have to work out.
- **Through MCP.** `get_translation_status` returns exactly this per language: `current` / `behind` / `missing` / `manual` / `orphaned`, the percentage, `in_sync`, whether a run is in flight and how far along, and what the last run did — including which agent run started it. The tool's own description tells a caller to read it *before* `run_translation_pass`, because a language already level with the source costs money to re-translate and changes nothing.
- **By webhook.** `translation.needed` fires when a page in an enabled language is about to be translated, `translation.completed` when one durably lands, and `translation.outdated` when a translation falls behind its source. `translation.completed` fires only when the page was actually persisted, so a listener re-indexing a CMS is never told about a translation that does not exist.

### The one figure that is a comparison, not a measurement

The **Savings** figure on the Translations dashboard prices what a human translator would have charged for the same characters, at a rate of **$5.00 per 1,000 characters**, minus what the AI translation actually cost you. Two things about it:

- It is priced **per character, not per word**, deliberately. A word count is a property of the target language — Chinese and Japanese have no whitespace-delimited words — so a per-word measure reads as near zero for exactly the languages it should measure.
- It is a **counterfactual, not an invoice**. Nobody was paid either amount. The rate is a fixed constant in Docsbook, not a quote you received. Read the figure as an order of magnitude.

## Can I correct a translation, and will the correction survive?

You can correct one, and the correction is protected from being overwritten by a later pass — that part is enforced in the database write itself. Whether readers are then served your corrected text is a separate question, and the honest answer is below.

**How to correct one.** Edit the translation in the Translations panel, or send it with `upload_translation`. Uploads arrive as **draft**; `list_pending_translations` shows the drafts and `approve_translation` publishes one. Editing a translation's content marks the row as a manual upload.

**Why it survives a pass.** Automatic passes write through a database upsert whose conflict clause only overwrites rows whose origin is `docsbook_ai`. A row marked as a manual upload is skipped by that write, and coverage counts it as `manual` — a state that is never "behind", because freshness of a page a person wrote is that person's call, not a hash comparison's. Replacing a live AI translation this way also returns `replaced_ai_translation: true` to the caller, so an agent can warn a human that it just swapped out something readers were already seeing.

> **Under question.** Docsbook's docs have said that once you upload a correction, "Docsbook serves your version from then on".
> **What is verifiable:** the corrected row is stored, is never overwritten by a later automatic pass (the upsert's conflict clause only writes over rows whose origin is `docsbook_ai`), and is counted as `manual` in coverage rather than as stale.
> **What is not:** that readers are served it. Read against the code as it stands, three things point the other way. The reader-facing page reads a translation from the hot cache and, on a miss, from stored rows filtered to `origin = 'docsbook_ai'`. The same filter decides whether a locale belongs in this page's `hreflang` cluster and whether its URL enters the sitemap. And the cache-invalidation path states outright that manual and external rows "never write SSR Redis page keys", so there is no cached copy for the first read to find either. A manually uploaded or hand-edited row matches none of that. We have published no measurement of a corrected page being served, and the mechanism as written does not predict one — so treat manual uploads as a way to *protect* a page from re-translation and to drive an external pipeline, not as a way to change what a reader sees. If a specific sentence is wrong for you today, the reliable fix is to change the source page and let the pass re-translate it.

This is exactly the kind of claim [our evidence rule](../evidence.md) requires us to mark rather than quietly delete.

## What search engines do with translated documentation

### Separate URLs per language, and a per-page `hreflang` cluster

Each language is its own URL path — never a subdomain, never a query parameter. On top of that, every documentation page emits an `hreflang` set as `<link rel="alternate">` alternates, plus `x-default` and `en` pointing at the original-language URL.

The rule that makes it work is **reciprocity**, and it is enforced per page rather than per site:

| Rule | Why | Where you can check it |
|---|---|---|
| A locale appears in this page's cluster only when **this page** is genuinely translated into it | An untranslated `/fr/…` URL renders the original and declares the original as its canonical. Listing it as an alternate publishes a cluster member that contradicts its own canonical, and the whole cluster — including the locales that *are* translated — is discarded | The `<head>` of any translated page |
| An untranslated locale URL canonicals **to the original-language page** | It is a near-duplicate of the original competing against it, not a separate page | Any `/fr/…` URL for a page French has not reached yet |
| `/en/…` canonicals to the unprefixed URL | English is served byte-identically at both; the pair collapses into one indexable page instead of two self-canonical duplicates | Any `/en/…` URL |
| A `noindex` page is dropped from the cluster **entirely**, not merely omitted from others | Search engines fetch every alternate to verify reciprocity — which is precisely the crawl budget a `noindex` page was pulled from the index to stop spending | A page with `noindex: true` in frontmatter |
| The sitemap emits **no** `hreflang` alternates at all | Sitemap-level and page-level `hreflang` are merged into one cluster and must agree. The sitemap cannot check per-page translation state affordably, so anything it emitted would list every enabled locale — reintroducing the exact member that voids the cluster | `sitemap.xml` |

Docsbook builds the canonical and the alternates from the same function that routes the URL, so the address it advertises is the one that answers with a 200 rather than one that redirects — a canonical pointing at a redirect is resolved by Google by dropping the page.

One more mechanism sits under the same rule. Google says plainly that it *"uses the visible content of your page to determine its language"* and *"We don't use any code-level language information such as lang attributes, or the URL"* — so a fully translated page that still ships an English `<title>` is sending its strongest on-page signal in the wrong language. Docsbook recovers the title from the translated HTML it already stored, by reading that page's own translated `<h1>`, with no extra model call. The meta description is deliberately left as the original in that case: inventing a translation for it is not something a metadata build may do, and a correct title over an original-language description beats both being wrong.

### Why each of those rules is the right one

| Rule | Why it works on the machine that consumes it | Source |
|---|---|---|
| Publish each language on its own URL and annotate the set with `hreflang` | Google's instruction is to "Use hreflang to tell Google about the variations of your content" | [Google Search Central: localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions) |
| Make every cluster reciprocal, and never list a locale this page is not translated into | "Each language version must list itself as well as all other language versions." Google lists the failure first among its common `hreflang` mistakes, under **Missing return links**: "If page X links to page Y, page Y must link back to page X. If this is not the case for all pages that use hreflang annotations, those annotations may be ignored or not interpreted correctly" | [Google Search Central: localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions) |
| Canonical an **untranslated** locale URL to the original page | Google's line is exact: "Localized versions of a page are only considered duplicates if the main content of the page remains untranslated." A `/fr/` URL serving the English body is that case, by definition | [Google Search Central: localized versions](https://developers.google.com/search/docs/specialty/international/localized-versions) |
| Keep a **translated** page self-canonical, never canonicalled to the original | Google's canonicalization guidance says to "make sure to specify a canonical page in the same language", and that `rel="canonical"` annotations carrying `hreflang` "are not used for canonicalization" | [Google Search Central: canonicalization](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) |
| Translate the **body**, not just navigation and footers | "Google uses the visible content of your page to determine its language." and "We don't use any code-level language information such as lang attributes, or the URL." A locale URL with an untranslated body is not a page in that language, whatever it declares | [Google Search Central: managing multi-regional sites](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites) |
| Put the locale in a path segment | Subdirectories are one of the three URL structures Google documents, alongside ccTLDs and subdomains. Its listed drawback is human: "Users might not recognize geotargeting from the URL alone" | [Google Search Central: managing multi-regional sites](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites) |
| Emit bare two-letter language codes | For `hreflang`, Google requires ISO 639-1 language codes with ISO 3166-1 Alpha 2 region codes, and rejects anything else: "other codes that aren't listed in those standards, such as es-419, aren't supported". BCP 47 agrees on shape — its own guidance is that a subtag "SHOULD only be used when it adds useful distinguishing information", which W3C restates as "the golden rule is to keep your language tag as short as possible" | [Google](https://developers.google.com/search/docs/specialty/international/localized-versions) · [RFC 5646 (BCP 47)](https://www.rfc-editor.org/rfc/rfc5646) · [W3C](https://www.w3.org/International/questions/qa-choosing-language-tags) |
| Never redirect a reader to a language automatically | "Avoid automatically redirecting users from one language version of a site" — "These redirections could prevent users (and search engines) from viewing all the versions" | [Google Search Central: managing multi-regional sites](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites) |

Note what the second-to-last row implies about valid tags: `es-419` is a perfectly legal BCP 47 tag — W3C uses it as a worked example — and Google explicitly does not accept it in `hreflang`. Valid language tag and valid `hreflang` value are not the same set.

### Is machine translation against Google's rules?

No — and the answer is more specific than either side of the usual argument, so it is worth getting exactly right.

**Translated pages are not duplicates.** Google states the boundary in one sentence: *"Localized versions of a page are only considered duplicates if the main content of the page remains untranslated."* A fully translated page is a distinct page. A locale URL that serves the original body is a duplicate — which is why Docsbook canonicals that case to the original instead of publishing it as an alternate. And on duplication in general, Google's long-standing position is that *"Duplicate content on a site is not grounds for action on that site unless it appears that the intent of the duplicate content is to be deceptive and manipulate search engine results"* ([Demystifying the duplicate content penalty](https://developers.google.com/search/blog/2008/09/demystifying-duplicate-content-penalty), 2008).

**The old "machine translation is spam" rule is gone.** Google's [spam policies](https://developers.google.com/search/docs/essentials/spam-policies) contain no machine-translation bullet at all — the strings "machine translation" and "automatically translated" do not appear on the page. What is there is *scaled content abuse*, defined as *"creating large amounts of unoriginal content that provides little to no value to users, **no matter how it's created**"*. The word *translating* survives only inside one example of scraping under that same policy: *"Scraping feeds, search results, or other content to generate many pages (including through automated transformations like synonymizing, translating, or other obfuscation techniques), where little value is provided to users"*. Google's changelog records the cleanup on 11 June 2025: *"Removed a section from our multilingual documentation about using robots.txt to block all automatically translated pages"*, *"To align with our spam policy update in March 2024"* ([Search Central documentation updates](https://developers.google.com/search/updates#spring-cleaning-in-our-multilingual-documentation)).

**The live position is quality-conditional, not method-conditional.** Asked directly whether auto-translation hurts ranking, Gary Illyes answered *"if the auto translation is of low quality, maybe"*, and advised sites to *"ensure that a human native in those languages reviews (and perhaps fixes) the translations"*. In the same session John Mueller noted there is *"no special markup that you can add to your pages"* to declare a translation machine-made, that the test is whether *"the pages are well-translated"*, that *"a good localization is much more than just a translation of words and sentences"*, and that low-quality output is a case where *"you could just include the noindex robots meta tag on them"* ([Google SEO Office Hours, June 2024](https://developers.google.com/search/help/office-hours/2024/june)).

The practical reading for a documentation team:

- What is penalised is **volume without value**, not the tool. Translating a hundred pages of documentation your readers actually need is not scaled content abuse; generating locale pages nobody asked for is.
- **Review is the variable Google names.** Docsbook gives you the surfaces — the per-language coverage page, `list_pending_translations` with `approve_translation`, and `external` mode for routing every page through your own pipeline before publication — and does not force you to use them. `auto` mode publishes as it goes. Choose knowingly.
- The cheapest useful review is not every page. It is the pages that carry your money: the quick start, anything pricing-adjacent, the top pages in your analytics for that language, and anything where a mistranslated instruction breaks a reader's setup. If a language reads badly and you are not going to fix it, `noindex` is a sanctioned answer.

### What AI assistants do with them

Nothing special, and that is the point. A generative engine retrieves the same static HTML a crawler reads. Opening a language creates pages *in that language* for an assistant to retrieve and quote when the question is asked in that language — which an original-language-only corpus cannot be. Docsbook additionally indexes the translated text for on-site full-text search under that language code, so a reader searching in German matches German pages rather than the English source. See [GEO](../geo/README.md) for what is added to the page itself.

## Limits — what machine translation still gets wrong in technical docs

Take this section as seriously as the rest of the page.

- **Terminology consistency is not managed, and this is the measured weak point of the whole field.** Docsbook has no glossary, no term base and no do-not-translate list you can supply. Consistency comes from three weaker sources: requests run at temperature 0, an unedited section is served verbatim from cache and so cannot drift, and navigation labels and title/description are translated as sets. Two different pages using the same term were translated independently and may disagree.

  How much that matters has been measured. Moslem et al. ("Domain Terminology Integration into Machine Translation: Leveraging Large Language Models", WMT 2023, [arXiv:2310.14451](https://arxiv.org/abs/2310.14451)) report that across DE-EN, EN-CS and ZH-EN blind sets *"the number of terms incorporated into the translations of the blind dataset increases from an average of 36.67% with the generic model to an average of 72.88% by the end of the process"* — *"successful utilisation of terms nearly doubles across the three language pairs"*. Read the metric precisely: it counts whether the required term was **used**, and the 72.88% is the end of a four-step pipeline built for the purpose, not a stronger model on its own.

  The [WMT25 terminology shared task](https://aclanthology.org/2025.wmt-1.30/) puts a number on the other side of the same coin. Its Track 1 data was produced by SAP from its online help portal (EN→DE/RU/ES, 500 test instances per language pair, 20 systems from 13 teams), and *"strong systems achieve very high terminology accuracy of above 97%"* — **only when the correct glossary is handed to the system at inference time**, which is precisely the input Docsbook does not have. The task also runs the same systems with a random dictionary and with none: its top system scores **99.1 with the proper glossary, 49.2 with a random one and 44.4 with none**. On longer text it reports that *"systems frequently fall short"* and that *"the document track remains a more challenging task"*. Read that as: terminology fidelity is engineered in, not inherited, and Docsbook has not engineered it in yet.

  The general framing is the same. The WMT24 general translation task ([Kocmi et al.](https://aclanthology.org/2024.wmt-1.1/)), which collected translations from *"8 different large language models (LLMs) and 4 online translation providers"* across 11 language pairs, is titled *"The LLM Era Is Here but MT Is Not Solved Yet"*. Its domains are news, literary, speech and social — not technical documentation — so cite it for "not solved", and cite the two above for anything about domain text. Its test suites do report weakness in terminology, but narrowly: the sentence is about one direction and one system, *"For English-Russian, Yandex is weaker in named entities and terminology"*, and it is not a finding about LLM translation in general.
- **Bare identifiers in prose are protected only by an instruction.** Code inside fences and backticks is removed from the request and restored byte-for-byte — that is mechanical. A parameter name written as ordinary prose with no backticks reaches the model, and stays in the source language only because the prompt says so. Marking identifiers up as code is the single highest-value thing you can do for your own translations. We looked for a published measurement of how often LLM translation mangles *code identifiers* specifically and did not find one; the nearest published evidence is the terminology work cited above. Treat the size of this risk as unmeasured rather than small.
- **Image `alt` text is not translated.** It is an HTML attribute, and the rule that protects `href` and `id` protects `alt` with it.
- **Docsbook has published no measurement of its own.** No accuracy figure, no error rate, no per-language ranking. If you need one for your corpus, the honest way to get it is to have a fluent reader review a sample of your own pages — and coverage tells you which pages are worth sampling.
- **The model can change under you.** The default translation model is a configuration constant, and the picker lets you change it. A page translated last month was translated by whatever was selected then; nothing re-translates a page because the model improved.
- **Regional variants are not modelled.** One `pt` for Brazil and Portugal, one `zh` for Simplified and Traditional. For products where that distinction sells, this is a real limitation rather than a rounding error.

## Related

- [AI translations](./ai-translations.md) — the pipeline itself: chunking, protection, failure handling
- [Translation settings](./settings.md) — enabling a language, the model, the mode, locale URLs
- [SEO](../seo/README.md) — canonicals, sitemap and structured data on every page
- [GEO](../geo/README.md) — what makes a page quotable by an assistant
- [How Docsbook proves what it claims](../evidence.md) — the rule this page is written to
