---
title: "Webhook Events Reference"
description: "Subscribe to Docsbook workspace events — content indexed, translations, AI chat, feedback, plan changes — with HMAC-signed retries and typed payloads."
---

# Webhooks

Docsbook can notify your systems about events that happen inside a workspace —
new content indexed, translations needed, chat questions asked, traffic anomalies
and more. Each webhook is **typed**: you subscribe to one specific event, and
Docsbook only POSTs to your URL when that exact event fires.

## How it works

1. You register a webhook with `event_type`, `url`, and an optional `secret`.
2. When the event occurs, Docsbook enqueues a delivery (outbox pattern).
3. The worker (Vercel cron, every minute) POSTs the JSON body to your URL.
4. We retry **up to 3 attempts** with exponential backoff (1s, 10s, 60s).

### Request format

```
POST https://your-url.example.com
Content-Type: application/json
User-Agent: Docsbook-Webhooks/1.0
X-Docsbook-Event: content.indexed
X-Docsbook-Signature-256: sha256=<hex hmac of body>
X-Docsbook-Delivery: 12345
X-Docsbook-Attempt: 1
```

```json
{
  "event": "content.indexed",
  "workspace_id": 42,
  "occurred_at": "2026-05-23T12:34:56.000Z",
  "data": { /* event-specific payload */ }
}
```

### Verifying signatures

```ts
import crypto from "node:crypto"
const expected = "sha256=" + crypto.createHmac("sha256", SECRET).update(rawBody).digest("hex")
if (expected !== req.headers["x-docsbook-signature-256"]) reject()
```

A 2xx response = delivered. Anything else triggers retry until the attempt budget is exhausted.

## Seeing what your workspace emits

The **Feeds** panel in your admin shows every event the workspace produced, newest first —
**including events no alert was watching**, and every MCP tool call made against it. You do not need a webhook registered to see the feed
fill up, which is the point: it is how you find out which events your docs actually emit before you
decide what to be notified about. The feed is live — it refreshes itself every few seconds while
you're looking at it, so there is no time range to pick and nothing to remember to reload.

### Picking a feed

Which feed you're reading — the built-in ones or a list you saved — is picked from rows in the
sidebar's **Feeds** section rather than a page of its own; the row you're on is highlighted, and a
`+` on the section creates a new list from an empty filter. There is no separate title above the
feed: the highlighted row already says what you're looking at.

Four feeds are built in — **All events** (unfiltered), **Reader events**, **Reader
feedback** and **MCP calls** — so there is something to open on your first visit, before
you have saved anything of your own. **Reader events** is everything the people reading your docs
did — pages read, searches run, questions asked of the AI, feedback left — and **MCP calls** is
every metered call an agent made; both are feeds to read, since neither kind of event is one an
alert can be attached to. They are starting filters rather than saved lists, so they
cannot be deleted and nothing can be pointed at them directly. Narrow one and **Save as list**
turns it into a feed of your own, which appears as its own row in the sidebar and is the form an
alert can be attached to.

### Reading the feed

The feed reads in day sections, and each item is **one line**: the reader's avatar when a reader
caused the event (a plan, usage or MCP event has nobody to attribute it to), a coloured tile for its
type, the event name, the one-line summary, and where it went. Status, event type and destination
show as small glyphs with the word a click away in a popover, so the whole thing stays one line.
Times are clock times, since the day is already named by the section above. Clicking a row expands
it in place to show the full event — every delivery attempt with its response, replay, and the raw
payload. An event carries a single status, folded from its deliveries with the worst outcome
winning:

| Status | Meaning |
|---|---|
| `delivered` | Every destination accepted it. |
| `pending` | Queued; the worker has not attempted it yet. |
| `retrying` | A destination refused it and it is inside the attempt budget. |
| `failed` | A destination refused it and the budget is exhausted. |
| `not sent` | It happened, and no alert was subscribed to it. |

### MCP tool calls in the feed

The feed also shows **every MCP tool call an agent made against this workspace**, alongside the
events your docs dispatched. One line per call: the tool it called, whether it worked, how long it
took and what it cost at the list price on the [MCP rate card](/ai/mcp). Failed calls say so.
Calls that were not about any one project — describing the server, listing your projects, creating
one — belong to your account rather than to a project, so they appear in no project's feed.

