---
title: "How a page gets discovered, re-crawled and measured"
description: "Sitemaps, IndexNow pushes, Search Console reporting and the caches between a commit and a crawler — what is fast, what is slow, and what actually gates it."
tldr: "Docsbook advertises every page through a per-owner sitemap linked from robots.txt, pushes changes to IndexNow engines for its own apex-hosted sites, and reads Google Search Console positions back into the admin panel. A change published through Docsbook invalidates its caches immediately; a commit pushed straight to GitHub is picked up by timers instead, within 30 minutes to 24 hours."
---

# How a page gets discovered and re-crawled

There are three separate questions here and they have three different answers: how a
crawler **finds** a page, how fast it learns the page **changed**, and what you can
**see** about the result. This page answers all three with the actual timers.

## How does a crawler find a page at all?

Two pull-based paths, both automatic:

1. **The sitemap.** Each owner gets one `sitemap.xml` listing every page of every
   indexed repository, plus one entry per genuinely translated locale. It is served
   at the site's own host and rebuilt at most once an hour.
2. **`robots.txt` names it.** Every Docsbook-hosted host serves a `robots.txt` with
   a `Sitemap:` line pointing at the sitemap that belongs to that host. The apex
   carries several: its own, one per product documentation site, and one per public
   showcase site with SEO switched on — because those sites are only reachable from
   the apex, so nothing else would point a crawler at them.

Beyond that, the sidebar is rendered as real HTML links on every page, so every
crawl of any page is also a crawl of the map of your content.

## How fast does a change reach an engine?

**Push.** When a change is published *through Docsbook* — the editor, an agent, the
MCP tools, a workspace settings change — Docsbook invalidates its own caches for
that site immediately, and for sites hosted on the `docsbook.io` apex it also sends
an IndexNow notification naming the site root and its sitemap. That call is
fire-and-forget: it names two URLs rather than the changed pages (at that point only
"this site changed" is known, and the sitemap lets a participating engine work out
the specifics), it never blocks or fails the publish, and an IndexNow outage is
logged rather than surfaced.

**Pull.** Everything else waits for a crawler to come back and re-read the sitemap.

**And the honest part:** *Docsbook has no GitHub webhook.* A commit pushed straight
to your repository, bypassing Docsbook, triggers no invalidation and no IndexNow
push. It is picked up by timers:

| Timer | Window | What it refreshes |
|---|---|---|
| Repository file tree | 30 minutes | Which pages exist |
| Default branch and commit dates | 1 hour | `lastmod`, `dateModified` |
| Cached anonymous page HTML | 24 hours | What a crawler is served |
| `sitemap.xml` and `robots.txt` | 1 hour | The crawlable index |
| Semantic index sweep | hourly, batched | On-site and AI search, not Google |

So a page edited in Docsbook is current for the next crawler within seconds; a page
pushed directly to GitHub can be served from cache for up to 24 hours. The 24-hour
window is a deliberate trade: bot crawls re-rendering every page every hour were the
single largest line on the hosting bill, and doc pages are read far more often than
they are written.

## What happens when a page is renamed?

A move made **through Docsbook** writes the old page path → new page path into a
`.docsbook/redirects.json` file in the same commit as the move, and the old URL then
answers a **308 permanent redirect** to the new one. Permanent, not temporary,
because a temporary redirect tells search engines to keep the dead URL as the
canonical one — which loses exactly the ranking the redirect exists to preserve. The
map holds up to 500 entries, oldest dropped first, and it is only consulted for
requests that were already heading for a 404.

A rename made by moving the file yourself in git gets **no** redirect: nothing wrote
the map. You can add the entry by hand — it is a plain file in your repository, and
both sides are page paths, the thing that appears in a URL.

## What does the Search Console integration actually do?

It reads. Data flows one way, Google → Docsbook, over the read-only Search Analytics
scope. Docsbook does not submit URLs, request indexing, or write anything into your
Search Console account, and there is nothing for you to connect: Docsbook reads a
Search Console **domain property** on `docsbook.io`, which by Google's definition
"aggregates data for all subdomains, protocols, and subpaths", and filters the rows
down to the URLs that belong to your site.

What lands in the admin panel: average position, impressions, clicks, the queries
your pages rank for, a daily trend, and an "worth improving" set — the queries
sitting at position 5–20, already visible and not yet winning. Windows of 7, 28 and
30 days; 7 is the default because 30 days of history is all that is kept, so it is
the only window with an equal period behind it to compare against.

Three constraints are shown rather than hidden. Google's data lags about two days,
so a "data through" date is always on screen. A refresh is allowed once every 24
hours, because Google itself refreshes daily and a second pull would spend quota to
return identical numbers. And headline totals are rolled up from the **page** grain,
not by summing the query rows: Google withholds low-volume queries for privacy, so
the query breakdown covers a fraction of real traffic. Our own measurement, on
Docsbook's own documentation property: 91 impressions when totalled by query against
413 when totalled by page. That is one site on one day and is quoted to show the
direction of the gap, not its size on yours.

