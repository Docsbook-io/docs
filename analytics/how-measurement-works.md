---
title: "How Docsbook measures your readers, and why you can trust it"
description: "What Docsbook collects on your docs site and what it refuses to: cookieless visitor identity, two-layer bot filtering, clipped read time, retention, and where the data lives."
tldr: "Docsbook sets no cookie and stores no identifier in the reader's browser — a visitor is a salted hash of their IP, scoped to your project. Bots are filtered twice (user-agent and behaviour), read time is clipped at 300 seconds per segment because background tabs keep counting, and every event is deleted after 30 days."
---

# How measurement works

Documentation analytics usually lie in the same four ways: crawlers counted as
readers, background tabs counted as reading, the owner's own visits counted as
an audience, and percentages quoted over a handful of visits. This page is the
mechanism, written out, so you can check each of those for yourself before you
act on a number.

## What you get

Every figure in the Docsbook analytics panel is derived from one event stream,
under one definition of a visit and one definition of a human — not from a set
of independent counters that can disagree. When a number cannot be said
honestly, you get a dash, a "not measured" label, or a suppressed percentage,
never a confident `0`. And nothing is stored in your readers' browsers to
produce any of it.

## What is collected, and what deliberately is not

Docsbook records **36 named `docs.*` events** on your documentation site — page
views, read-time segments, headings scrolled into view, searches, AI chat
actions, copies, navigation clicks, outbound clicks, feedback votes and exits.
The full list is the [tracked events reference](./tracking/events.md).

Each event carries the project it belongs to, the page path, and whichever of
these apply: seconds, heading anchor, referrer, destination host, language,
User-Agent, and the country/region/city/coordinates the edge resolved from the
request. The reader's IP is attached **server-side**, at the ingest endpoint,
never by the browser.

| Not collected | Why |
|---|---|
| Cookies, `localStorage` or any browser-side identifier for analytics | Nothing has to be stored on the reader's device to count them, so nothing is |
| Cross-site or cross-project identity | The visitor hash is salted with your project's own name, so the same IP on two Docsbook sites produces two unrelated ids |
| Device fingerprinting (canvas, fonts, audio) | Not implemented anywhere in the tracker |
| Form input, keystrokes, session replay, mouse paths | No such collector exists |
| Raw IPs in any report, export or MCP response | The IP stays in the event store; everything downstream sees the hash |
| Secrets that leak into an event | Raw-event reads pass through a redactor that masks any field whose key or value looks like a token, key, JWT or authorization header |

## How a visitor and a visit are defined

**A visitor is `sha256(secret salt + project + IP)`, truncated to 16 hex
characters.** That is the whole identity. It is stable — the same person next
week gets the same handle — and it is scoped: the salt is a server-side secret
and the project name is part of the input, so the id cannot be joined to any
other site's traffic, including another Docsbook project.

**A visit is reconstructed from the events, not tracked with a session
cookie.** One visitor's events are sorted by time and cut wherever there is a
gap of more than **30 minutes**. That is an inactivity gap, not a fixed clock
bucket, on purpose: bucketing splits a visit that straddles a boundary, so a
reader active from 12:29 to 12:31 would otherwise be reported as two visits.

## How bots and crawlers are filtered

Filtering runs in **two independent layers**, because either one alone is known
to fail.

1. **User-Agent.** A regex covering crawlers, spiders, headless browsers,
   scripted HTTP clients, SEO suites and link-preview fetchers, plus every AI
   bot in the classifier's table. Two literal UA strings are pinned because they
   were observed crawling in volume while claiming to be ordinary phones — a
   Googlebot Smartphone reference device and a stale iOS build.
2. **Behaviour.** A visit that produced no event only a JavaScript runtime can
   emit — no read-time segment, no heading view, no exit, no click — did not run
   JavaScript, and is a crawler whatever its User-Agent says.

On top of that, **your own team is excluded from every reader figure.** A
visitor whose IP also sent an admin-session beacon for this project within the
last 30 days is flagged as the owner and dropped from reader metrics — kept
separate from the bot flag, because they are a real human, just not your
audience. Optionally, a server-side IP allowlist drops internal traffic before
it is ever written.

Bot and owner visits are **retained and labelled**, not deleted, so the panel
can show you the split rather than quietly shrinking your numbers.

## How read time is actually computed

The tracker starts a clock when a page mounts and reads it when the reader
leaves — on `pagehide`, on `visibilitychange → hidden` on iOS (where `pagehide`
is unreliable), and on in-site navigation. Each reading emits one
`docs.read_time` **segment** and resets the clock, so a page returned to
produces two segments rather than one double-counted stretch. Segments shorter
than **3 seconds** are not emitted at all.

