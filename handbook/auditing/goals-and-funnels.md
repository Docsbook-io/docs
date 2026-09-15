---
title: "Goals and funnels: declaring what the docs were for, then reading whether it happened"
description: "How to declare one macro goal and a funnel that can carry a conclusion, and how to read the result afterwards without mistaking a broken matcher for a reader problem."
tldr: "A goal is one thing you want a reader to do; a funnel is an ordered route through several of them, and together they are the only place the owner states what the documentation is for. Declare exactly one macro goal and two to four micro goals, keep a funnel to three to five steps that start broad and end on a business outcome, and before believing any goal number resolve its matcher against the docs as they stand — a goal that cannot fire looks exactly like a goal with 100% drop-off."
---

# Goals and funnels

Every other number in an audit reports what readers **did**. Goals and funnels
are the only place the **owner** said what readers were supposed to do, which
makes them the only signals that can say a site is failing *at its purpose*
rather than merely changing.

That also makes them the easiest signals to misread, because a goal is a
definition somebody wrote and a definition can be wrong in ways a pageview
count cannot. So this page has two parts, in the order the work happens:
**declaring** what the docs are supposed to achieve, and **reading** those
numbers afterwards. The product mechanics underneath both — how a step is
counted, what is suppressed on thin data — are documented in
[Goals and funnels](../../analytics/reports/goals-and-funnels.md). What follows
is the judgement.

**Nothing here is a one-way door.** Goals are matched *retroactively* against
history already recorded, so a goal declared today fills its chart immediately
instead of starting from zero. Declare one, look at it, archive it if it says
nothing. That is the opposite of instrumentation that only counts forward, and
it is why the right posture is to iterate rather than to design perfectly
first.

---

## Part 1 — Declaring what the docs are supposed to achieve

This half is configuration, not content: it changes what the site measures,
never what a page says.

### What do you look at before naming a single goal?

Three things, in this order:

1. **What is already declared.** A workspace that already has goals has a
   decision in it. Adding a fifth without reading the four is how a list
   becomes a log.
2. **The traffic volume for the period.** It sets how many goals the site can
   support at all, and whether a funnel will have a denominator worth reading.
3. **How visits currently end, and what readers already do.** A goal is a
   statement about the gap between that and what should happen. Without the
   first half you are declaring a wish.

Then get the **page tree with its heading anchors**. Section goals match
anchors, so the outline is the menu of goals available without adding any
tracking whatsoever.

### One macro goal, a few micro goals

A **macro-conversion** changes revenue: a click out to the app, the pricing
page or signup; a demo booked. A **micro-conversion** is evidence a reader is
moving toward it: reaching the pricing section, copying the install command,
asking the assistant.

**Declare exactly one macro goal and two to four micro goals that plausibly
lead to it.** The micro goals exist to *localise a failure* in the macro one.
They are not targets of their own, and optimising one in isolation is how a
site ends up with a rising "reached pricing" line and a falling revenue line —
a common outcome, not a hypothetical.

**Above about six goals the list stops ranking anything and becomes a log.**
The limit is statistical: a typical docs workspace sees a couple of hundred
human visits in thirty days, so a goal firing for 5% of them produces roughly
ten events a month. Its line is flat against the axis, its row reads "not
enough data" most weeks, and it dilutes attention from the goals that carry
signal. Archive one before adding another.

### The four kinds of goal, and what each actually matches

| Kind | Matches | Declare it for |
|---|---|---|
| `section` | a heading came into view | "scrolled as far as pricing", "reached the auth section" |
| `event` | one of the events the docs already emit | copied code, asked the assistant, gave feedback |
| `page` | a **page view** of a path | "opened the quickstart" |
| `outbound` | a click leaving for a host | the macro goal, almost always |

Three things worth knowing before picking one:

- **`section` is how scroll depth exists here.** The heading-view event already
  fires when a heading enters the viewport, so a "scrolled as far as pricing"
  goal needs nothing added to the docs — it needs a heading with an `id`, which
  the page already has. This is the cheapest goal kind and the most under-used.
- **`outbound` matches by HOST, not URL.** `/pricing` and `/pricing?utm=launch`
  are one destination; you never enumerate URLs.
- **`page` is a page view and nothing else.** A reader who scrolled past a link
  to `/pricing` has not reached `/pricing`, and the matcher agrees.

