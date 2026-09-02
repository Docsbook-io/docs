---
title: "New markets changelog"
description: "Everything Docsbook shipped that opens an audience the docs did not serve before — translations, languages, locales and market expansion."
---

# New markets changelog

Everything Docsbook shipped that moves one number: **New markets** — audiences the docs did not previously serve. On this axis, up is better.

The readers who bounced because the docs were not in their language. This is the New markets slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`

### Changed

- Admin settings now open as a page everywhere on a documentation site — the settings gear, the account menu's settings rows and the language picker's "Activate languages" all navigate to the dashboard instead of throwing a full-height panel over the docs. An anonymous draft keeps its own page, so its unsaved work survives the trip. `Changes`
- The admin panel's sidebar now groups Overview, Analytics, Users, Translations and Chat above a plain rule, Changes and Issues above a second one, and the rest below — three bands instead of one flat list, with no heading spelling out what already reads by position. `Panel`

## NEW - 30.08.2026

### Added

- `Analytics` gained a **Spend** figure right of Revenue: what this project's AI actually cost over the period on screen — reader chat, your own chat, translations, embeddings and MCP calls — with a chart of when it was spent and the billed calls behind each point. It needs no setup, it keeps working in a period nobody visited (an overnight translation run is a real bill with no reader behind it), and its arrow stays grey because spend has no good direction. `Analytics`
- Every new project now starts with **$1** of real credit, and a few minutes in a card offers **$5 more** to claim — yours to spend on AI chat, translations, MCP calls or an agent run, with nothing to pay until it runs out. It appears in the sidebar and as a strip across the top of `Billing`, and claiming it is one button. `Billing`
- Every panel readout now has a guide of its own — `Conversations`, `Dialogs`, `Goals & funnels`, `Users`, `Live`, `Changes`, `Search rankings`, `Feeds`, the translation reports and the MCP cards included — instead of a three-line summary derived from its upgrade copy. `Dashboard`
- Every finding carries the call that would fix it, so an audit hands straight over to `run_docs_create`, `run_docs_manage` or `run_docs_automate` without anyone translating it in between. All nineteen change nothing themselves and work with a read-only token. `MCP`
- `Feeds` gained a **Usage** button that swaps the live stream for the sum: what this project's money went on over a window, dearest first, as three tables — every AI answer, translation and indexing run by model, every MCP tool call by tool, and every event by type. A price on one row at a time was never a column anybody could add up. `Feeds`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- **Settings ▸ Translations** gained a **Translation Model** of its own, on every plan. The estimate you see before a run is priced on the model you picked, so the quote and the charge describe the same model. `Translations`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`
- Every section of the panel that has its own release notes now carries a **Change Log** button in its header, beside `Dashboard` — `Changes`, `MCP`, `Prompts`, `Chat`, `SEO & GEO`, `Translations` and `Feeds` each open only what shipped in that section, instead of the whole product's history. `Dashboard`

### Changed

- A card with no data of yours yet now draws the report itself over sample figures, faded behind the line saying what would fill it and the **Fix it** button that asks the assistant why it has not. It used to be blank space, or a grey outline with nothing in it, under a sentence describing a thing you had never seen. This is every empty card, not only the ones still behind **Turn on**: the tabs in `Analytics`, the readers table, `Feeds`, `Changes`, `Search rankings`, the chat reports and the translation impact tiles. `Dashboard`
- Every tab in an `Analytics` card now says on hover what its list actually counts, so "Exit" reads as the page people leave from rather than one that failed, "Direct / None" as traffic with no referrer rather than missing data, and "Lang" as the reader's browser preference rather than the language your docs are written in. `Analytics`
- Three feeds joined the built-in roster: **Translations** (every language generated, outdated or still needed), **Language events** (which languages readers switch the docs into) and **Chat events** (questions the AI assistant was asked, where it came up empty, which answers got a thumbs-down). `Feeds`
- `Translations` now works the way `Analytics` does. Each of its two pages carries a **Turn on** over sample figures, and pressing it runs a guide that names what a tile counts, what it does not prove and the move it leads to: one for the overview, covering the tiles and the reader map, and one for a language's own page, covering its tiles, the commit ledger and the readers table. Until now the tab had none of this — the button existed everywhere else in the panel and had never been drawn here. `Translations`
- Saying yes on one language covers the rest, so a project publishing in twelve of them is not walked through the same page twelve times. `Translations`
- A translation report with nothing in it yet now draws itself over sample figures, faded, with one line saying what is missing and a **Fix it** under it — instead of a column of zeros, em dashes and a grey sentence. That is the tiles on both pages, the commit ledger and the readers table; an empty reader map says the same over sample traffic, with the same button in the middle of it. `Translations`
- The readers table on a language's page finally shows its **Fix it**. The button was already written into that table; this page had simply never given it anywhere to send the question. `Translations`