Delivery is by `navigator.sendBeacon` to a same-origin endpoint, batched at up
to 100 events per beacon. The ordinary logging transport debounces for two
seconds over `fetch`, which does not survive a tab close — read time, heading
views and exits are the events that must survive it, so they take the beacon
path instead.

**Then every segment is clipped at 300 seconds before anything sums it.** This
is the single most important number on this page. The emitter keeps counting
while a desktop tab sits in the background, and on a sweep of 11,176 real
sessions across 7 workspaces, 40 individual segments exceeded two hours, the
99th percentile was 81,342 seconds, and summing raw segments inflated total read
time roughly thirtyfold — 1,268,422 seconds against 42,160 once clipped. The
same clip is applied by every surface that quotes a time figure, so the panel,
the per-page column, the goals layer and the MCP tools cannot disagree.

Per-page average read time divides the clipped total by **segment count**, not
by visit count: a reader who tabbed away and back contributes two segments to
one visit, and averaging by visit would credit that visit twice.

## How AI-assistant traffic is told apart from human traffic

Requests are classified into three groups that are never merged:

| Group | Example agents | What it means for you |
|---|---|---|
| **Answers** — a human is being answered right now | `ChatGPT-User`, `Perplexity-User`, `Claude-Web`, `DuckAssistBot` | Your page was quoted at a person. This is warm traffic, and it usually arrives with no referrer |
| **Indexing** — building the corpus an assistant retrieves from | `OAI-SearchBot`, `PerplexityBot`, `Bingbot`, `Applebot`, `GoogleOther` | The precondition for ever being cited |
| **Training** — bulk collection | `GPTBot`, `ClaudeBot`, `CCBot`, `Google-Extended`, `Bytespider` | Supports one decision only: whether to allow it |

An unrecognised AI bot name is treated as **training** — the claim that promises
you the least. Classification is by User-Agent, in first-match-wins order, so
`Applebot-Extended` is never swallowed by `Applebot`.

## Sampling, caps and retention

**There is no sampling.** No figure in the panel is extrapolated from a subset
of traffic. What exists instead is a hard cap: session reconstruction reads at
most **50,000 events** per window, and when it hits that cap the result carries a
`truncated` flag that consumers must surface, because rates computed off a
truncated window are wrong. A query that *fails* is also reported as failed
rather than as zero — an empty dashboard and a broken read are different
answers.

**Reader events are kept for 30 days, on every plan.** Thirty days is where the
data ends, not a tier: it is the retention of the event store. Every period
picker in the product reads the same constant, so no control can offer a window
the data cannot fill. The AI usage ledger is a separate store and is kept
longer — 90 days, pruned daily — so a disputed bill can still be reconstructed
after the reports have stopped showing it; no report offers more than 30 days
of it either way.

## Where the data lives

| Data | Where | Kept for |
|---|---|---|
| `docs.*` reader events, including the raw IP that produces the hash | Axiom, a third-party event warehouse | 30 days |
| Goals, funnels and their definitions; the AI and MCP billing ledgers; workspace settings | Docsbook's own Postgres database | Goals and funnels until you archive them; the AI ledger 90 days, pruned daily; MCP call rows are not currently pruned |
| Chat answer verdicts | Docsbook's Postgres database, written once per conversation | With the conversation |

Search Console figures shown in the panel are fetched from Google against the
connection you authorise, and are Google's data, not Docsbook's.

## Privacy and GDPR — what is technical fact, and what is your call

**Technical facts, verifiable in the behaviour of the site:**

- Docsbook's docs-site analytics writes nothing to the reader's device and
  reads nothing from it. There is no analytics cookie and no browser-stored id.
- Reader identity is derived from the IP by a keyed hash, server-side, scoped to
  your project. The hash is one-way; the raw IP is not exposed by any report,
  export or MCP tool.
- No identifier is shared across projects, and none is sold, syndicated or used
  to build a cross-site profile.
- Retention is 30 days and is enforced by the store, not by a report filter.

**What we do not claim.** Docsbook does not assert that running it makes your
site consent-free, GDPR-compliant, or exempt from any national rule. Two things
your own counsel has to decide:

1. **Whether the ePrivacy consent rule bites.** Article 5(3) of Directive
   2002/58/EC (as amended) conditions "the storing of information, or the
   gaining of access to information already stored, in the terminal equipment"
   on consent. Docsbook stores and reads nothing on the device, which is the
   trigger that provision names — but the EDPB's *Guidelines 2/2023 on the
   Technical Scope of Art. 5(3)* devote a section specifically to "Tracking
   based on IP only", so treat "no cookie therefore no consent" as an argument,
   not a settled answer.
