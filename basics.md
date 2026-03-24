# Core Concepts

## What is a Workspace?

**Workspace** — your documentation linked to a single GitHub repository.

A workspace includes:
- Your repository with markdown files
- Documentation site (address and appearance)
- Settings (domain, translation, styling)

## How Does It Work?

```
1. You create a Workspace from your GitHub repo
                    ↓
2. Docsbook reads markdown files from GitHub
                    ↓
3. Transforms them into a beautiful site
                    ↓
4. Site is available at: docsbook.io/{user}/{repo}
                    ↓
5. You update files in GitHub
                    ↓
6. Site updates automatically
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
- Beautiful formatting
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
│ ✨ Premium             │
│ ⚙️ Settings            │
│ 🚪 Sign out            │
└─────────────────────────┘
```

### What can you do with the widget?

1. **See avatar** — click for the menu
2. **See status** — Free or Premium
3. **Open settings** — to change domain, enable translation
4. **Sign out** — log out

## Public Access

Your documentation is **open to everyone**. Even if the repository is private, the documentation is visible to all.

Benefits:
- SEO optimization (indexed by Google)
- Beautiful look instead of plain GitHub
- Fast loading
- Mobile-friendly
- Full-text search (coming soon)

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

## Free vs Premium

### Free Plan

- ✅ 1 public repository
- ✅ GitHub synchronization
- ✅ SEO optimization
- ✅ Beautiful design
- ✅ Mobile-friendly
- ❌ Custom domain
- ❌ Remove "Powered by Docsbook"
- ❌ Translations to other languages

### Premium ($29 one-time lifetime)

Get everything from Free, plus:

- ✅ Unlimited repositories
- ✅ Custom domain (docs.example.com)
- ✅ Remove "Powered by Docsbook" badge
- ✅ Translation to any language
- ✅ Priority support

## How to Get Started?

Ready? [Create your first workspace](./quick-start.md) in 3 minutes.

Have questions? See the [FAQ](./faq.md).