## Why these mechanisms (evidence)

| Mechanism | What the source actually says | Source |
|---|---|---|
| Sitemap advertises, it does not guarantee | "submitting a sitemap is merely a hint: it doesn't guarantee that Google will download the sitemap or use the sitemap for crawling URLs" | [Build a sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap) |
| `Sitemap:` in `robots.txt` is a real discovery path | "Google, Bing, and other major search engines support the `sitemap` field in robots.txt", with "no limit to the number of sitemaps you can include" | [robots.txt spec](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt) |
| IndexNow is a recrawl hint, not indexing | "Submitting a URL does not guarantee immediate indexing"; the engine still "evaluates whether it should crawl the URL based on its crawl quota, scheduling logic, and quality signals" | [IndexNow FAQ](https://www.indexnow.org/faq) |
| One IndexNow call, one host | The submission body carries a single `host` field, and the documented error for breaking it is "422 — Unprocessable Entity — In case of URLs which don't belong to the host"; up to 10,000 URLs per post | [IndexNow docs](https://www.indexnow.org/documentation) |
| A domain property covers every subdomain | "A Domain property aggregates data for all subdomains, protocols, and subpaths of the property" | [Search Console properties](https://support.google.com/webmasters/answer/34592) |
| The Search Console API can be authorised read-only | `webmasters.readonly` is one of the two scopes the method lists, and it is the one Docsbook requests. The dimensions it groups by — query, page, country, device, date — are all valid values of `dimensions[]` (`date` via the method's "as well as 'date' and 'hour'" clause, not as a filterable dimension) | [Search Analytics: query](https://developers.google.com/webmaster-tools/v1/searchanalytics/query) |
| Query rows undercount on purpose | "To protect user privacy, the Performance report doesn't show all data… we might not track some queries that are made a very small number of times" | [About Search Console data](https://support.google.com/webmasters/answer/96568) |
| `noindex` needs the page to stay crawlable | "For the `noindex` rule to be effective, the page or resource **must not** be blocked by a robots.txt file, and it has to be otherwise accessible to the crawler" — which is why a `noindex` page stays in the sitemap and stays allowed | [Block indexing](https://developers.google.com/search/docs/crawling-indexing/block-indexing) |

## Limits and open questions

- **IndexNow is not sent for customer sites today.** The protocol requires every URL
  in a submission to share one host, and requires a key file at that host's root.
  Docsbook hosts that key on the `docsbook.io` apex only, so pushes go out for
  Docsbook's own documentation and for showcase sites on the apex — not for
  `<owner>.docsbook.io` sites and not for custom domains. Per-tenant key hosting is a
  separate piece of work and is not built.
- **Under question: how fast IndexNow actually is.** Docsbook's code comment says
  "within minutes instead of waiting for their next scheduled crawl". IndexNow's own
  FAQ will only say it "increases the likelihood that important changes are
  discovered and crawled faster", and avoids naming a timeline. Treat minutes as a
  hope, not a measurement — we have published none.
- **Google is not an IndexNow participant.** [indexnow.org](https://www.indexnow.org/)
  names its support as coming from "Microsoft Bing, Naver, Seznam.cz, Yandex, Yep" —
  five engines, and Google is not among them, on that page or in the protocol
  documentation. Google discovery still runs on the sitemap and on ordinary crawling.
- **Under question: how secret the IndexNow key is.** Docsbook treats the key as a
  public identifier — it is hardcoded in the open, and the key file is served
  unauthenticated at the apex root, which is what the FAQ requires ("no login
  required", so a search engine can "confirm domain ownership"). What contradicts
  the "it is not a secret" reading is IndexNow's own protocol page, which says
  ["Only you and the search engines should know the key and your file key
  location"](https://www.indexnow.org/documentation). Both cannot be fully true of a
  file any client may fetch. What the key can do if copied is bounded — it says "this
  host changed", nothing more — but treat "public by construction" as our reading of
  a protocol that does not say it.
- **Search Console coverage stops at Docsbook-hosted hosts.** The domain property
  covers `docsbook.io` and its subdomains. A site on your own custom domain is not in
  that property, so no positions are read for it. Serving those numbers needs a
  per-customer Google authorisation flow, which does not exist yet — use your own
  Search Console account for a custom domain in the meantime.
- **Search Console history is 30 days here.** Google keeps considerably more;
  Docsbook stores a 30-day rolling window per site, which is why the 30-day view has
  no comparison period.
- **Nothing here makes a page rank.** Discovery and re-crawl are the parts Docsbook
  can automate. Whether a crawled page ranks is Google's call on your content, and no
  timer on this page changes it.

## Related

- [SEO — what Docsbook does for search visibility](./README.md)
- [How Docsbook builds the head of a page](./how-it-works.md)
- [Analytics](../analytics/README.md)
- [GEO — being cited by AI assistants](../geo/README.md)
- [AI translations](../translation/ai-translations.md)
