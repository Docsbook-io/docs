---
title: "Every reader action Docsbook records, and what each one carries"
description: "The complete catalogue of the 36 docs.* events Docsbook records on a documentation site: what fires each one, the fields it carries, and how it is delivered."
tldr: "Docsbook records 36 named docs.* events across seven categories. Every one carries your project name; most carry a page path, and the ones that must survive a tab closing — read time, heading views, exits, outbound and cited-link clicks — are sent with navigator.sendBeacon instead of the ordinary debounced request. There is no tracking switch: an event exists when the feature that produces it exists."
---

# Tracked events

A pageview says which page was opened. It does not say whether the reader
copied the snippet, asked the assistant, scrolled past the intro, or left for
your signup page. This page is the whole list of what else is recorded, field
by field, so you can tell before you build a goal or a funnel whether the thing
you want to measure is already being measured.

## What you get

Thirty-six named `docs.*` events, in seven categories, recorded on every
documentation site with no configuration and no tag manager. Each one is a row
you can filter in Feeds, match a [goal](../reports/goals-and-funnels.md)
against, rank in the [analytics overview](./overview.md), or read back per
visitor over MCP.

Recording them costs nothing against your project's balance, and nothing about
the list changes with your plan.

## The catalogue

Every event carries your project's full name (`owner/repo`). The **Also
carries** column is what it adds on top of that. Events marked **beacon** are
delivered by `navigator.sendBeacon` at the moment the reader leaves; the rest
ride the ordinary logging transport, which batches for two seconds.

### AI assistant

| Event | Fires when | Also carries |
|---|---|---|
| `docs.ai_open` | The reader opens the assistant panel | `conversation_id` |
| `docs.ai_query` | A question is submitted | `question`, `answer`, `conversation_id`, `turn` |
| `docs.ai_like` / `docs.ai_dislike` | A thumb is given on an answer | `path`, `conversation_id`, `question` |
| `docs.ai_copy` | An answer is copied | `conversation_id` |
| `docs.ai_navigate` | A link the answer *cited* is clicked | `query`, `path`, `conversation_id`, `source` (`badge` or `sources`) — **beacon** |
| `docs.ai_outbound` | A link in the answer takes the reader off your site | `href`, `host`, `conversation_id`, `question` — **beacon** |
| `docs.ai_conversation` | Once per conversation, when its first successful answer is titled | `topic`, `intent`, `competitor`, `question`, `answer_completeness`, `gap_type` |
| `docs.ask_ai_outline` | "Ask AI" is pressed from the page outline | — |

`docs.ai_navigate` and `docs.ai_outbound` are deliberately two events, not one.
The first says the reader trusted the answer enough to open the page it cited;
the second says the assistant handed them to your app, your repo, or somewhere
else entirely — a commercial question, not a comprehension one.

### Search

| Event | Fires when | Also carries |
|---|---|---|
| `docs.search_open` | The on-page search box is opened | — |
| `docs.search_navigate` | A search result is clicked | `query`, `path` |
| `docs.search_no_result` | A query returns nothing | `query` |

### Reading and engagement

| Event | Fires when | Also carries |
|---|---|---|
| `docs.pageview` | A page is served | `path`, `lang`, `trafficType`, `referrer`, `userAgent`, `source`, and the country/region/city/coordinates the edge resolved |
| `docs.read_time` | The reader leaves a page | `path`, `seconds` — **beacon** |
| `docs.heading_view` | A heading scrolls into view | `path`, `heading` (as `#anchor`) — **beacon** |
| `docs.scroll_to_top` | The back-to-top control is used | — |
| `docs.widget_toggle` | A content widget is opened or closed | `widget`, `enabled` |
| `docs.theme_toggle` | Light/dark is switched | `theme` |
| `docs.language_switch` | The language picker is used | `from`, `to` |

`docs.pageview` is the one event the browser does not send. It is written
server-side, so it exists for readers with JavaScript disabled — which is also
why a visit made of nothing but pageviews is treated as a crawler. On pages
served from the cache the pageview is beaconed from the browser instead, and
the ingest endpoint fills in the same IP and geography, so the two paths
produce the same row.

`seconds` is emitted raw and clipped at 300 seconds before any report sums it.
That clip, and why it exists, is in [read time](../reports/read-time.md).

### Content actions

