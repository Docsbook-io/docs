---
title: "What changed in Docsbook Translations, and in which release"
description: "Every release that touched Translations: automatic translation of your pages, the review and approval step, and how coverage is tracked per language."
---

# What changed in Docsbook Translations, and in which release

Everything that shipped in **Translations**. This is the Translations slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 04.09.2026

### Changed

- Translating a page now costs roughly a third of what it did. Translations run on GPT-5.6 Luna by default instead of GPT-4o mini, which is the same rewrite-this-prose job at $0.055/$0.22 per 1M tokens against $0.15/$0.60, so the same balance stretches over about three times as many pages and a language you were putting off is affordable now. Projects that had explicitly chosen a pricier model were moved with the default; the picker in **Settings ▸ Translations ▸ Translation Model** still offers every model, and the estimate shown before a run is priced on whichever one you pick. `Translations`

## NEW - 30.08.2026

### Added

- **Settings ▸ Translations** gained a **Translation Model** of its own, on every plan. The estimate you see before a run is priced on the model you picked, so the quote and the charge describe the same model. `Translations`

### Changed

- `Translations` now works the way `Analytics` does. Each of its two pages carries a **Turn on** over sample figures, and pressing it runs a guide that names what a tile counts, what it does not prove and the move it leads to: one for the overview, covering the tiles and the reader map, and one for a language's own page, covering its tiles, the commit ledger and the readers table. Until now the tab had none of this — the button existed everywhere else in the panel and had never been drawn here. `Translations`
- Saying yes on one language covers the rest, so a project publishing in twelve of them is not walked through the same page twelve times. `Translations`
- A translation report with nothing in it yet now draws itself over sample figures, faded, with one line saying what is missing and a **Fix it** under it — instead of a column of zeros, em dashes and a grey sentence. That is the tiles on both pages, the commit ledger and the readers table; an empty reader map says the same over sample traffic, with the same button in the middle of it. `Translations`
- The readers table on a language's page finally shows its **Fix it**. The button was already written into that table; this page had simply never given it anywhere to send the question. `Translations`

### Fixed

- The empty state on `Translations`' overview totals no longer blurs, matching the reader map's card a few hundred pixels below it on the same page: a dimmed sample with a floating card, not a blurred one. `Translations`

## NEW - 28.08.2026

### Added

- Each language's Translations page now carries a **commit ledger**: the commits that changed your source docs, a verdict on how many of that commit's pages are behind in this language, the state of each page, and the patch for one page read live from GitHub when you open it. It is the one block on the page that names something to go fix. `Translations`
- That page now also shows what a language cost beside who it reached: spent, saved, reused from cache and converted readers, on the same tile row as the audience figures. Reader counts alone cannot say whether a language paid off. Every tile in both rows explains itself on a `?`. `Translations`
- A language's Translations page now shows what its readers were worth as an **Earned** tile, priced from your Call To Action and Average Product Price, next to spend, savings and cache reuse. `Translations`
- The Translations overview now has a zoomable map of every reader below its figures — countries at first, then regions and cities, then the readers themselves as avatars. `Translations`

### Changed

- Your languages are now a tab strip at the top of the Translations page instead of a second sidebar column, on every screen size. They are views of one subject, not separate sections. `Translations`
- A language's sync state, coverage, source commit and any halt reason now live in a popover on the state chip, next to the switch and **Translate now** on one line. The 200px card that held them pushed "did this language pay off" below the fold. `Translations`
- The readers table on a language's page now opens on its widest column set — source, potential, visits, pages, read time, first seen — since by the time you reach it the aggregate questions are already answered. `Translations`
- "Saved" on the Translations pages is now priced at $5 per 1,000 characters instead of per word, so the figure reads correctly for languages like Chinese and Japanese that have no whitespace-delimited words to count. `Translations`
- Each commit in a language's commit ledger now also shows what translating it into that language cost and which AI model did the work, next to the author's GitHub avatar. Opening a page's patch now says whether you are looking at the source revision or the translation. `Translations`
- The Translations overview is now the same tile grid as a language's own page, aggregated across every language, in place of three figures and a country table. `Translations`

### Removed

- A language's page no longer shows the capture bar, the trend chart, the per-country split or the most-read list. Each restated the first two tiles or asked a follow-up the Analytics pages answer with filters this page cannot offer, and together they buried the commit ledger. `Translations`
- A language's cost row no longer ends on a bare count of converted readers — see the **Earned** tile above. `Translations`

### Fixed

- Automatic translations run again. The scheduled job had been failing on every tick since 23.08 and translating nothing. `Translations`

## NEW - 25.08.2026

### Changed

- The Translations tab's text now reads at the app's normal size, with explanations that duplicated an existing tooltip removed. `Translations`

## NEW - 24.08.2026

### Fixed

- A language page can now be opened on mobile, where the Translations tab previously offered no way to reach one. `Translations`

## NEW - 23.08.2026

### Added

- Your docs now follow your commits: on the `Auto` translation mode, a push that changes a page re-translates it in every enabled language without being asked, within your existing budget and provider limits. `Translations`
- Every language page opens on whether that language is keeping up — coverage split into current, fallen behind and never translated, when it was last written to, and which commit your docs stand at. `Translations`
- A translation in progress now says what started it: you, someone else on the dashboard, switching the language on, or a commit Docsbook followed. `Translations`
- A language's last dozen runs are shown as a strip coloured by how each one ended, so a single failed run reads differently from a language that has not finished cleanly in weeks. `Translations`
- Each language can be switched on and off from its own page, with the same cost confirmation you get in settings. `Translations`

