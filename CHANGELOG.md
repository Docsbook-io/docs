# Releases

## 0.13.0 - 18.05.2026

- Added `Source of Truth documentation graph` (Enterprise) — new MCP server feature for Enterprise plan that indexes documentation structure and relationships; AI agents can query `get_doc_graph` to find affected pages when code changes, improving documentation consistency across large projects
- Added `documentation reindexing endpoint` — new `reindex_doc_graph` MCP tool with 100 reindexes per month for Enterprise; users can manually rebuild the documentation graph from GitHub repository via FloatWidget or API
- Added `Source of Truth settings panel` — new enterprise-only tab in FloatWidget showing MCP server URL, last indexation time, reindex usage, and reindex button; non-Enterprise workspaces see upgrade modal when attempting to enable

## 0.12.0 - 17.05.2026

- Added `llms.txt generation` for AI model discovery — `/llms.txt` endpoint now dynamically generates a structured file containing full documentation sitemap, feature descriptions, and guidelines for AI models and LLM crawlers; helps AI systems understand Docsbook documentation structure when indexing
- Fixed `HTML entities in outline headings` — ampersand and other symbols in headings now display correctly in the Outline (table of contents) instead of showing encoded entities like `&#x26;`
- Fixed `sidebar folder collapse interaction` — folder toggle buttons in the documentation sidebar now respond to clicks and properly collapse/expand subfolders; added client-side JavaScript to handle folder state toggling for SSR-rendered sidebar tree

## 0.11.1 - 17.05.2026

- Improved `documentation content SSR` — article HTML now renders on the server using `dangerouslySetInnerHTML` instead of being injected client-side, ensuring markdown content is present in the initial page HTML for search engines and faster First Contentful Paint
- Added `server-side sidebar tree rendering` in documentation — navigation sidebar now renders as static HTML on the server via new `SidebarTree` component; sidebar links and folder structure are included in SSR response instead of being built on the client, improving page speed and SEO

## 0.11.0 - 16.05.2026

- Improved `i18n language auto-detection` in documentation — when workspace language is auto-detected as non-English, UI strings now load in the detected language by default instead of always showing English; visitors see fully localized interface without requiring a URL language prefix
- Fixed `theme override when toggles disabled` in documentation — when theme switching widgets are disabled in both sidebar and header, the admin-configured default theme now always applies instead of allowing `localStorage` to override it with previously selected values
- Improved `parallel translation indexing` in admin settings — when activating multiple languages simultaneously, all languages now index in parallel using `Promise.all` instead of sequentially, significantly reducing setup time
- Improved `stale translation content handling` — when documentation content updates on GitHub, users see a loading popup over the cached translation while the fresh version indexes; ensures transparent indication that an update is in progress instead of silently serving stale content
- Fixed `sidebar translation updates` — sidebar labels now translate immediately on the client side when cached, no longer requiring a page refresh to display translated navigation labels
- Fixed `English language sidebar labels` in documentation — when users explicitly select English from the language widget, sidebar navigation labels now correctly translate to English instead of staying in the original language; the client-side translation hook now handles English as a target language along with other languages, ensuring consistent behavior whether using server cache or on-demand translation
- Added `header navigation links translation` in documentation — custom navigation links (headerLinks) in documentation header now translate to active language using cached translation logic, same as sidebar labels; subheader folder tabs and "Overview" label also now localize when language is active
- Fixed `prev/next button page names` in documentation — Previous/Next navigation buttons now display translated page names when language is active instead of showing original language titles; `translatedLabels` prop now correctly passed to PageNav component

## 0.10.0 - 15.05.2026