They are shown **by default**; there is nothing to switch on. In the **Add event** picker they sit
in their own **MCP calls** section, filtered by the call's *billing class* — `mcp.read`,
`mcp.write`, `mcp.query`, `mcp.egress`, `mcp.generate`, `mcp.agent` — rather than by tool name,
which is the axis that costs you money and the one that keeps working as new tools ship. The tool's
own name is on every row and in every payload, so filtering to one tool is a payload search away.
Free calls (`get_info`, `find_skill`, `find_widget` and the rest of discovery) are never metered
and so leave no row.

A tool call was never forwarded anywhere, so it reads as **not sent** and, like reader activity, it
drops out the moment you filter by destination or by a delivery status. Pinning a *visitor* also
drops it: an agent holding a token is not one of your readers, and counting its calls as somebody's
browsing would be wrong.

### Narrowing the feed

Filter the feed by event type, status, destination, visitor, a completed goal, or free text matched
anywhere in the payload — one toolbar row above the feed, no title above it. Each of the first five
facets is an icon button: hover or focus it to see its name, and once it's set it fills in with the
value itself, and clicking that value edits it again. Free text is its own always-visible search box
at the end of that row rather than a facet you open first. A visitor filter is one click away
from **Analytics** — open a reader there and jump straight to everything they did — one click away
from a row's own avatar in the feed itself, or a pasted-in id by hand. Pinning a reader widens what
the feed searches: alongside the events your docs dispatched, it pulls that reader's own activity on
the site — the pages they read, what they searched, what they asked — so a pinned feed is everything
that reader did, not only the parts an alert could have fired on. It also puts a card above the
feed saying who that reader is: where they read from, on what device, system and browser, the
language they read in, the page they keep coming back to, how long they have spent reading your
docs in total, the goals they have reached, and what they are worth today as well as what they
might still be. The card is for a single pinned reader
only, since a goal filter is a crowd and one country and one browser averaged over a crowd
describe nobody. Saving a filter turns it into
an **event list** — so narrowing the feed and defining what to be notified about are the same
gesture. Test pings appear in the feed like any other event; a replay shows up as another attempt
under the event it belongs to. **Export** downloads exactly what you are looking at, filters applied
and unbounded by time, as CSV, JSON or NDJSON. It sits at the end of that same toolbar row next to
**Set up alert** — the two controls that act on the whole view rather than on one event.

## Notifiers: where events go

A **notifier** is a destination — a channel, its URL and its credentials — and it lives apart from
the events it carries. You create it once — **Set up alert** in the title row, or **New notifier**
at the bottom of **Add notifier** — and then tick it onto as many event lists as it should serve. One
Slack channel fed by three lists is one notifier, with one signing secret, paused or deleted in one
place.

The notifiers already firing on the list you are looking at sit beside the filter chips as labelled
chips of their own — each with its channel's real mark, its name, and `paused` when it is switched
off. Clicking one opens that notifier, so you can see what a list delivers to, and change it,
without leaving the feed. A notifier that fires on some *other* list — or on none yet, which is
where every new one starts — is reached from the **Add notifier** menu, where each row has an edit
control beside its checkbox.

Untick a list and the notifier stops firing on it; untick the last one and the destination stays,
attached to nothing, delivering nothing until you point it somewhere again. Deleting an event list
does the same to whatever fired on it — a subscription is never widened by losing its list.

Only saved lists can be served: the built-in feeds, **All events** among them, are filters rather
than lists, so save the one you want as a feed of your own first.

## Event catalog

