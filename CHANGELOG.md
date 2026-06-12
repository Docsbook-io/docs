---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, fixes, and improvements to the AI-powered documentation platform shipped across every version."
---

# Releases

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.
- **Agent daemon:** Enhanced reliability with revised `auto-commit.sh` lock handling and improved logging for task transitions.

## 0.26.3 - 11.06.2026

### Fixed

- **Limits card:** "Usage by source" bars now show each category's share of *actual spend* instead of a tiny fraction of the full budget ceiling — so you can see at a glance where your tokens go (AI Chat readers vs. Admin vs. AI Translations) and what to optimize.
- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.2 - 11.06.2026

### Improved

- **Agent daemon:** Token diet for `spawn_session()` — now selects model by priority (P1 → Sonnet, P2/P3 → Haiku instead of fixed Sonnet) and adds bash pre-checks in merger role (skip if PR already merged or base=main). Selective directory copy by role (merger copies only `routines/` + `agents/branch-merger.md` instead of full context).

## 0.26.1 - 11.06.2026

### Fixed

- **Daemon:** Unreleased `agent:working` labels no longer hang forever — added reconcile sweep in `sweep_locks()` to auto-remove labels without live lock files; also fixed repo context (added `-R Docsbook-io/docsbook` to all gh-calls) and network hangs (wrapped git/gh in 20/30s timeouts)
- **Merger:** Now closes issues explicitly after merge instead of relying on GitHub's unreliable `Closes #N` auto-close for feature branches; added fallback search for already-merged PRs (`--state merged`) to prevent zombie cycles when PR is merged manually
- **Labels:** New `awaiting-release` label (blue, `#0075CA`) for base=main PRs awaiting manual `/merge` — separates "blocked and needs human intervention" (`needs-human`) from "queued for release" (`awaiting-release`)
- **Hooks:** `auto-commit-hook.sh` now removes stale lock files (>10 min) instead of skipping forever after crash

## 0.26.0 - 11.06.2026

### Added
- New `/chat` page with full AI agent for docs: search, edit settings, publish changes, and get answers — all in one conversation interface.
- `DocsAskInput` floating panel on every docs page — readers can ask questions without leaving the page.
- `AuthModal` with Google, Apple, and email-OTP sign-in alongside existing GitHub OAuth.
- `LimitsCard` in admin dashboard — unified token budget view with per-workspace usage breakdown.
- `AdminCard` manifest system — all FloatWidget settings tabs now driven by a single `ADMIN_CARDS` registry, making tabs easier to add and test.
- `applyWorkspacePatch` shared layer — workspace PATCH API consolidated from 400 lines of inline conditionals into one validated, plan-gated function.
- Workspace list sorted by most-recently-used first (`last_used_at DESC NULLS LAST`).
- New-chat `+` button in `/chat` header to reset conversation without page reload.
- Interactive upsell card when Pro/Pro+ features are mentioned in chat.
- Demo login button for Vercel preview deployments.
- `watch-issues.sh` script and local agent daemon for automated pipeline tasks.
- `code-scout` subagent — investigates code by problem description and creates GitHub Issues with technical context, so Buddy stays in orchestration mode without reading code directly.
- `qa-agent` now accepts a `FOCUS` parameter when called directly via Agent tool, enabling targeted testing without a full `/qa-plan` sweep.

### Fixed
- Agent pipeline `agent:working` lock now released automatically on any session exit (trap on EXIT in nohup subprocess) — no more manual lock cleanup after agent crashes.
- `merger` now finds PRs by branch name `claude/issue-N` as fallback when `Closes #N` body search returns empty — eliminates false NEEDS_HUMAN blocks.
- `task-builder` now verifies `Closes #N` is present in every PR body and auto-adds it if missing — prevents merger from losing the PR link.
- Auth `CSRF` error on Vercel preview deploys — `AUTH_URL` now overridden to preview origin.
- Redirect loop on preview deploys — `vercel.app` added to `isDev` proxy check.
- Cold-start Neon timeout on preview auth — DB lookup skipped in `preview-bypass` authorize.
- `ask_user` deduplication in LLM transcript — prevents 400 errors on Idea path.
- `MenuGroupRootContext` crash in ProjectSelector dropdown — owner groups wrapped in `DropdownMenuGroup`.
- Chat close button used hardcoded `docsbook.io` URL — switched to relative path.
- `/api/auth/signin` now redirects to `AuthModal` via `pages.signIn` instead of blank form.

## 0.25.1 - 08.06.2026

### Fixed

- **Accessibility**: Added `aria-label` to 4 icon-only buttons in the AI Chat mock on the landing page — screen readers and WCAG 2.1 AA compliance restored
- **Docs**: Removed internal operational files (`TWITTER_SETUP`, `outreach/`) from the public documentation sidebar — visitors no longer see private tooling pages
- **Skills**: Corrected the `npx install` link on the `/skills` page — now points to the correct `Docsbook-io/docs-skills` package

