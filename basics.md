---
title: "Core Concepts: Workspaces in Docsbook"
description: "Learn the core concepts behind Docsbook — what a workspace is, how it's created from a GitHub repo, a website, or an idea, and how markdown becomes a documentation site."
---

# Core Concepts

## What is a Workspace?

**Workspace** — your documentation site and its settings, backed by a GitHub repository (either your own, or one Docsbook hosts for you).

A workspace includes:
- A repository with markdown files (yours, or Docsbook-hosted if you started from a website/idea)
- Documentation site (address and appearance)
- Settings (domain, translation, styling)

## How Does It Work?

There are two ways to create a workspace:

**From your own GitHub repo:**
```
1. You link a Workspace to your GitHub repo
                    ↓
2. Docsbook reads markdown files from GitHub
                    ↓
3. Transforms them into a documentation site
                    ↓
4. Site is available at: docsbook.io/{user}/{repo}
                    ↓
5. You update files in GitHub
                    ↓
6. Site updates automatically
```

**From a website scan or an idea (no repo needed):**
```
1. You describe a website URL or an idea at docsbook.io/create
                    ↓
2. Docsbook generates draft pages — browse them as a real docs site and customize before signing in
                    ↓
3. You sign in, and the draft becomes a live Workspace automatically
                    ↓
4. Site is available at: docsbook.io/{owner}/{repo} (Docsbook-hosted repo)
                    ↓
5. Optional: move the project to your own GitHub from the chat header
   (creates the repo, copies every page — the public URL changes)
```

## Site Structure

### Left Panel — Navigation (Sidebar)

The sidebar is built from your repository's file structure:

```
docs/
├── README.md          → "Home"
├── getting-started.md → "Getting Started"
├── api/
│   ├── auth.md        → "API / Auth"
│   └── endpoints.md   → "API / Endpoints"
└── faq.md             → "FAQ"
```

Displayed as:

```
📘 Home
📄 Getting Started
📁 API
  └─ Auth
  └─ Endpoints
📄 FAQ
```

### Main Content

The center area shows the content of the selected markdown file.

**Features:**
- Formatted text
- Syntax highlighting
- Tables and lists
- Links to other pages

### Right Panel — Outline

The right side automatically builds a table of contents from the current page's headings.

```
Outline:
  - Installation
    - Requirements
    - Steps
  - Usage
  - Troubleshooting
```

Click a heading → scrolls the page to it.

## Float Widget — Control Widget

When you are **logged in** and viewing **your own documentation**, a widget appears in the bottom-right corner.

### Who sees the widget?

- ✅ You — see your widget
- ❌ Other people — don't see it (only on your account)

### What does it show?

```
┌─────────────────────────┐
│ 👤 alice               │
│ ✨ PRO                 │
│ 💬 Select Chat       ▸ │
│ 📁 Select Repository ▸ │
│ 🖥️ Select Mode       ▸ │
│ ⚙️ Settings            │
│ 🚪 Sign out            │
└─────────────────────────┘
```

### What can you do with the widget?

1. **See avatar** — click for the menu
2. **See status** — Free, Pro, or Business
3. **Switch chat, repository or mode** — the three pickers at the top of the menu
4. **Open settings** — to change domain, enable translation
5. **Sign out** — log out

## Public Access

By default, your documentation is **open to everyone**. Even if the repository is private, the documentation is visible to all.

Benefits:
- SEO optimization (indexed by Google)
- Polished design instead of plain GitHub
- Fast loading
- Mobile-friendly
- Full-text search

On Pro and Business, you can flip this: switch a workspace to **private** and require a password
or SSO sign-in before anyone but the owner can view it. See [Managing Your Docs](/guides/getting-started/managing-docs) for how to set it up.

## GitHub Synchronization

### How does synchronization work?

Docsbook **does not use webhooks**. Instead:

1. You update files in GitHub
2. You visit the documentation site
3. Docsbook checks GitHub for new content
4. If there are changes — shows the new version

**Result:** Documentation is always up to date as soon as you look at it.

### What is synchronized?

- ✅ New `.md` files
- ✅ Text updates
- ✅ File deletions
- ✅ File renames
- ✅ New folders

### What is NOT synchronized?

- ❌ Code comments
- ❌ Commit history
- ❌ Branch information
- ❌ Other formats (`.txt`, `.rst`, etc.)

## Free, Pro, and Business

A paid plan is bought once per account and grants project seats — a project is paid while it holds one, and seats can be moved between projects. Free projects are unlimited.

### Free ($0 forever)

- ✅ Unlimited public repositories
- ✅ GitHub synchronization
- ✅ Customizable design (brand, themes, fonts)
- ✅ Mobile-friendly
- ✅ Basic analytics (last 24h)
- ✅ AI chat ($0.15/month AI budget), with your choice of AI model
- ✅ Full SEO / GEO / AEO (sitemap, OpenGraph, JSON-LD)
- ❌ Custom domain
- ❌ AI translations

### Pro (monthly, 7-day free trial)

Everything in Free, plus:

- ✅ AI translations (15 languages)
- ✅ Advanced AI chat config (custom system prompt, chat hooks)
- ✅ $59/month AI budget
- ✅ 1 paid project seat (buy extra seats if you need more)
- ✅ Search & feedback analytics
- ✅ Analytics for 7 days
- ✅ Priority support
- ❌ Webhooks, bring-your-own API key, semantic search (Business only — see below); custom domain needs Pro

### Business (monthly, 14-day free trial)

Everything in Pro, plus Business-exclusive capabilities, plus higher usage limits:

- ✅ Custom domain (docs.example.com) with free SSL
- ✅ Webhooks (unlimited)
- ✅ Bring your own AI chat / translation API key (with custom model)
- ✅ Semantic search (meaning-based chat search over an embedding index of your docs)
- ✅ $200/month AI budget
- ✅ Unlimited paid project seats
- ✅ Higher translation limit than Pro

<!-- widget:cta -->

## How to get started?

Creating your first workspace takes about three minutes.

[Create your first workspace](./quick-start.md) · [Read the FAQ](./faq.md)

<!-- /widget -->
