---
title: "Time to answer changelog"
description: "Everything Docsbook shipped that shortens the hunt inside your docs — navigation, structure, on-site search, vocabulary and the first-run path."
---

# Time to answer changelog

Everything Docsbook shipped that moves one number: **Time to answer** — readers reaching an answer sooner. On this axis, down is better.

How long a reader hunts before the page they needed is in front of them. This is the Time to answer slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`

## NEW - 31.08.2026

### Fixed

- Header navigation links on a docs site served at an apex path (like `docsbook.io/docs`) no longer 404 — they used to resolve against the site root instead of the site's own base path, so a link meant for that site could bounce through a subdomain that doesn't exist. `Changes`

## NEW - 30.08.2026

### Added

- Five **collectors** in `MCP` hand back the evidence an audit is built on, without the opinion, at **$0.0040** a call against the audit's $0.25. `collect_page_text` fetches your live pages and reports what the wire actually serves — status, title, headings, and how many words survive with no JavaScript — beside the size of the source stored for the same path. `collect_corpus_map` maps every page with its size, depth and whether navigation reaches it. `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search` return what readers asked, how their visits ended, and what they typed into your search box. `MCP`
- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Those figures say nothing they cannot support. A page already doing better than its position predicts shows how much traffic the change touches rather than a gain; a structure or settings recommendation carries no prediction at all, because neither changes how often a listing is clicked; and a page with too little search history shows an empty space rather than a zero. Every prediction is marked an estimate while the assumption behind it is reasoned rather than measured against what past changes actually did. `AI Chat`

### Changed

- A card with no data of yours yet now draws the report itself over sample figures, faded behind the line saying what would fill it and the **Fix it** button that asks the assistant why it has not. It used to be blank space, or a grey outline with nothing in it, under a sentence describing a thing you had never seen. This is every empty card, not only the ones still behind **Turn on**: the tabs in `Analytics`, the readers table, `Feeds`, `Changes`, `Search rankings`, the chat reports and the translation impact tiles. `Dashboard`
- Recommendations are now grouped by the kind of work they are — page text, structure, and workspace settings — each under its own heading with a count, instead of naming the kind in small grey text at the end of the row. `AI Chat`

## NEW - 28.08.2026

### Added

- A **Getting started** checklist now sits at the bottom of the admin panel's sidebar, showing what your site still needs — its content, your branding, the AI chat, languages, your agent, your domain, and being findable. It ticks steps off as they are configured, collapses to a single row, and disappears once you are done. `Dashboard`
- The admin panel's sidebar now warns you before your AI allowance runs out: a small card above **Getting started** showing the share left, when the cycle resets, and a way through to your usage or a plan. It appears at a quarter left, again at a tenth, and once more when nothing is left, and closing it keeps it quiet until one of those actually happens. `Limits`

### Changed

- The project's name in the admin panel's sidebar is now the same size as the navigation under it, and a paid plan shows as a crown beside the name instead of a text label competing with it for the row. `Dashboard`

### Improved

- Every row and switcher in the admin panel's sidebar is now one text size and one icon size, a step smaller than before, so the navigation reads as navigation rather than competing with the page beside it. `Dashboard`

### Fixed

- The **Getting Started** folder can no longer be hidden from the sidebar. Hiding it stranded any reader who closed the introduction early with no way back to it. `Dashboard`

## NEW - 25.08.2026

### Changed

- The setup checklist's first step now opens Settings directly, instead of a sign-up wall. `Onboarding`

## NEW - 24.08.2026

### Fixed

- Cards that had nothing to show a signed-out visitor are now filled with sample data instead of an error or an empty state — goals and funnels, the commit list, chat conversations and their transcripts, repository folders, navigation and social links, and every language page. `Preview`

## NEW - 14.08.2026

### Changed

- The onboarding wizard builds the docs inside itself and lands you on the finished site, without asking the same question twice. `Onboarding`

## NEW - 10.08.2026

### Changed

- The preview tour introduces branding second-to-last, closer to the point where you would use it. `Onboarding`

### Fixed

- The wizard's `See the magic` step failed with an error instead of building your site. `Onboarding`

## NEW - 01.08.2026

### Added

- Signing up now starts by asking what you do — founder, developer, technical writer, marketing, support — so the product can speak to your job rather than treat everyone the same. `Onboarding`
- The welcome questions now end by asking where your docs should send readers, so your first pages are written towards a real destination. The step is optional and can be skipped. `Onboarding`

### Changed

- A site built before signing up now keeps the call to action found on your own website, so the published project starts with a goal instead of a blank field. `Onboarding`
- If you built a site before signing up, the welcome questions no longer ask what you are documenting: your site publishes while you answer, and finishing takes you straight to it instead of an empty chat. `Onboarding`
- A conversation you started before signing up carries over to your new project and reopens beside your documentation, so you can pick it up where you left off. `Onboarding`

## NEW - 31.07.2026

### Fixed

- The sidebar now opens with your introduction and quick start instead of whatever page happens to come first alphabetically, and leaves reference pages, changelogs and FAQs at the end. Previous/next links follow the same order. `Navigation`

## NEW - 30.07.2026

### Added

- Add a [lucide](https://lucide.dev/icons) icon next to any page or folder in the left sidebar, and to any tab in the subheader folder navigation. `Sidebar`

## NEW - 28.07.2026

### Changed

- A draft generated before signing in now opens as a real documentation site — header, sidebar tree, outline, breadcrumbs and prev/next — so you can browse every generated page and tune branding, layout and SEO before deciding to publish. `Design`

## NEW - 24.07.2026

### Added

- You can now generate a documentation site without an account — pick a website URL to scan, a GitHub repo to link, or just describe an idea in text at `docsbook.io/create`, then preview and AI-chat-edit the draft before signing in. `Onboarding`
- Anonymous drafts get a live split-screen chat + preview (or a full-screen preview at `/draft`), with a short trial of AI edits before you're asked to sign in. `Onboarding`
- Signing in after building an anonymous draft automatically publishes it as a live workspace — no re-work needed. `Onboarding`

### Changed

- Homepage copy and structured data now frame Docsbook around growth and conversion outcomes, not just docs hosting. `Landing`

## NEW - 18.07.2026

### Added

- Guided setup after sign-up: a short questionnaire asks whether you have a site, a GitHub repo, or just an idea, then takes you straight to your docs or starts generating them. `Onboarding`

## NEW - 17.07.2026

### Fixed

- Section breadcrumbs now link to that section's own landing page instead of an arbitrary first page. `Navigation`

## NEW - 14.07.2026

### Fixed

- Account switcher dropdown in settings sidebar was too narrow, squeezing org names and links. `Navigation`

## NEW - 12.07.2026

### Fixed

- Navigation link button color picker restored in workspace settings — links with a saved color could no longer be recolored or reset to a plain text link. `Navigation`

## 0.26.5 - 29.06.2026

### Fixed

- Free-text questions in the onboarding AI chat now render a text field so you can type your answer — previously a question with no preset options left nowhere to respond. `AI Chat`
- Creating docs from just an idea no longer stalls with a "process did not complete" error — the underlying request was being rejected; the onboarding chat now runs through to a published site. `AI Chat`

## 0.25.0 - 04.06.2026

### Added

- **Onboarding**: Interactive 7-step onboarding guide on first login to Docsbook — guided tour highlights key features in FloatWidget toolbar, adapts to user's plan (Free/PRO/PRO+/Enterprise), and remembers when dismissed with `hasSeenOnboarding` flag in `workspaces`
- **Onboarding**: New `about/feature-access.md` — private single source of truth matrix (Preview Anonymous × Free × PRO × PRO+ × Enterprise) documenting 80+ features, their availability per tier, limits, and onboarding rules for what to highlight to each user persona

## 0.22.3 - 30.05.2026

### Fixed

- Fix 503 errors on sidebar RSC prefetch in preview mode — prefetch disabled so navigation still works on click

## 0.22.1 - 28.05.2026

### Fixed

- Fixed broken navigation on `docs.docsbook.io` alias — clicking any sidebar/inline link returned 404 because cached HTML carried the `/docs/` repo prefix while middleware rewrote it again. Added `x-docs-alias` header in `src/proxy.ts` and routed `basePath` to empty in `src/app/[user]/[repo]/[[...path]]/page.tsx` so links render as `/ai/mcp` instead of `/docs/ai/mcp`. Existing `docsbook-io.docsbook.io/docs/*` paths keep working unchanged

## 0.21.6 - 27.05.2026

### Fixed

- Fixed mobile outline (right table-of-contents panel) backdrop overlay no longer covering the header in `src/components/docs/Outline.tsx` — same treatment as the sidebar overlay so the header stays clickable when the outline drawer is open on mobile

## 0.21.4 - 26.05.2026

### Chore

- Optimized Claude Code token usage with `claude-token-optimizer`: added Session Start Protocol, filled `.claude/QUICK_START.md`, `.claude/COMMON_MISTAKES.md`, `.claude/ARCHITECTURE_MAP.md` with project-specific content — auto-loaded tokens reduced from ~137k to ~121k

## 0.20.1 - 25.05.2026

### Changed

- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.18.0 - 24.05.2026

### Added

- Mobile Outline drawer — on screens <1280px the right-hand "On this page" panel is now reachable via a floating button in the bottom-left corner that opens a slide-up sheet with the same heading list and actions (scroll to top, ask AI, copy markdown, edit on GitHub, page feedback); desktop layout unchanged
- Sitelinks-friendly structured data on the landing — added `SiteNavigationElement` JSON-LD for 8 key sections (Quick Start, AI Features, MCP Server, Agent Skills, Documentation, FAQ, Blog, Changelog), an `ItemList` with top destinations, and `WebSite.hasPart` linking the main pages so Google has explicit signals for generating sitelinks under the docsbook.io result

## 0.17.3 - 23.05.2026

### Changed

- Reworked landing header navigation — replaced old category dropdowns (AI, Analytics, Branding, Widgets, Translation) with 3 direct links (`AI`, `MCP`, `Skills`) plus 2 curated dropdowns: `Documentation` (Quick Start, Basics, Creating Docs, Custom Domain, AI Translations, FAQ) and `Blog` (all 5 posts)

## 0.17.2 - 23.05.2026

### Added

- `get_doc_graph` now supports `format` parameter: `"toon"` (default) returns a compact text tree ~10x smaller than JSON with `@canonical/ref` syntax that LLMs parse natively; `"json"` preserves the previous full structured response for programmatic clients

## 0.16.3 - 23.05.2026

### Fixed

- Neutralize green styling on "Get Support" button in workspace settings sidebar — now matches the muted look of other navigation items

## 0.15.0 - 22.05.2026

### Added

- `SoftwareApplication` structured data schema on `Landing Page` for AI search visibility

## 0.12.0 - 17.05.2026

### Fixed

- Special characters (e.g. `&`) now display correctly in the page outline

## 0.11.0 - 16.05.2026

### Added

- Header navigation links now translate to the active language

### Fixed

- Previous/Next navigation buttons now show translated page names

## 0.8.1 - 12.05.2026

### Added

- FAQPage structured data for Google rich snippets on landing page

### Fixed

- Landing page HTML structure and heading hierarchy corrected

## 0.7.0 - 11.05.2026

### Added

- Custom background color support for individual header navigation links

## 0.6.0 - 10.05.2026

### Added

- Subheader navigation with folder tabs and hover dropdowns

## 0.4.0 - 10.05.2026

### Added

- Getting started guide, GitHub editing instructions, Claude Code and VS Code guides in documentation

## 0.2.0 - 08.05.2026

### Added

- SEO panel — control search engine indexing, canonical URLs, and structured data

## 0.1.1 - 07.05.2026

### Added

- Scroll shadow on document outline to indicate scrollable content

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
