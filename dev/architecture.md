# Architecture — src/ structure

## File tree

```
src/
├── app/
│   ├── page.tsx                          # Landing page (Hero, Features, BentoFeatures, FAQ, CTA, Footer)
│   ├── layout.tsx                        # Root layout + Providers + WebVitals
│   ├── opengraph-image.tsx               # Dynamic OG for the homepage
│   ├── twitter-image.tsx                 # Dynamic Twitter image
│   ├── sitemap.ts, robots.ts             # SEO infrastructure
│   ├── llms.txt/, llms-full.txt/         # Platform-level AI discovery
│   ├── [user]/[repo]/[[...path]]/        # Public documentation viewer
│   ├── [user]/llms.txt, llms-full.txt    # Workspace-level AI discovery
│   ├── mcp/                              # MCP server promo landing (/mcp)
│   │   ├── page.tsx                      #   Hero + chat mockup + install snippets
│   │   ├── authorize/                    #   OAuth Authorization Code flow UI
│   │   └── _components/                  #   CopyCommand, AiClientsRow
│   ├── skills/                           # docs-skills marketing catalog (SSG)
│   │   ├── page.tsx                      #   List with filters
│   │   └── [name]/page.tsx               #   SKILL.md detail page
│   ├── connect/                          # GitHub OAuth sign-in
│   ├── start/                            # Onboarding (creating the first workspace)
│   ├── no-projects/                      # Empty state
│   ├── success/                          # Successful Paddle checkout
│   ├── docs-proxy/                       # Proxy for custom domains
│   ├── privacy/, terms/, licenses/       # Legal pages
│   ├── .well-known/                      # OAuth metadata endpoints
│   │   ├── oauth-authorization-server/
│   │   └── oauth-protected-resource/
│   └── api/
│       ├── mcp/server/                   # MCP server (OAuth + ~40 tools)
│       ├── ai-chat/                      # AI chat on documentation (streaming)
│       ├── ai-title/                     # AI title generation
│       ├── translate/, translations/     # AI translation + CRUD translations
│       ├── detect-default-language/      # franc-based user language detection
│       ├── workspaces/                   # CRUD workspaces
│       ├── paddle/                       # Paddle webhooks + checkout
│       ├── analytics/                    # Axiom analytics
│       ├── search/, search-index/        # Documentation search
│       ├── events/                       # Server-side event tracking
│       ├── vitals/                       # Web Vitals endpoint
│       ├── md/                           # Raw markdown by path
│       ├── docs/                         # Workspace content access
│       ├── webhooks/, webhook-deliveries/# Webhook registry + history
│       ├── google-fonts/                 # Google Fonts API proxy
│       ├── cron/stale-check/             # Cron: stale pages check
│       ├── auth/                         # next-auth v5 (GitHub OAuth)
│       ├── axiom/, _axiom/               # Axiom logging
│       └── github/                       # GitHub API integration
│
├── components/
│   ├── landing/                          # Hero, Features, BentoFeatures, FAQ,
│   │                                     #   CtaBand, SocialProof, Footer, Header,
│   │                                     #   AiSupportsLogos, GitHubHintBanner,
│   │                                     #   PreviewModal
│   ├── docs/                             # DocsLayout, AiPanel, AiReferenceCard,
│   │                                     #   Content, DocHeader, Outline, PageNav,
│   │                                     #   Sidebar, SidebarTree, SearchBar,
│   │                                     #   PricingModal, PoweredBadge,
│   │                                     #   PreviewConnectBanner, WorkspaceColorInjector
│   ├── analytics/                        # DocsAnalytics, AiUsagePanel,
│   │                                     #   LandingAnalytics, OwnApiKeySection, TrackClick
│   ├── ai/                               # reasoning.tsx, shimmer.tsx
│   ├── seo/JsonLd.tsx                    # JSON-LD blocks
│   ├── ui/                               # shadcn/ui primitives
│   ├── animate-ui/                       # Motion wrappers
│   ├── icons/                            # SVG icons
│   ├── FloatWidget.tsx                   # Main dashboard — 15 tabs: analytics, ai-agent,
│   │                                     #   domain, languages, branding, left-sidebar,
│   │                                     #   right-sidebar, header, content, seo, pricing,
│   │                                     #   mcp, skills, webhooks, support
│   ├── webhooks/WebhooksPanel.tsx        # CRUD subscriptions, delivery history, replay, test
│   ├── ai/SystemPromptSection.tsx        # System prompt for AI chat (PRO)
│   ├── ai/ChatHooksSection.tsx           # pre/post/streaming hook URLs (PRO+)
│   ├── translations/TranslationModeSection.tsx
│   ├── translations/PendingTranslationsList.tsx
│   ├── mcp/SourceOfTruthControls.tsx     # Reindex now + 100/month counter
│   ├── PaddleCheckout.tsx                # Paddle overlay checkout
│   ├── PaddleQueryHandler.tsx            # Handling ?paddle_* query params
│   ├── *UpgradeModal.tsx                 # AiUpgradeModal, ProUpgradeModal,
│   │                                     #   EventsUpgradeModal, SourceOfTruthUpgradeModal
│   ├── TranslationLanguagesModal.tsx     # Workspace language management
│   ├── ConnectPicker.tsx                 # GitHub repository selector
│   ├── Confetti.tsx                      # Success animation
│   ├── WebVitals.tsx                     # Core Web Vitals collection
│   ├── FlagIcons.tsx                     # Country/language flags
│   ├── Providers.tsx, theme-provider.tsx # Context providers
│   └── analytics-mocks.tsx               # Analytics mocks for landing page
│
├── lib/
│   ├── plan-capabilities.ts              # Plan-based access logic
│   ├── source-of-truth.ts                # Documentation graph indexing
│   ├── mcp-auth.ts                       # MCP authentication (OAuth + Bearer)
│   ├── webhook-dispatcher.ts             # Webhook delivery (HMAC + retry)
│   ├── webhook-worker.ts                 # Worker with exponential backoff
│   ├── dispatch-event.ts                 # Type-safe wrapper + Zod event schemas
│   ├── generate-llms-txt.ts              # llms.txt for the platform
│   ├── generate-workspace-llms-txt.ts    # llms.txt for workspace
│   ├── skills/find.ts                    # find_skill MCP tool (Redis cache + etag)
│   ├── skills-index.ts                   # index.json loading for /skills
│   ├── redis.ts                          # ioredis client
│   ├── axiom/                            # Axiom helpers
│   └── utils.ts                          # cn() and shared helpers
│
├── db/schema.ts                          # Drizzle DB schema (users, workspaces,
│                                         #   mcp_tokens, mcp_auth_codes, payments,
│                                         #   indexed_repos, webhook tables)
│
└── utils/
    ├── constants.ts                      # Prices, limits, languages, APP_URL
    ├── vercel/                           # addDomain / removeDomain (Vercel API)
    ├── translation/                      # AI translation logic
    ├── ai/                               # AI providers (OpenRouter/OpenAI/Gemini/Anthropic)
    ├── paddle/                           # handleWebhook, checkout
    └── analytics/                        # Event logging
```

