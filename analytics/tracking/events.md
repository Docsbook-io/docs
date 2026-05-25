---
title: "Tracked Events Reference"
description: "Every interaction Docsbook tracks — AI chat opens, code copies, outbound clicks, sidebar navigation, language switches — for engagement insights."
---

# Events Analytics

Track what visitors *do* on your docs — not just what they view.

## Tracked Events

| Event | What it means |
|---|---|
| AI chat opens | Visitor opened the AI assistant panel |
| AI queries | Number of questions asked to the AI |
| Code copies | Visitor copied a code block |
| Outbound link clicks | Visitor clicked an external link |
| Sidebar navigation | Visitor navigated via the left sidebar |
| Language switches | Visitor changed the display language |

## How to Open

Float Widget → **Analytics** tab → scroll to the **Events** section.

Events are shown as a breakdown with counts and percentages for the selected time range.

## How to Use This Data

**High AI opens, low queries** → Visitors are curious about AI but find the suggested questions unclear. Try updating your [custom questions](https://docsbook.io/Docsbook-io/docs/analytics/tracking/events).

**High code copies** → Your code examples are useful. Consider adding more.

**High language switches** → Visitors want content in their language. [Enable more translations →](https://docsbook.io/Docsbook-io/docs/translation/settings)

**High outbound clicks on a specific page** → That page is a good traffic handoff point to your product.

## Drill into a single visitor (MCP, PRO+)

You can investigate what one specific anonymous visitor actually did, end-to-end, via the MCP server.

```text
get_top_visitors(period: "7d", limit: 25)
  → [{ visitor_id: "a1b2…", pageview_count: 14, first_seen, last_seen, country }, …]

get_visitor_activity(visitor_id: "a1b2…", period: "7d")
  → { first_seen, last_seen, country, language, pageview_count,
      events: [
        { event: "docs.pageview",     at, path: "guides/quick-start" },
        { event: "docs.page_feedback", at, path: "guides/quick-start", details: { vote: "down" } },
        { event: "docs.pageview",     at, path: "faq" },
        …
      ] }
```

**`visitor_id` is a salted SHA-256 hash** of the visitor's IP scoped to your workspace. It's stable across sessions (the same person visiting next week gets the same id), but raw IPs never leave Axiom and are never exposed via MCP.

Use cases:

- "Who looked at our pricing page three times then dropped off?" → filter `get_top_visitors`, then `get_visitor_activity` for each candidate.
- "This support ticket mentions a confusing page — let me see their full journey." → grab their `visitor_id` from `get_page_journeys` and drill in.
- "Are AI questions and pageviews coming from the same people, or different cohorts?" → cross-reference `get_visitor_activity` across visitors.

Only events that carry server-side IP (`docs.pageview`, `docs.page_feedback`, `landing.cta_click`) can be attributed to a visitor. Pure client-side events (theme toggles, code copies) are visible in aggregate but not per-visitor.

---

> **See your events data live.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
