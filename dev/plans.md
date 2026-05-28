# Plans and capabilities

All plans are **lifetime** or **monthly** via Paddle. No limits on the number of repositories.

**Plan logic file:** `src/lib/plan-capabilities.ts`
**Constants (prices, limits):** `src/utils/constants.ts` — `proLifetime: 150`, `proPlusMonthly: 59`

## Free — $0 (forever)

| Category | Capabilities |
|---|---|
| Publishing | Any public GitHub repository |
| Branding | Name, icon, logo, colors (accent, muted, fg, bg for light/dark), Google Font |
| Theme | Default theme (light/dark/system), theme switcher |
| UI | Show/hide: header, search, copy button, prev/next, breadcrumbs, scroll-to-top, page feedback, edit on GitHub |
| Navigation | Header links (with colors), social links, folder tabs |
| Analytics | Last 24 hours: page views, visitors, top pages, referrers |
| MCP | All basic tools (create, branding, ui, navigation) |

## PRO — $150 one-time (lifetime)

Everything in Free, plus:

| Category | Capabilities |
|---|---|
| AI chat | 200 AI requests/month (beyond the limit: $0.01/request) |
| AI translation | 50 translations/month, 15 languages |
| Domain | Custom domain `docs.yourcompany.com` + free SSL |
| SEO | Meta tags, sitemap, OpenGraph, JSON-LD |
| GEO | TL;DR block, dateModified, Person/Author in JSON-LD, semantic HTML — for Perplexity, ChatGPT Search, Google AI Overviews |
| AEO | Auto-markup FAQPage / HowTo / speakable from markdown — for featured snippets and voice assistants |
| Analytics | 7 / 14 / 30 days (instead of only 24h) |
| MCP | `update_ai_settings`, `update_seo`, `update_geo`, `update_aeo`, `update_domain`, `update_languages` |

## PRO+ — $59/month

Everything in PRO, plus:

| Category | Capabilities |
|---|---|
| White-label | Remove "Powered by Docsbook" |
| AI chat | 2000 AI requests/month |
| AI translation | 500 translations/month |
| MCP | `get_chat_system_prompt`, `set_chat_system_prompt`, `set_chat_hooks`, `test_chat_hook`, `set_translation_mode`, `upload_translation`, `approve_translation`, `delete_translation` |

---

## Features by section

### GitHub integration
- Support for `README.md` and `docs/` folders in the repository
- Automatic sync on push to main
- No CI/CD, no GitHub Actions, no configuration
- Authorization via GitHub OAuth

### AI chatbot
- Trained on the specific documentation content
- Document search (tool calls: Search → Reading → Answer)
- Configurable suggested questions
- Custom AI provider and API key (OpenAI, Gemini, Anthropic, OpenRouter)
- Real-time response streaming
- Usage counter + plan-based limits
- Landing metric: "847 deflected tickets this month"

### AI translations
- **15 languages:** EN, ES, FR, DE, PT, IT, RU, ZH, JA, KO, AR, HI, TR, PL, NL
- Each language version is indexed by Google separately
- Language switcher in the sidebar or header
- Automatic user language detection
- Translation via OpenRouter / custom provider

### Branding and design (Free)
- Custom site name
- Icon (favicon) and logo
- Accent color (light + dark)
- Muted color (light + dark)
- Foreground / Background (light + dark)
- Custom Google Font
- Default theme: light / dark / system
- Background glow effect

### UI settings (Free)
Enable/disable page components:
- Search button, Search in sidebar
- Copy page button
- Prev / Next navigation
- Breadcrumbs
- Scroll to top
- Page feedback (thumbs up / down)
- Edit on GitHub
- AI button, AI header, AI outline, Copy markdown
- Ask AI on selection — floating bubble when text is selected, 1 click sends the fragment to AI Chat
- Language toggle (sidebar / header)
- Theme toggle in header

### Navigation (Free)
- Header links with custom colors
- Social links: GitHub, Discord, Twitter
- Folder tabs — tabs per repository folder

