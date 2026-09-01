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

The **Feeds** section opens on a page of cards — one per feed, each with a line saying what it
holds, plus a **Create your own feed** card at the end. Opening a card switches to that feed itself,
with no title or back link above it: you got here by picking a card, and the sidebar row for **Feeds**
is the way back to them.

The same feeds are also rows under that sidebar section, for switching between them without leaving
the one you're reading — but that list starts **closed**. Hover the **Feeds** row and a chevron
takes over from its icon; click it to show up to five feeds, most-recently-opened first, with
**Show N more** for the rest, and Docsbook remembers whether you left it open the next time you're
back. The `+` that creates a new list from an empty filter sits both on that row and as a card in
the gallery.

Seven feeds are built in, so there is something to open on your first visit before you've saved
anything of your own: **Reader events** (everything people reading your docs did — pages read,
searches run, questions asked of the AI, feedback left), **Translations** (every language generated,
outdated or still needed), **Language events** (which languages readers switch the docs into),
**Chat events** (questions the AI assistant was asked, where it came up empty, which answers got a
thumbs-down), **Reader feedback** (thumbs-down and comments, on a page or an answer), **MCP calls**
(every metered call an agent made), and **All events** — everything, unfiltered, last on the list
since it's the one you reach for when none of the named ones fit. **Reader events**, **Language
events** and **MCP calls** are feeds to read rather than to subscribe to, since none of their events
is one an alert can be attached to; the other four are exactly what you'd point a notifier at. All
seven are starting filters rather than saved lists, so they cannot be deleted and nothing can be
pointed at one directly — narrow one and **Save as list** turns it into a feed of your own, which
appears as its own row and is the form an alert can be attached to.

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
and unbounded by time, as CSV, JSON or NDJSON — unbounded because the feed itself carries no time
range: it is live, and a file narrower than the view it copies is worse than no file. It sits at the
end of that same toolbar row beside **Set up Prompt** and **Set up alert** — the three controls that
act on the whole view rather than on one event.

### Have a prompt run on a feed

An alert forwards a feed's events to a person. **Set up Prompt**, next to it on the same row, hands
them to your assistant instead: pick a prompt and it runs by itself every time something lands in
this feed, with no one watching. The button carries a count, so a feed with something on it never
looks like a feed with nothing on it, and each armed prompt gets a chip beside the destination chips
— filled while it is running, hollow while it is paused, with its last run in the tooltip.

Clicking a chip does not open its settings. It opens the **conversation** the prompt has been
having: the transcript of what it actually did the last time this feed moved, in the assistant's
Triggers group. That is the only thing that can tell you a prompt is working rather than merely
switched on.

A prompt watches a **saved** feed, so a view you have narrowed but not saved yet says so and points
at **Save as list**. The same arming is available from the other side — the Prompts page's
**On event** picker now lists your feeds above the individual events — and deleting a feed
disarms whatever watched it rather than deleting the prompt.

### What it all cost

Every row in the feed carries a price, and one row at a time is not a column anyone can add up.
**See usage** on the balance card in the sidebar swaps the stream for the sum: what this project's
money went on over a window, dearest first, in three sections. It is not on the feed's own toolbar,
because the figure is about the whole project rather than about the feed you are looking at.

| Section | One row per | What the figure is |
|---|---|---|
| **AI & tokens** | surface and model | What each AI answer, translation or indexing run was priced at |
| **MCP tool calls** | tool | The list price of the calls that tool actually made |
| **Events logged** | event type | What recording that traffic costs, at the rate card |

The first two are **charged**: that money came off the project's balance. The third is **not** —
events are priced so the traffic is not invisible, and nothing is deducted for them. The two totals
are therefore printed as two figures under two different words, and each section carries a `charged`
or `not charged` badge, because one number covering all three would be a bill for money nobody took.

Pick a window of **24 hours**, **7 days** or **30 days**. There is nothing longer because there is
nothing longer to read: reader analytics are kept for 30 days and the AI ledger is pruned to match,
so a 90-day button would answer for 30 days under the wrong label.

**Export** here offers the breakdown itself as a CSV — one line per model, tool or event type, with
its count and its cost as a plain number you can sum, and a column saying whether that line was
charged — as well as the raw events behind it, bounded by the window you are looking at.

The same screen is what **See usage** opens from the sidebar's balance notice — the card that warns
when this project is running low. Topping up is in the account menu's **Balance** block: one answers
how much is left, this one answers what took it.

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
