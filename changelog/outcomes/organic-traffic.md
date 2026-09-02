---
title: "Organic traffic changelog"
description: "Everything Docsbook shipped that brings more readers in from search — rankings, keywords, sitemaps, metadata and indexation."
---

# Organic traffic changelog

Everything Docsbook shipped that moves one number: **Organic traffic** — more readers arriving from search. On this axis, up is better.

Pages that already rank 5–20 are the cheapest traffic you will ever buy. This is the Organic traffic slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`
- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`

### Changed

- The 44 previous audit-shaped tools (`audit_seo`, `map_capabilities`, `diagnose_traffic_drop` and the rest) have been replaced rather than renamed. The tools reference lists what took over each one; the four `run_docs_*` background jobs, `audit_geo` and the five `collect_*` collectors are unchanged. `MCP`

## NEW - 01.09.2026

### Fixed

- The signed-out preview priced a chat conversation at $0.21-$0.41 while the Cost tile above it worked out to about a cent and a half. The rows are the figure an owner multiplies by their own traffic before deciding whether to switch the chat on, and they were eighteen times the truth. `AI Chat`

## NEW - 30.08.2026

### Added

- Five **collectors** in `MCP` hand back the evidence an audit is built on, without the opinion, at **$0.0040** a call against the audit's $0.25. `collect_page_text` fetches your live pages and reports what the wire actually serves — status, title, headings, and how many words survive with no JavaScript — beside the size of the source stored for the same path. `collect_corpus_map` maps every page with its size, depth and whether navigation reaches it. `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search` return what readers asked, how their visits ended, and what they typed into your search box. `MCP`
- That makes the cheap one the right one more often than it sounds. With no Search Console connected, `audit_seo` still charges a quarter of a dollar to score its ranking axes as unmeasured, while `collect_corpus_map` needs no search data, no traffic and no history and returns real rows on a site that went up this morning. `MCP`
- Every panel readout now has a guide of its own — `Conversations`, `Dialogs`, `Goals & funnels`, `Users`, `Live`, `Changes`, `Search rankings`, `Feeds`, the translation reports and the MCP cards included — instead of a three-line summary derived from its upgrade copy. `Dashboard`
- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Hovering a point on the traffic chart now offers **Analyze** beside the date, which accounts for that one hour or day: whether it is unusual at all against the days around it, and what a spike was actually made of, a crawler and a launch being identical in a visitor count. The chart is now reachable by keyboard as well, with the arrow keys walking between points. `Analytics`
- Each ranked query in `Search rankings` now offers both **Improve**, for how to climb, and **Analyze**, for what the person typing it actually wants and what happens to them after the click. `Search rankings`
- The `SEO`, `GEO` and `AEO` cards each gained the same pair, and Analyze reads your live pages rather than the switch: a setting that is on while the markup never renders is exactly what a green Active pill cannot tell you. `SEO`
- Each improvement the assistant recommends now carries what it is expected to gain: a range of extra search clicks, and beside it what that is worth per month. Both are computed from your own Search Console history and the value you have declared a visit to have, never written by the assistant, and hovering the row shows the arithmetic — impressions, clicks, the rate the page converts at today, and the rate pages at its position typically manage on your site. `AI Chat`
- Those figures say nothing they cannot support. A page already doing better than its position predicts shows how much traffic the change touches rather than a gain; a structure or settings recommendation carries no prediction at all, because neither changes how often a listing is clicked; and a page with too little search history shows an empty space rather than a zero. Every prediction is marked an estimate while the assumption behind it is reasoned rather than measured against what past changes actually did. `AI Chat`
- The two figures above those tables are kept apart on purpose. AI answers and MCP calls are **charged** — that money came off your balance — while events are **priced** so the traffic is not invisible and nothing is deducted for them, and every section says which it is. One total covering both would be a bill for money nobody took. `Feeds`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- `assess_content_roi` is the one that gives you permission to stop: which pages earn their upkeep, and which to merge, redirect or retire. It works out which low-traffic pages are protected by inbound links or assistant citations **first**, and never proposes retiring one of those — deleting a page something external points at spends a link profile that cannot be bought back. `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`
- Forty-two more worked examples in the `MCP` catalog, and ten existing prompts now call one of the new tools where it changes the answer — the unanswered-questions prompt now splits "the page is missing" from "the page exists and nothing can retrieve it", and the striking-distance prompt now says whether the page is simply the wrong shape for the query. `MCP`
- Every section of the panel that has its own release notes now carries a **Change Log** button in its header, beside `Dashboard` — `Changes`, `MCP`, `Prompts`, `Chat`, `SEO & GEO`, `Translations` and `Feeds` each open only what shipped in that section, instead of the whole product's history. `Dashboard`