## How it works

1. User signs in via GitHub OAuth (`next-auth`)
2. Creates a workspace — specifies `owner/repo`
3. Docsbook indexes the repository via GitHub API
4. Documentation site is available at `docsbook.io/owner/repo`
5. On push to main → automatic update
6. Workspace settings (branding, AI, domain) are stored in PostgreSQL

## Landing and promo pages

| Page | File | Purpose |
|---|---|---|
| Homepage | `src/app/page.tsx` | Hero, BentoFeatures, Features, FAQ, CtaBand, SocialProof, Footer |
| MCP promo | `src/app/mcp/page.tsx` | MCP server landing — Hero, chat mockup with dialogue, install snippets for Claude / Cursor / ChatGPT |
| Skills catalog | `src/app/skills/page.tsx` | SSG catalog of 25 docs-skills with filters (category / plan / keyword) |
| Skill detail | `src/app/skills/[name]/page.tsx` | SSG page with SKILL.md, install + MCP snippets |
| Privacy / Terms / Licenses | `src/app/{privacy,terms,licenses}/` | Legal pages |

**Key landing components (`src/components/landing/`):**
- `Hero.tsx` — main screen with GitHub input
- `BentoFeatures.tsx`, `Features.tsx` — features grid
- `AiSupportsLogos.tsx` — logos of supported AI providers
- `FAQ.tsx` / `FAQClient.tsx` — FAQ with JSON-LD markup
- `CtaBand.tsx`, `SocialProof.tsx` — conversion blocks
- `Header.tsx`, `Footer.tsx` — navigation
- `PreviewModal.tsx`, `GitHubHintBanner.tsx` — auxiliary UX blocks
- `demo_preview.gif` — animated demo
