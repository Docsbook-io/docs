---
title: "Did it work? Judging a documentation change, and shipping the next one so it can be judged"
description: "Comparing edited pages against untouched ones, the four verdicts allowed, and how to land a fix — the route, the rules, and the baseline the next run needs."
tldr: "A before-after difference is not an effect: docs traffic moves for reasons that have nothing to do with you, so the pages you did not touch are the control and they are the point. Only four verdicts are allowed — it worked, it did nothing distinguishable, it made things worse, cannot tell — and every change ships with a written baseline so the next run can judge it."
---

# Did it work?

Most documentation analysis runs in one direction: find something wrong,
recommend a change, stop. Nothing goes back afterwards to ask whether the
change helped, so the same recommendation gets made twice, with the same
confidence, on the same page, and nobody is any wiser the second time.

That open loop has a specific cost. Teams keep making the kind of edit that
feels productive — splitting long pages, adding "next steps" blocks, rewriting
intros — with no idea which of those ever moved anything. And **a change that
made things worse is indistinguishable from one that did nothing**, because
both look like "we shipped it and moved on".

This page closes the loop from both ends: first how to judge a change that has
already landed, then how to land the next one so that it can be judged.

## Judging a change that already landed

### When is this worth the most?

- **Before repeating a kind of change.** You are about to restructure six more
  pages the way you restructured one last month. Check the first one first.
- **After acting on any recommendation.** Any analysis can tell you a page has
  a problem. Only this tells you whether your fix worked.
- **In a retrospective on a docs push.** Which of the twelve commits mattered
  is not knowable from the diff.
- **When a metric moved and a docs change is the suspect.** Confirm or clear it
  rather than assuming.
- **Not** for a change that shipped in the last day or two. There is no "after"
  yet, and reading one that has barely started filling is how a random Tuesday
  becomes a strategy.

### The rules that make the answer mean anything

- **A before-after difference is not an effect.** Docs traffic moves for
  reasons that have nothing to do with you: a release, a launch, a link from
  somewhere big, a holiday, a ranking change. Any read that looks only at the
  edited pages confidently credits your edit with all of it.
- **The pages you did not touch are the control, and they are the point.** If
  dead ends fell on the edited pages *and fell just as much everywhere else*,
  your edit is not the reason.
- **Volume and quality are different questions.** More visits to a page you
  rewrote might mean the rewrite drew people in — or that it now ranks for
  something it cannot answer. The question here is whether the visits went
  *well*; traffic is context for it, not the answer.
