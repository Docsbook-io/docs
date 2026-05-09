# Releases

## 0.4.0 - 10.05.2026

- Added `empty projects state` — users with no accessible repositories after signing in are now redirected to a dedicated onboarding page with step-by-step instructions
- Added `getting started guide` in documentation — comprehensive guide for creating first documentation project including options to create new or fork example repositories
- Added `GitHub editing instructions` — users can now edit documentation directly on GitHub web interface with step-by-step instructions for creating, editing, and deleting files
- Added `Claude Code section` — guide for using Claude Code to edit documentation with AI assistance; includes instructions for staging and committing changes with git
- Added `VS Code local editing guide` — complete setup and workflow instructions for editing documentation locally with recommended extensions (Markdown All in One, Prettier, Spell Checker)
- Improved `repository selection flow` — ConnectPicker now shows helpful empty state when no repositories available, with link to create new repository on GitHub
- Fixed `landing page mobile layout` — hero section gradient shards now adapt to mobile viewport; hero heading size increased for mobile readability; tab switcher made more compact on small screens; gradient blocks now extend properly to edges on mobile without overflow issues

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