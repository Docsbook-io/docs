---
title: "Docsbook Overview"
description: "Understand what Docsbook is, how it works, its architecture, and why it's the fastest way to publish beautiful documentation from GitHub."
---

# Docsbook Overview

**Docsbook** is an AI-powered documentation platform that turns any GitHub repository into a beautiful, fully-featured documentation site in seconds. No setup, no configuration, no CI/CD needed.

## What is Docsbook?

Docsbook is a knowledge platform that automatically:

1. **Reads your GitHub repository** — any public repo with a `README.md` or `docs/` folder
2. **Publishes instantly** — your documentation appears at `docsbook.io/owner/repo` in seconds
3. **Stays in sync** — every `git push` automatically updates your live documentation
4. **Adds intelligence** — AI chatbot, 15-language translations, full analytics, custom domains
5. **Keeps your data safe** — files stay in GitHub, no vendor lock-in

In one sentence: **GitHub repo → Beautiful docs + AI chat + SEO + analytics in 5 seconds.**

## How Docsbook Works

```
┌─────────────────────────────────────────────────────────────┐
│  Your GitHub Repo (public)                                   │
│  ├─ README.md or docs/                                       │
│  └─ Markdown files                                           │
└──────────────────┬──────────────────────────────────────────┘
                   │ GitHub OAuth + Git fetch
                   ▼
┌─────────────────────────────────────────────────────────────┐
│  Docsbook Indexer                                             │
│  ├─ Parse markdown + frontmatter                             │
│  ├─ Extract headings, links, metadata                        │
│  ├─ Build Source of Truth graph (LSP-style navigation)       │
│  └─ Index for search & AI embedding                          │
└──────────────────┬──────────────────────────────────────────┘
                   │ Reindex on every push
                   ▼
┌─────────────────────────────────────────────────────────────┐
│  Live Documentation Site                                      │
│  docsbook.io/owner/repo                                      │
│  ├─ Beautiful, responsive design                             │
│  ├─ Full-text search                                         │
│  ├─ Dark/light themes (customizable)                         │
│  ├─ Mobile-friendly                                          │
│  └─ Custom domain (docs.yourcompany.com)                     │
└──────────────────┬──────────────────────────────────────────┘
                   │ Static HTML + CDN
                   ▼
┌─────────────────────────────────────────────────────────────┐
│  AI-Powered Features (PRO+)                                   │
│  ├─ AI chatbot trained on your docs                          │
│  ├─ 15-language automatic translations                       │
│  ├─ Source of Truth graph for agents                         │
│  └─ Analytics + webhooks for integrations                    │
└─────────────────────────────────────────────────────────────┘
```

## Core Concepts

### Workspace
A **workspace** = one documentation site. You can create unlimited workspaces from any GitHub repositories you own or have access to.

**Example:**
- Workspace 1: `acme/api-docs` → `docsbook.io/acme/api-docs`
- Workspace 2: `acme/sdk` → `docsbook.io/acme/sdk`

### Plans
| Plan | Cost | What You Get |
|---|---|---|
| **Free** | $0 | Unlimited docs, branding, basic UI controls, analytics (24h) |
| **PRO** | $150 lifetime | AI chat (200 req/mo), translations (50/mo), custom domain, SEO, AEO, GEO |
| **PRO+** | $59/month | Everything + 2K AI req/mo, 500 translations/mo, Source of Truth graph, advanced analytics |

All plans: **unlimited repositories, forever.**

## Key Features by Category

### 🚀 Publishing
- **Instant publication** — docs live in seconds, no builds or deploys
- **Auto-sync** — push to GitHub, documentation updates automatically
- **Multiple repos** — create unlimited workspaces
- **No configuration** — Docsbook detects your markdown structure automatically

### 🎨 Design & Branding
- Custom colors (light/dark), fonts, logo, favicon
- Light/dark theme toggle
- Mobile-responsive design
- Show/hide UI elements (search, breadcrumbs, feedback, prev/next buttons)