- Improved `subheader dropdown performance` in documentation — pre-compute folder contents from available files list to eliminate hover-triggered API requests; dropdown now loads instantly without network latency
- Fixed `Ask AI button styling` — button now uses consistent styling matching the Copy Page button with rounded corners, proper padding, and updated hover state
- Fixed `browser tab title on root page` — when viewing workspace root documentation, the page title now shows just the workspace name instead of duplicating it (e.g., "agentctl" instead of "agentctl — agentctl")
- Fixed `favicon background color` — workspace favicon now uses the configured `accentColor` when available, falling back to generated color based on repository name for consistent branding
- Fixed `workspace icon favicon` — favicon now correctly displays the workspace's custom icon when configured instead of showing the letter fallback; added cache busting and improved content-type validation for external icon URLs
- Added `bring-your-own-api-key` for AI features — Pro/Enterprise users can now configure custom API keys from OpenRouter, OpenAI, Google Gemini, or Anthropic in the AI Agent admin panel; replaces "Extra Usage" feature; custom keys bypass platform usage limits and allow selecting any model from the provider
- Fixed `relative image paths` in documentation — image sources with relative paths (e.g., `./public/favicon.svg`, `../assets/image.png`) now properly resolve to correct GitHub Raw URLs instead of creating malformed paths; path normalization handles `./` and `../` segments correctly across all documentation files
- Fixed `HTML img tags with relative src` in markdown — images embedded as HTML tags (e.g., `<img src="public/logo.png">`) now correctly resolve to GitHub Raw URLs instead of remaining as relative paths that fail to load
- Added `folder visibility toggles` in left sidebar admin panel — workspace owners can now control which top-level folders appear in the documentation sidebar; hidden folders are automatically excluded from Previous / Next page navigation for a cleaner navigation experience
- Fixed `AI Agent scroll shadow` in admin panel — bottom fade-out gradient indicator now correctly disappears when content is fully visible and scrolled to the bottom
- Fixed `subheader links with enabled translations` — when a translation is enabled in the admin panel, subheader tabs and dropdown menu links now correctly navigate to translated pages instead of the original language version
- Reorganized `theme and branding settings` in admin panel — merged Theme tab into Branding section, moved Default Theme and Background Glow toggles under Branding, relocated Remove Branding setting to Left Sidebar tab for clearer UI structure
- Consolidated `page feedback analytics` into Events section — removed standalone Page Feedback block; page ratings (thumbs up/down) now appear as collapsible "Page Rates" group in the main Events dashboard
- Fixed `AI chat analytics in Chats Analysis` — AI responses now properly populate in the analytics table instead of showing empty; tracking logs the full response text after streaming completes so that response content is visible in the Chats Analysis dashboard
- Fixed `custom questions inputs` in AI Agent settings — admin panel now always displays exactly 3 question input fields even when fewer are saved, ensuring consistent form layout and allowing users to add or edit questions without reloading
- Fixed `globe icon styling` in language picker — globe icon now matches flag icon size (16px) and inherits text color for visual consistency in the sidebar footer widget
- Fixed `Paddle checkout initialization` — payment modal now opens correctly when triggered; moved Paddle script to provider component with `onLoad` callback instead of relying on `lazyOnload` strategy to ensure script is fully loaded before initialization
- Added `per-theme color customization` in Branding panel — workspace owners can now configure separate accent, muted, and base colors for light and dark themes; Colors card includes Light/Dark toggle synced to documentation theme; Accent Color remains consistent across themes for brand continuity
- Added `live Google Font preview` in font picker — font names in the dropdown now display using their actual typeface, giving users a visual preview before applying to documentation; dynamically loads font stylesheets to show typography examples
- Added `accent color tinting` across documentation UI — inline code, fenced code blocks, kbd shortcuts, and sidebar item hover states now subtly tint with the workspace accent color (4-12% opacity) for visual cohesion with brand settings
- Improved `header button consistency` in documentation — Ask AI, Search, and Language buttons now use unified transparent background (`bg-muted/20 hover:bg-muted/50`) across both light and dark themes for a polished, cohesive appearance
- Added `MCP server for AI-powered workspace administration` — new HTTP endpoint at `/api/mcp/server` lets AI assistants (Claude, etc.) administer workspaces via natural language; includes 13 tools for branding, UI, navigation, AI, SEO, domain, translation, and analytics management; features OAuth-style browser auth flow, plan-gating with structured upgrade hints, and Bearer token persistence
- Fixed `z-index stacking in sidebar dropdown` — sidebar active page highlight no longer overlaps with subheader dropdown menu; adjusted z-index layering so dropdown content renders on top
- Fixed `AI panel z-index over live preview popup` — AI panel now appears above the "Connect GitHub to publish" popup when opening live preview, ensuring users can interact with the panel while preview modal is displayed