### Changed

- A draft you generate without an account now opens on its own admin panel instead of on the documentation full screen. The site is pictured as it stands, with its pages listed, where the content came from, and every section for branding, layout, SEO and the assistant — the same room a published project gets, for a site that only lacks an address. `Dashboard`
- A card with no data of yours yet now draws the report itself over sample figures, faded behind the line saying what would fill it and the **Fix it** button that asks the assistant why it has not. It used to be blank space, or a grey outline with nothing in it, under a sentence describing a thing you had never seen. This is every empty card, not only the ones still behind **Turn on**: the tabs in `Analytics`, the readers table, `Feeds`, `Changes`, `Search rankings`, the chat reports and the translation impact tiles. `Dashboard`
- MCP traffic in `Feeds` is now filterable per tool as well as per price class, so one filter can mean the expensive half of a single tool's calls. The narrowing rides the export and saved lists too, so a downloaded file matches what was on screen. `Feeds`
- Every tab in an `Analytics` card now says on hover what its list actually counts, so "Exit" reads as the page people leave from rather than one that failed, "Direct / None" as traffic with no referrer rather than missing data, and "Lang" as the reader's browser preference rather than the language your docs are written in. `Analytics`
- A translation report with nothing in it yet now draws itself over sample figures, faded, with one line saying what is missing and a **Fix it** under it — instead of a column of zeros, em dashes and a grey sentence. That is the tiles on both pages, the commit ledger and the readers table; an empty reader map says the same over sample traffic, with the same button in the middle of it. `Translations`
- The button on `Search rankings` no longer switches SEO, GEO and AEO on for you. It walks you to them instead: the panel moves to `Settings` ▸ `SEO & GEO`, lights each of the three in turn and says what it does and who it is for — search engines, AI answer engines, or featured snippets and voice — and the last step brings you back to `Search rankings`. Each switch stays live under the light, so you can turn one on where you are standing or just press Next. `SEO`
- Nothing is switched on unless you switch it. If you turned one on along the way, the walkthrough ends pointing at **Load your Google positions**; if you turned none on, it says so and how to go back, rather than promising data that is not coming. `SEO`

### Fixed

- Custom-domain workspaces are no longer crawled twice. The same pages were reachable through the `docsbook.io` mirror as well as your own domain, so search engines indexed both and split the ranking between them; the mirror now points at your domain as the original. `SEO`
- The public skills catalog now spells names the way the rest of the product does — `SEO` and `GEO` rather than "Seo" and "Geo". `Skills`

## NEW - 29.08.2026

### Added

- The Entry and Exit hover cards now show which channels readers arrived from and left through, so a page's traffic can be read by source without leaving the breakdown. `Analytics`

## NEW - 28.08.2026

### Added

- Signing in now opens a **Dashboard** of every project you own, with its traffic for the last 7 days, a search box, and one click into its admin panel, its assistant, or the published site. `Dashboard`

### Fixed

- Opening a project's admin panel no longer adds a visit to that project's own traffic figures. `Analytics`
- Each documentation page in your sitemap is now dated by its own last change instead of the moment the sitemap was requested, so search engines can tell what actually moved. `SEO`

## NEW - 26.08.2026

### Fixed

- Russian-language pages now emit the FAQ and how-to markup that makes them eligible for rich results and AI answers, and a procedure written as a `stepper` widget is picked up as steps. Widget markers no longer leak into that markup. `SEO`

## NEW - 23.08.2026

### Added