| Event | Fires when | Also carries |
|---|---|---|
| `docs.copy_code` | A code block is copied | — |
| `docs.copy_page` | The whole page is copied | — |
| `docs.copy_markdown` | The page is copied as Markdown | — |
| `docs.copy_dropdown` | The copy menu is used | `action` |
| `docs.edit_on_github` | "Edit on GitHub" is clicked | `path` |

### Navigation

| Event | Fires when | Also carries |
|---|---|---|
| `docs.sidebar_nav` | A sidebar entry is clicked | `path` |
| `docs.heading_nav` | An entry in the on-page outline is clicked | `heading`, `path` |
| `docs.page_nav` | Previous/next is used | `direction` (`prev` or `next`), `path` |
| `docs.internal_link` | An in-page link to another of your pages is clicked | `href` |

`docs.heading_nav` and `docs.heading_view` share the `#anchor` format on
purpose, so a section aggregates the same whether readers jumped to it or
scrolled to it.

### Exits and sources

| Event | Fires when | Also carries |
|---|---|---|
| `docs.outbound_link` | A link leaves your documentation | `href`, `host`, `path` — **beacon** |
| `docs.header_link` | A link in your site header is clicked | `label`, `href` |
| `docs.utm` | A visit arrives with campaign tags | the `utm_*` parameters as given |
| `docs.page_exit` | The reader leaves the site or reloads | `path` — **beacon** |
| `docs.claim_banner_seen` | The publish/claim banner is shown | `claim_token` |
| `docs.claim_click` | The publish/claim banner is clicked | `claim_token` — **beacon** |

`docs.page_exit` fires only on a real exit or reload. In-site navigation does
not produce one, which is what makes the last `docs.page_exit` of a visit the
page the reader actually left from.

### Feedback

| Event | Fires when | Also carries |
|---|---|---|
| `docs.page_feedback_up` | A page is voted helpful | `path`, country |
| `docs.page_feedback_down` | A page is voted unhelpful | `path`, country |

The direction lives in the event **name**, not in a `vote` field: the event
store's schema is a fixed set of field names, and an unrecognised field is
rejected outright rather than dropped. Votes are recorded through a server
route so a webhook can fire on them; if that request fails, the browser records
the same event directly, so the count survives.

## Automatic, or dependent on a feature

There is no tracking toggle anywhere in Docsbook, and no `enabled` flag on any
event. Every event above is emitted whenever the thing that produces it exists,
which splits the list in two:

| Always | Only once the feature is in use |
|---|---|
| Pageviews, read time, heading views, exits, copies, internal and outbound links, sidebar and prev/next navigation, search, theme, scroll-to-top | Every `docs.ai_*` event (needs the reader-facing assistant, which is a paid capability — see [pricing](https://docsbook.io/pricing)), `docs.language_switch` (needs a second language), `docs.edit_on_github` (needs a linked repository), `docs.utm` (needs links you tagged yourself), `docs.widget_toggle` (needs a widget on the page), the feedback pair (needs the vote widget), the two `docs.claim_*` events (only on an unclaimed site) |

An "empty" event in your reports therefore has two possible readings, and they
are different: nobody did it, or nothing can do it yet.

## How it is delivered

Ordinary events go through a transport that batches for two seconds and posts
over `fetch`. That is fine for a click that leaves the page standing, and it
loses everything for a click that does not — which is why the events tied to
leaving take a second path:

1. Components register an **exit collector**. On `pagehide`, every collector is
   drained into **one** beacon, capped at 100 events, posted to a same-origin
   endpoint.
2. On iOS, `visibilitychange → hidden` triggers the same flush, because
   `pagehide` is unreliable there.
3. Collectors return only what they have not already sent, so an iOS flush
   followed by a real exit does not double-count, and a page restored from the
   back/forward cache can flush again.

Heading views are collected with an `IntersectionObserver` at threshold 0 with
a `-15%` bottom margin, and each heading is unobserved once seen: a heading
counts once per pageview, and only after it clears the bottom of the viewport
rather than the instant it peeks in.

## Why this is the right way

| Rule | Why it works on the browser that runs it | Source |
|---|---|---|
| Exit-time events go by beacon, never a debounced `fetch` | Beacon requests are "guaranteed to be initiated before page is unloaded and are allowed to run to completion without requiring blocking requests" | [W3C Beacon API](https://www.w3.org/TR/beacon/) |
| Do not block the exit to get the event out | The alternatives the Beacon spec was written against — "issuing blocking requests via synchronous XMLHttpRequest's, inserting no-op busy loops" — "block the user agent from executing time-critical operations … and hurt the user experience" | [W3C Beacon API](https://www.w3.org/TR/beacon/) |
| Listen on `pagehide`, and additionally on visibility change | `unload` "is still unreliable, so avoid using it unless absolutely necessary"; `pagehide` "fires in all cases where the `unload` event fires" and also on entry to the back/forward cache | [web.dev: bfcache](https://web.dev/articles/bfcache) |
| Detect heading views with `IntersectionObserver`, not a scroll handler | Position calculation by DOM query is "known to cause (expensive) style recalculation and layout", and sites "abusing scroll handlers" cause "jank on scroll"; asynchronous delivery "eliminates the need for costly DOM and style queries, continuous polling" | [W3C Intersection Observer](https://www.w3.org/TR/intersection-observer/) |
| Count a heading once it has cleared the fold, using `rootMargin` | `rootMargin` applies "offsets … effectively growing or shrinking the box that is used to calculate intersections" — the honest way to say "actually reached", not "technically overlapped" | [W3C Intersection Observer](https://www.w3.org/TR/intersection-observer/) |
| A page that keeps counting while hidden measures the wrong thing | The Page Visibility API exists because "web developers have been designing web pages as if they are always visible" | [W3C Page Visibility Level 2](https://www.w3.org/TR/page-visibility-2/) |

## How to read one visitor's events

Two MCP tools reconstruct one anonymous visitor's path end to end, and both are
reads: `get_top_visitors` lists the busiest visitors over a period,
`get_visitor_activity` returns one visitor's events in order.

```text
get_top_visitors(period: "7d", limit: 25)
  → [{ visitor_id: "a1b2…", pageview_count: 14, first_seen, last_seen, country }, …]

get_visitor_activity(visitor_id: "a1b2…", period: "7d")
  → { first_seen, last_seen, country, language, pageview_count,
      events: [
        { event: "docs.pageview",           at, path: "guides/quick-start" },
        { event: "docs.page_feedback_down", at, path: "guides/quick-start" },
        { event: "docs.search_no_result",   at, query: "rotate api key" },
        … ] }
```

`visitor_id` is a salted hash of the reader's IP scoped to your project; raw
IPs are never returned. See
[how measurement works](../how-measurement-works.md).

## Limits and open questions

- **No webhook can fire on a `docs.*` event.** These events live in the event
  warehouse, and nothing dispatches them. They can be *filtered* in Feeds and
  saved into a list, and they read as `not_sent` there because that is what
  they are. Alerting on reader behaviour goes through the derived webhook
  events — traffic drop, popular search, no-result search — not through this
  catalogue. See [webhooks](../../reference/webhooks.md).
- **Events are counted per event, not per visit.** One reader copying five
  snippets is five `docs.copy_code` rows. Anything that has to be counted per
  visit — bounce, conversion, a goal — is derived by reconstructing the visit,
  not by summing this list.
- **A reader with JavaScript disabled contributes only `docs.pageview`.** Every
  other event above needs a running script, which is exactly what the
  behavioural crawler filter relies on.
- **`question` and `answer` fields carry whatever the reader typed.** Raw event
  reads are passed through a redactor that masks any field whose key or value
  looks like a token, key, JWT or authorization header, but a reader who types
  something personal into your assistant has typed it into your event store.
  Retention is 30 days.
- **Under question: the catalogue is authoritative, but not exhaustive of the
  stream.** What is verifiable is that these 36 names are the ones every
  surface — the panel, Feeds, goal validation, MCP — reads from one shared
  list, so a goal can only be declared on a name in it. What is not: a handful
  of additional `docs.*` names are emitted by the unclaimed-site teaser flow
  and are not in that list, which means they reach the store and are invisible
  in the UI. Treat the 36 as the complete set of events you can *act* on, not
  as a complete inventory of every string in the stream.

## Related

- [How measurement works](../how-measurement-works.md) — visitor identity, bot filtering, retention and privacy for everything on this page
- [Analytics overview](./overview.md) — the cards and figures these events feed
- [Goals and funnels](../reports/goals-and-funnels.md) — declaring an outcome on one of these event names
- [Read time](../reports/read-time.md) — `docs.read_time` as a report
- [Webhooks](../../reference/webhooks.md) — the events that *can* notify you