### Fixed

- The empty state on `Translations`' overview totals no longer blurs, matching the reader map's card a few hundred pixels below it on the same page: a dimmed sample with a floating card, not a blurred one. `Translations`
- Every other card that shows a sample behind its **Fix it** button — the docs assistant's tabs, `Goals & funnels`, and the rest sharing that same backdrop — no longer blurs it either, matching the `Translations` fix above. `Dashboard`

## NEW - 28.08.2026

### Added

- A **Getting started** checklist now sits at the bottom of the admin panel's sidebar, showing what your site still needs — its content, your branding, the AI chat, languages, your agent, your domain, and being findable. It ticks steps off as they are configured, collapses to a single row, and disappears once you are done. `Dashboard`
- The Overview now shows a **Reader map** of where this week's readers are, coloured by whether a translation reaches them, without leaving the front page. `Dashboard`
- A **Users** page in the admin panel lists every reader of your docs in one table: where they came from, what they read, which goals they reached and how long each one took them, and what that reader is worth. The same table now backs the User and Journey tabs of Goals, and each language's Translations page. `Analytics`
- Each language's Translations page now carries a **commit ledger**: the commits that changed your source docs, a verdict on how many of that commit's pages are behind in this language, the state of each page, and the patch for one page read live from GitHub when you open it. It is the one block on the page that names something to go fix. `Translations`
- That page now also shows what a language cost beside who it reached: spent, saved, reused from cache and converted readers, on the same tile row as the audience figures. Reader counts alone cannot say whether a language paid off. Every tile in both rows explains itself on a `?`. `Translations`
- Narrowing a feed to one reader now puts a card above it saying who that reader is: their country, device, system and browser, the language they actually read in, the page they keep coming back to, how long they have spent reading your docs in total, the goals they have reached, and what they are worth today as well as what they might still be. A stream of pageviews under a pseudonym could not answer "who is this". `Feeds`
- A language's Translations page now shows what its readers were worth as an **Earned** tile, priced from your Call To Action and Average Product Price, next to spend, savings and cache reuse. `Translations`
- The Translations overview now has a zoomable map of every reader below its figures — countries at first, then regions and cities, then the readers themselves as avatars. `Translations`

### Changed

- The Conversations table now shows one line per row, with a reader's country and device as icons beside their name and the site that referred them shown with its own favicon. Cost and Savings are their own columns, the topic column is labelled Topic, and a Time column shows how long the conversation ran and how long that reader has spent on your docs. `AI Chat`
- A reader's country and the language your pages were served in are now two columns instead of one, so a German reader who landed on the English original is visible rather than merged away. `Analytics`
- Your languages are now a tab strip at the top of the Translations page instead of a second sidebar column, on every screen size. They are views of one subject, not separate sections. `Translations`
- A language's sync state, coverage, source commit and any halt reason now live in a popover on the state chip, next to the switch and **Translate now** on one line. The 200px card that held them pushed "did this language pay off" below the fold. `Translations`
- The readers table on a language's page now opens on its widest column set — source, potential, visits, pages, read time, first seen — since by the time you reach it the aggregate questions are already answered. `Translations`
- "Saved" on the Translations pages is now priced at $5 per 1,000 characters instead of per word, so the figure reads correctly for languages like Chinese and Japanese that have no whitespace-delimited words to count. `Translations`
- Each commit in a language's commit ledger now also shows what translating it into that language cost and which AI model did the work, next to the author's GitHub avatar. Opening a page's patch now says whether you are looking at the source revision or the translation. `Translations`
- The Translations overview is now the same tile grid as a language's own page, aggregated across every language, in place of three figures and a country table. `Translations`
- A funnel step's tooltip now draws each top source with that site's own favicon and each top country with its flag, and groups referrers by site: one site linking in from four pages used to fill the list with four truncated copies of the same name and push a real source out of it. `Analytics`
- The live reader map now opens on the whole world instead of framing itself around whoever is online, so a single reader no longer opens the page as a close-up of one country and the scale no longer changes between visits. `Analytics`