## 0.25.0 - 04.06.2026

### Added

- **Onboarding**: Interactive 7-step onboarding guide on first login to Docsbook — guided tour highlights key features in FloatWidget toolbar, adapts to user's plan (Free/PRO/PRO+/Enterprise), and remembers when dismissed with `hasSeenOnboarding` flag in `workspaces`
- **Onboarding**: New `about/feature-access.md` — private single source of truth matrix (Preview Anonymous × Free × PRO × PRO+ × Enterprise) documenting 80+ features, their availability per tier, limits, and onboarding rules for what to highlight to each user persona
- **Admin**: Fix FloatWidget (toolbar) not appearing for authenticated repo owners after "Start for free" — added direct GitHub repo ownership check in `ensureWorkspaceIfMember()` so owners see the admin interface immediately
- **Skills**: SKILL.md schema preview on detail pages (`/skills/[name]`) — developers now see required/optional frontmatter fields, YAML example from the current skill, and copy-paste instructions before installing with `npx docs-skills install`

## 0.24.0 - 04.06.2026

### Added

- **Landing**: New `PricingSection` — 3-column plan comparison block (Free / PRO $150 / PRO+ $59/mo) placed on homepage between CtaBand and FAQ so founders can compare plans at a glance without reading paragraphs
- **Enterprise**: Add WorkOS SSO/SAML integration scaffold — `@workos-inc/authkit-nextjs` package, `enterprise` plan enum added to `users` and `workspaces` tables, new `workosUserId`, `ssoOrganizationId`, `ssoDomain` columns

### Fixed

- **Landing**: Reframe CI/CD copy in `Features.tsx` to be positive trust signal for devs; add Mintlify to migration sources list alongside Confluence, GitBook, Docusaurus
- **Landing**: Fix `/skills` install command showing hardcoded "25 skills" — now uses dynamic `index.skills.length` (currently 36)
- **Admin**: Fix branding Save not updating sidebar/header name live in preview mode — `DocsContentArea` now resolves `previewSettings` fields with workspace fallback for `customName`, `iconUrl`, `logoUrl`, `fontFamily`

## 0.23.0 - 03.06.2026

### Added