An `event` goal can be **scoped to a path**, which is how one event becomes two
goals: "copied the quickstart snippet" and "copied the auth snippet" are
different facts about the reader, and merging them hides which page does the
work.

### Naming a goal

Name a goal for **what the reader did**, past tense, lowercase with
underscores: `reached_pricing`, `copied_install`, `clicked_to_app`,
`asked_about_limits`.

Never put a path, an id, an email or a query string in the name. Two reasons,
both real: one goal per URL is a log rather than a ranking, and an address in a
goal name travels into exports and chat replies. The path belongs in the
matcher; the name belongs to the behaviour.

The name is also the **handle** — funnel steps refer to goals by name, and a
name already in use is refused rather than merged. Pick it as though it is
permanent, because for every funnel built on it, it is.

### When should a goal carry money?

Attach a value **only if you can defend the number.**

- A macro goal can carry the real average sale.
- A micro goal can only carry an *expected* value: the average sale multiplied
  by the share of readers who reach that point **and** go on to buy. If that
  share is unknown, the value is unknown.

Leaving the value empty is a real answer and usually the better one: every
money figure derived from that goal stays switched off rather than displaying
an invented one. **A value of zero is refused outright** — `$0` renders as a
measurement, and "worth nothing" is a different claim from "nobody said".

### Designing the funnel

#### Order is the whole point

A visit counts as reaching step N only if it hit steps 1..N **in sequence**.
Counting each step independently — "how many visits saw the pricing page at
all" — is the classic funnel bug: it credits step 3 to readers who never
touched steps 1 and 2 and reports a conversion rate for a journey nobody made.

State the consequence to the owner, because it is the check that catches a
broken implementation: **reordering the steps must change the numbers.** If it
does not, something is counting events instead of ordered visits.

Detours are tolerated — a reader who wanders off between two steps and comes
back still counts as continuing. The order is a constraint on sequence, not on
adjacency.

#### Step 1 broad, last step real

**Start broad.** Most docs readers arrive deep — on `/docs/api/webhooks`, from
a search engine or an AI answer — and almost nobody starts at the index. A
funnel only counts visits that entered at step 1, so a step 1 of "viewed
`/docs/`" excludes the majority of the audience before measuring anything, and
reports a denominator describing a rare visitor. Make step 1 *any docs visit*.

**End on a real outcome.** A funnel whose last step is a scroll or a section
view measures attention, and no decision follows from it. The last step should
be the thing that changes revenue — usually an outbound click to the product
host.

A funnel whose first and last steps are both micro-conversions is a reading
report wearing a funnel's clothes.

#### How many steps?

**Three to five.** Beyond eight, declaration refuses.

The reason is multiplicative: five steps at a healthy 50% each leaves 3% at the
end; eight leaves 0.4%. Every added step shrinks the final denominator and adds
one more place for a definition error to hide. Docs sites carry less traffic
than the ecommerce flows the industry's 5–8 range was set for, so the low end
is the right default here, not the middle.

If the route genuinely has more steps, **split it into two funnels** — the
split below is the one that almost always applies.

#### The conversion window

The window bounds how long after step 1 a later step still counts. **Leave it
empty and the visit itself is the boundary — the honest default for docs**: a
reader who returns a week later is a new visit, not a slow conversion.

If you do set one, the method is a lookup, not an estimate: **the 90th
percentile of observed time-to-convert among readers who did convert, rounded
up to a natural unit.** The per-conversion list reports that p90 directly. Too
short truncates real conversions; too long lets unrelated later behaviour glue
itself to an old step 1 — "she read the quickstart in March and signed up in
June, so the quickstart converted her."

**A window longer than the plan retains can never complete.** It reports
permanent drop-off that is an artefact of the plan, not of the docs. The window
is clamped to what is retained and you are told so — relay that, because the
funnel the owner asked for and the funnel they got are then different funnels.
On the free tier retention is a single day, which makes any multi-day window
meaningless there; read the actual limit from what the clamp reports rather
than assuming a tier.

There is a subtler version of the same trap: **a window as long as retention
makes the most recent bucket always look worse**, because the newest entrants
have not had their full window yet. Keep the window comfortably shorter than
retention so a closed cohort is never compared against an open one.

### The two docs funnels