### Removed

- A language's page no longer shows the capture bar, the trend chart, the per-country split or the most-read list. Each restated the first two tiles or asked a follow-up the Analytics pages answer with filters this page cannot offer, and together they buried the commit ledger. `Translations`
- A language's cost row no longer ends on a bare count of converted readers — see the **Earned** tile above. `Translations`

### Fixed

- Automatic translations run again. The scheduled job had been failing on every tick since 23.08 and translating nothing. `Translations`

## NEW - 26.08.2026

### Fixed

- Russian-language pages now emit the FAQ and how-to markup that makes them eligible for rich results and AI answers, and a procedure written as a `stepper` widget is picked up as steps. Widget markers no longer leak into that markup. `SEO`

## NEW - 25.08.2026

### Changed

- Live auto translations are now included on the Pro plan, not just Business. `Pricing`
- The Translations tab's text now reads at the app's normal size, with explanations that duplicated an existing tooltip removed. `Translations`

## NEW - 24.08.2026

### Fixed

- Cards that had nothing to show a signed-out visitor are now filled with sample data instead of an error or an empty state — goals and funnels, the commit list, chat conversations and their transcripts, repository folders, navigation and social links, and every language page. `Preview`
- A language page can now be opened on mobile, where the Translations tab previously offered no way to reach one. `Translations`

## NEW - 23.08.2026

### Added

- A `Lang` tab on the `Conversations` card in `Chat` shows which languages readers write in, each row with its flag, so a workspace serving several languages can see the split at a glance. `AI Chat`
- Every conversation in `Chat` — the dialog list, the sidebar, and the open conversation — now shows the flag of the language it was written in. `AI Chat`
- `Changes` now puts the cash figures up front: what re-translating the edited pages cost, what readers asking the chat cost either side of the commit, and total AI spend. `Changes`
- Every row of the analytics cards now carries revenue beside visitors, so you can see which pages, referrers, channels, countries, browsers and languages brought the readers who *bought* — not only the readers who came. One click switches all four cards between ranking by `Visitors` and by `Revenue`. `Analytics`
- Filtering by a row narrows the whole dashboard — the other cards and the six figures above the chart — so a country, device or referrer can be read end to end. Filters stack, and each is a chip you can remove. `Analytics`
- New breakdowns: `Entry` and `Exit` pages, traffic `Channels` (organic search, social, referral, AI assistant, direct), `Countries` and `Languages`. `Analytics`
- `Languages` rows carry a flag, and `Referrers` rows show the subdomain in grey so the list reads by domain. `Analytics`
- Your docs now follow your commits: on the `Auto` translation mode, a push that changes a page re-translates it in every enabled language without being asked, within your existing budget and provider limits. `Translations`
- Every language page opens on whether that language is keeping up — coverage split into current, fallen behind and never translated, when it was last written to, and which commit your docs stand at. `Translations`
- A translation in progress now says what started it: you, someone else on the dashboard, switching the language on, or a commit Docsbook followed. `Translations`
- A language's last dozen runs are shown as a strip coloured by how each one ended, so a single failed run reads differently from a language that has not finished cleanly in weeks. `Translations`
- Each language can be switched on and off from its own page, with the same cost confirmation you get in settings. `Translations`

## NEW - 22.08.2026

### Added