Registering **any** webhook requires the **Business** plan (see [Webhook count limits](#webhook-count-limits) below) — the "Min plan" column below is the additional capability an event itself needs on top of that; for the three "advanced" events, Business already satisfies it.

| Event | Min plan | Payload fields |
|---|---|---|
| `content.indexed` | Business | `pages_count`, `relations_count`, `indexed_at` |
| `content.outdated` _(deprecated — no longer fired automatically)_ | Business | `last_indexed_at`, `repo_head_sha` |
| `translation.needed` | Business | `source_path`, `language` |
| `translation.completed` | Business | `source_path`, `language`, `origin` |
| `translation.outdated` | Business | `source_path`, `language`, `source_hash_changed` |
| `chat.question_asked` | Business | `question`, `answered`, `chat_id` |
| `chat.no_answer` | Business | `question`, `chat_id` |
| `chat.negative_feedback` | Business | `chat_id`, `question`, `answer` |
| `search.no_results` | Business | `query` |
| `search.popular` | Business | `query`, `count_24h` |
| `traffic.spike` _(advanced event)_ | Business | `path`, `views`, `baseline` |
| `traffic.drop` _(advanced event)_ | Business | `path`, `views`, `baseline` |
| `feedback.received` | Business | `path`, `rating`, `comment` |
| `plan.upgraded` | Business | `from`, `to` |
| `plan.downgraded` | Business | `from`, `to` |
| `usage.limit_approaching` | Business | `metric` (`ai`\|`translation`), `used`, `limit` |
| `mcp.tool_called` _(advanced event)_ | Business | `tool_name`, `args` |

## Webhook count limits

Each workspace has a maximum number of active webhooks, based on plan:

| Plan | Max webhooks |
|---|---|
| Free | 0 |
| Pro | 0 |
| Business | 25 |

Webhooks are a **Business-exclusive** capability — Free and Pro/Pro+ workspaces cannot register any webhooks; only Business unlocks them (up to 25 per workspace).

## Registering a webhook

### Via REST

```bash
curl -X POST https://docsbook.io/api/webhooks \
  -H "Content-Type: application/json" \
  -d '{"workspace_id": 42, "event_type": "content.indexed", "url": "https://you.example.com/hook"}'
```

The response includes the `secret` exactly once — store it.

`event_type` accepts either spelling of an event name: the dotted form used throughout this page (`content.indexed`) or the underscored form (`content_indexed`). Both register the same subscription.

### Optional Authorization header

Some receivers (for example a Claude Code routine trigger URL) require their own
bearer token on every request, separate from HMAC signature verification. Pass
`auth_header` when creating the webhook and Docsbook sends it verbatim as the
`Authorization` header on every delivery:

```bash
curl -X POST https://docsbook.io/api/webhooks \
  -H "Content-Type: application/json" \
  -d '{"workspace_id": 42, "event_type": "content.indexed", "url": "https://you.example.com/hook", "auth_header": "Bearer sk-..."}'
```

If the value has no space, it's sent as `Bearer <value>`; if it already contains
a scheme (e.g. `Bearer sk-...`), it's sent unchanged.

### Via MCP

Each event has a dedicated MCP tool, so an AI agent can subscribe to a specific
notification stream without picking strings:

```
register_webhook_content_indexed(workspace_id: 42, url: "https://...")
register_webhook_translation_needed(repo: "owner/repo", url: "https://...")
register_webhook_traffic_spike(workspace_id: 42, url: "https://...")
```

Other MCP tools:

- `list_webhooks(workspace_id)` — Free
- `unregister_webhook(webhook_id)` — Free
- `test_webhook(webhook_id)` — Free (enqueues a synthetic ping)
- `list_webhook_deliveries(webhook_id)` — Pro
- `replay_webhook_delivery(delivery_id)` — Pro

### REST endpoints

- `GET  /api/webhooks?workspace_id=X` — list
- `POST /api/webhooks` — create
- `PATCH /api/webhooks/:id` — rename, pause/resume, or re-point at another event list
- `POST /api/webhooks/:id/attach` — `{ "list_id": N }`, serve one more list from the same
  destination (same URL, same secret)
- `DELETE /api/webhooks/:id` — delete
- `POST /api/webhooks/:id/test` — test ping
- `GET  /api/webhooks/:id/deliveries` — recent deliveries
- `POST /api/webhook-deliveries/:id/replay` — re-enqueue an existing delivery

## Retry & failure semantics

- Worker runs every minute via Vercel cron.
- A delivery is attempted up to 3 times.
- Backoff is enforced from `created_at` of the row: 1s, 10s, 60s.
- After the 3rd failure → `status = "failed"`. Use `replay_webhook_delivery` to re-attempt.
- Response code and (truncated) body are stored on every delivery row.
