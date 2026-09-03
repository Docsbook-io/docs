---
title: "Migrating from Docusaurus to Docsbook, step by step"
description: "Move a Docusaurus site to Docsbook without losing search traffic — adapt MDX, retire the CI pipeline, port redirects, and keep every URL working."
---

# Migrating from Docusaurus to Docsbook, step by step

Docusaurus is great until the next major migration lands and you spend a sprint on it instead of shipping the product. This guide walks through the realistic migration path.

We make Docsbook. We will also tell you when migration is not worth it.

## When you should not migrate

Skip this migration if:

- Your Docusaurus site uses heavy React component embeds (interactive demos, custom plugins). Docsbook is markdown-first.
- You have a dedicated docs engineer whose job partly includes Docusaurus. The platform has real strengths in their hands.
- You need a deeply custom React theme. Docsbook gives you color tokens, fonts, layout switches, header/footer config — not full theme swizzle.

If any of those apply, [stay on Docusaurus](./docusaurus-vs-docsbook-2026.md) and read the rest of this guide later.

## TL;DR

1. Strip MDX-specific syntax to standard markdown
2. Push to a GitHub repo (you already have one)
3. Connect Docsbook
4. Wire custom domain
5. Port redirects
6. Drop the CI pipeline and the hosting bill

## Step 1: MDX to markdown

Docusaurus uses MDX, which is markdown + JSX. Docsbook uses standard markdown with extensions.

Three classes of MDX that need handling:

### Imports and React components

```mdx
import Foo from '@site/src/components/Foo';

<Foo />
```

Solutions:

- For static visuals: replace with a hosted image and a link to a live demo
- For interactive elements: link out to your app
- For tabs/admonitions: use Docsbook's native blocks (see below)

### Admonitions

Docusaurus:

```mdx
:::note Title
Content
:::
```

Docsbook (GitHub-flavored markdown):

```markdown
> [!NOTE]
> Content
```

Find-and-replace:

```bash
find . -name "*.mdx" -exec rename 's/\.mdx$/\.md/' {} \;
find . -name "*.md" -exec sed -i.bak -E 's/:::note/> [!NOTE]/g; s/:::tip/> [!TIP]/g; s/:::warning/> [!WARNING]/g; s/:::caution/> [!CAUTION]/g; s/:::info/> [!NOTE]/g; s/^:::$//' {} \;
```

### Tabs and code groups

Docsbook supports tabs via a standard syntax:

```markdown
<Tabs>
  <Tab title="npm">npm install foo</Tab>
  <Tab title="pnpm">pnpm add foo</Tab>
</Tabs>
```

Most Docusaurus tabs translate one-to-one.

## Step 2: Sidebar and navigation

Docusaurus uses `sidebars.js` to define navigation. Docsbook builds navigation from your folder structure and frontmatter.

If you want a specific order:

```markdown
---
title: "Quick Start"
order: 1
---
```

If you do not specify order, Docsbook sorts alphabetically. Move files into ordered folders if you need explicit grouping.

You can delete `sidebars.js`, `docusaurus.config.js`, `babel.config.js`, and the `src/` directory after migration.

## Step 3: Connect Docsbook

Your docs are already in `docs/`. Connect the repository:

- [docsbook.io](https://docsbook.io) → Sign in with GitHub
- Paste `github.com/yourorg/yourrepo`
- Site live at `docsbook.io/yourorg/yourrepo`

## Step 4: Custom domain

Docsbook serves `docs.yourcompany.com` with automatic SSL.

- Docsbook dashboard → Settings → Domain
- Enter `docs.yourcompany.com`
- Update DNS: CNAME `docs` → `cname.vercel-dns.com`
- Wait 5 minutes for SSL

## Step 5: URL preservation

Docusaurus URLs typically look like:

```
docs.yourcompany.com/docs/intro
docs.yourcompany.com/docs/category/guides/getting-started
```

Docsbook URLs match your file paths:

```
docs.yourcompany.com/intro.md → docs.yourcompany.com/intro
docs.yourcompany.com/guides/getting-started.md → docs.yourcompany.com/guides/getting-started
```

If your Docusaurus had a `/docs/` prefix and you want to keep parity:

**Option A**: rename the local `docs/` folder to keep the prefix in URLs (Docsbook will serve from a different path).

**Option B**: add redirects from old `/docs/*` URLs to new `/*` URLs at your CDN or DNS layer.

## Step 6: Drop the CI/CD

Once Docsbook is serving traffic:

```bash
# Files you can delete
rm -rf .docusaurus/
rm -rf build/
rm -rf node_modules/
rm docusaurus.config.js
rm sidebars.js
rm babel.config.js
rm -rf src/
rm -rf static/
# Keep docs/ — it is your source
```

GitHub Actions workflow file for Docusaurus deployment: also delete.

The result: docs deploy on every `git push` to `main`, no CI minutes used.

## What you gain

| | Docusaurus | Docsbook |
|---|---|---|
| Build time | 30–120 seconds per push | 5 seconds total setup |
| Hosting cost | Vercel/Netlify pro tier | Included |
| AI chat | Plugin work | Built-in |
| Translations | Per-locale config + translation pipeline | Built-in, 15 languages |
| Major version migrations | Every 18 months | Never |
| Theme maintenance | Swizzle drift | Color tokens, no maintenance |

## What you give up

- React component embeds inside docs (host them elsewhere, link in)
- Full swizzle theme control (you get color/font/layout tokens)
- Plugin ecosystem (most cases are built-in already)

## Edge cases

### Algolia DocSearch

You can keep using Algolia DocSearch on Docsbook (point it at your new domain). Or use Docsbook's built-in search, which is included for free.

### Custom landing page

Docusaurus often has a custom landing page at `/` built in React. Docsbook serves your `README.md` at `/`. If you want a marketing-style landing page, host that separately and point Docsbook at `docs.yourcompany.com` instead of `yourcompany.com`.

### Versioning

Docusaurus's `docs/versioned_docs/version-1.0/` pattern is not directly supported. Options:

- Use separate Docsbook workspaces per version (`docsbook.io/yourorg/yourrepo-v1`)
- Use Git branches and switch the indexed branch
- Drop old versions (most teams find they were maintaining them out of habit)

## Timing

- OSS project, ~80 pages, minimal MDX: 2 hours
- Startup, ~300 pages, moderate MDX: half a day
- Mid-stage, ~1000 pages, heavy MDX: 1–2 days

Test the migration before committing to it. Publishing a second site from the same repository costs nothing and changes nothing about the Docusaurus deploy still serving your readers — if the result does not reach parity, you have lost the five seconds it took.

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [Should you move off Docusaurus in 2026?](./docusaurus-vs-docsbook-2026.md) — the decision, if you have not made it yet
- [Docusaurus alternatives in 2026: 9 platforms compared](./docusaurus-vs-docsbook.md) — the wider field
- [Custom domain for docs](./custom-domain-for-docs-howto.md) — the DNS and redirect half of this migration
- [Docs as code vs a managed platform](./docs-as-code-vs-managed-platform.md) — the principle behind the move