Documentation serves two different jobs, and merging them is the most common
design error on this page. They have different entrants, different timescales,
and different people who would fix a problem — so a merged funnel produces one
number neither of them can act on.

#### A. Evaluation — "should we adopt this"

The reader is deciding. One session to a few days.

```
1. any docs visit                          (event: page view)
2. reached a capability or price section   (section: #pricing / #limits / #security)
3. clicked through to the product          (outbound: app.theirdomain.com)   ← macro
```

Three steps. Whoever writes the comparison and positioning pages owns a fix.

#### B. Implementation — "make it work"

The reader has already decided. Minutes to days, with long gaps.

```
1. landed on the quickstart        (page: /docs/quickstart)
2. copied the install command      (event: code copied, scoped to that page)
3. reached the configure section   (section: #configuration)
4. reached first success           (section: #your-first-request)
```

Four steps, and the one case where a multi-day window is defensible — "I will
come back after lunch" is the norm here. Whoever wrote the quickstart owns a
fix.

Note this funnel ends on a **product** event, not a business one. Its revenue
shows up later, which is exactly the case where a value is set by the
expected-value method above, or not at all.

#### Why "landing → problem → solution → pricing" does not transfer

That sequence assumes the visitor enters at the top and descends.
Documentation breaks the assumption structurally: readers enter deep, re-enter
at different depths across days, and the sidebar makes every page reachable
from every other. The marketing-site shape is valid *upstream* of the docs. The
docs-side motion is the reverse — the reader arrives with a question, gets it
answered, and only then becomes reachable by a call to action.

Which is the rule worth remembering: **the outbound step belongs after an
engagement step, never directly after the entry step.**

### What declaration refuses, and what it only warns about

Both are returned at the moment of writing, and **both are worth relaying
verbatim.** They name a specific defect in a specific definition; summarising
them into "there were some warnings" throws away the entire value. A refusal
means nothing was written; a warning means it was written and is worth looking
at.

#### Refused — nothing was saved

| What happened | Why it is refused rather than warned |
|---|---|
| No name, or nothing to match | There is no goal to save. |
| An event the docs do not emit | The goal could never fire, and a goal that never fires is visually identical to a goal with 100% drop-off. The owner would go looking for a UX problem that does not exist. |
| A value of zero | `$0` renders as a measurement. Empty is the way to say "nobody declared a value". |
| The name is already taken | Names are the handle funnels refer to a goal by. The fix is a different name or an edit to the existing goal — never a retry of the same name. |
| A funnel with fewer than two steps | With one step there is no transition to measure. That is a goal. |
| A funnel past eight steps | The tail is meaningless whatever the site. Split it. |
| A step naming a goal that does not exist | A funnel silently dropping a step reports a **better** conversion rate than the real route — the one failure mode a funnel must never have. |
| A window of zero or less | Empty means "the visit", which is a real answer. Zero is not. |

#### Warned — it was saved, and it is worth acting on

| The warning | What to do about it |
|---|---|
| The name looks like it holds a path, id or address | Rename for the behaviour and move the address into the matcher. Both a cardinality problem and a privacy one — names travel into exports. |
| A value on a scroll goal, with no average price set | Either work out the expected value properly, or clear it. |
| More than about six goals already | Archive one first. Past six the list stops ranking. |
| More than five funnel steps | Split into evaluation and implementation. |
| Step 1 is a single page | Broaden it to any docs visit, or accept that the funnel describes a minority of readers and say so every time it is quoted. |
| The funnel ends on a scroll or a reading signal | Ask what business event should terminate it. Usually an outbound click. |
| The window is longer than retention | It has been clamped. Decide whether the clamped funnel is still the one you wanted. |
| A step matches the same thing as an earlier step | It will be reached by everyone who reached that one — a flat 100% segment carrying no information. Remove it. |

**Archive, never delete, to tidy up.** A funnel that silently loses a step
reports a better conversion rate than the real one, which is why removal is
archival — and why "cleaning up" a goal that a funnel still references is the
most expensive tidy available here.

---

## Part 2 — Reading the numbers afterwards

### When should goals come into an audit at all?

Not every run needs them. Reach for them when:

- The question is about **conversion, activation, revenue or "why don't they
  sign up"** — nothing else answers it.