### 🤖 AI Features (PRO+)
- **AI Chatbot** — answers questions based on your documentation
- **Source of Truth graph** — structured data about your docs (for AI agents)
- **LSP-style tools** — semantic search, link resolution, outline navigation

### 🌍 Translation & Localization (PRO)
- **15 languages** — English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch
- **SEO per language** — each translation is indexed separately by Google
- **Auto-detect** — shows readers content in their browser language
- **Manual or AI-powered** — choose your translation workflow

### 📊 Analytics (Free+)
- Page views, unique visitors, top pages, referrers
- AI usage tracking (queries, remaining quota)
- Countries & languages of readers
- **PRO+:** Advanced journey mapping, visitor drill-down, failed searches, negative feedback

### 🔗 Integrations
- **Custom domain** — `docs.yourcompany.com` with free SSL
- **Webhooks** — 15 event types (chat questions, translations, traffic spikes)
- **MCP server** — control Docsbook from Claude Code, Cursor, ChatGPT
- **GitHub integration** — "Edit on GitHub" links on every page

### 🔍 Search Engine Optimization (PRO)
- **SEO** — meta tags, sitemap.xml, JSON-LD schema, OpenGraph
- **GEO** — TL;DR blocks, publication date, author attribution for AI search engines (Perplexity, ChatGPT Search, Google AI Overviews)
- **AEO** — FAQ markup, HowTo schema, voice assistant optimization

## Technology Stack

### Frontend
- Next.js 16 + React 19
- TypeScript, Tailwind CSS, shadcn/ui
- Framer Motion (animations)

### Backend
- PostgreSQL (Neon serverless)
- Redis (caching)
- Drizzle ORM (database)

### AI & Features
- OpenRouter (multi-provider LLM support)
- OpenAI, Gemini, Anthropic (custom API keys)
- MCP 1.0 (OAuth 2.0 compatible)

### Infrastructure
- Vercel (hosting, CDN, custom domains)
- Axiom (analytics & logging)
- Paddle (billing & subscriptions)

### Markdown & Parsing
- **markdown-lsp** — our open-source LSP parser for documentation
- unified / remark / rehype (markdown processing)
- Shiki (syntax highlighting)

## Quick Links

- **[Getting Started](./quick-start.md)** — Set up your first workspace in 3 minutes
- **[Core Concepts](./basics.md)** — Workspace, plans, and how everything connects
- **[AI Features Guide](./ai/)** — Chat, translations, Source of Truth
- **[MCP Server](./ai/mcp.md)** — Use Docsbook from Claude Code and other AI tools
- **[Webhooks Reference](./webhooks.md)** — Integrate Docsbook with your tools
- **[Skills Catalog](./ai/skills.md)** — Automation & docs-specific tools

## Why Docsbook?

### vs. GitBook / Notion
- **Cheaper** — $150 lifetime vs. $8-10/month/user
- **Faster** — 5 seconds to deploy vs. 2-3 days to set up
- **No vendor lock-in** — your docs stay in GitHub
- **Built-in AI** — chat + translations included

### vs. Docusaurus / Mintlify
- **Zero config** — Docsbook auto-detects your markdown
- **Auto-sync** — no build pipelines or GitHub Actions
- **AI out of the box** — no integration setup
- **Better analytics** — understand who reads what

### vs. ReadTheDocs / Sphinx
- **Modern design** — beautiful by default
- **AI-first** — chat, translations, semantic search
- **Easier maintenance** — just write markdown in GitHub

## Getting Started

1. **Connect your GitHub repo**  
   Sign in with GitHub at [docsbook.io](https://docsbook.io)

2. **Create a workspace**  
   Pick a public repo — Docsbook indexes it in seconds

3. **Share your docs**  
   Your documentation is live at `docsbook.io/owner/repo`

4. **Customize** (optional)  
   Add branding, enable AI chat, set up a custom domain

5. **Keep it updated**  
   Push to GitHub, docs update automatically

That's it! No build step, no deployment, no CI/CD.

---

**Ready to publish?** [Create your first workspace →](https://docsbook.io/connect)

**Questions?** [See our FAQ](./faq.md) or [contact us](mailto:support@docsbook.io).