- Every commit in `Changes` now shows what it cost: AI spend for the week before and the week after in dollars and percent, the share readers' own questions account for, cost per visit, and what re-translating the edited pages cost — with the sections served free from cache priced out. `Changes`
- `Changes` now breaks each commit's visits down by country, reader language and device — every slice beside the same slice's move on the pages the commit did not touch, so growth that happened everywhere is not read as growth this edit caused. `Changes`
- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`
- Every language you translate into now has a page of its own under `Translations` — pick it from the sidebar to see how many readers arrive from that language's countries in the first place, how many of them actually read in it, where it landed and where it missed, what they read, and what the language has cost against a human translator. `Translation`
- A language you switch off keeps its page, so its stored pages and past readers stay readable next to the audience that is still arriving — which is what tells you whether to turn it back on. `Translation`
- The `Translations` tab has a reader map that plots every country your readers come from as its own flag, ringed in a colour saying whether a translation is actually reaching it — green where they read the docs in their language, amber where the translation exists and most still read the original, red where readers arrive and none of them do. It never counts your own language as a missing translation. `Translation`
- The reader map opens framed on the countries you have readers in, and you can drag it to pan and zoom in on a crowded region — the flags keep their size as you zoom, so neighbours spread apart instead of overlapping harder. `Translation`
- Every country in the `Countries` breakdown now carries the share of its readers who landed on a translated page, coloured by the same verdict as its marker; point at a row to read what the colour means and light that country on the map. `Translation`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`

### Changed

- The `Translations` tab is one page instead of three stacked cards: a single interval control now governs the impact figures, the reader map and both country breakdowns, which could previously each report a different period. `Translation`
- `Visitor Countries` and `Language Countries` are one card with `Countries` and `Languages` tabs, sitting beside the reader map instead of under it — the same Countries/Languages split used to appear twice on the tab, once as map tabs and once as two separate tables. `Translation`
- The reader map dropped its colour legend: the breakdown rows beside it carry the colours now, on figures that say what they measure. `Translation`

### Fixed

- The translation savings, visitor and conversion figures no longer render blurred on a paid plan. `Translation`
- Reader-language traffic is now measured against the language your docs are actually written in, so a workspace whose original is not English no longer counts its own pages as translated ones. `Translation`
- Hovering the reader map now opens the country you are pointing at. `Translation`
- Reader-map markers are now sized against the map's real width instead of always falling back to their smallest size. `Translation`
- `www.docsbook.io` now redirects to the apex domain instead of showing a 404. `Marketing`

## NEW - 21.08.2026

### Fixed

- A page you have translated now shows its title in that language. Translated pages could fall back to the original-language title, so the line a reader sees in a search result was in a different language from the page itself. `Translation`
- Your sitemap now lists a language's URL only for pages actually translated into it. Enabling a language does not translate anything, so those URLs served your original text and asked search engines to crawl a page that points back to the original. `SEO`
- Translated pages of a site with several languages are now grouped correctly for search engines. One URL in the group that served untranslated content was enough for the whole group to be discarded, including the languages that were translated. `SEO`

### Changed

- An empty chat with no project selected now opens with your projects to pick from, and the connectable repositories under them. It used to open with the setup checklist, whose every step configures one specific site, so it asked you to brand, translate and publish a project you had not chosen yet. `AI Chat`

## NEW - 14.08.2026

### Changed

- Opening the language switcher on your own site before any language is enabled now offers to activate them and takes you to the translation settings, instead of reporting that none are added. Readers of your published docs still see the plain notice. `Translations`

### Fixed

- Country flags in the translation language picker now render the same on every platform instead of depending on the operating system's emoji font. `Translations`
- Switching or resetting the sidebar language now lands on the right URL. `Docs`

## NEW - 08.08.2026

### Added

- Enabling a language now asks you to confirm, showing how many pages will be translated, the estimated cost and your remaining budget. When the run does not fit, it says what share of your docs the budget covers and offers the upgrade. `Translations`
- Each enabled language shows what its translation run is doing: a progress counter while it works, and a `Stopped` marker you can hover for the reason when a run ended early. `Translations`
- Long translation runs resume on their own until every page is done, and the pages a commit changed are translated first. `Translations`

### Fixed

