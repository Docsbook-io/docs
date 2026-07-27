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
│  AI-Powered Features                                           │
│  ├─ AI chatbot trained on your docs (all plans)              │
│  ├─ 15-language automatic translations (Pro/Growth/Business) │
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
| **Free** | $0 | Unlimited docs, branding, basic UI controls, analytics (24h), AI chat ($0.15/mo AI budget), SEO / AEO / GEO |
| **Pro** | $59/mo, 7-day free trial | 1 project seat, translations, advanced AI chat config (custom prompt, hooks, Source of Truth graph), search & feedback analytics, $59/mo AI budget |
| **Growth** | $349/mo | Same feature set as Pro, with 5 project seats and a $349/mo AI budget — for teams that have outgrown Pro's usage limits |
| **Business** | $159/mo, 14-day free trial | Everything in Pro, plus 3 project seats, custom domain, white-label, webhooks (25), bring-your-own API key, a $159/mo AI budget, and higher translation limits |
| **Scale** | $899/mo | Same feature set as Business, with 15 project seats and a $899/mo AI budget, the largest of any plan — for teams that have outgrown Business's usage limits |

All monthly plans (Pro, Growth, Business, Scale) can also be billed annually at a 20% discount. All plans: **unlimited repositories, forever.**

A subscription is bought once per account and grants project seats — a project is paid while it holds one, and you can move a seat between projects. The AI budget is shared across every paid project on the account, and free projects are unlimited.

Every paid plan includes an AI budget equal to its price: Pro costs $59/month and includes $59 of AI usage, Business $159, Growth $349, Scale $899.

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

### 🤖 AI Features
- **AI Chatbot** — answers questions based on your documentation (every plan, limited by a monthly AI budget in dollars; Pro/Growth/Business/Scale get progressively larger budgets)
- **Source of Truth graph** — structured data about your docs, for AI agents (Pro / Growth / Business / Scale)
- **Custom AI chat config** — system prompt, chat hooks (Pro / Growth / Business / Scale)
- **LSP-style tools** — semantic search, link resolution, outline navigation

### 🌍 Translation & Localization (Pro / Growth / Business / Scale)
- **15 languages** — English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch
- **SEO per language** — each translation is indexed separately by Google
- **Auto-detect** — shows readers content in their browser language
- **Manual or AI-powered** — choose your translation workflow

### 📊 Analytics (Free+)
- Page views, unique visitors, top pages, referrers
- AI usage tracking (queries, remaining quota)
- Countries & languages of readers
- **Pro / Growth / Business / Scale:** Advanced journey mapping, visitor drill-down, failed searches, negative feedback

### 🔗 Integrations
- **Custom domain (Business / Scale)** — `docs.yourcompany.com` with free SSL
- **Webhooks (Business / Scale)** — 15 event types (chat questions, translations, traffic spikes)
- **MCP server** — control Docsbook from Claude Code, Cursor, ChatGPT
- **GitHub integration** — "Edit on GitHub" links on every page

### 🔍 Search Engine Optimization (all plans)
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
- **Cheaper** — Docsbook Pro vs. $8-10/month/user on GitBook/Notion
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

1. **Generate a draft — no account needed**  
   Click "Create website" at [docsbook.io](https://docsbook.io), then pick a source: a website URL to scan, a GitHub repo to link, or just an idea in text

2. **Preview and refine**  
   For website/idea sources, chat with the AI to tweak the generated draft and preview it live, all before signing in

3. **Sign in to publish**  
   Choose GitHub, Google, Apple, or email — your draft becomes a live workspace automatically, no re-work needed. GitHub-sourced sites authorize repo access at this step.

4. **Share your docs**  
   Your documentation is live at `docsbook.io/owner/repo`

5. **Customize** (optional)  
   Add branding, enable AI chat, set up a custom domain, or make it private with a password/SSO gate

6. **Keep it updated**  
   Push to GitHub, docs update automatically (GitHub-sourced sites)

That's it! No build step, no deployment, no CI/CD.

---

**Ready to start?** [Create your first site →](https://docsbook.io/create)

**Questions?** [See our FAQ](./faq.md) or [contact us](mailto:support@docsbook.io).