- **Analytics**: Exclude internal (founder/admin) traffic from Axiom with `INTERNAL_IPS` env allowlist — single source of truth in `src/utils/analytics/internal.ts` with consistent IP extraction across all six ingest points (`/api/axiom`, server pageview logger, `/api/vitals`, `/api/_axiom/web-vitals`, `/api/analytics/{cta,feedback}`)
- **Growth**: New `/enrich-audience` command for the first growth-reasoning team — reasons over `about/` + Axiom analytics and appends insights back into the product business-layer. Adds cross-artifact drift contract in `CLAUDE.md` + `AGENTS.md` (MCP ↔ docs-skills ↔ docs-subagents ↔ docs-claude-plugins dependency graph)

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/pricing` route returning 404 — now redirects to `/` instead of broken `pricing.docsbook.io` subdomain
- Fix `/blog` and `/blog/:path*` returning 500 — now redirects to `docsbook.io/docs/blog` for marketer SEO entry-points
- Fix SEO/GEO/AEO toggles showing "Active" in anonymous mode — toggle now rolls back and shows an inline error when unauthenticated
- Fix 503 errors on sidebar RSC prefetch in preview mode — prefetch disabled so navigation still works on click
- Fix copy button position in multiline code blocks — now anchored to top-left so it's always accessible in long snippets
- Fix scroll shadow in Webhooks (Events) tab — shadow now appears only when content is scrollable

### Improved

- Resized folder visibility and subheader folder toggles to match the standard Search Bar checkbox size for visual consistency

## 0.22.2 - 28.05.2026

### Changed
- Official documentation now served at `docsbook.io/docs` — middleware rewrites `/docs/*` internally instead of redirecting to `docsbook-io.docsbook.io`; canonical URLs, sitemap, JSON-LD, and all links updated across landing, admin, and MCP pages
- `docs.docsbook.io` and `docsbook-io.docsbook.io` now return `Disallow: /` in robots.txt so search engines index only the canonical `docsbook.io/docs` path

## 0.22.1 - 28.05.2026

### Fixed
- Fixed broken navigation on `docs.docsbook.io` alias — clicking any sidebar/inline link returned 404 because cached HTML carried the `/docs/` repo prefix while middleware rewrote it again. Added `x-docs-alias` header in `src/proxy.ts` and routed `basePath` to empty in `src/app/[user]/[repo]/[[...path]]/page.tsx` so links render as `/ai/mcp` instead of `/docs/ai/mcp`. Existing `docsbook-io.docsbook.io/docs/*` paths keep working unchanged

## 0.22.0 - 28.05.2026

### Removed
- Removed server-side Source of Truth indexing — `get_doc_graph`, `read_doc_sections`, `reindex_doc_graph` and the 17 `doc_*` LSP-style MCP tools are gone. Graph search now runs locally via the [docs-claude-plugins](https://github.com/Docsbook-io/docs-claude-plugins) package (`/plugin install docs-sync@docs-claude-plugins`). Deleted `src/lib/source-of-truth.ts`, `src/lib/mcp/lsp-tools.ts`, the reindex REST route, the daily `stale-check` cron and the two smoke scripts

### Changed
- Replaced the admin Source of Truth card in `src/components/mcp/SourceOfTruthControls.tsx` — the reindex usage counter (`/100`) and Reindex button are gone, replaced by a promo card with the install command and a link to the docs-claude-plugins repository
- Updated `src/components/SourceOfTruthUpgradeModal.tsx` bullet from "100 reindexes/month" to "Local indexing via Claude Code"
- Cleaned `src/app/mcp/page.tsx`, `src/app/mcp/_data/prompts.ts` (239 lines dropped) and `src/lib/generate-llms-txt.ts` of references to the removed tools

## 0.21.7 - 27.05.2026

### Fixed
- Mobile sidebar overlay no longer covers sticky subheader in `src/components/docs/Sidebar.tsx` and `src/components/docs/Subheader.tsx` — overlay `top` now adds the subheader's `2.25rem` when present, and subheader `z-index` raised from `z-30` to `z-40` so it stays above the overlay just like the main header

## 0.21.6 - 27.05.2026

### Fixed
- Fixed mobile sidebar backdrop overlay no longer covering the header in `src/components/docs/Sidebar.tsx` — overlay now starts below the header (h-12 + preview banner offset) and z-index lowered from 40 to 30 so the header stays interactive while the sidebar is open
- Fixed mobile outline (right table-of-contents panel) backdrop overlay no longer covering the header in `src/components/docs/Outline.tsx` — same treatment as the sidebar overlay so the header stays clickable when the outline drawer is open on mobile

## 0.21.5 - 27.05.2026

### Changed
- Restyled TL;DR block in docs to Vercel-style neutral border in `src/app/globals.css` — removed blue accent border-left and background fill, replaced with thin 1px border all around, transparent background, and muted-gray uppercase label for a cleaner minimal look in both light and dark modes

## 0.21.4 - 26.05.2026

### Fixed
- Ask AI on selection bubble: no longer interrupts text selection — bubble appears only after `mouseup`/`touchend` so selecting words and lines works normally
- Copy button on single-line code blocks: now vertically centered (`top: 50%`) so it appears on hover for all code block heights

### Chore
- Optimized Claude Code token usage with `claude-token-optimizer`: added Session Start Protocol, filled `.claude/QUICK_START.md`, `.claude/COMMON_MISTAKES.md`, `.claude/ARCHITECTURE_MAP.md` with project-specific content — auto-loaded tokens reduced from ~137k to ~121k

## 0.21.3 - 25.05.2026

### Fixed
- Mobile `/skills` and `/mcp` pages: added hamburger mobile menu to `Header` with full nav links, "Start for free" and "Log in" CTAs
- Mobile `/skills` top padding: reduced from `pt-28` to `pt-20` on mobile (consistent with `/mcp`)
- `SkillsInstallSelector`: install/use columns no longer stack on tablets — now `lg:grid-cols-2`
- `SkillInstallGuide`: install/use columns now split at `sm:` breakpoint for earlier two-column layout
- `PromptsFilters`: tags hidden on mobile (`hidden sm:inline-flex`), tool hover-state hidden on mobile to prevent overflow

## 0.21.2 - 25.05.2026

### Fixed
- Mobile header: removed the second nav-links row on small screens — header now shows only logo + CTA button
- Hero badge animation on Safari/iOS: `@property` conic-gradient is not supported in Safari; added CSS fallback via `border-beam-rotate` keyframe + `@supports` guard so the animated border renders correctly on all browsers
- Footer layout on mobile: removed `max-w-4xl mx-auto` from the `<footer>` tag, added `w-full` + horizontal padding on the inner container — background and `border-t` now stretch full-width on all screen sizes
- Hero top padding reduced from `pt-40` to `pt-28` on mobile (was over-compensating for the now-removed second header row)

## 0.21.1 - 25.05.2026

### Added
- Short marketing alias `docs.docsbook.io` for the product documentation — opens the same content as `docsbook-io.docsbook.io/docs/*` without redirect (URL stays clean in the browser). New `DOCS_ALIAS_SUBDOMAINS` map in `src/proxy.ts` rewrites `docs.docsbook.io/{path}` → `/docsbook-io/docs/{path}`; `/api/*` is passed through untouched, original subdomain URLs keep working.

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

## 0.19.0 - 25.05.2026

### Added
- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed
- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added
- Devices, Browsers and AI Visits analytics — new row of cards under Pages/Referrers in the Analytics tab. First card has tabs for `Devices` (Mobile/Desktop/Tablet) and `Browsers` (Chrome, Safari, Firefox, Edge, Brave, Arc, Vivaldi, Yandex…) with favicon icons. Second card lists AI crawler visits (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Bingbot, Applebot-Extended, Meta-ExternalAgent, CCBot, Bytespider, MistralAI-User and 12+ more) grouped by provider so you can see exactly which AI agents read your docs
- Ask AI on text selection — when readers highlight a snippet inside the docs, a floating `Ask AI` bubble appears above the selection; one click sends the selected text to AI Chat as a ready prompt. Tooglable per-workspace (Content tab in admin and `show_ask_ai_on_selection` in MCP `update_ui_settings`). On by default. Reduces friction for "explain this paragraph" / "rephrase this" use cases and pushes AI engagement
- Mobile Outline drawer — on screens <1280px the right-hand "On this page" panel is now reachable via a floating button in the bottom-left corner that opens a slide-up sheet with the same heading list and actions (scroll to top, ask AI, copy markdown, edit on GitHub, page feedback); desktop layout unchanged
- Signup attribution tracking — capture UTM parameters and referrer on landing pages, persist as first-touch cookie (`ds_attr`, 90 days), and write `signup_source` / `signup_medium` / `signup_campaign` / `signup_referrer` / `signup_landing_path` to `users` on GitHub OAuth signup so we can measure which channel (Twitter, HN, Product Hunt, dev.to, blog, organic, AI assistants) actually converts
- New FAQ sections covering subscription model, cancel behaviour, GitBook migration (3-step guide), annual vs monthly trade-offs, and grandfathered lifetime users
- Updated refund Q&A — 30-day money-back on first payment, prorated refunds for annual after the window
- Sitelinks-friendly structured data on the landing — added `SiteNavigationElement` JSON-LD for 8 key sections (Quick Start, AI Features, MCP Server, Agent Skills, Documentation, FAQ, Blog, Changelog), an `ItemList` with top destinations, and `WebSite.hasPart` linking the main pages so Google has explicit signals for generating sitelinks under the docsbook.io result
- New sitemap entries — `/mcp` and `/skills` with priority `0.9`, plus `/connect` with `0.5`, so Google can discover and weigh these promo pages
- FAQ reply notebook for community comments at `docs/blog/faq-replies.md` — 32 ready-to-paste answers (TL;DR + Long versions) across 8 sections (General, Pricing, Competitors, AI, SEO, Tech, Security, Objections) for Reddit, X, IndieHackers, and HackerNews distribution
- Simplified install/use guide on each skill page `/skills/[name]` — tabs for 7 AI clients (Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, Copilot), two steps (Install + Use) with the command pre-filled for this specific skill, plus a runtime-discovery block via Docsbook MCP
- Install snippets for 8 AI clients on `/mcp` — interactive selector with tabs for Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, GitHub Copilot (VS Code), and ChatGPT; each one shows its own command or config (bash/JSON/TOML) with filename and optional install steps
- Expanded the `Install in your AI client` section in [docs/ai/mcp](./ai/mcp.md) from a single Claude snippet to 8 subsections — one per client
- New blog tutorial `/blog/how-to-host-docs-from-github` — walks through three ways to turn a GitHub repo into a live docs site (GitHub Pages + Jekyll, Docusaurus, Docsbook) with step-by-step setup, tradeoffs, and a decision matrix; targets the "how to host documentation from github" high-intent SEO query
- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries
- Rewrote `/blog/docusaurus-vs-docsbook` into a full "Docusaurus Alternatives in 2026" guide (2.7k words) — TL;DR decision matrix, four reasons teams leave Docusaurus, 9 alternatives compared (Docsbook, Mintlify, GitBook, ReadMe, Archbee, VitePress, Nextra, Starlight, MkDocs Material) with pros/cons/pricing/migration, a "how to choose" section with three decision questions, a step-by-step migration guide, and a 7-question FAQ — targets the "docusaurus alternatives" SEO query instead of the narrower 1:1 comparison

### Changed
- Pivoted pricing FAQ from one-time lifetime to subscription model — PRO now $19/month or $190/year, PRO+ stays $59/month or $590/year (annual saves 2 months)
- Replaced legacy "Will the price increase?" answer with a price-lock guarantee for active subscriptions
- Moved "Get Support" out of the admin sidebar — replaced the bulky "Help & Support" section with a subtle "Need help? Contact support" footer link pinned to the bottom of the settings modal sidebar, freeing vertical space
- Reordered and trimmed the floating admin toolbar — now 5 quick-access buttons (Analytics, AI Chat, AI Translations, Design, SEO) instead of 6; removed setup-once entries (Custom Domain, MCP Server) and surfaced SEO, which was previously only reachable via the settings modal

### Fixed
- AI Skills cards in the admin no longer 404 on workspace subdomains — clicking a card now opens an in-place modal with the full `SKILL.md` (description, install snippets for 7 AI clients, keywords, MCP tools, GitHub link) instead of routing to `/skills/<name>` which only exists on `docsbook.io`. Landing-page behavior is unchanged
- Mobile adaptation for `/mcp` promo page — Hero `pt-28` reduced to `pt-20` on mobile, H1 base set to `text-3xl`, endpoint URL no longer overflows the screen
- `CopyCommand` on mobile — reduced padding/height, font-size scaled down, long install command no longer breaks the layout
- `AiClientsRow` — `gap-x-5` on mobile (was 9) so client icons line up more evenly at 375px
- `PromptsFilters` — category/plan selects use `grid-cols-2` on mobile instead of a single row; prompt row padding reduced, prompt text set to `13px` on mobile

### Removed
- Broken `SearchAction` from the landing JSON-LD — it pointed at `/search?q=`, a page that does not exist, sending a negative signal to Google instead of unlocking the Sitelinks Search Box

## 0.17.4 - 23.05.2026

### Fixed
- Replaced broken `(#)` CTA links across 5 blog posts (`mintlify-vs-docsbook`, `docusaurus-vs-docsbook`, `why-documentation-matters`, `documentation-seo-guide`, `ai-search-documentation`) — all now point to `https://docsbook.io/start`
- Removed misleading "free for 14 days" copy in `mintlify-vs-docsbook` — Free plan is free forever; added note that the 14-day trial applies only to PRO+ ($59/month)

## 0.17.3 - 23.05.2026

### Changed
- Reworked landing header navigation — replaced old category dropdowns (AI, Analytics, Branding, Widgets, Translation) with 3 direct links (`AI`, `MCP`, `Skills`) plus 2 curated dropdowns: `Documentation` (Quick Start, Basics, Creating Docs, Custom Domain, AI Translations, FAQ) and `Blog` (all 5 posts)

### Added
- Anonymous MCP access: any AI model can now connect to `https://docsbook.io/{owner}/{repo}/api/mcp/server` without authentication and use `get_info`, `get_doc_graph`, and `read_doc_sections` for PRO+ workspaces
- Scoped MCP endpoint `/{owner}/{repo}/api/mcp/server` — connecting to this URL auto-scopes the server to the specified repository
- Scoped `/{owner}/{repo}/.well-known/oauth-protected-resource` for OAuth discovery per workspace
- Every documentation page now includes `<link rel="mcp-server">` meta tag so AI models can auto-discover the MCP server from any docs URL
- `llms.txt` now includes a full MCP Server section with connect instructions, tool list, and discovery notes

## 0.17.2 - 23.05.2026

### Added
- `get_doc_graph` now supports `format` parameter: `"toon"` (default) returns a compact text tree ~10x smaller than JSON with `@canonical/ref` syntax that LLMs parse natively; `"json"` preserves the previous full structured response for programmatic clients

### Fixed
- Paginate MCP `get_doc_graph` to avoid hitting the MCP response token limit on large repos (previously a single 110k+ character JSON line blew past the limit and made the tool unusable in Claude). Added `page`/`page_size` (default 50), `path_prefix`, `include_headings`, `include_relations`, and `include_github_urls` flags; relations are only emitted on `page=1` to save bytes

## 0.17.1 - 23.05.2026

### Fixed
- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint
- Roll back the reserved reindex slot when `fetchAndIndexRepo` fails so transient errors no longer eat the monthly quota

## 0.17.0 - 23.05.2026

### Changed
- Remove live preview modal from landing — `GitHub to DocsBook` input now navigates directly to `/<owner>/<repo>?preview=true` instead of opening an overlay
- Replace dark-background OG/Twitter image with a landing-style preview — light gradient, "The AI Knowledge Platform" headline, feature badges, and a docs UI mockup — improves appearance when sharing links on X/Twitter

### Fixed
- Wrap long project names in sidebar to prevent overflow outside the sidebar boundary

### Changed
- Enable `Ask AI` button near the page title by default for new workspaces — previously off by default
- Fix system theme not applying correctly due to shared `localStorage` key across workspaces
- Fix `docs-proxy` route ignoring saved `defaultTheme` and always falling back to `light`

### Changed (previous)
- Rename `MCP Server` to `MCP Source of Truth` in Pro+ pricing rows and add a hover `?` tooltip explaining the AI-coupled indexing graph
- Enable Source of Truth by default for Pro+ workspaces — removed the manual toggle from the admin MCP tab
- Add a Pro+ badge next to `Reindex Usage` that opens the Source of Truth promo modal on click

### Added
- 10 new MCP Example Questions in admin (copy brandbook from a URL, change logo, custom domain, translations, social links, AI key, analytics, reindex, read sections); moved the `authentication module` example to the bottom of the list

## 0.16.3 - 23.05.2026

### Fixed
- Neutralize green styling on "Get Support" button in workspace settings sidebar — now matches the muted look of other navigation items
- Remove duplicate `opengraph-image.tsx` inside `[[...path]]` catch-all route that broke the Next.js build (parent route already handles all path scenarios)

## 0.16.2 - 23.05.2026

### Changed
- Open docs in `?preview=true` mode after submitting GitHub URL on `/start` — newly published documentation now lands directly in Preview Mode

## 0.16.1 - 22.05.2026

### Added
- New `/start` page replaces the `LivePreviewExpanded` modal on "Start for free" — logo, GitHub URL input, Sign in with GitHub, email/Discord support links, social icons, hero-style shards background, cascade animations

## 0.16.0 - 22.05.2026

### Changed
- Rework billing model — Pro is now $150 lifetime one-time payment, Pro+ replaces Enterprise as $29/mo subscription with white-label and Source of Truth
- New AI query limits — `Free` 0/mo, `Pro` 200/mo, `Pro+` 2000/mo (was 20/1000/unlimited)
- New translation limits — `Free` 0/mo, `Pro` 50/mo, `Pro+` 500/mo (was 30/300/unlimited)
- Existing `pro` workspaces (legacy $29 one-time) grandfathered as lifetime Pro at no extra cost
- Existing `enterprise` workspaces auto-migrated to `pro_plus` keeping all features

### Fixed
- Auth redirect loop after GitHub OAuth — stale `callbackUrl` cookie pointing at a subdomain `/connect` caused an infinite redirect cycle; NextAuth `redirect` callback now normalises any subdomain `/connect` → `docsbook.io/connect`
- `/connect` on a workspace subdomain now redirects to `docsbook.io/connect` instead of 404
- `ConnectPage` now redirects to sign-in when the session cookie is present but invalid/expired, preventing a broken `ConnectPicker` state
- Workspace redirect after sign-in always uses `APP_DOMAIN` instead of the request `host` header, preventing wrong subdomain redirects
- Infinite redirect loop for workspaces whose repo is named `connect` — subdomain middleware no longer intercepts `user.docsbook.io/connect` as a `/connect` auth route

### Added
- Paddle `SubscriptionPaymentFailed` webhook handler — downgrades workspace to Free and sends Resend email to the owner with payment-update link
- Subscription management UI in `FloatWidget` pricing tab — shows current plan, subscription status, next billing date, and Manage subscription button linking to Paddle Customer Portal (Pro+ only)
- `pricing-spec.md` in `docs/content/setup` — source of truth for the new billing model
- Two-option upgrade layout in `AiUpgradeModal` and `ProUpgradeModal` — side-by-side Pro lifetime vs Pro+ monthly cards
- Subscription metadata columns on `workspaces` — `paddle_subscription_id`, `paddle_customer_id`, `subscription_next_billed_at`, `subscription_status`

## 0.15.2 - 22.05.2026

### Fixed
- Show "AI not enabled" message with owner contact link in `AiPanel` instead of generic error when AI is disabled for a workspace — users now see a helpful message with a link to the project owner's GitHub profile to request enabling the feature

## 0.15.1 - 22.05.2026

### Added
- Animated growth counters in `CtaBand` — 4 stats (workspaces, pages indexed, countries, AI queries) count up over 6 seconds on scroll-into-view
- Before→After traffic animation in `BentoFeatures` analytics cell — visitors climb from 11 to 1,240 and page views from 34 to 8,900 in a 9-second loop
- Ticket deflection counter above AI chat mock — shows 0→847 tickets saved this month, growing over 6 seconds
- Concrete numbers in `SocialProof` tabs — `2,400+ workspaces`, `3× more signups`, `40% fewer tickets`, `15 languages`

## 0.15.0 - 22.05.2026

### Added
- `Get Support` tab in admin panel with email, Discord, and Twitter contacts
- Email support link in landing `Footer` for quick access to `support@docsbook.io`
- `SoftwareApplication` structured data schema on `Landing Page` for AI search visibility
- `llms-full.txt` endpoint with complete product brief for AI crawlers
- Explicit allow rules for GPTBot, ClaudeBot, PerplexityBot, Google-Extended in `robots.txt`
- Events webhook endpoint in `API` for receiving real-time workspace events
- Blog section in `docs` with 5 SEO-optimized posts for distribution — competitor comparisons (Mintlify, Docusaurus), AI search, documentation SEO guide
- New `SEO Optimization` page in `docs` explaining automatic meta tags, JSON-LD, static pages, sitemap, canonical URLs, hreflang, and llms.txt — with compounding ROI timeline
- Expanded `AI Translations` page in `docs` with sections on why Claude outperforms generic translation tools and how each language version is indexed separately for multilingual SEO

### Fixed
- Image-only paragraphs (e.g. GitHub release badges) in `prose` content now center-align instead of left-align
- `Preview mode` Connect GitHub button now redirects to main domain `/connect` instead of subdomain path
- Replaced PNG logo with inline SVG in `opengraph-image` for correct social preview branding
- `Copy Page` dropdown now uses fixed positioning to stay within viewport on mobile instead of overflowing off the left edge

### Added
- Confetti animation on `/success` page after successful payment via `canvas-confetti`

### Improved
- Search widget UX with breadcrumb paths and "Ask AI assistant" option in `Search Bar`
- `AI Panel` input field now receives focus automatically when the panel opens
- `Organization` schema expanded with founder, email, foundingDate, and social sameAs links
- `FAQPage` schema expanded to 9 Q&A pairs with detailed AI-citable answers
- `WebSite` schema now includes SearchAction for Google Sitelinks Search Box
- `llms.txt` now serves full product brief — pricing, features, audience, competitors
- FAQ answers server-rendered in HTML for Googlebot (no JS required to read)
- Page title, og:title, and twitter:title unified to single consistent value
- `llms.txt` fallback content replaced with full product brief

### Fixed
- GitHub icon removed from primary CTA button on `Landing Page`
- Missing top padding in `Content` area when breadcrumbs are disabled
- Left `Sidebar` collapsible folders not opening when navigating via subheader links without full page reload
- `Copy Markdown` button no longer shown on pages without a workspace
- Translation toggle now enabled for preview admins on pages without a workspace
- `MCP Server` tab in admin panel now shows sign-in overlay in preview mode instead of raw content

### Security
- Added `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy` headers
- HSTS upgraded with `includeSubDomains` and `preload` directives

## 0.14.0 - 20.05.2026

### Improved
- Follow-up question suggestions after each AI response in `AI Chat`
- Animated "Thinking…" indicator while AI is generating a response in `AI Chat`
- Share and Copy as Markdown buttons, plus a Report Issue option in `AI Chat`
- Smoother entrance animations on the `AI Chat` welcome screen
- Source of Truth automatically enabled for Enterprise workspaces in `AI Chat`

### Removed
- DeepSearch and References toggles from `AI Chat` — simplified to core Q&A

## 0.13.0 - 18.05.2026

### Added
- Documentation graph indexing for AI agents in `Source of Truth` (Enterprise)
- Manual reindex button with 100 uses/month in `Source of Truth` (Enterprise)
- Source of Truth settings panel in `FloatWidget` (Enterprise)

### Fixed
- Reindex button now works correctly for logged-in users in `Source of Truth`

## 0.12.0 - 17.05.2026

### Added
- `/llms.txt` endpoint so AI crawlers can discover and understand your docs

### Fixed
- Special characters (e.g. `&`) now display correctly in the page outline
- Sidebar folder collapse/expand now works correctly

## 0.11.1 - 17.05.2026

### Improved
- Documentation content and sidebar now render on the server for faster load and better SEO

## 0.11.0 - 16.05.2026

### Added
- Header navigation links now translate to the active language

### Improved
- Interface language auto-detected from workspace settings — no URL prefix needed
- Enabling multiple languages at once is now significantly faster
- A loading banner appears while fresh translations are being prepared in the background

### Fixed
- Default theme now always applies when theme-switching widgets are disabled
- Sidebar labels translate instantly without requiring a page refresh
- English sidebar labels now work when switching back to English
- Previous/Next navigation buttons now show translated page names

## 0.10.0 - 15.05.2026

### Added
- Bring-your-own API key for OpenAI, Gemini, Anthropic, OpenRouter in `AI Agent` (Pro/Enterprise)
- Folder visibility toggles — hide specific folders from the sidebar in `Admin Panel`
- Per-theme accent, muted, and base color customization in `Branding`
- Live font preview — font names in the picker display in their actual typeface
- Accent color tinting on inline code, code blocks, and sidebar hover states
- MCP server for AI-assisted workspace administration via natural language

### Improved
- Subheader dropdown loads instantly — no more network requests on hover
- Ask AI, Search, and Language header buttons now have a unified consistent style
- Theme and Branding settings reorganized for clarity in `Admin Panel`
- Page feedback ratings moved into the Events section in `Analytics`

### Fixed
- Ask AI button styling now matches other header buttons
- Browser tab no longer shows duplicate workspace name on root page
- Favicon correctly shows custom workspace icon and uses accent color as background
- Images with relative paths now load correctly in documentation
- Subheader links navigate to correct translated pages when translations are active
- AI chat responses now appear in `Chats Analysis` analytics
- AI Agent settings always shows 3 question input fields
- Globe icon size and color now consistent in language picker
- Paddle checkout modal now opens correctly

## 0.8.2 - 13.05.2026

### Fixed
- Language code now inserts at the correct position in sidebar links
- Custom AI panel questions now load correctly from workspace settings
- Sidebar footer border no longer shows when all footer controls are hidden

## 0.8.1 - 12.05.2026

### Added
- FAQPage structured data for Google rich snippets on landing page

### Improved
- Language switching now instant — translation happens in the background with a loading indicator
- Hero image now uses Next.js optimized loading for faster page speed

### Fixed
- Sidebar dividers now only appear when there is content to separate
- Multi-line folder names in sidebar now left-align correctly
- Paddle script no longer blocks page render
- Landing page HTML structure and heading hierarchy corrected

## 0.8.0 - 11.05.2026

### Improved
- Live Preview replaced modal with a smooth inline animation experience

## 0.7.0 - 11.05.2026

### Added
- Custom background color support for individual header navigation links

## 0.6.0 - 10.05.2026

### Added
- Subheader navigation with folder tabs and hover dropdowns
- Heading anchor now copies full link URL to clipboard with a success toast

## 0.5.0 - 10.05.2026

### Added
- Open in Cursor IDE option in `Copy Page` dropdown
- Open in Windsurf IDE option in `Copy Page` dropdown

### Improved
- `Copy Page` button redesigned with modern styling and check icon feedback on copy

## 0.4.1 - 10.05.2026

### Improved
- Auto-detect button in Translation panel detects documentation language from README and updates language picker with native name and flag

## 0.4.0 - 10.05.2026

### Added
- Country flag icons in language switcher with native language names
- Background glow effect using accent color in `Theme Settings`
- Empty state page for users with no repositories after sign-in
- Getting started guide, GitHub editing instructions, Claude Code and VS Code guides in documentation

### Fixed
- Landing page mobile layout and hero section scaling
- Header and sidebar horizontal alignment on desktop

## 0.3.1 - 09.05.2026

### Added
- Double-clicking inline `code` now selects all content inside the backticks

### Improved
- Sidebar folders auto-expand and scroll to active page on nested pages

### Fixed
- Hamburger menu now toggles closed on second click
- Keyboard shortcut display shows `⌘ K` on Mac and `Ctrl K` on Windows/Linux
- Heading anchors now appear to the right on mobile to prevent text wrapping

## 0.2.3 - 09.05.2026

### Improved
- Syntax highlighting switched to native GitHub themes (light and dark)
- SEO Optimization upsell card now shows as a centered overlay with pricing details
- Translation tab layout — usage card moved above country stats
- Features cards on landing page now always show icon and description

### Fixed
- Sidebar stays fixed during scroll — no more jumping
- Mobile burger menu positioning and z-index corrected
- Page titles no longer include "| Docsbook" suffix
- Web Vitals analytics no longer produce CORS errors

## 0.2.0 - 08.05.2026

### Added
- System theme option — respects OS-level dark/light preference
- Theme dropdown picker in sidebar and header (Light / Dark / System)
- Per-plan monthly translation quotas with usage tracking and progress bar
- SEO panel — control search engine indexing, canonical URLs, and structured data
- Subdomain root page listing all user's documentation projects
- GitHub URL paste detection with a helpful redirect banner

### Improved
- Upgrade plan button styled with blue background for better visibility

### Fixed
- DeepSearch and References toggles now persist correctly
- AI panel no longer returns 403 when toggling DeepSearch/References
- GitHub rate limit errors eliminated — content now fetched from raw.githubusercontent.com
- `?preview=true` query string preserved on subdomain redirects
- AI Agent tab now loads with a single request instead of three

## 0.1.1 - 07.05.2026

### Added
- Scroll shadow on document outline to indicate scrollable content

### Improved
- Sidebar Language and Theme toggle button padding and visual style

### Fixed
- Pro plan features now accessible when workspace has an active Pro subscription
- Language switcher now visible to all visitors when enabled, even before languages are added

## 0.1.0 - 06.05.2026

### Added
- Mini analytics dashboard preview on landing page

### Fixed
- Custom workspace favicons now display correctly in browser tabs
- Inline badge images no longer break to new lines in documentation
- Subdomain authentication no longer blocks authorized users with 403 errors
