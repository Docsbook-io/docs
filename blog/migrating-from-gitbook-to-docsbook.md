---
title: "Migrating from GitBook to Docsbook: A Step-by-Step Guide"
description: "How to move your docs from GitBook to Docsbook without breaking SEO — export, GitHub import, redirects, custom domain. The migration most teams complete in under an afternoon."
---

# Migrating from GitBook to Docsbook

You hit the GitBook per-editor wall. Or the AI Search add-on price. Or you noticed your team is paying $2,400/year for a docs site that does not index well. This is the practical migration guide.

Most teams complete this in under three hours. The expensive part is the redirects.

## TL;DR

1. Export GitBook content as markdown
2. Push to a new GitHub repository
3. Connect Docsbook to that repo (5 seconds)
4. Verify the site at `docsbook.io/yourorg/yourrepo`
5. Wire your custom domain `docs.yourcompany.com` to Docsbook (PRO+)
6. Set up redirects from old GitBook paths
7. Update internal links across your site

## Step 1: Export from GitBook

GitBook supports markdown export through the workspace settings:

- Open your GitBook space
- Settings → Synchronize with Git → "Sync GitBook with Git provider"
- Choose GitHub, pick a new private or public repo
- GitBook syncs your content as markdown with frontmatter

Alternative (no Git Sync): use the "Export to Markdown" option from the space menu and unzip the result locally.

The folder structure GitBook exports:

```
README.md
SUMMARY.md
docs/
  introduction.md
  guides/
    quick-start.md
  api/
    auth.md
```

## Step 2: Adjust for Docsbook conventions

Two small differences to handle:

### SUMMARY.md is optional in Docsbook

GitBook uses `SUMMARY.md` as the navigation source. Docsbook builds navigation from your folder structure and frontmatter `title` automatically.

You can keep `SUMMARY.md` (Docsbook ignores it) or delete it. Most teams delete it.

### Frontmatter

GitBook frontmatter:

```yaml
---
description: How to authenticate
---
```

Docsbook reads the same `description` field plus optional `title`. If `title` is missing, the first H1 is used.

A simple migration script:

```bash
find . -name "*.md" -not -path "./.git/*" -exec \
  sed -i.bak '1,/^---$/ s/^description:/description:/' {} \;
```

(No changes needed in most cases — GitBook and Docsbook frontmatter are compatible.)

## Step 3: Connect Docsbook

- Go to [docsbook.io](https://docsbook.io)
- Sign in with GitHub
- Paste `github.com/yourorg/yourrepo`
- Site live at `docsbook.io/yourorg/yourrepo` in 5 seconds

If your repo has `docs/` folder, Docsbook uses it. If your docs live at the root, that works too.

## Step 4: Custom domain

Business ($159/month) includes custom domain. Free and Pro do not.

In Docsbook dashboard:

- Settings → Domain
- Enter `docs.yourcompany.com`
- Update your DNS: CNAME `docs` → `cname.vercel-dns.com`
- SSL is automatic and free

## Step 5: The redirects

This is the only step that matters for SEO. GitBook URLs look like:

```
docs.yourcompany.com/v/1.0/api/authentication
```

Docsbook URLs:

```
docs.yourcompany.com/api/authentication
```

You have two options:

### Option A: redirect at DNS/CDN level

If you have Cloudflare in front of your domain, add page rules:

```
docs.yourcompany.com/v/*/api/* → docs.yourcompany.com/api/$2 [301]
```

### Option B: redirect via Docsbook

Add a `_redirects` file (if your stack supports it) at the root of your repo:

```
/v/1.0/api/auth /api/auth 301
/v/1.0/api/webhooks /api/webhooks 301
```

A 301 preserves SEO authority. A 302 does not — use 301.

## Step 6: Update internal references

Search and replace across your codebase:

```bash
grep -rl "docs.yourcompany.com/v/" . | xargs sed -i.bak 's|docs.yourcompany.com/v/[0-9.]*/|docs.yourcompany.com/|g'
```

Update:

- Your product app footer link
- Your marketing site
- Your README links on GitHub
- Your support team's saved replies

## Step 7: Verify the AI surface

Docsbook generates `llms.txt`, `llms-full.txt`, JSON-LD, and sitemap automatically. Check:

```bash
curl https://docs.yourcompany.com/llms.txt | head -20
curl https://docs.yourcompany.com/sitemap.xml | head -10
```

See [llms.txt: the complete guide](./llms-txt-guide.md) for what to expect.

## What gets better

| | GitBook | Docsbook |
|---|---|---|
| Cost | ~$200/mo per editor | $0 / $59 mo / $159 mo |
| AI chat | Add-on | Built-in |
| AI translation | Not available | 15 languages |
| MCP server | Not available | Built-in |
| llms.txt | Manual | Automatic |
| Source of truth | GitBook DB | Your GitHub repo |

## What might break

- **GitBook-specific blocks** — collapsible sections, hint blocks, tabs. Docsbook supports standard markdown + Docsbook-specific blocks. Most GitBook hints rewrite cleanly to `> [!NOTE]` callouts.
- **Custom OpenAPI integration** — GitBook has its API reference renderer. Docsbook renders OpenAPI through your existing tools or links out.
- **GitBook AI chat history** — does not transfer. The chat starts fresh with your new content.

## Timing

In our experience helping teams migrate:

- Solo founder, ~50 pages: 1 hour
- Small startup, ~200 pages: 3 hours
- Mid-stage company, ~1000 pages, custom domain: half a day

The expensive part is socializing the URL change internally and updating saved replies in your support tool.

## Related reading

- [GitBook vs Docsbook](./gitbook-vs-docsbook.md) — feature-by-feature
- [Custom domain for docs how-to](./custom-domain-for-docs-howto.md)
- [Documentation SEO guide](./documentation-seo-guide.md)

---

Start the migration: paste your GitHub repo at [docsbook.io](https://docsbook.io). Site live in 5 seconds, custom domain in 5 minutes.