- Every row of the analytics cards now carries revenue beside visitors, so you can see which pages, referrers, channels, countries, browsers and languages brought the readers who *bought* — not only the readers who came. One click switches all four cards between ranking by `Visitors` and by `Revenue`. `Analytics`
- New breakdowns: `Entry` and `Exit` pages, traffic `Channels` (organic search, social, referral, AI assistant, direct), `Countries` and `Languages`. `Analytics`
- A `Keyword` tab in `Sources` shows the Google queries you rank for, with position, impressions, clicks and click-through rate, from your connected Search Console. `Analytics`

### Changed

- `Read Time` is no longer a separate tab — it is a `Reading time` ranking on `Pages` and `Headings`, still on `Pro`. `Analytics`

## NEW - 22.08.2026

### Added

- A new `Changes` tab lists every commit that touched your docs, with the page traffic before and after each one — and an on-demand check of whether a specific edit actually beat the rest of the site. `Changes`
- `Changes` now reports what Google did with the pages a commit touched: average position, impressions, clicks and click-through rate against the rest of the site, a daily chart with the commit marked on it, and a per-URL rank table. `Changes`
- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`
- `Search rankings` now opens with a one-click activation prompt when SEO, GEO and AEO are all off — showing what your rankings will look like and turning any of them on, free on every plan, instead of an empty tab. `SEO`

### Fixed

- Reader-language traffic is now measured against the language your docs are actually written in, so a workspace whose original is not English no longer counts its own pages as translated ones. `Translation`

## NEW - 21.08.2026

### Added

- Keep a single page out of search with `noindex: true` in its frontmatter. Until now the only control was the site-wide `SEO` toggle, so a changelog or a page of internal notes could not be hidden without hiding everything. `SEO`

### Fixed

- Your sitemap now lists a language's URL only for pages actually translated into it. Enabling a language does not translate anything, so those URLs served your original text and asked search engines to crawl a page that points back to the original. `SEO`
- Translated pages of a site with several languages are now grouped correctly for search engines. One URL in the group that served untranslated content was enough for the whole group to be discarded, including the languages that were translated. `SEO`

### Changed

- The documented behaviour on renaming a page has been corrected: Docsbook does not create a redirect from the old URL. `SEO`

## NEW - 14.08.2026

### Changed

- Disabled `SEO`, `GEO` and `AEO` toggles now sort to the top of the SEO panel so you see what to turn on first; a toggle you just enabled stays put until you reopen the panel. `Settings`

## NEW - 10.08.2026

### Fixed

- Showcase sites had a canonical URL that pointed in a loop and no sitemap of their own. `SEO`

## NEW - 07.08.2026

### Added

- `Search rankings` leads with four figures — impressions, clicks, average position and the queries you rank for — each with its own trend, and every query row carries the action to take on it. `SEO`

### Fixed

- The semantic index now builds when you ask for it and keeps itself up to date as your docs change, instead of staying empty and leaving meaning-based answers falling back to keyword search. `AI Chat`
- Long URLs in `Search rankings` are shortened to fit the card instead of pushing the table sideways. `SEO`

## NEW - 03.08.2026

### Fixed

- Pricing pages across the docs (blog comparisons, MCP reference, AI features overview, quick-start, branding guide) no longer show AI chat, SEO/GEO/AEO, or the MCP server as paid-tier features — they are free on every plan, including Free. Custom domain and white-label are now correctly attributed to Business (not Pro), and the Source-of-Truth content graph to Business (not Pro). `Docs`

## NEW - 01.08.2026

### Fixed

- The sitemap now lists each marketing page's real publication date instead of the time it was last crawled, so Google can trust which pages actually changed. `SEO`
- Steps in the assistant's trail now name what they did and what they found, such as the traffic numbers they read, rather than repeating the name of the operation. `AI Chat`

## NEW - 29.07.2026

### Fixed

- The Search rankings card in a preview no longer claims Search Console is not connected. `SEO`

## NEW - 28.07.2026

### Added

- You can now see whether each visit actually succeeded — visits, outcomes, dead-end pages and exit pages are reconstructed from your existing events, with crawler traffic and inflated read time filtered out. `Analytics`
- The SEO/GEO tab now shows your real Google Search Console positions, including which queries are worth improving, with no OAuth or domain verification needed on a `*.docsbook.io` subdomain. `SEO`
- Search rankings gained a Search Health Score, period-over-period comparison, rising and falling queries, and pages Google shows but nobody clicks. `SEO`
- Business plans can now build a semantic index over their docs, so readers' chat questions find the right page by meaning even when it shares no keywords, plus a relationship graph of how pages connect. `AI Chat`

### Changed

- A draft generated before signing in now opens as a real documentation site — header, sidebar tree, outline, breadcrumbs and prev/next — so you can browse every generated page and tune branding, layout and SEO before deciding to publish. `Design`

### Fixed

- Visitors, page views, top pages, referrers and events now exclude crawler traffic, which was up to 93% of pageviews on some sites. AI Visits remains the one card that reports bot volume. `Analytics`
- Search rankings now report your full search volume instead of only the fraction Google exposes per query, and time windows are anchored to the date Google's data actually covers. `SEO`

## NEW - 24.07.2026

### Changed

- Landing page copy reworded to lead with outcomes (traffic loss, AI vs Google attribution) instead of pricing gimmicks or raw tech specs. `Landing`
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

## 0.23.0 - 03.06.2026

### Added

- **Analytics**: Exclude internal (founder/admin) traffic from Axiom with `INTERNAL_IPS` env allowlist — single source of truth in `src/utils/analytics/internal.ts` with consistent IP extraction across all six ingest points (`/api/axiom`, server pageview logger, `/api/vitals`, `/api/_axiom/web-vitals`, `/api/analytics/{cta,feedback}`)

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/blog` and `/blog/:path*` returning 500 — now redirects to `docsbook.io/docs/blog` for marketer SEO entry-points
- Fix SEO/GEO/AEO toggles showing "Active" in anonymous mode — toggle now rolls back and shows an inline error when unauthenticated