## NEW - 22.08.2026

### Added

- Every language you translate into now has a page of its own under `Translations` — pick it from the sidebar to see how many readers arrive from that language's countries in the first place, how many of them actually read in it, where it landed and where it missed, what they read, and what the language has cost against a human translator. `Translation`
- A language you switch off keeps its page, so its stored pages and past readers stay readable next to the audience that is still arriving — which is what tells you whether to turn it back on. `Translation`
- The `Translations` tab has a reader map that plots every country your readers come from as its own flag, ringed in a colour saying whether a translation is actually reaching it — green where they read the docs in their language, amber where the translation exists and most still read the original, red where readers arrive and none of them do. It never counts your own language as a missing translation. `Translation`
- The reader map opens framed on the countries you have readers in, and you can drag it to pan and zoom in on a crowded region — the flags keep their size as you zoom, so neighbours spread apart instead of overlapping harder. `Translation`
- Every country in the `Countries` breakdown now carries the share of its readers who landed on a translated page, coloured by the same verdict as its marker; point at a row to read what the colour means and light that country on the map. `Translation`

### Changed

- The `Translations` tab is one page instead of three stacked cards: a single interval control now governs the impact figures, the reader map and both country breakdowns, which could previously each report a different period. `Translation`
- `Visitor Countries` and `Language Countries` are one card with `Countries` and `Languages` tabs, sitting beside the reader map instead of under it — the same Countries/Languages split used to appear twice on the tab, once as map tabs and once as two separate tables. `Translation`
- The reader map dropped its colour legend: the breakdown rows beside it carry the colours now, on figures that say what they measure. `Translation`

### Fixed

- The translation savings, visitor and conversion figures no longer render blurred on a paid plan. `Translation`
- Reader-language traffic is now measured against the language your docs are actually written in, so a workspace whose original is not English no longer counts its own pages as translated ones. `Translation`
- Hovering the reader map now opens the country you are pointing at. `Translation`
- Reader-map markers are now sized against the map's real width instead of always falling back to their smallest size. `Translation`

## NEW - 21.08.2026

### Fixed

- A page you have translated now shows its title in that language. Translated pages could fall back to the original-language title, so the line a reader sees in a search result was in a different language from the page itself. `Translation`

## NEW - 14.08.2026

### Changed

- Opening the language switcher on your own site before any language is enabled now offers to activate them and takes you to the translation settings, instead of reporting that none are added. Readers of your published docs still see the plain notice. `Translations`

### Fixed

- Country flags in the translation language picker now render the same on every platform instead of depending on the operating system's emoji font. `Translations`

## NEW - 08.08.2026

### Added

- Enabling a language now asks you to confirm, showing how many pages will be translated, the estimated cost and your remaining budget. When the run does not fit, it says what share of your docs the budget covers and offers the upgrade. `Translations`
- Each enabled language shows what its translation run is doing: a progress counter while it works, and a `Stopped` marker you can hover for the reason when a run ended early. `Translations`
- Long translation runs resume on their own until every page is done, and the pages a commit changed are translated first. `Translations`

### Fixed

- A translation run that is interrupted no longer blocks that language for hours. Stalled runs are detected and picked up automatically. `Translations`
- Re-translating a page you barely touched no longer pays to translate the parts that did not change. `Translations`
- Turning a language off explains that nothing is deleted and that turning it back on does not pay again for unchanged pages. `Translations`

## NEW - 28.07.2026

### Added

- The language of your docs is now detected automatically, so there is no Auto-detect button to press. `Translation`
- Translation Activity is now a searchable table of your pages: each row shows whether a page changed in git and whether its translations followed, per language, with a retranslate button on the row. `Translation`
- Opening a page from that table shows every language's state side by side, your source text next to the translation, and lets you correct a translation by hand without it being overwritten by later automatic runs. `Translation`

## NEW - 27.07.2026

### Added

- Translation activity and spend breakdown. `Translations`
- Re-translate a single page or a whole language on demand, straight from the Translation Activity panel. `Translations`
- Translation Activity now reports how many pages have fallen behind your source content, and how many point at files that were renamed or deleted. `Translations`
- Per-language coverage shows, for every page in your docs, how many are translated and current, how many are behind, and how many have no translation at all — so you can tell at a glance whether a language is genuinely complete. `Translations`
- Filling in a language translates only the missing and outdated pages; pages already up to date are skipped and cost nothing. `Translations`
- Live progress while a translation run is going, including why a run stopped early when it hits your budget or the provider's quota. `Translations`
- Translation spend is now shown next to how many page sections were reused from cache instead of re-translated. `Translations`
- Correct a machine translation by editing its text directly, instead of re-uploading the whole page. `Translations`

### Fixed

- Translation freshness is now measured against your actual source content. The previous check never flagged anything, so sites could serve translations of long-changed pages while reporting everything as current. `Translations`
- The per-language "Last update" time was off by your timezone offset, making fresh translations look hours old. `Translations`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [Translations](../translation/README.md) — how a page becomes fifteen
- [AI translations](../translation/ai-translations.md) — what gets translated, and when
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