- A behavioural finding needs a **denominator with intent behind it**. "31%
  dead-end rate" is a fact about everybody; "of readers who reached the pricing
  section, 8% clicked through" is a fact about buyers.
- The owner is asking **whether a change worked**, and the change was meant to
  move a specific behaviour. A goal is the pre-declared success criterion,
  which is the only kind that cannot be chosen after the fact. The method for
  that question is [did it work?](./did-it-work.md).
- A finding is about a **route** rather than a page — the funnel localises it
  to one transition, which no page-level detector can do.

Skip them when the question is findability, content quality, accessibility or
freshness. A goal has nothing to say about whether a page is well written, and
reaching for one anyway produces a paragraph of irrelevant numbers that buries
the finding that mattered.

And when **nothing is declared at all**, that is itself the finding, reported
once and without an upsell: the site has no stated definition of success, so no
audit can say whether it is succeeding. Read the routes readers actually walk
instead — that needs no hypothesis — and hand the declaration back to Part 1.

### What has to be checked before believing any number?

Four checks, in this order. Each one is cheap and each one has, on its own,
invalidated an entire audit.

**1. Does the matcher still resolve?** A section goal on a renamed anchor, a
page goal on a moved path, an outbound goal on a host the calls to action no
longer point at — all of them save fine and match nothing. **A goal that cannot
fire is visually identical to a goal with 100% drop-off.** The distinguisher is
history: a goal that fired last month and reads zero now is a change in the
docs or the readers; a goal that has never fired is a definition. Resolve the
matcher against the docs as they are now before writing a word about readers.

**2. Was the definition edited inside the window?** A goal or funnel changed
mid-window is two measurements drawn as one line. Note the date and start the
comparison after it; never draw a single conclusion across it.

**3. Is the denominator real?** A funnel is a hypothesis about a path, and
**most readers are not on it.** The share of all visits that enter step 1 is
itself a number worth quoting: a funnel describing 4% of traffic cannot carry a
site-wide conclusion, however clean its transitions look.

**4. Is the sample above the floor?** Percentages are withheld per step below
about 30 visits into it, and time percentiles below about 5 conversions. Where
the surface withholds a rate, report the count — do not helpfully compute the
percentage yourself. Every figure here is an estimate regardless: visitors are
identified by a hashed IP, so corporate NAT merges readers into one and a
mobile network splits one across many.

### The four surfaces, and what each cannot answer

| Surface | Answers | Does **not** answer |
|---|---|---|
| **Goal totals and trend** | Is this behaviour becoming more or less common | Whether it causes anything. A micro goal rising while the macro falls means the micro-conversion got easier, not that the site got better |
| **Funnel** | Which single transition loses the most people | What most visitors do — they are not in this funnel |
| **Visitor list** | Who is evaluating you right now, and how far each got | How many people. **Read this list; do not count it** |
| **Per-conversion journeys** | The shape of the decision — how long it takes | What caused it. The source is **last touch** and systematically over-credits whatever was clicked last, which on a docs site is usually Direct |

Two habits follow from the table:

- **Compare a goal only to itself last period.** There is no docs-funnel
  industry benchmark; anyone quoting one is quoting an ecommerce number from a
  checkout flow with a cart in it.
- **Read the worst transition, not the smallest step.** The last step is almost
  always the smallest and says nothing. The transition is where the route
  breaks.

### What should a drop-off look like?

There is no universal healthy rate, but the expectation is keyed to what the
step **asks of the reader**:

| The step asks them to… | Expect to lose | Alarming |
|---|---|---|
| keep reading — next page, next heading; costs nothing | 20–50% | over 70% |
| act inside the page — open search, ask the assistant, copy code | 50–80% | over 95% |
| leave for another site — the macro step | 90–99% | — |

