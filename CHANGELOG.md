# Releases

## 0.2.3 - 09.05.2026

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