- **Split a search movement before you attribute it.** Fewer impressions, a
  worse average position and flat impressions with falling click-through are
  three different failures wearing the single word "traffic", and each has a
  different fix — the classic error being a rewrite aimed at what was actually
  a click-through collapse caused by an answer sitting above you. Google's own
  recovery guidance asks for exactly that split, and adds that after a core
  update you should wait at least a full week after the rollout completes
  before analysing anything, and avoid quick fixes in the meantime
  ([Google Search Central, core updates](https://developers.google.com/search/updates/core-updates)).
- **Small numbers cannot be rescued by a percentage.** A page that went from 9
  visits to 12 has no story in it.
- **Some changes are not measurable and never will be.** A change older than
  the data window has no reconstructable "before". An unmeasurable change
  reported as a neutral one quietly becomes evidence that the change did
  nothing.
- **One change is weak evidence; a pattern across similar changes is strong.**
  Prefer answering "does this KIND of edit work here" over "did this one commit
  work", whenever there is more than one instance.

### Method

1. **Pick the change and state the prediction first.** Write down what you
   expected it to do — "splitting this page should cut the number of readers
   who give up on it" — *before* looking at any number. A hypothesis stated
   afterwards fits whatever the data did, and it always fits.
2. **Establish what was measurable at all.** The change must be old enough to
   have an after-window and recent enough that its before-window is still
   visible. If either side is missing, stop and report that: a verdict built on
   half a comparison gets quoted without its caveat.
3. **Compare edited pages against untouched pages, in both windows.** The same
   numbers for both groups — the outcome mix of visits, and how long readers
   took to reach something of value. Anything less is not a comparison. For a
   change that arrived as a commit,
   [`get_page_diff_impact`](../../mcp/analytics/get-page-diff-impact.md) does
   exactly this split and reports "cannot measure" rather than zeroes when a
   window is missing.
4. **Subtract the site trend explicitly.** The number you report is not "dead
   ends fell 8 points". It is "dead ends fell 8 points on the edited pages
   while falling 7 everywhere else, so about 1 point is attributable, and that
   is inside the noise". Do the arithmetic in the report so a reader can
   disagree with it.
5. **Check whether the edited page was read at all.** A page nobody visited in
   either window cannot show an effect no matter how good the edit was. That is
   a finding of its own — you fixed something no reader reaches — and it points
   at navigation and search, not at the page.

### Four verdicts, and no others

| Verdict | What it means | What follows |
|---|---|---|
| **It worked** | The edited pages improved meaningfully more than the control | Say what to repeat, and on which pages next |
| **It did nothing distinguishable** | Whatever moved, moved everywhere | The most common answer and the most useful — it is the one that stops a team investing in a ritual |
| **It made things worse** | The edited pages moved against the control | Say so directly, and read the page again before repeating that kind of change |
| **Cannot tell** | Sample too thin, window incomplete, or the data does not reach back far enough | A real verdict, not a failure |

### What this catches

| Pattern | What it looks like | Why it matters |
|---|---|---|
| **The ritual that does nothing** | A kind of edit the team keeps making, whose pages track the site average every time | Weeks of work with no effect, repeated because nobody checked |
| **The regression nobody noticed** | Dead ends rose on the edited pages while the rest of the site held steady | A "cleanup" that removed something readers relied on |
| **The false win** | Metrics improved right after a change — and improved just as much on every untouched page | Credited to the edit, becomes the template for the next ten, none of which do anything |
| **The invisible fix** | An edited page with almost no visits in either window | The content was never the bottleneck; discovery was |
| **The unmeasurable claim** | A change too old for a before-window, cited in a retrospective as a success | An unfalsifiable claim hardens into team folklore |

---

## Applying the next fix so it can be judged

An audit changes nothing. Applying a finding is the one crossing point between
reading and writing, and the owner of the docs owns it.

### Where does the change land?

If the owner has not already said, ask — once, with these options, before
writing anything:

| Route | What happens | When it fits |
|---|---|---|
| **Pull request** | Create a branch, make the edits, open a PR whose description carries the finding, the evidence and the expected effect | The docs live in a reviewed repository. Mandatory for anything touching prices, limits, or claims about other companies |
| **Approve in chat** | Show the before and after per change; apply only what is approved | A handful of changes, a person present, no review process worth the ceremony |
| **Direct update** | Write straight to the source | The owner explicitly asked, the changes are mechanical, and they are reversible |

Do not guess. A direct write into a repository somebody reviews is not a small
mistake, and a pull request nobody wanted adds a week of latency to a one-line
fix. [Publishing](../planning/publishing.md) covers the mechanics of each
route.

If the answer is a pull request, **one PR per coherent group of findings, not
one per line**. The description says which number is expected to move and by
when, so the next run can check it.

Some findings never take the direct route regardless of what was chosen: a
wrong price, a claim about a partner or a competitor, or a deprecation notice.
Those are proposals for a human even when everything else is being applied
automatically. Say so rather than silently making an exception.

### Who writes the words

The audit decides **which** pages change and **why**. What they then *say* —
page type, structure, register, retrieval shape, conversion pattern — is the
writing half of this handbook: [writing rules](../writing/writing-rules.md),
[writing for retrieval](../writing/retrieval.md) and
[conversion](../writing/conversion.md). Write to those rather than improvising.
[From finding to change](../writing/from-finding-to-change.md) is the hand-off
itself.

### Rules for the edit

- **Preserve meaning and preserve URLs.** A rewrite that changes what a page is
  about forfeits the ranking it was supposed to protect. If a title change
  implies the slug should change, flag the redirect requirement rather than
  silently breaking links.
- **Never create a page here.** A gap goes to the
  [page set](../planning/page-set.md), with the evidence and a draft outline
  attached.
- **Never rewrite a body when the finding was about a title.** If the body is
  also wrong, that is a separate, larger and more expensive finding — note it
  and move on. Mixing the two destroys the one thing that made the title fix
  worth doing: it was cheap.
- **One recommendation per page per run.** If a page needs a title rewrite, a
  restructure and a merge, ship the title and re-measure. Bundled changes make
  the next run unable to say which one worked.
- **Ship the replacement verbatim.** A proposed title, a proposed description,
  and the opening sentence — paste-ready. Never "improve the title" or
  "consider something like".
- **Never edit a price, and never rewrite a claim about another company.**
  Propose the corrected sentence; a human decides what to assert.
- **Deprecated content gets a banner and a migration path, never deletion.**
- **A merge or split decision belongs to a human.** Two pages cannibalising one
  query get flagged, not merged.

### Write the baseline before the change lands

This is the step that makes the whole loop possible, and it is the one that
gets skipped because it produces nothing today.

For each affected page, write down: **the numbers today, the window they came
from, the date, and the one number you expect to move, with a horizon.**
Behavioural effects need a full window before they say anything; search effects
take weeks — Google's own guidance on recovery talks in terms of months for its
systems to confirm a change, which is the horizon to quote rather than the next
sprint
([Google Search Central, core updates](https://developers.google.com/search/updates/core-updates)).
Without a written baseline the next run cannot tell a real improvement from a
seasonal one, and the loop stays open.

The same applies when there is **no prior change to compare** and the judging
half of this page has nothing to work on. Say so, and record a baseline now:
the pages you are about to change, the numbers on them today, the date, and the
prediction. That baseline is what makes the next run able to judge this one,
and writing it costs a minute.

### Then offer the automation

A finding you have now made twice is a monitor waiting to be created. When the
same class of problem recurs — a price drifting after every pricing change,
translations falling behind, a page going stale between releases — say so once
at the end and point at
[setting up automation](../automation/setting-it-up.md). Do not set anything up
mid-run.

## Related

- [Business translation](./business-translation.md) — the effect line you
  promised in the report is the number this page comes back to check.
- [Goals and funnels](./goals-and-funnels.md) — a pre-declared success
  criterion is the only kind that cannot be chosen after the fact.
- [Monitoring](../automation/monitoring.md) — making the recheck recur without
  anyone remembering.
- [Metrics](./metrics.md) — what the before and after are actually made of.