### SEO (PRO)
- Automatic meta tags (`<title>`, `<description>`, `<og:*>`)
- Sitemap.xml
- OpenGraph / Twitter cards
- JSON-LD: WebSite, Organization, SoftwareApplication, TechArticle, BreadcrumbList
- Canonical URLs
- Separate SEO indexing for each language version

### GEO — Generative Engine Optimization (PRO)
Toggle in the admin panel `SEO / GEO`. When enabled:
- **TL;DR block** at the top of each page — from `tldr:` in frontmatter or auto-extracted from the first paragraph. Rendered as `<aside class="tldr" role="note">` for AI parsers.
- **Visible update date** at the bottom of the article with `<time dateTime="...">` tag — taken from the last git commit of the file.
- **Person/Author in JSON-LD TechArticle** — from `author:` / `authorUrl:` in frontmatter or fallback to the last git author.
- **Semantic HTML** — `<article>`, `role="note"` on TL;DR.

Goal: getting cited by Perplexity, ChatGPT Search, Google AI Overviews, and Claude. See [`docs/content/features/geo.md`](../content/features/geo.md).

### AEO — Answer Engine Optimization (PRO)
Toggle in the admin panel `SEO / GEO`. When enabled:
- **FAQPage JSON-LD** automatically from `## FAQ` sections and `### Question?` headings.
- **HowTo JSON-LD** automatically from `## How to ...` with a numbered list — each item → `HowToStep`.
- **Speakable markup** in TechArticle — selectors for voice assistants (`.tldr`, first paragraph, H1).

Goal: featured snippets, People Also Ask, voice assistants (Google Assistant, Alexa). See [`docs/content/features/aeo.md`](../content/features/aeo.md).

### AI discovery: llms.txt and llms-full.txt
`llms.txt` files (standard for AI agents and AI search engines — Perplexity, ChatGPT Search, Cursor, Cline) are generated automatically:

| Level | URL | What it returns |
|---|---|---|
| Docsbook (product) | `docsbook.io/llms.txt`, `docsbook.io/llms-full.txt` | Description of the platform itself and navigation |
| Each workspace | `docsbook.io/[user]/llms.txt`, `docsbook.io/[user]/llms-full.txt` | Structured list of documentation pages for the repo/user |

**Files:**
- `src/lib/generate-llms-txt.ts` — generation for the platform
- `src/lib/generate-workspace-llms-txt.ts` — generation for workspace (reads the documentation graph)
- `src/app/llms.txt/route.ts`, `src/app/llms-full.txt/route.ts` — platform endpoints
- `src/app/[user]/llms.txt/route.ts`, `src/app/[user]/llms-full.txt/route.ts` — workspace endpoints

Available on all plans (including Free) — this is the primary discovery surface for AI agents.

### Custom domain (PRO)
- `docs.yourcompany.com` — any subdomain
- Automatic SSL (via Vercel)
- Management via Vercel API (`addDomain` / `removeDomain`)
- Files: `src/utils/vercel/`

### Web Vitals and event tracking
- `src/components/WebVitals.tsx` collects Core Web Vitals (LCP, INP, CLS, FCP, TTFB) and sends them to `/api/vitals`
- `src/app/api/events/route.ts` — server-side reception of custom events from the landing page and dashboard
- `TrackClick`, `LandingAnalytics` (`src/components/analytics/`) — client-side trackers
- All events are sent to Axiom, accessible via MCP tool `query_events` (PRO+)
- For drill-down on a single visitor — `get_top_visitors` (entry point) → `get_visitor_activity` (full timeline). Visitor is identified by a stable `visitor_id` = `sha256(VISITOR_ID_SALT + repoFullName + ip)`. Raw IPs are not returned via MCP. Env var: `VISITOR_ID_SALT` (required in production)

### Onboarding flow
- `/connect` — GitHub OAuth sign-in
- `/start` — creating the first workspace (choosing a repository from a list)
- `/no-projects` — empty state when there are no workspaces
- `/success` — after a successful Paddle checkout (trigger Confetti + plan update)
