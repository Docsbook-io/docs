---
title: "Read the analytics panel: what each figure is, and is not, evidence of"
description: "Every tile, card and tab in the Docsbook analytics panel — what it measures, where the number comes from, what it cannot tell you, and which decision it supports."
tldr: "Seven tiles across the top, four breakdown cards under them, and an AI-crawler card below those. Six of the seven tiles are properties of a visit and are computed from one reconstructed event stream, so they cannot disagree; the seventh, Spend, is read off the billing ledger and is the only figure here whose zero is a measurement rather than a gap."
---

# Analytics overview

A documentation dashboard is easy to make impressive and hard to make usable.
The difference is whether each number states what it cannot see. This page goes
through the panel tile by tile and tab by tab, and for each one says what it
counts, where it comes from, and the reading it does **not** support. The
definitions underneath all of it — who counts as a visitor, how bots and your
own team are excluded, how long data is kept — are in
[how measurement works](../how-measurement-works.md) and are not repeated here.

## What you get

One page that answers the questions an owner actually has, from one source.
Six of the seven headline tiles are properties of a **visit**, and all six are
derived from the same reconstructed event stream rather than from six
independent counters — so bounce rate here and bounce rate in the outcome split
are the same computation, not two numbers with one name. Reading any of it
costs nothing against your project's balance, and none of it is gated by plan.

## How it is built

### The seven tiles

| Tile | Definition | Chartable |
|---|---|---|
| Visitors | Distinct visitors with at least one human visit in the window, split new / returning | yes |
| Revenue | Conversions × your average product price | **no** |
| Spend | What left this project's balance — AI calls plus MCP calls | yes |
| Conversion rate | Conversions ÷ visitors | yes |
| Revenue/visitor | Revenue ÷ visitors | yes |
| Bounce rate | Visits classified as a bounce ÷ visits | yes |
| Session time | Mean visit duration | yes |

**Revenue is a tile but never a chart.** It is conversions multiplied by a
constant, so its line would be the conversion line with a different axis label:
one fact drawn twice. Its shape over time is read off Conversion rate.

**A conversion is a click out of your documentation to the host of your Call To
Action URL.** Matched by host, with `www.` folded in and other subdomains
deliberately *not* folded — your docs usually live on a subdomain, and folding
would count "went back to the docs" as a sale. A visitor who clicks through
five times is one conversion.

**Both money tiles stay off until two settings exist**: the Call To Action URL
decides *which* click is a conversion, the Average Product Price decides what
it is *worth*. Until both are set they report a dash and name the missing one —
never `$0`. A missing price is not a price of zero, and revenue is the figure
an owner acts on without checking how it was produced. Both live in
[Branding](../../design/style/branding.md). A stored price of `0` is refused by
the validator for the same reason.

**Spend is the exception on every count.** It is money leaving rather than a
property of a visit, it comes from the billing ledger rather than the event
stream, and it is the one figure here whose `0` is a real reading. Consequences
worth knowing:

- **It is not netted.** A top-up does not make it dip; Spend answers "what did
  this project cost me", and that question has one direction.
- **It ignores your filters.** A filter cuts *visits*, and a translation run is
  not a visit — "United States" has nothing to say about an embedding job.
- **It survives an empty window.** A translation run at 3am is a real bill with
  no reader behind it, and that is often the most useful thing this tile has to
  show. Every other tile prints "no visits to measure" over such a window.
- **Its arrow has no colour.** Spend rising because readers are asking more is
  the product working; spend rising because a job is stuck is a fire. Every
  other delta is green for good news — bounce rate going *down* is green — and
  this one stays grey, because the panel has no evidence for which case it is.
- **An unreadable ledger disables the tile** and says so, rather than showing
  `$0`. What it counts is in [AI usage and cost](./ai-usage.md).

Each tile also shows the change against the immediately preceding window of the
same length. Growth from a previous value of zero draws **no arrow at all**: it
is undefined, not `+100%`.

### The four breakdown cards

Each card is a scrolling strip of tabs; ten of the tabs are ranked dimensions
cut from the same visit stream as the tiles, and four come from elsewhere.

| Card | Tabs | One value per visit? |
|---|---|---|
| Pages | Pages, Headings, Entry, Exit | Entry and Exit yes; Pages and Headings no |
| Sources | Referrers, Channels, UTM, Keyword | Referrers and Channels yes |
| Audience | Devices, Browsers, Countries, Languages | yes |
| Conversions | CTA Clicks, Feedback, Searches | counted per event |

