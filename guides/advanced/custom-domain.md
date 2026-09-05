---
title: "Point your own domain at your Docsbook documentation"
description: "Add docs.yourcompany.com in settings, create the DNS record Docsbook shows you, wait for propagation, and get an automatic SSL certificate."
---

# Set up a custom domain

A custom domain serves your Docsbook documentation from an address you own — `docs.example.com` instead of `docsbook.io/user/repo`. Docsbook issues the SSL certificate automatically once DNS resolves.

Serving the site, the domain and its certificate call no AI model, so a custom domain does not draw on the project's balance no matter how much traffic it carries.

## Why serve docs from your own domain

- **Search authority accrues to your domain.** Links people make to your documentation point at `example.com`, so the authority those links carry lands on the domain you are trying to rank, not on `docsbook.io`.
- **Readers see one company.** The address bar matches the product they came from.
- **The address survives a move.** If you ever leave Docsbook, `docs.example.com` keeps working against whatever serves it next; a `docsbook.io/user/repo` URL does not.

## Before you start

You need two things:

1. **A domain you control**, registered at any registrar.
2. **Access to that domain's DNS settings**, so you can add one record.

## Step 1: open the Custom domain setting

1. Open your documentation while signed in.
2. Click the Float Widget in the bottom right.
3. Open **Settings** → **Custom Domain**.

## Step 2: enter your domain

1. Type your domain, for example `docs.example.com`.
2. Click **Save**.

Docsbook generates the DNS record you need and displays it immediately, with a **Copy** button on every value.

## Step 3: add the DNS record at your registrar

The record type depends on whether you use a subdomain or the root of the domain.

**Subdomain** — recommended, e.g. `docs.example.com`. Add a **CNAME**:

| Name / Host | Type | Value |
|---|---|---|
| `docs` (the subdomain only) | CNAME | `cname.vercel-dns.com` |

**Root or apex domain** — e.g. `example.com`. Most registrars reject a CNAME on the root, so add an **A** record instead:

| Name / Host | Type | Value |
|---|---|---|
| `@` | A | `216.150.1.1` |

> Copy the values from the **Custom Domain** panel rather than from this page. The panel shows the exact target for *your* domain; the values above are the usual defaults and can differ.

### Where the DNS settings live at common registrars

**GoDaddy**

1. Sign in at [godaddy.com](https://godaddy.com).
2. Go to **My Domains** → your domain → **DNS**.
3. Click **Add** and fill in: Type `CNAME`, Name `docs`, Points to `cname.vercel-dns.com`.
4. Save.

**Namecheap**

1. Sign in at [namecheap.com](https://namecheap.com).
2. Go to **Domain List** → **Manage** → **Advanced DNS**.
3. Add a record: Type `CNAME`, Host `docs`, Value `cname.vercel-dns.com`, TTL `3600`.
4. Save.

**Ionos (formerly 1&1)**

1. Sign in and open **Domains**.
2. Select your domain and open **Manage DNS**.
3. Add a record: Type `CNAME`, Subdomain `docs`, Alias `cname.vercel-dns.com`.
4. Save.

Any other registrar works the same way: find the DNS or nameserver panel, add a record of the type shown in the Docsbook panel, and paste the value.

### If you want the root domain instead of a subdomain

Use `docs.example.com` where you can. It is easier to configure and leaves `example.com` free for your product site.

If you do need the root, use the **A** record above — copy the exact IP shown in the Custom Domain panel — and write to [support@docsbook.io](mailto:support@docsbook.io) if your registrar's interface does not offer one.

## Step 4: wait for DNS to propagate

DNS changes usually take 15–30 minutes to become visible and can take up to 48 hours.

Click **Check domain status** in the **Custom Domain** panel. It reports one of three states:

| Status | What it means | What to do |
|---|---|---|
| **Domain verified** (green) | DNS resolves and the domain is live | Nothing; open the site |
| **Waiting for DNS verification** (yellow) | The record is not visible yet | Wait 15–60 minutes and check again |
| **Conflicting DNS record found** (yellow) | Another record on the same name is interfering | Remove the conflicting record and check again |

To confirm from outside Docsbook, run a lookup:

```bash
nslookup docs.example.com
```

The answer should name `cname.vercel-dns.com`. [DNSChecker](https://dnschecker.org) shows the same answer from several countries at once, which is useful while propagation is partial.

## Step 5: let the SSL certificate issue

Once DNS resolves, Docsbook detects the domain, requests a Let's Encrypt certificate, and enables HTTPS. Nothing to click.

Your documentation is then served at:

```text
https://docs.example.com
```

## Troubleshooting

<!-- widget:accordion -->

### The domain still does not work after two hours

1. Check the record in [DNSChecker](https://dnschecker.org) — if it is not visible there, the record is wrong or not saved.
2. Confirm the record type and value match the Custom Domain panel exactly.
3. Open the site in a private browser window, which skips your local cache.
4. Allow up to 48 hours before treating it as a failure.

### The old site keeps showing

Your browser cached it. Press Ctrl+F5 (Cmd+Shift+R on macOS) or open a private window. If the old version persists for more than 24 hours, check the domain status in the panel.

### HTTPS shows a certificate error

The certificate is issued after DNS resolves, so a fresh domain can serve HTTP before HTTPS is ready. Wait an hour, confirm DNS has propagated, and check the domain name for typos. If it persists, write to [support@docsbook.io](mailto:support@docsbook.io).

### The domain shows a Vercel error page

The domain resolves but is not yet attached. Click **Check domain status** in **Settings** → **Custom Domain**, confirm the domain is saved in Docsbook, and confirm the DNS record matches. Allow one to two hours for the two sides to agree.

### Cloudflare proxying blocks verification

Set the DNS record to **DNS only** — the grey cloud, not the orange one. The orange cloud proxies traffic before the domain can be verified, which shows up as a domain that never verifies or as SSL errors. Switch to grey, then click **Check domain status** again.

<!-- /widget -->

## Change or remove the domain

To move to a different domain: open **Settings** → **Custom Domain**, replace the value, click **Save**, and add the DNS record for the new domain. The old domain stops serving your docs.

To go back to the Docsbook address: clear the **Custom Domain** field and click **Save**. Your documentation returns to `docsbook.io/username/repo`.

## After the domain is live

- **Update every link that points at the old address** — your GitHub README, your product site, your email signature, and your social profiles. Links left on the old address send authority to `docsbook.io`.
- **Prefer a subdomain per purpose** — `docs.example.com`, `guide.example.com`, `api.example.com`. Putting docs on the root competes with your main site.
- **Watch the traffic that arrives.** [Web analytics](../../analytics/tracking/overview.md) reports views, referrers and search queries against the new domain from the first visit.

## Next steps

- [Enable AI translations](../../translation/settings.md) — each language is served under the same domain as its own indexed path.
- [Restrict who can read your docs](./sso.md) — a custom domain and a password or SSO gate work together.
- [Manage your documentation site](../getting-started/managing-docs.md) — the rest of the settings panel.
