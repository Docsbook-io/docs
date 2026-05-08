# Releases

## 0.2.1 - 08.05.2026

- Fixed `DeepSearch and References toggles` — admin panel settings now correctly persist and hide/show the AI mode buttons in the documentation
- Fixed `AI panel 403 error` — toggling DeepSearch/References in admin settings no longer returns "Starter or Pro required" error

## 0.2.0 - 08.05.2026

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