2. **Whether you still need a lawful basis under the GDPR.** An IP address that
   identifies a reader is personal data regardless of the cookie question, so
   your notice, your basis and your processor terms with the vendors above are
   yours to set. The CNIL's own exemption criteria for audience measurement are
   a useful checklist here, and Docsbook meets several of them (single
   publisher, no cross-site linkage, purpose limited to audience measurement)
   and not all of them — notably, it does **not** truncate the last byte of the
   IP before storing it.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Read time must be clipped, not summed raw | The Page Visibility spec exists because "web developers have been designing web pages as if they are always visible" — a page that keeps counting while hidden is exactly that error | [W3C Page Visibility Level 2](https://www.w3.org/TR/page-visibility-2/) |
| Serious analytics defines engagement as foreground time | Google Analytics 4 defines it as "the amount of time someone spends with your web page in focus" — the clip is our approximation of the same intent, and it is stated rather than implied | [GA4: User engagement](https://support.google.com/analytics/answer/11109416) |
| Exit-time events must go by beacon, not `fetch` | Beacon requests "are guaranteed to be initiated before page is unloaded and are allowed to run to completion" | [W3C Beacon API](https://www.w3.org/TR/beacon/) |
| Listen on `pagehide`, not `unload` | `unload` "is still unreliable, so avoid using it unless absolutely necessary"; `pagehide` "fires in all cases where the `unload` event fires" and also on bfcache entry | [web.dev: bfcache](https://web.dev/articles/bfcache) |
| A User-Agent is a claim, not an identity | Google publishes crawler verification precisely because of "spammers or other troublemakers … claiming to be from Google" — hence the second, behavioural layer | [Google Search Central: verifying Googlebot](https://developers.google.com/search/docs/crawling-indexing/verifying-googlebot) |
| "Answers", "indexing" and "training" are three different visitors | OpenAI ships three separate agents: GPTBot may "crawl content that may be used in training", OAI-SearchBot exists "to surface websites in search results", and "ChatGPT-User is not used for crawling the web in an automatic fashion". Perplexity draws the same line: PerplexityBot "is not used to crawl content for AI foundation models" | [OpenAI bots](https://developers.openai.com/api/docs/bots), [Perplexity bots](https://docs.perplexity.ai/guides/bots) |
| Measure whether the visit succeeded, not how many pages it touched | "if users can't accomplish their target task, all else is irrelevant" (Nielsen & Budiu, 2001, reviewed 2021) | [NN/g: Success Rate](https://www.nngroup.com/articles/success-rate-the-simplest-usability-metric/) |
| Consent for analytics is a legal judgement, not a product setting | Art. 5(3) turns on "storing of information, or the gaining of access to information already stored, in the terminal equipment"; the CNIL's exemption criteria add first-party scope, purpose limits and IP truncation | [ePrivacy Directive, consolidated](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02002L0058-20091219), [CNIL Sheet 16](https://www.cnil.fr/en/sheet-ndeg16-use-analytics-your-websites-and-applications) |

## Limits and open questions

- **Every visitor count is an estimate, and the product says so in its own
  responses.** A hashed IP merges everyone behind one corporate NAT into a
  single reader and splits one commuter across several. Read visitor figures as
  a trend; never quote them as a headcount.
- **Read time is clipped, not gated on visibility.** On desktop, a tab left open
  in the background keeps accruing seconds until the 300-second clip stops it.
  This is honest about the direction of its error — read time is biased upward,
  bounded — but it is not the same measurement as GA4's focus-based engagement
  time, and this documentation does not claim it is.
- **The bot filters are heuristics with no verification step.** Docsbook does no
  reverse-DNS or published-IP-range check on a crawler's claimed identity, so a
  spoofed User-Agent is classified at face value. The behavioural layer catches
  the common case a UA regex misses; neither layer is a security control.
- **Owner exclusion depends on one beacon.** A teammate who reads the docs but
  has never opened the admin panel from that IP in the last 30 days is counted
  as a reader.
- **Geo-IP resolves the network, not the person.** A corporate VPN places a
  reader in whichever city terminates the tunnel; a mobile network can be a
  hundred kilometres out.
- **Under question: "no cookie" is not the same as "no consent needed".** What is
  verifiable is that Docsbook's docs-site analytics stores and reads nothing in
  the browser, and that reader identity is a salted server-side hash. What is
  not settled is the legal consequence: the EDPB has explicitly opened the
  question of IP-only tracking under Art. 5(3), and no public source resolves it
  for a hashed, first-party, 30-day case. Treat the compliance conclusion as
  your counsel's to reach.
- **Thirty days is a hard ceiling.** No year-over-year, no seasonal read, and no
  cohort longer than four weeks is possible from this data at all.

## Related

- [Tracked events reference](./tracking/events.md) — the 36 events this page describes
- [Analytics overview](./tracking/overview.md) — the panel these definitions produce
- [Read time](./reports/read-time.md) — the clip, applied to one report
- [Goals and funnels](./reports/goals-and-funnels.md) — what a visit is judged to have achieved
- [Countries](./reports/countries.md) — geo resolution and its limits in practice