## 0.8.2 - 13.05.2026

- Fixed `sidebar links with active subheader` — when a subheader folder was active, language switcher now correctly inserts language code before the repo segment instead of inside the subfolder path (e.g. `/ru/docs/analytics` instead of `/docs/ru/analytics`)
- Fixed `custom AI panel questions` — workspace admin settings now properly load and display custom suggested questions in the AI panel instead of showing default questions
- Fixed `sidebar footer border visibility` — footer border and spacing no longer display when all footer controls (language picker, theme toggle) are hidden or disabled and badge is not shown

## 0.8.1 - 12.05.2026

- Fixed `sidebar dividers` — left sidebar divider now hides when no footer controls or badge are present; right sidebar divider only shows when outline (table of contents) has content above it
- Fixed `document translation hang` — language switching now returns instantly with original text while translation happens in background; removed blocking LLM calls from render path for both page HTML and sidebar labels; added loading spinner to language picker button and "indexing" banner that shows during background translation
- Fixed `sidebar text alignment` — multi-line folder names in the left sidebar now align to the left instead of centering when text wraps across multiple lines
- Added `FAQPage rich snippet` in landing page — structured data schema for FAQ section helps Google display Q&A snippets directly in search results
- Improved `hero image performance` in landing — replaced plain `<img>` with `next/image` for automatic WebP conversion, preloading, and proper lazy-loading; reduces LCP time on landing page
- Fixed `Paddle script loading` in landing — moved from synchronous head script to `next/script lazyOnload` strategy to prevent blocking page render; payment modal still works normally when needed
- Fixed `landing page HTML structure` — moved `<WebVitals>` component inside `<body>` for valid HTML document structure
- Fixed `landing page heading hierarchy` — corrected section subheadings from `<h3>` to `<h2>` ("GitHub to DocsBook", "Your docs, delivered") for proper semantic structure and SEO

## 0.8.0 - 11.05.2026

- Improved `Live Preview UX` — replaced modal popup with an animated inline experience; clicking "Live Preview" blurs the background and smoothly animates the input to center with three example doc cards appearing below with staggered animation; clicking outside or pressing Escape closes the overlay

## 0.7.0 - 11.05.2026

- Added `header link colors` — navigation links now support optional background color customization; users can assign unique colors to individual header links (e.g., CTA buttons like "Get Started") with automatic text color contrast (white/black) for readability; existing links without color display as before

## 0.6.0 - 10.05.2026

- Improved `heading anchors` — replaced text "#" symbol with SVG link icon, added copy-to-clipboard functionality that copies the full heading link URL on click, and displays success toast notification "Ссылка скопирована"; URL hash updates automatically in browser address bar, improving documentation sharing and navigation experience
- Added `subheader navigation` — new sub-header displays 1-level folder tabs below the main header with optional hover menus for nested content; includes "Overview" tab and accent color styling with active page indicators, improving navigation for multi-section documentation

## 0.5.0 - 10.05.2026

- Redesigned `Copy Page button` — updated with modern styling including improved padding, border-radius, and hover states for a more polished UI
- Added `visual feedback on copy` — shows Check icon instead of text when content is copied to clipboard, providing instant feedback
- Enhanced `dropdown menu styling` — improved typography, spacing, and hover states throughout the copy options menu
- Added `Cursor IDE support` — new dropdown option to open documentation pages directly in Cursor IDE
- Added `Windsurf IDE support` — new dropdown option to open documentation pages directly in Windsurf IDE
- Improved `dropdown arrow icon` — replaced inline SVG with ChevronDown icon from lucide-react for consistent icon styling

## 0.4.1 - 10.05.2026

- Added `auto-detect default language` — new "Auto-detect" button in Translation panel uses AI language detection to analyze repository README and determine documentation language; updates language picker to show detected language name and flag instead of generic "Language" label, improving UX for non-English documentation
- Improved `language picker UX` — when default language is detected, it displays native language name (e.g., "Русский" for Russian) and corresponding flag instead of globe icon, giving readers immediate clarity about documentation language

