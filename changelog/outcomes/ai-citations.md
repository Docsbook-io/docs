---
title: "What Docsbook has shipped that wins more AI citations"
description: "Every release that makes assistants quote you: llms.txt, structured data, answer blocks, and the machine-readable surfaces ChatGPT and Perplexity read."
---

# What Docsbook has shipped that wins more AI citations

Everything Docsbook shipped that moves one number: **AI citations** — more answers from assistants that cite you. On this axis, up is better.

Whether ChatGPT, Claude and Perplexity can read you — and quote you. This is the AI citations slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 05.09.2026

### Fixed

- Analytics no longer keeps auto-refreshing a historical range you're not watching live — the 30-second poll now only fires while `Now` is selected. The AI Views card opens on Pages instead of Crawlers by default, and its crawler and page rows get the same Improve button already on other analytics rows. `Analytics`

## NEW - 04.09.2026

### Changed

- An agent's issue now opens on what it FOUND. Why the run happened, what earlier steps handed it, what happens to anything it writes and the raw call all moved into one collapsed block at the bottom, so deciding what to do about a finding no longer means scrolling past four headings about the machinery to reach it. `Issues`

## NEW - 03.09.2026

### Added

- Two new content widgets. **Tabs** put parallel versions of the same instruction — npm/pnpm/yarn, macOS/Windows, curl/Python — behind one switch, so a reader stops scrolling past two thirds of a page looking for their own variant; the panels are all in the page source and the switching is CSS-only, so every variant stays readable with JavaScript off and visible to crawlers. **Pricing** turns plans into cards a reader can choose between, or a plan table into a comparison matrix, so the shape of the choice is visible instead of being something the reader has to work out from a table. `Content Widgets`

### Fixed

- Showcase demos served on the apex path (`docsbook.io/[demo]`) now answer `llms.txt` and `llms-full.txt`, named after the demo rather than the account, and their translated pages open at `docsbook.io/[demo]/[lang]/…` with a canonical that points at itself, so an AI assistant can read and cite every public demo and search engines index its translations instead of following 112 sitemap entries into a noindex 404. `SEO`
- A documentation page's own `title` and `description` now reach the HTML head. Both were being ignored: the `<title>` was built from the body's H1 and the meta description from the first paragraph of the page, which on an index page shipped the widget's `{compass}` icon markers into the Google result. The brand was appended twice on top of that (`— Docsbook | Docsbook`), spending 22 of the title's characters on a repeat, and the JSON-LD `headline` named the page a third way, from the filename. Every page's search result and AI-assistant citation now says what the author wrote, on the apex domain and on custom domains alike. `SEO`

## NEW - 02.09.2026

### Added

- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`
- Copying a prompt from the Prompts table now appends what the receiving assistant cannot know: which project it is about, the project's docs URL and repository, the Docsbook MCP endpoint, the tools that prompt calls, and an instruction not to invent what only those tools could have answered. The same sentence pasted into Claude, ChatGPT, Cursor or Codex used to read as a request about no particular site. The note is composed at the clipboard only — it is never stored and never sent on a scheduled run. `Prompts`

### Changed

- The 44 previous audit-shaped tools (`audit_seo`, `map_capabilities`, `diagnose_traffic_drop` and the rest) have been replaced rather than renamed. The tools reference lists what took over each one; the four `run_docs_*` background jobs, `audit_geo` and the five `collect_*` collectors are unchanged. `MCP`

## NEW - 30.08.2026

### Added

- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Hovering a point on the traffic chart now offers **Analyze** beside the date, which accounts for that one hour or day: whether it is unusual at all against the days around it, and what a spike was actually made of, a crawler and a launch being identical in a visitor count. The chart is now reachable by keyboard as well, with the arrow keys walking between points. `Analytics`
- The `SEO`, `GEO` and `AEO` cards each gained the same pair, and Analyze reads your live pages rather than the switch: a setting that is on while the markup never renders is exactly what a green Active pill cannot tell you. `SEO`
- The event picker now offers every event your workspace can actually react to, in plain words with the machine name under them, grouped the way `Feeds` groups the same events, with a filter box pinned above a list that is now past forty. `Prompts`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- Ten new scenario tools answer a question about your **business** rather than about your docs. What every product a buyer considers instead of yours gives away for free, and the need none of them serves (`map_competitor_free_offers`). Which reader question is answered by a working calculator or validator rather than by a paragraph, and whether it is an existing widget, a custom one, or something needing a service behind it (`design_free_tools`). Whether a repeating axis in your product justifies a generated page family, and whether a machine can keep that family correct (`plan_page_family`). `MCP`
- `assess_content_roi` is the one that gives you permission to stop: which pages earn their upkeep, and which to merge, redirect or retire. It works out which low-traffic pages are protected by inbound links or assistant citations **first**, and never proposes retiring one of those — deleting a page something external points at spends a link profile that cannot be bought back. `MCP`
- Every section of the panel that has its own release notes now carries a **Change Log** button in its header, beside `Dashboard` — `Changes`, `MCP`, `Prompts`, `Chat`, `SEO & GEO`, `Translations` and `Feeds` each open only what shipped in that section, instead of the whole product's history. `Dashboard`

### Changed

- The button on `Search rankings` no longer switches SEO, GEO and AEO on for you. It walks you to them instead: the panel moves to `Settings` ▸ `SEO & GEO`, lights each of the three in turn and says what it does and who it is for — search engines, AI answer engines, or featured snippets and voice — and the last step brings you back to `Search rankings`. Each switch stays live under the light, so you can turn one on where you are standing or just press Next. `SEO`

### Fixed

- The public skills catalog now spells names the way the rest of the product does — `SEO` and `GEO` rather than "Seo" and "Geo". `Skills`

## NEW - 28.08.2026

### Added

- A commit in `Changes` now reads as a commit and is then measured: its labels, title, description and byline above ten indicators — readers, time reading, dead rate, CTA rate and AI citations measured, then score, earned, revenue, spent and steps to the CTA estimated — over a gallery of the files it touched. Picking a file re-points every number at that file alone. `Changes`

### Changed

- The Overview is now one card for the site itself — its picture, address, plan and source repository, with **Visit** and a menu carrying the address and `llms.txt` — above a row of three readouts. `Dashboard`

## NEW - 23.08.2026

### Changed

- The AI crawler chart moved from the metrics row into the `AI` tab of the `Referrers` card, above the per-bot totals it explains. `Analytics`

## NEW - 22.08.2026

### Added

- `Search rankings` now opens with a one-click activation prompt when SEO, GEO and AEO are all off — showing what your rankings will look like and turning any of them on, free on every plan, instead of an empty tab. `SEO`

### Changed

- Tool, agent and skill names across the `Agents` tab read as names (`Docs Planner`, not `docs-planner`), with the machine id kept verbatim under each title. `Agents`

## NEW - 14.08.2026

### Changed

- Disabled `SEO`, `GEO` and `AEO` toggles now sort to the top of the SEO panel so you see what to turn on first; a toggle you just enabled stays put until you reopen the panel. `Settings`

## NEW - 03.08.2026

### Fixed

- Pricing pages across the docs (blog comparisons, MCP reference, AI features overview, quick-start, branding guide) no longer show AI chat, SEO/GEO/AEO, or the MCP server as paid-tier features — they are free on every plan, including Free. Custom domain and white-label are now correctly attributed to Business (not Pro), and the Source-of-Truth content graph to Business (not Pro). `Docs`

## NEW - 31.07.2026

### Fixed

- The auto-generated TL;DR block now replaces the opening paragraph it was taken from, instead of repeating the same sentence directly below itself. `GEO`

## NEW - 28.07.2026

### Added

- You can now see whether each visit actually succeeded — visits, outcomes, dead-end pages and exit pages are reconstructed from your existing events, with crawler traffic and inflated read time filtered out. `Analytics`
- The SEO/GEO tab now shows your real Google Search Console positions, including which queries are worth improving, with no OAuth or domain verification needed on a `*.docsbook.io` subdomain. `SEO`
- Analytics can now chart AI Visits as one line per crawler, so you can see which AI assistants read your docs and how that changes over time. `Analytics`

### Fixed

- Answers in the docs chat now cite the pages they came from. Citations were previously empty on every answer, so readers had no way to jump to the source. `AI Chat`
- Visitors, page views, top pages, referrers and events now exclude crawler traffic, which was up to 93% of pageviews on some sites. AI Visits remains the one card that reports bot volume. `Analytics`

## NEW - 27.07.2026

### Added

- Correct a machine translation by editing its text directly, instead of re-uploading the whole page. `Translations`

## NEW - 24.07.2026

### Changed

- Business plan price corrected to $159/month everywhere — pricing page, FAQ, and machine-readable `/pricing.md` and `/llms.txt` now agree with the actual checkout price. `Pricing`
- MCP tool count claims corrected to the real number across the site and `/llms.txt`. `MCP`
- `/llms.txt` and the shared preview image now describe Docsbook's current positioning instead of an outdated tagline. `SEO`

### Fixed

- `/llms-full.txt` no longer silently serves a "Failed to generate" stub when the docs source is unavailable — it now falls back to the same content as `/llms.txt`. `SEO`

## NEW - 18.07.2026

### Changed

- SEO, GEO, and AEO optimization now apply to docs on every plan, no longer Pro-only. `SEO`

## NEW - 14.07.2026

### Added

- `Copy page menu` card — independent toggles for each item in the `Copy page` dropdown (Skills.md URL, view as Markdown, and shortcuts for ChatGPT, Claude, Cursor, Windsurf, VS Code MCP). `Content`

### Improved

- "Create docs from a website" now generates a foldered 8-page site (features, guides, use-cases, FAQ) instead of 5 flat pages — a stronger starting point and a real FAQ page for AI-answer citability. `AI Chat`

## 0.22.3 - 30.05.2026

### Fixed

- Fix SEO/GEO/AEO toggles showing "Active" in anonymous mode — toggle now rolls back and shows an inline error when unauthenticated

## 0.21.0 - 25.05.2026

### Added

- SEO / GEO / AEO admin cards with real functionality — admin tab renamed from "SEO" to "SEO / GEO" (key `seo-geo`) and split into three toggleable cards, each with a `Learn more about …` footer link. GEO toggle injects a TL;DR `<aside class="tldr">` at the top of every page (from `tldr:` frontmatter or auto-extracted first paragraph), shows a visible `Updated DD MMM YYYY` `<time>` at the article end, and switches author in JSON-LD `TechArticle` to a full `Person` schema (frontmatter `author`/`authorUrl` or fallback to last git commit author). AEO toggle gates the existing `FAQPage` JSON-LD, auto-detects `HowTo` JSON-LD from `## How to …` / `## Как …` headings followed by numbered lists (`src/utils/seo/extractHowTo.ts`), and adds a `speakable` `SpeakableSpecification` to `TechArticle` for voice assistants. New MCP tools `update_geo` and `update_aeo` (PRO-gated) mirror `update_seo`. Markdown pipeline migrated from regex-strip to `gray-matter` for typed frontmatter (new `src/utils/markdown/parseFrontmatter.ts`); 4 call-sites refactored. New `docs/content/features/geo.md` and `aeo.md` document the behavior and authoring patterns; `seo.md` updated with cross-links. DB columns `workspaces.geo_enabled` and `aeo_enabled` (migration `0028_public_marvex.sql`)

