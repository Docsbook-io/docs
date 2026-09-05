---
title: "Every reader action Docsbook records on your docs site"
description: "The full list of events Docsbook records on a documentation site: chat opens, questions, code copies, outbound clicks, navigation, language and heading views."
---

# Events Analytics

Docsbook records what a reader *does* on your documentation site, not only which page they opened. Seven event types are tracked on every site; each is counted per event rather than per visit, and event tracking costs nothing against your project's balance.

## Tracked events

| Event | What it means |
|---|---|
| AI chat opens | Visitor opened the AI assistant panel |
| AI queries | Number of questions asked to the AI |
| Code copies | Visitor copied a code block |
| Outbound link clicks | Visitor clicked an external link |
| Sidebar navigation | Visitor navigated via the left sidebar |
| Language switches | Visitor changed the display language |
| Heading views | Visitor scrolled a heading into view while reading the page |

## How to open the events breakdown

Float Widget → **Analytics** tab → scroll to the **Events** section.

Events are shown as a breakdown with counts and percentages for the selected time range.

## What each pattern means, and what to do about it

Each row below is a shape these events take on a real documentation site, and the move it points at.

**High AI opens, low queries** → Readers open the assistant and then do not ask. The suggested questions are the thing they read first; see [AI chat](../../ai-chat/chat.md) for setting them.

**High code copies** → Your code examples are useful. Consider adding more.

**Heading views concentrated near the top of a long page** → Readers aren't scrolling past the intro. Consider moving key content up or shortening the page.

**High language switches** → Readers want content in their own language. See [translation settings](../../translation/settings.md) for enabling one.

**High outbound clicks on a specific page** → That page is a good traffic handoff point to your product.

## How do I see what one visitor did?

Two MCP tools reconstruct a single anonymous visitor's session on your documentation, end to end: `get_top_visitors` lists the busiest visitors over a period, and `get_visitor_activity` returns one visitor's events in order. Both are analytics reads over the event warehouse — they change nothing.

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

## Related

- [Analytics overview](./overview.md) — the cards and figures these events feed
- [MCP tools reference](../../reference/mcp-tools.md) — `get_top_visitors`, `get_visitor_activity` and the rest of the analytics tools
- [Webhooks](../../reference/webhooks.md) — being told when an event fires instead of checking for it
- [AI usage & cost statistics](./ai-usage.md) — the conversations behind the AI chat events