- A translation run that is interrupted no longer blocks that language for hours. Stalled runs are detected and picked up automatically. `Translations`
- Re-translating a page you barely touched no longer pays to translate the parts that did not change. `Translations`
- Readers no longer see a banner claiming they are looking at the original when a translation is on screen. `Docs`
- The sidebar no longer shows translated labels on a page whose body is still in the original language. `Docs`
- Turning a language off explains that nothing is deleted and that turning it back on does not pay again for unchanged pages. `Translations`
- Search finds the right page for questions asked in ordinary language, instead of failing on filler words and word endings. `Search`

## NEW - 07.08.2026

### Added

- Per-source spend limits let you cap what one source may spend each cycle, so AI translations or the semantic index can never eat the whole budget. Each bar under `Spend by source` now shows your limit next to the plan's own. `Limits`

### Fixed

- Switching the doc language from inside a subfolder no longer leads to a 404 page. `Docs`

## NEW - 02.08.2026

### Fixed

- Asking a question on a docs site that has no AI chat connected now explains that in plain language instead of showing `HTTP 400`. `AI Chat`

## NEW - 01.08.2026

### Added

- Your AI agent can now read a public web page and get it back as clean Markdown, so it can check your docs against a competitor's pricing, your own marketing site, or a link that may have gone dead. `MCP`
- Signing up now starts by asking what you do — founder, developer, technical writer, marketing, support — so the product can speak to your job rather than treat everyone the same. `Onboarding`

### Fixed

- The sitemap now lists each marketing page's real publication date instead of the time it was last crawled, so Google can trust which pages actually changed. `SEO`

## NEW - 29.07.2026

### Improved

- Every paid feature in the plan comparison now carries a question-mark tooltip explaining what it buys your business, in plain language rather than capability names. `Billing`

### Fixed

- The guided tour no longer crashes on the Translations step. `Preview`
- Unlock cards now quote the real numbers instead of stale ones: your monthly AI budget in dollars rather than a query count, 15 supported languages rather than "50+", and the actual chat model and MCP tool counts. `Billing`

## NEW - 28.07.2026

### Added

- Filters are now a searchable multi-select dropdown per dimension, offered only where the current view supports them, and language is filterable for the first time. `Analytics`
- The language of your docs is now detected automatically, so there is no Auto-detect button to press. `Translation`
- Translation Activity is now a searchable table of your pages: each row shows whether a page changed in git and whether its translations followed, per language, with a retranslate button on the row. `Translation`
- Opening a page from that table shows every language's state side by side, your source text next to the translation, and lets you correct a translation by hand without it being overwritten by later automatic runs. `Translation`

### Changed

- Growth and Scale now include every Business capability — custom domain, white-label, webhooks, your own AI and translation keys, UTM analytics and API reference — which the higher-priced tiers were previously denied. `Pricing`

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
- Translation docs no longer claim that pushing to GitHub re-translates changed pages on its own — it does not, and the new Translation Activity panel is how you catch pages up. `Docs`

## NEW - 24.07.2026

### Added

- Two new pages for API-first SaaS teams and AI/LLM companies show how Docsbook fits their specific documentation needs. `Marketing`
- A case studies page, including a real look at how Docsbook documents itself, plus an ROI calculator that estimates support-ticket savings from self-serve docs and AI chat. `Marketing`

## NEW - 18.07.2026

### Added

- A live demo gallery on the homepage lets you page through real generated docs before signing up. `Marketing`

## NEW - 17.07.2026

### Added

- `GitBook` and `Mintlify` comparison pages with a feature-by-feature table and FAQ. `Marketing`

## NEW - 05.07.2026

### Added

- New `Business` plan — everything included in `Pro`, with higher AI chat, translation, and webhook limits. `Billing`

## 0.26.5 - 29.06.2026

### Improved

- Updated landing page feature names for clarity: "AI Agents", "Live Sync", "Auto Translations", "Auto Distribution". `Landing`

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

## 0.26.3 - 11.06.2026

### Fixed