## 0.20.2 - 25.05.2026

### Added

- UTM parameters on all internal CTAs leading from `/skills`, `/mcp`, `/docs` (Preview banner), and the blog to the landing page — every `/start` and `/connect` link now carries `utm_source` (`skills` / `mcp` / `preview` / `blog`), `utm_medium` (`nav` / `cta` / `banner`), and `utm_campaign` (e.g. `header_signup`, `mcp_start_free_top`, `preview_connect`, post slug for blog). New `src/utils/utm.ts` helper (`withUtm()`) wires the landing `Header`/`Footer` via an optional `utmSource` prop, the two inline CTAs on `/mcp`, and the `PreviewConnectBanner` on workspace pages. Blog post CTAs (`docusaurus_vs_docsbook`, `mintlify_vs_docsbook`, `gitbook_vs_docsbook`, `ai_search_documentation`, `documentation_seo_guide`, `how_to_host_docs_from_github`, `why_documentation_matters`) now tag their conversions per post. The landing page itself stays UTM-free so internal scroll-to-CTAs aren't mis-attributed

## 0.20.1 - 25.05.2026

### Changed

- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.18.0 - 24.05.2026

### Added

- Devices, Browsers and AI Visits analytics — new row of cards under Pages/Referrers in the Analytics tab. First card has tabs for `Devices` (Mobile/Desktop/Tablet) and `Browsers` (Chrome, Safari, Firefox, Edge, Brave, Arc, Vivaldi, Yandex…) with favicon icons. Second card lists AI crawler visits (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Bingbot, Applebot-Extended, Meta-ExternalAgent, CCBot, Bytespider, MistralAI-User and 12+ more) grouped by provider so you can see exactly which AI agents read your docs
- Install snippets for 8 AI clients on `/mcp` — interactive selector with tabs for Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, GitHub Copilot (VS Code), and ChatGPT; each one shows its own command or config (bash/JSON/TOML) with filename and optional install steps
- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`

## 0.17.3 - 23.05.2026

### Added

- `llms.txt` now includes a full MCP Server section with connect instructions, tool list, and discovery notes

## 0.15.0 - 22.05.2026

### Added

- `llms-full.txt` endpoint with complete product brief for AI crawlers
- Explicit allow rules for GPTBot, ClaudeBot, PerplexityBot, Google-Extended in `robots.txt`
- New `SEO Optimization` page in `docs` explaining automatic meta tags, JSON-LD, static pages, sitemap, canonical URLs, hreflang, and llms.txt — with compounding ROI timeline

### Improved

- `FAQPage` schema expanded to 9 Q&A pairs with detailed AI-citable answers
- `llms.txt` now serves full product brief — pricing, features, audience, competitors
- `llms.txt` fallback content replaced with full product brief

## 0.12.0 - 17.05.2026

### Added

- `/llms.txt` endpoint so AI crawlers can discover and understand your docs

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