## 0.22.2 - 28.05.2026

### Changed

- Official documentation now served at `docsbook.io/docs` — middleware rewrites `/docs/*` internally instead of redirecting to `docsbook-io.docsbook.io`; canonical URLs, sitemap, JSON-LD, and all links updated across landing, admin, and MCP pages

## 0.21.0 - 25.05.2026

### Added

- SEO / GEO / AEO admin cards with real functionality — admin tab renamed from "SEO" to "SEO / GEO" (key `seo-geo`) and split into three toggleable cards, each with a `Learn more about …` footer link. GEO toggle injects a TL;DR `<aside class="tldr">` at the top of every page (from `tldr:` frontmatter or auto-extracted first paragraph), shows a visible `Updated DD MMM YYYY` `<time>` at the article end, and switches author in JSON-LD `TechArticle` to a full `Person` schema (frontmatter `author`/`authorUrl` or fallback to last git commit author). AEO toggle gates the existing `FAQPage` JSON-LD, auto-detects `HowTo` JSON-LD from `## How to …` / `## Как …` headings followed by numbered lists (`src/utils/seo/extractHowTo.ts`), and adds a `speakable` `SpeakableSpecification` to `TechArticle` for voice assistants. New MCP tools `update_geo` and `update_aeo` (PRO-gated) mirror `update_seo`. Markdown pipeline migrated from regex-strip to `gray-matter` for typed frontmatter (new `src/utils/markdown/parseFrontmatter.ts`); 4 call-sites refactored. New `docs/content/features/geo.md` and `aeo.md` document the behavior and authoring patterns; `seo.md` updated with cross-links. DB columns `workspaces.geo_enabled` and `aeo_enabled` (migration `0028_public_marvex.sql`)

## 0.20.2 - 25.05.2026

### Added

- UTM parameters on all internal CTAs leading from `/skills`, `/mcp`, `/docs` (Preview banner), and the blog to the landing page — every `/start` and `/connect` link now carries `utm_source` (`skills` / `mcp` / `preview` / `blog`), `utm_medium` (`nav` / `cta` / `banner`), and `utm_campaign` (e.g. `header_signup`, `mcp_start_free_top`, `preview_connect`, post slug for blog). New `src/utils/utm.ts` helper (`withUtm()`) wires the landing `Header`/`Footer` via an optional `utmSource` prop, the two inline CTAs on `/mcp`, and the `PreviewConnectBanner` on workspace pages. Blog post CTAs (`docusaurus_vs_docsbook`, `mintlify_vs_docsbook`, `gitbook_vs_docsbook`, `ai_search_documentation`, `documentation_seo_guide`, `how_to_host_docs_from_github`, `why_documentation_matters`) now tag their conversions per post. The landing page itself stays UTM-free so internal scroll-to-CTAs aren't mis-attributed

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.18.1 - 25.05.2026

