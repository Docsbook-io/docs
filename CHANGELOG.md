---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, fixes, and improvements to the AI-powered documentation platform shipped across every version."
---

# Releases

## 0.18.1 - 24.05.2026

### Added
- Simplified install/use guide on each skill page `/skills/[name]` — tabs for 7 AI clients (Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, Copilot), two steps (Install + Use) with the command pre-filled for this specific skill, plus a runtime-discovery block via Docsbook MCP

### Changed
- Moved "Get Support" out of the admin sidebar — replaced the bulky "Help & Support" section with a subtle "Need help? Contact support" footer link pinned to the bottom of the settings modal sidebar, freeing vertical space

## 0.18.0 - 24.05.2026

### Added
- Install snippets for 8 AI clients on `/mcp` — interactive selector with tabs for Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, GitHub Copilot (VS Code), and ChatGPT; each one shows its own command or config (bash/JSON/TOML) with filename and optional install steps
- Expanded the `Install in your AI client` section in [docs/ai/mcp](./ai/mcp.md) from a single Claude snippet to 8 subsections — one per client

## 0.17.5 - 24.05.2026

### Fixed
- Mobile adaptation for `/mcp` promo page — Hero `pt-28` reduced to `pt-20` on mobile, H1 base set to `text-3xl`, endpoint URL no longer overflows the screen
- `CopyCommand` on mobile — reduced padding/height, font-size scaled down, long install command no longer breaks the layout
- `AiClientsRow` — `gap-x-5` on mobile (was 9) so client icons line up more evenly at 375px
- `PromptsFilters` — category/plan selects use `grid-cols-2` on mobile instead of a single row; prompt row padding reduced, prompt text set to `13px` on mobile

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