When a drop is alarming there are exactly three candidate causes, and they need
three different fixes: **the link** (the path from the previous step is not
discoverable, or is broken), **the promise** (the previous page led them to
expect something else), or **the page** (the step's own content fails). Check
the link first — it is the cheapest to verify, and a step whose link 404s will
absorb unlimited content effort and never move.

### Read the pair, not the number

Almost every goal number is ambiguous alone. The disambiguation is always a
second signal, and these are the pairs that carry it.

| What you see | Read it with | Because |
|---|---|---|
| A goal total | The funnel it sits in | A total says how often; only the transition says where they were lost getting there |
| Macro goal | The micro goals under it | Both up is real. Micro up, macro flat is a reachability change, not a selling improvement |
| Goal completions | Traffic | Completions falling while traffic rises is a **mix change**, not a quality drop. Judge the rate, then find where the new traffic enters |
| Funnel completion | Dead-end rate | A clean funnel beside a high dead-end rate means the docs convert the readers who already knew what they wanted and fail everyone else |
| Funnel completion | The routes readers actually walked | Low completion while some *other* route is frequent and succeeds means readers found a better path than the declared one. Adopt theirs |
| A conversion count | Its median and p90 time | Minutes means one session and an on-page fix. Days means they leave and come back, and being remembered matters more than any rewrite |
| Any goal | Its own last period | The only valid comparison there is |

### Worked readings

Each of these is the same class of number producing a different conclusion
depending on what sits beside it. They are the shapes worth recognising; the
numbers are illustrative.

#### A. The leak is upstream of where it looks

```
1. any docs visit      1,600
2. reached pricing       210   (−87%)
3. clicked to app         97   (−54%)   ← worst transition: 1 → 2
```

**Naive read:** 6% end-to-end, the pricing page is not converting, rewrite it.
**Actual read:** of readers who reach the price, more than four in ten click
through. That is a *good* conversion, and rewriting the pricing page is work
spent on the part that already works. Only 13% of readers ever reach the price
at all.
**Do:** check the link (is the pricing section linked from the pages readers
actually land on), then the promise (do those pages suggest there is a paid
product), then the page (is the section so far down that nobody scrolls to it).
In that order — cheapest first.

#### B. The same funnel, inverted

```
1. any docs visit      1,600
2. reached pricing     1,100   (−31%)
3. clicked to app         38   (−97%)   ← worst transition: 2 → 3
```

**Naive read:** the funnel works until the end, so the product must be too
expensive.
**Actual read:** the reach is excellent and the ask fails. Price is one
candidate and the weakest one to assume, because two cheaper explanations come
first: there may be **no call to action** at the point of interest, or the
reader arrives at the price already knowing something disqualifies them — a
missing integration, a limit, a licence.
**Do:** read what those readers searched for and asked the assistant *before*
reaching the price. Rejections are usually written down in the reader's own
words somewhere in the run.

#### C. Micro goals rising, macro flat

```
reached_pricing    +180% over the quarter
copied_install      +90%
clicked_to_app        +2%
```

**Naive read:** engagement is up, revenue will follow.
**Actual read:** the micro-conversions got *easier to reach* — the anchor moved
up the page, or the section landed in the navigation. Nothing says more of the
right readers are arriving.
**Do:** check whether the pages carrying those anchors were restructured in the
period, and whether the traffic mix changed. Treat this as a warning that the
micro goals have stopped being evidence and become a target — which is the
failure mode declaring them was supposed to prevent.

#### D. A healthy goal inside a collapsing funnel

```
funnel `evaluation` completion:  1.1%
goal `clicked_to_app` total:     840 completions, steady
```

**Naive read:** the funnel says the site is broken.
**Actual read:** the goal is fine, so readers *are* converting — they are
simply not doing it along the declared route. The funnel is measuring a
hypothesis that most converters do not follow.
**Do:** work backwards from the visits that ended well and read which entry
pages actually lead to success. This is a **navigation finding**, not a content
one: the fix is to promote the route readers found, not to push the one that
was designed. Then re-declare the funnel to match reality, and note the date so
the two are never compared as one series.

#### E. A step at exactly 100%

```
1. any docs visit          2,400
2. reached the overview    2,390   (−0.4%)
3. copied install            310   (−87%)
```

**Naive read:** step 2 is healthy.
**Actual read:** step 2 is not measuring anything. An anchor sitting above the
fold, or a heading rendered in the sidebar on every page, fires for everyone
who loads a page — so the step adds a flat segment and no information, and it
inflates the step count while shrinking nothing.
**Do:** drop the step, or move it to an anchor deeper in the page that a reader
has to actually arrive at. Any step that loses under a few percent is a
candidate for the same reading.

#### F. Two funnels, opposite verdicts

```
funnel `evaluation`      completion 4.2%   (healthy for a docs site)
funnel `implementation`  completion 0.6%   worst transition: copied install → reached configure
```

**Naive read:** conversion is fine, do nothing.
**Actual read:** the docs sell well and onboard badly. This is the shape that
shows up as churn one or two billing cycles later, and it will never appear in
a traffic report. The two funnels exist separately precisely so this cannot
average out into "fine".
**Do:** treat it as an activation defect owned by whoever wrote the quickstart,
not as a marketing problem. Check whether the configure step is reachable from
the install step at all — a missing "next" link between two pages produces
exactly this.

#### G. Completions flat, traffic up

```
traffic          +140%
goal completions   +4%
```

**Naive read:** the docs got worse under load.
**Actual read:** a mix change. A new source is sending readers with a different
intent — a link aggregator, an AI answer citing one page, a campaign. The rate
fell because the denominator changed, not because anything on the site did.
**Do:** judge the rate per entry page and per source before touching anything.
If the new traffic enters on one page and leaves, that page is now a
top-of-funnel page and needs a route onward — a content job, not a repair.

#### H. A one-day spike

```
goal `clicked_to_app`: 3 completions/day, then 214 in one day, then 4
```

**Naive read:** something worked; find it and do it again.
**Actual read:** almost always one of three things, and none of them is a
conversion improvement — an automated client, one visitor whose hashed identity
split or merged, or a genuine referral burst that carried no intent.
**Do:** read the individual visits behind that day before it enters the report.
A spike quoted as a finding and later explained as a crawler costs more
credibility than the finding was worth.

#### I. Median minutes, p90 days

```
goal `clicked_to_app`: median 6 min, p90 9 days
```

**Naive read:** average time to convert is a few hours.
**Actual read:** there is no average reader here. The distribution is two
populations — readers who arrived ready and readers who evaluated for over a
week — and any mean lands in the empty valley between them, describing a
visitor who does not exist. **Quote both numbers, never one.**
**Do:** the two halves need different work. The fast half is served by an
on-page call to action; the slow half is served by being *findable again* — a
page worth bookmarking, a name they can search for, a reason to return. If the
window was set shorter than that p90, part of the slow half is being cut off
and the funnel is understating itself.

#### J. The funnel improved right after the rewrite

**Naive read:** the rewrite worked.
**Actual read:** unknown, until edited pages are compared against untouched
ones across both windows. Docs traffic moves for reasons that have nothing to
do with the edit, and before-versus-after alone cannot separate them. This is
the phase most audits skip; the method is in
[did it work?](./did-it-work.md) and it applies to goals exactly as it does to
traffic.
**Do:** give one of the four verdicts and no others: it worked, it did nothing
distinguishable, it made things worse, cannot tell. If the goal was declared
*after* the edit, its retroactive history covers the pre-edit period too —
which makes this comparison available immediately, and is the one case where a
goal declared late is as good as one declared early.

#### K. The most recent days always look worse

**Naive read:** conversion is trending down.
**Actual read:** a window artefact — the one described under the conversion
window above. When the window is long relative to the period, the newest
entrants have not had their full window yet, so the latest bucket compares an
open cohort against closed ones and is guaranteed to look worse.
**Do:** exclude the trailing period equal to the window before reading a trend,
and say that you did.

### Traps

- **Never report a zero as reader behaviour** until the matcher has been
  resolved against the docs as they are now. This is the single most expensive
  mistake available on this page.
- **Never quote a funnel rate without the share of traffic that entered step
  1.** A rate without its coverage reads as a fact about the site.
- **Never compare a funnel to another site's numbers.** The only valid
  comparison is this funnel last period.
- **Never draw one conclusion across a definition change.** A funnel edited
  mid-window is two funnels.
- **Never present the visitor list as a count**, and never present the
  last-touch source as attribution — describe it as a hint, every time it is
  quoted.
- **Never convert a goal value into revenue on the owner's behalf.** A declared
  value is their assumption; label it as theirs. A null value is not zero, and
  money derived from a null-valued goal is invented. The rest of that
  discipline is in
  [business translation](./business-translation.md).
- **Never recommend optimising a micro goal on its own.** It exists to localise
  a failure in the macro one; promoting it to a target is how a site gets a
  rising engagement line and a falling revenue line.
- **Do not change a declaration in the middle of an audit.** Noticing that
  measurement is missing or broken is a finding; rewriting it is Part 1 work,
  after somebody has agreed to it.

---

## Measurement drift — after the content changes

**A goal is a claim about a page that still exists.** Content moves and the
declaration does not move with it, silently: a section goal keeps matching an
anchor that was renamed in a rewrite, a page goal keeps pointing at a path that
now redirects, a funnel keeps describing a route whose middle page was merged
into another. Nothing fails. The chart keeps drawing. It just draws a flat line
at zero, which reads exactly like readers refusing to convert — and the owner
spends a quarter rewriting a page that was never the problem.

This is the one drift class with **no external source of truth to compare
against**: the code did not change, the pricing page did not change, no link is
broken. Only the declaration and the docs disagree, and nothing else in the
system will ever surface it.

So run this check whenever a change lands that could move what a goal matches.
The trigger is structural, not cosmetic — a typo fix does not need it, and
these five things always do:

| What changed | What it can break |
|---|---|
| A heading renamed, removed, or its anchor changed | Every `section` goal on that anchor drops to zero |
| A page moved, merged, renamed or deleted | Every `page` goal and every funnel step on that path |
| Navigation or internal links restructured | The funnel's route still exists but nobody walks it any more |
| A call to action added, removed, or pointed at a different host | The macro `outbound` goal now measures a destination nobody clicks |
| A new page, section or conversion action shipped | Nothing breaks — but the thing you just built is unmeasured, which is the more common failure |

The check itself, in four steps:

1. **Read what is declared**, with what each goal matches. This costs nothing;
   the results are the paid part, and the check does not need them.
2. **Resolve every matcher against the docs as they are now.** Does the anchor
   exist on a page? Does the path resolve without a redirect? Is the outbound
   host still the one the calls to action point at? Is the event still emitted
   from the page the goal is scoped to?
3. **Report a broken matcher as a finding, not as a reader problem.** A matcher
   that resolves to nothing is a measurement defect; naming it as a conversion
   problem is the mistake this whole section exists to prevent. Fix it by
   re-pointing the goal at the new anchor or path, which keeps the history
   comparable.
4. **Ask the additive question, which is the one everyone skips:** does the
   change that just shipped introduce something worth measuring that nothing
   currently measures? A new pricing section, a new quickstart, a new call to
   action, a new integration page with its own outbound destination. If a page
   was built to make readers do something, and no goal names that something,
   the page ships unmeasured and the next audit will have nothing to say about
   it.

**Two cautions on acting.** Re-pointing a matcher keeps one series that spans a
definition change — note the date, and never draw a single conclusion across
it. And declaring a *new* goal costs nothing and loses nothing, because
matching is retroactive: the new goal arrives with its own history already
filled in, so there is no reason to defer it to "next time we look at
analytics".

Making this recur without anyone remembering — on a push, in CI, or on a
schedule — is covered in [drift](../automation/drift.md).

---

## Before you call a goal set done

- What was already declared was read before anything new was proposed.
- Traffic volume and current visit outcomes were established first — no goal
  declared against a wish.
- Exactly one macro goal, and between two and four micro goals that plausibly
  lead to it.
- Every goal is named for the behaviour, past tense, with no path, id or
  address in the name.
- Every value attached is defensible, or absent. No zero values, no invented
  expected values.
- Step 1 is broad, the last step is a business outcome, and there are between
  three and five steps.
- The window is empty, or is a p90 lookup that sits comfortably inside what the
  plan retains.
- Evaluation and implementation are separate funnels, not one merged route.
- The route was walked once as a reader before the funnel was built on it.
- Every refusal and every warning was relayed verbatim, not summarised.
- After any structural content change, every matcher was resolved against the
  docs as they now are, and the additive question was asked.

## Related

- [Goals and funnels](../../analytics/reports/goals-and-funnels.md) — the
  product mechanics: how a step is counted, what is suppressed, what the
  validator enforces.
- [Behaviour](./behaviour.md) — the readings that describe what every reader
  did, not only the ones on the declared route.
- [Did it work?](./did-it-work.md) — judging a change against a control, which
  is the only way a goal movement becomes evidence.
- [Business translation](./business-translation.md) — saying a funnel number in
  terms an owner can act on.
- [Conversion](../writing/conversion.md) — writing the page that the macro step
  is asking a reader to act on.