### Changed

- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added

- Signup attribution tracking — capture UTM parameters and referrer on landing pages, persist as first-touch cookie (`ds_attr`, 90 days), and write `signup_source` / `signup_medium` / `signup_campaign` / `signup_referrer` / `signup_landing_path` to `users` on GitHub OAuth signup so we can measure which channel (Twitter, HN, Product Hunt, dev.to, blog, organic, AI assistants) actually converts
- New sitemap entries — `/mcp` and `/skills` with priority `0.9`, plus `/connect` with `0.5`, so Google can discover and weigh these promo pages
- FAQ reply notebook for community comments at `docs/blog/faq-replies.md` — 32 ready-to-paste answers (TL;DR + Long versions) across 8 sections (General, Pricing, Competitors, AI, SEO, Tech, Security, Objections) for Reddit, X, IndieHackers, and HackerNews distribution
- New blog tutorial `/blog/how-to-host-docs-from-github` — walks through three ways to turn a GitHub repo into a live docs site (GitHub Pages + Jekyll, Docusaurus, Docsbook) with step-by-step setup, tradeoffs, and a decision matrix; targets the "how to host documentation from github" high-intent SEO query
- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries
- Rewrote `/blog/docusaurus-vs-docsbook` into a full "Docusaurus Alternatives in 2026" guide (2.7k words) — TL;DR decision matrix, four reasons teams leave Docusaurus, 9 alternatives compared (Docsbook, Mintlify, GitBook, ReadMe, Archbee, VitePress, Nextra, Starlight, MkDocs Material) with pros/cons/pricing/migration, a "how to choose" section with three decision questions, a step-by-step migration guide, and a 7-question FAQ — targets the "docusaurus alternatives" SEO query instead of the narrower 1:1 comparison

### Changed

- Reordered and trimmed the floating admin toolbar — now 5 quick-access buttons (Analytics, AI Chat, AI Translations, Design, SEO) instead of 6; removed setup-once entries (Custom Domain, MCP Server) and surfaced SEO, which was previously only reachable via the settings modal

### Fixed

- AI Skills cards in the admin no longer 404 on workspace subdomains — clicking a card now opens an in-place modal with the full `SKILL.md` (description, install snippets for 7 AI clients, keywords, MCP tools, GitHub link) instead of routing to `/skills/<name>` which only exists on `docsbook.io`. Landing-page behavior is unchanged

## 0.17.4 - 23.05.2026

### Fixed

- Replaced broken `(#)` CTA links across 5 blog posts (`mintlify-vs-docsbook`, `docusaurus-vs-docsbook`, `why-documentation-matters`, `documentation-seo-guide`, `ai-search-documentation`) — all now point to `https://docsbook.io/start`

## 0.15.1 - 22.05.2026

### Added

- Animated growth counters in `CtaBand` — 4 stats (workspaces, pages indexed, countries, AI queries) count up over 6 seconds on scroll-into-view
- Before→After traffic animation in `BentoFeatures` analytics cell — visitors climb from 11 to 1,240 and page views from 34 to 8,900 in a 9-second loop

## 0.15.0 - 22.05.2026

### Added

- Blog section in `docs` with 5 SEO-optimized posts for distribution — competitor comparisons (Mintlify, Docusaurus), AI search, documentation SEO guide
- New `SEO Optimization` page in `docs` explaining automatic meta tags, JSON-LD, static pages, sitemap, canonical URLs, hreflang, and llms.txt — with compounding ROI timeline
- Expanded `AI Translations` page in `docs` with sections on why Claude outperforms generic translation tools and how each language version is indexed separately for multilingual SEO

## 0.11.1 - 17.05.2026

### Improved

- Documentation content and sidebar now render on the server for faster load and better SEO

## 0.2.3 - 09.05.2026

### Improved

- SEO Optimization upsell card now shows as a centered overlay with pricing details

## 0.2.0 - 08.05.2026

### Added

- SEO panel — control search engine indexing, canonical URLs, and structured data

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