**Single-valued dimensions partition the window** — their visitor counts sum to
the total. **Pages and Headings do not**: a visit's conversion is credited to
every page it touched, so those rows are assisted credit and deliberately add
up to more than the headline. The card says so on screen.

Every row on a ranked tab carries **both** figures — how many visitors it
brought and what they were worth — with two bars behind it: one for whatever
the list is ranked by, one always for the money. Rows are ordered server-side
by visitors and re-sorted in the browser, because a server returning "the top
rows by revenue" would hand back a *different* set depending on a toggle, and
rows would appear and disappear as you switched.

**Pages and Headings offer two extra rankings**, `Views` and `Reading time`.
They mean something for a row that names a place in your documentation and
nothing for a row that names a country, so they are offered there and nowhere
else. A page with no read-time measurements shows a dash, never `0`.

### Filtering

Filtering by a row narrows **everything** — the other cards and the tiles above
the chart — so a country, a device or a referrer can be read end to end.
Filters stack and are removed by clicking their chip. Cards and tiles apply the
same predicate to the same reconstructed visits, which is what stops "United
States" meaning one thing in a card and another in the chart above it.

Tabs counted per **event** rather than per visit — Headings, UTM, AI Views, CTA
Clicks, Feedback and Searches — cannot be cut this way. They say so above their
rows while a filter is on, instead of showing unfiltered numbers under a
filtered heading.

### The four tabs that do not come from your visitors

- **Keyword** comes from Google Search Console. An impression that never became
  a click is invisible to anything running on your site, so this is Google's
  data: queries, position, impressions, clicks and CTR. Connect Search Console
  first. Its revenue column is explicitly an **estimate** — clicks × your
  site-wide revenue per visitor — labelled and drawn as one, because a modelled
  figure sitting next to measured ones must not look like one.
- **CTA Clicks** ranks every destination readers left your documentation for,
  and from which page.
- **Feedback** ranks pages by the thumbs they were given, dislikes first: the
  page people voted down is the one to rewrite. Both vote widgets count
  together — the rating at the foot of a page and the thumbs on an AI answer
  given there — because the question is which page readers approve of, not
  which button they pressed. Zeros are always shown.
- **Searches** ranks what readers typed into your on-page search box, with how
  often it found something and how often it came back empty — the same words
  can carry both counts. A query with no results is a reader telling you in
  their own words what the docs should cover. It has no metric menu: these rows
  are per search, not per visit, so there is no revenue to sort on.

### Channels, and why a channel row is not enough

The Channels tab groups visits by the *kind* of source — organic search, paid
search, social, AI assistant, referral, direct, internal — classified when the
event is written rather than when it is read. That matters twice: AI referrals
arrive with an empty referrer, so grouping by referrer alone buries them in
Direct; and a paid Google click and an organic Google result share the same
referrer, so a paid `utm_medium` has to win over it. Hovering a channel names
the three sites it actually consists of, with their shares — an organic-search
row that is almost entirely Google and one spread across five engines are
different situations.

### AI Views

Three tabs, one for each reason a crawler came, because the three support
completely different decisions:

| Tab | What it is | The decision it supports |
|---|---|---|
| Answers | A live fetch made while someone was being answered | Your page was quoted at a person. Worth a link and a current price on it |
| Indexing | Building the corpus an assistant later retrieves from | The precondition for ever being cited |
| Training | Bulk collection for model training | Only one: whether to allow it |

Within each tab you can group by **Pages** (which pages assistants read) or by
**Crawlers** (one line per bot, labelled with its provider). Classification is
by User-Agent against a table of 23 named bots, first match wins — so
`Applebot-Extended` is never swallowed by `Applebot` — and an unrecognised AI
bot is treated as training, the claim that promises you the least.

### Time ranges

| Range | What it covers |
|---|---|
| Now | A rolling **hour**, bucketed per minute, refreshing live |
| Today | The current **UTC** calendar day so far |
| Yesterday | The previous UTC calendar day, whole |
| Last 24 hours | A rolling day back from now |
| Last 7 days | A rolling week |
| Last 30 days | A rolling month — the longest window there is |

Today and Yesterday are calendar days in **UTC**, not in your local timezone,
and not a rolling 24 hours: early in the UTC day, Today covers less than Last
24 hours does. Thirty days is where the data ends.

