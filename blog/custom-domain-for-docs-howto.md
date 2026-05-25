---
title: "Custom Domain for Documentation: docs.yourcompany.com Setup Guide"
description: "How to set up a custom domain for documentation — DNS, SSL, redirects, subdomain vs subdirectory, and why this matters for SEO. Includes exact steps for Docsbook, GitBook, Mintlify."
---

# Custom Domain for Documentation

`docs.yourcompany.com` looks more professional than `docsbook.io/yourorg/yourrepo`. It also matters for SEO, trust, and the "is this a real product" first impression. This is how to set it up correctly.

## TL;DR

1. Decide subdomain (`docs.yourcompany.com`) vs subdirectory (`yourcompany.com/docs/`)
2. Add a CNAME or A record in DNS pointing to your docs host
3. Wait for SSL to provision (usually under 5 minutes)
4. Set up redirects from any prior URL
5. Update internal links and external mentions

## Subdomain vs subdirectory

The SEO debate is real. Both work in 2026, but they have different tradeoffs.

| | Subdomain (`docs.yourcompany.com`) | Subdirectory (`yourcompany.com/docs/`) |
|---|---|---|
| Setup complexity | Easier (one DNS record) | Harder (reverse proxy or shared platform) |
| SEO authority | Mostly inherited from root domain | Fully inherited |
| Hosting flexibility | Independent of main site | Shares the main site infra |
| Brand cohesion | Clear separation | Tightly coupled |
| Common in 2026 | Most docs sites | Stripe, GitHub, AWS |

For most teams, the subdomain is easier and the SEO difference is small. Only go subdirectory if your main site is on a platform that supports reverse-proxying docs cleanly.

## Setting up the subdomain (Docsbook example)

Three steps:

### 1. In Docsbook dashboard

- Open your workspace settings
- Settings → Domain
- Enter `docs.yourcompany.com`
- Click Save

The dashboard shows the DNS records you need to add.

### 2. In your DNS provider

Add a CNAME record:

```
Type:  CNAME
Name:  docs
Value: cname.vercel-dns.com
TTL:   300 (or default)
```

If your DNS provider doesn't support CNAME at the root (Cloudflare's flattening or similar), use the A record alternative your platform provides.

### 3. SSL

SSL is automatic. Docsbook (via Vercel) provisions a Let's Encrypt cert within 5 minutes. You will see "Active" status in the dashboard.

Total time: usually 5–15 minutes including DNS propagation.

## When SSL takes longer

If SSL stays "Pending" after 30 minutes:

- Check that DNS has propagated globally: `dig docs.yourcompany.com` should resolve to the CNAME target
- Remove any CAA records that block Let's Encrypt
- Check that your domain isn't already serving HTTPS from another provider

## Redirects

If you previously hosted docs at a different URL, set up 301 redirects to preserve SEO.

### From a docs subdirectory to the new subdomain

```
yourcompany.com/docs/* → docs.yourcompany.com/* (301)
```

Most platforms support this via redirect rules.

### From GitBook v-paths to Docsbook

GitBook URLs typically have `/v/1.0/` patterns:

```
docs.yourcompany.com/v/1.0/api/auth → docs.yourcompany.com/api/auth (301)
```

If you use Cloudflare in front of your domain, you can do this with a single page rule. See [migrating from GitBook to Docsbook](./migrating-from-gitbook-to-docsbook.md).

### From Docusaurus prefix to root

Docusaurus often uses `/docs/intro` paths. If you flatten to root:

```
docs.yourcompany.com/docs/* → docs.yourcompany.com/* (301)
```

See [migrating from Docusaurus to Docsbook](./migrating-from-docusaurus-to-docsbook.md).

## SEO considerations

Three things to verify after the cutover:

### Search Console

Add the new domain to Google Search Console. Submit the sitemap (Docsbook auto-generates `/sitemap.xml`). Watch the indexing report for 4–6 weeks.

### Canonical tags

If you keep the old URL live as a fallback for any reason, set canonical tags on the old URL pointing to the new one. Better: just 301-redirect.

### `llms.txt` propagation

When you move domain, AI agents need to re-discover your `llms.txt`. They usually do within a few crawls. Verify:

```bash
curl https://docs.yourcompany.com/llms.txt | head -10
```

See [the complete llms.txt guide](./llms-txt-guide.md).

## What changes for users

- Bookmarks to old URLs: covered by redirects
- Saved support replies: update them
- Internal product links: update them
- External backlinks: stay (the 301 transfers authority)

The user-visible experience should not change beyond the URL.

## Custom domain support by platform

| Platform | Custom domain on free | Custom domain on paid |
|---|---|---|
| **Docsbook** | No | PRO ($150 lifetime), PRO+ ($59/mo) |
| **Mintlify** | No | Yes ($150+/mo) |
| **GitBook** | No | Yes (paid plan, per editor) |
| **ReadMe** | No | Yes ($99+/mo) |
| **GitHub Pages** | Yes | Yes |
| **Vercel/Netlify** | Yes (50/account on Vercel free) | Yes |

For managed docs platforms, custom domain is a paid feature. The Docsbook lifetime PRO at $150 is the cheapest option in the comparable set.

## Common mistakes

- **Pointing the apex domain at a CNAME** — most DNS providers do not allow this; use subdomain (`docs.`) or a flattened A record
- **Forgetting to redirect** — old URLs 404 → SEO drops → loss of authority
- **HTTPS not enforced** — some platforms serve HTTP and HTTPS both; force redirect to HTTPS
- **Multiple `docs` subdomains** — only one CNAME at a time, drop old ones first

## Related reading

- [Migrating from GitBook to Docsbook](./migrating-from-gitbook-to-docsbook.md)
- [Migrating from Docusaurus to Docsbook](./migrating-from-docusaurus-to-docsbook.md)
- [Documentation SEO guide](./documentation-seo-guide.md)

---

Docsbook supports `docs.yourcompany.com` with free SSL on PRO ($150 lifetime). [See pricing →](https://docsbook.io)