- **Limits card:** "Usage by source" bars now show each category's share of *actual spend* instead of a tiny fraction of the full budget ceiling — so you can see at a glance where your tokens go (AI Chat readers vs. Admin vs. AI Translations) and what to optimize.

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/blog` and `/blog/:path*` returning 500 — now redirects to `docsbook.io/docs/blog` for marketer SEO entry-points

## 0.21.1 - 25.05.2026

### Added

- Short marketing alias `docs.docsbook.io` for the product documentation — opens the same content as `docsbook-io.docsbook.io/docs/*` without redirect (URL stays clean in the browser). New `DOCS_ALIAS_SUBDOMAINS` map in `src/proxy.ts` rewrites `docs.docsbook.io/{path}` → `/docsbook-io/docs/{path}`; `/api/*` is passed through untouched, original subdomain URLs keep working.

## 0.20.1 - 25.05.2026

### Changed

- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.19.0 - 25.05.2026

### Added

- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed

- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added

- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries

### Changed

- Reordered and trimmed the floating admin toolbar — now 5 quick-access buttons (Analytics, AI Chat, AI Translations, Design, SEO) instead of 6; removed setup-once entries (Custom Domain, MCP Server) and surfaced SEO, which was previously only reachable via the settings modal

## 0.17.3 - 23.05.2026

### Changed

- Reworked landing header navigation — replaced old category dropdowns (AI, Analytics, Branding, Widgets, Translation) with 3 direct links (`AI`, `MCP`, `Skills`) plus 2 curated dropdowns: `Documentation` (Quick Start, Basics, Creating Docs, Custom Domain, AI Translations, FAQ) and `Blog` (all 5 posts)

## 0.17.1 - 23.05.2026

### Fixed

- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint

## 0.17.0 - 23.05.2026

### Added

- 10 new MCP Example Questions in admin (copy brandbook from a URL, change logo, custom domain, translations, social links, AI key, analytics, reindex, read sections); moved the `authentication module` example to the bottom of the list

## 0.16.0 - 22.05.2026

### Changed

- New translation limits — `Free` 0/mo, `Pro` 50/mo, `Pro+` 500/mo (was 30/300/unlimited)

## 0.15.1 - 22.05.2026

### Added

- Concrete numbers in `SocialProof` tabs — `2,400+ workspaces`, `3× more signups`, `40% fewer tickets`, `15 languages`

## 0.15.0 - 22.05.2026

### Added

- Expanded `AI Translations` page in `docs` with sections on why Claude outperforms generic translation tools and how each language version is indexed separately for multilingual SEO

### Fixed

- Translation toggle now enabled for preview admins on pages without a workspace

## 0.11.0 - 16.05.2026

### Added

- Header navigation links now translate to the active language

### Improved

- Interface language auto-detected from workspace settings — no URL prefix needed
- Enabling multiple languages at once is now significantly faster
- A loading banner appears while fresh translations are being prepared in the background

### Fixed

- Sidebar labels translate instantly without requiring a page refresh
- Previous/Next navigation buttons now show translated page names

## 0.10.0 - 15.05.2026

### Added

- MCP server for AI-assisted workspace administration via natural language

### Improved

- Ask AI, Search, and Language header buttons now have a unified consistent style

### Fixed

- Subheader links navigate to correct translated pages when translations are active
- Globe icon size and color now consistent in language picker

## 0.8.2 - 13.05.2026

### Fixed

- Language code now inserts at the correct position in sidebar links

## 0.8.1 - 12.05.2026

### Improved

- Language switching now instant — translation happens in the background with a loading indicator

## 0.4.1 - 10.05.2026

### Improved

- Auto-detect button in Translation panel detects documentation language from README and updates language picker with native name and flag

## 0.4.0 - 10.05.2026

### Added

- Country flag icons in language switcher with native language names

## 0.2.3 - 09.05.2026

### Improved

- Translation tab layout — usage card moved above country stats

## 0.2.0 - 08.05.2026

### Added

- Per-plan monthly translation quotas with usage tracking and progress bar

## 0.1.1 - 07.05.2026

### Improved

- Sidebar Language and Theme toggle button padding and visual style

### Fixed

- Language switcher now visible to all visitors when enabled, even before languages are added

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