## 0.4.0 - 10.05.2026

- Added `flag icons` to language switcher — replaced emoji and globe icon with circular SVG country flags in sidebar and header language pickers; dropdown now shows native language names (Español, Français, 日本語, etc.) for a more recognizable and polished UX
- Added `background glow effect` — new customization option to add a soft radial gradient glow around documentation content using the workspace accent color, creating a modern polished appearance similar to popular SaaS products; available in Theme settings when accent color is configured
- Added `empty projects state` — users with no accessible repositories after signing in are now redirected to a dedicated onboarding page with step-by-step instructions
- Added `getting started guide` in documentation — comprehensive guide for creating first documentation project including options to create new or fork example repositories
- Added `GitHub editing instructions` — users can now edit documentation directly on GitHub web interface with step-by-step instructions for creating, editing, and deleting files
- Added `Claude Code section` — guide for using Claude Code to edit documentation with AI assistance; includes instructions for staging and committing changes with git
- Added `VS Code local editing guide` — complete setup and workflow instructions for editing documentation locally with recommended extensions (Markdown All in One, Prettier, Spell Checker)
- Improved `repository selection flow` — ConnectPicker now shows helpful empty state when no repositories available, with link to create new repository on GitHub
- Fixed `landing page mobile layout` — hero section gradient shards now adapt to mobile viewport; hero heading size increased for mobile readability; tab switcher made more compact on small screens; gradient blocks now extend properly to edges on mobile without overflow issues
- Fixed `navigation header sidebar alignment` — header now adds left padding on desktop to match sidebar width, preventing horizontal misalignment between header and content; sidebar and header are visually aligned on lg+ breakpoint

## 0.3.1 - 09.05.2026