**Now** is its own window rather than a relabelled day — a live view is only
readable at minute resolution, and a whole day bucketed by the minute is 1,440
points. In Now the tiles and chart refresh every 5 seconds and the cards every
30; switch to any other range and refreshing stops, so a historical range you
are not watching is never silently refetched under you.

**Online now** — readers active in the last 5 minutes — is not one of the seven
tiles. It is a right-now gauge rather than a total over the window you picked,
so it sits as its own chip beside the panel title; putting it in the strip
would invite comparing it against a period it does not belong to.

### A report you have no data for yet

A tab with none of your own rows renders over **faded sample figures** with
"Enable *Tab*" over them, and pressing it runs a short guide over those same
figures. It is **per tab**, not per card — Entry names one page per visit while
Pages credits every page a visit touched, and each caveat belongs to the tab it
is about. The switch gates nothing: every figure was collected the whole time,
and the choice is remembered in your browser per workspace.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Measure whether the visit succeeded, not how many pages it touched | "if users can't accomplish their target task, all else is irrelevant. User success is the bottom line of usability" — Nielsen & Budiu, 2001, reviewed 2021 | [NN/g: Success Rate](https://www.nngroup.com/articles/success-rate-the-simplest-usability-metric/) |
| Classify crawlers by purpose, not into one "bots" bucket | The vendors themselves draw the line: GPTBot may "crawl content that may be used in training", OAI-SearchBot exists "to surface websites in search results", and "ChatGPT-User is not used for crawling the web in an automatic fashion" | [OpenAI bots](https://developers.openai.com/api/docs/bots) |
| A User-Agent is a claim, not an identity | Google publishes crawler verification because owners are "concerned that spammers or other troublemakers are accessing your site while claiming to be from Google" | [Google Search Central: verifying Googlebot](https://developers.google.com/search/docs/crawling-indexing/verifying-googlebot) |
| Search Console figures are Google's, and provisional | Google states "The newest data can be preliminary, meaning it's still being collected and might change in the next few hours", and defines impressions as "How many times your site appeared in Search results" — a number no on-site tracker can see | [Google: Performance report](https://support.google.com/webmasters/answer/7576553) |
| A modelled figure must not look like a measured one | The Keyword tab's revenue is clicks × site-wide revenue per visitor; it is labelled `(est.)` and drawn with a dashed bar for exactly this reason | Mechanism, this page |

## Limits and open questions

- **Every visitor figure is an estimate and the product says so.** A visitor is
  a hashed IP: one corporate network merges into a single reader, one commuter
  splits across several. Read them as a trend, never as a headcount.
- **Percentages over few visits are a direction, not a measurement.** Below 30
  visits the panel says so under the figures rather than quoting a confident
  rate.
- **A very large window is read from a sample and admits it.** Session
  reconstruction reads at most 50,000 events; hitting that cap sets a
  `truncated` flag the card states in words, because rates computed off a
  truncated window are wrong.
- **Deltas vanish rather than lie.** If the previous window's read failed, no
  deltas are shown at all. **Pages and Headings rows over-attribute on
  purpose** — they are assisted credit; do not add them up.
- **Bounce is a description, not a verdict.** One page, under three seconds,
  nothing else — which is also what a reader who found their answer in one
  glance looks like.
- **Under question: "Session time" is not attention.** What is verifiable is
  the mechanism — segments, a three-second floor, a 300-second clip per
  segment, averaged over visits. What is not verifiable from any web analytics
  data is whether a person was looking at the screen, and this panel does not
  imply it. See [read time](../reports/read-time.md).
- **Thirty days is the whole history.** No year-over-year, no seasonality, no
  cohort longer than four weeks.

## How to open it

Open any page of your documentation site and click the **Analytics** tab in the
floating toolbar at the bottom. The overview loads with the range you picked
last, which it remembers across visits.

## Related

- [How measurement works](../how-measurement-works.md) — visitor identity, bot and owner filtering, retention, privacy
- [Tracked events](./events.md) — every event behind these figures
- [AI usage and cost](./ai-usage.md) — what the Spend tile is counting
- [Read time](../reports/read-time.md) — the Reading time ranking, in full
- [Countries](../reports/countries.md) — the Countries and Languages tabs as their own report
- [Goals and funnels](../reports/goals-and-funnels.md) — measuring an outcome you declared rather than a default
- [Branding](../../design/style/branding.md) — the two settings that switch Revenue on
