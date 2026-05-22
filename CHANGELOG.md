# Releases

## 0.15.0 - 22.05.2026

### Added
- `Get Support` tab in admin panel with email, Discord, and Twitter contacts
- Email support link in landing `Footer` for quick access to `support@docsbook.io`
- `SoftwareApplication` structured data schema on `Landing Page` for AI search visibility
- `llms-full.txt` endpoint with complete product brief for AI crawlers
- Explicit allow rules for GPTBot, ClaudeBot, PerplexityBot, Google-Extended in `robots.txt`
- Events webhook endpoint in `API` for receiving real-time workspace events

### Fixed
- `Preview mode` Connect GitHub button now redirects to main domain `/connect` instead of subdomain path

### Added
- Confetti animation on `/success` page after successful payment via `canvas-confetti`

### Improved
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