- Fixed `burger menu toggle` — hamburger button in the navigation header now closes the sidebar when clicked again instead of only opening it; users can now dismiss the mobile menu by clicking the burger icon, improving mobile navigation UX
- Improved `sidebar navigation` in `nested documentation` — folders now automatically expand when visiting a nested page, and the sidebar scrolls to keep the active page in view; provides better UX when navigating deeply nested documentation structures
- Fixed `search widget shortcut display` — now shows `⌘ K` on macOS and `Ctrl K` on Windows/Linux instead of always displaying the Command symbol; keyboard handler already supported both modifiers, but the UI now correctly reflects the appropriate shortcut for each platform
- Added `inline code selection` — double-clicking on inline `code` now selects all content within the backticks instead of selecting a single word; improves copy-to-clipboard workflow for developers reading code examples
- Fixed `heading anchors on mobile` — anchor symbols (#) now display to the right of headings instead of on the left, preventing text wrapping issues on small screens; anchors are more visible on mobile (60% opacity) and less intrusive on desktop (hover-only)

## 0.2.3 - 09.05.2026

- Fixed `sidebar jumping during scroll` — removed conflicting fixed positioning constraints (top/bottom) on desktop layout so sticky positioning works correctly when navigation header is enabled; sidebar now stays in place during scrolling
- Fixed `mobile burger menu` — hamburger button now correctly positioned on top-right when header is present and uses proper z-index layering; menu opens/closes smoothly with improved accessibility and visual feedback
- Fixed `documentation page titles` — removed "| Docsbook" suffix from public documentation page titles to improve user branding; customizable workspace names now display cleanly in browser tabs without Docsbook attribution
- Fixed `web-vitals analytics` — removed incorrect next-axiom rewrite that generated invalid Axiom endpoints; web-vitals are now collected via server-side API route, eliminating CORS errors on landing page and 404s on workspace subdomains
- Improved `SEO Optimization upsell card` in `admin panel` — when SEO is disabled, shows a centered overlay card with pricing details (Available for free), Learn More link, and Enable button; background content dims to 30% opacity to emphasize the card
- Improved `Translation tab layout` in `admin panel` — moved Translation Usage card above Visitor Countries and Language Countries sections for better information hierarchy
- Improved `code syntax highlighting` in `documentation` — switched from CSS color-remap hack to native dual-theme support (github-light for light mode, github-dark for dark mode), delivering native GitHub syntax colors with proper token highlighting in both themes
- Fixed `feedback button icons` in `documentation outline` — added shrink-0 to prevent icon collapse when button text wraps on long translations
- Fixed `Language Countries upgrade overlay` in `Translation panel` — overlay with lock icon and upgrade prompt now always visible by default instead of only appearing on hover; added scale animation on hover to clearly indicate clickability
- Improved `Features cards` in `landing page` — replaced complex hover-reveal pattern with always-visible icon and description for better information discoverability

## 0.2.0 - 08.05.2026

- Added `system theme option` — theme pickers now show three choices (Light, Dark, System) instead of a simple toggle; System respects the visitor's OS-level dark/light preference
- Added `theme dropdown pickers` — replaced theme toggle button with a dropdown menu in both the sidebar footer and top navigation header
- Added `auto-translation limits` — per-plan monthly page translation quotas in `admin panel`: Free 30 pages/mo, Pro 300 pages/mo, Enterprise unlimited
- Added `translation usage tracking` — batch and on-the-fly page translates now count toward monthly limit (+1 per page, not per chunk); limit resets monthly like AI queries
- Added `Auto-translation limit bar` in `admin analytics` — shows current usage alongside AI query limits in a violet-colored progress bar with monthly reset date
- Added `SEO Optimization panel` — admin can enable/disable search engine indexing; when enabled, robots meta allows indexing, canonical URLs and structured JSON-LD are included, and search engine crawling is activated
- Fixed `DeepSearch and References toggles` — admin panel settings now correctly persist and hide/show the AI mode buttons in the documentation
- Fixed `AI panel 403 error` — toggling DeepSearch/References in admin settings no longer returns "Starter or Pro required" error
- Added `subdomain root page` — when opening `user.docsbook.io/` without a repo, shows a list of all user's documentation projects, or auto-redirects if only one repo exists
- Added `GitHub URL paste detection` — detects when users paste GitHub URLs incorrectly (e.g., `docsbook.io/https://github.com/user/repo`) and guides them with a helpful banner to use the correct format
- Improved `Upgrade plan button` — styled with blue background (#0967ff) and white text in the admin toolbar for better visibility
- Fixed `GitHub rate limit errors` — file content is now fetched from `raw.githubusercontent.com` (no rate limit, CORS-safe) instead of the GitHub REST API, eliminating 404s for visitors when the server IP hits the anonymous request cap; added `GITHUB_TOKEN` env fallback and Next.js cache for tree and branch lookups
- Fixed `preview mode query string` — `?preview=true` parameter is now preserved when redirecting from main domain to subdomain, allowing preview modals to display correctly in production
- Fixed `AI Agent tab API calls` — reduced redundant requests by consolidating three separate data fetches into a single request, improving load performance when opening the admin panel's AI Agent settings

## 0.1.1 - 07.05.2026

- Add smooth shadows for the document outline to show if scrolling is available
- Enhance padding bottom layout for both side bars
- Enable Bot Protection for server side of every docs
- Enhance left sidebar Language, Theme Toggle buttons styles to be less rounded and adjust padding for better visual consistency
- Fixed `Pro features in admin panel` — Pro plan features are now properly accessible when the workspace has a Pro subscription, regardless of the user's account plan
- Fixed `language switcher visibility` — widget now appears for all visitors whenever enabled in header or sidebar settings, even when no languages have been added yet

## 0.1.0 - 06.05.2026

- Enhanced `landing analytics cell` — replaced static bar chart mock with a mini dashboard preview showing Visitors, Page Views, a line chart, and Pages/Referrers tables
- Enhanced `landing analytics cell` — added bottom fade-out gradient overlay for a smooth cut-off effect on the dashboard preview
- Fixed `workspace favicons` — custom workspace icons now display correctly in browser tabs instead of showing the default favicon
- Fixed `badge images` — inline badge images in documentation prose now render horizontally in a single line instead of breaking to new lines
- Fixed `subdomain authentication` — authorized users can now access documentation on subdomains without encountering 403 errors