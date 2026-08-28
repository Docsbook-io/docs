---
title: "Translation Settings"
description: "Configure multi-language publishing in Docsbook — enable target languages, toggle the language switcher in the sidebar or header, and control translations."
---

# Translation Settings

Publish your documentation in multiple languages — automatically, with no manual work.

## Settings

| Setting | What it does |
|---|---|
| Enabled languages | Which languages to publish your docs in |
| Language switcher in sidebar | Show the language selector in the left sidebar |
| Language selector in header | Show the language selector in the top header bar |

## How to Enable

1. Requires a **Pro plan**.
2. Open your docs site.
3. Float Widget → **Translation** tab.
4. Check the language you want to enable.
5. Confirm in the dialog that appears — translation then starts in the background.

If the language switcher is already showing on your site, you can also open it and press **Activate languages** — it opens the same **Translation** tab. That entry point appears only for you as the owner (or in admin preview), never for your readers.

Translation typically takes **1–5 minutes** for small repositories, up to 30 minutes for large ones.

### Before You Confirm

Turning a language on opens a confirmation dialog so you know the cost before you commit to it. It shows:

- **Pages to translate** — how many pages are not yet translated, out of the total. If everything is already translated, it says so and enabling costs nothing.
- **Estimated cost** — what the run is expected to cost, or *Billed to your own API key* if you brought your own provider.
- **Budget left** — how much of your AI budget (or translation limit) remains.

If the run does not fit in what is left, the dialog says what percentage of the docs your budget covers and offers an upgrade. You can still press **Translate what fits** — the pages that fit are translated now, and the rest are picked up automatically once your budget refreshes.

### Following a Running Translation

While a run is in progress, the language row shows a progress bar and a **35/80** counter (pages handled out of pages in the run). A language whose last run did not finish is marked **Stopped**; hover it to see the reason — budget exhausted, provider quota, or a failure. Long runs resume on their own, in chunks, until every page is done.

## Supported Languages

15 core languages are available:

| Language | Code |
|---|---|
| Spanish | `es` |
| French | `fr` |
| German | `de` |
| Portuguese | `pt` |
| Italian | `it` |
| Russian | `ru` |
| Chinese | `zh` |
| Japanese | `ja` |
| Korean | `ko` |
| Arabic | `ar` |
| Hindi | `hi` |
| Turkish | `tr` |
| Polish | `pl` |
| Dutch | `nl` |
| English | `en` (default) |

## Language Switcher Placement

The language switcher can appear in the **sidebar**, the **header**, or both.

**Recommendation:** Pick one location. Showing it in both places is redundant.

| Placement | Best for |
|---|---|
| Header | More visible, better for international audiences |
| Sidebar | Saves header space when header is already full |

Configure placement in:
- [Header Options →](../design/layout/header)
- [Sidebar Control →](../design/layout/sidebar)

## URL Structure

Each language gets its own URL path:

```
docsbook.io/{username}/{repo}           → English (default)
docsbook.io/{username}/es/{repo}        → Spanish
docsbook.io/{username}/fr/{repo}        → French
```

Each language version is indexed separately by search engines, which means passive SEO traffic in every language you publish.

## Was Translating Worth It?

Open **Translations** in the settings panel. One interval dropdown at the top governs the whole page, and everything under it reports the window you picked:

- **Savings** — what a human translator would have charged for the same word count, minus what the AI translation actually cost you. The translator rate is an industry estimate, not a quote you received, so read this as an order of magnitude rather than an invoice.
- **Visitors** — unique readers who landed on a translated page, with crawlers excluded.
- **Conversion** — how much better or worse readers of translated pages convert compared with readers of your original-language pages. A negative number is a real answer, not an error: it means the translated pages are reaching people who bounce, and it is worth knowing.

Below those three sit two cards side by side. The left one is a single breakdown list with two
tabs: **Countries** (unique visitors by country of origin) and **Languages** (pages viewed in each
translated language).

The right one is the **reader map**, and it answers a question neither list can on its own: *which
regions are arriving that you are not translating for?* Each country of origin is one marker,
drawn as that country's flag inside a coloured ring. The flag says which country; the ring says how
many of that region's readers actually landed on a translated page:

| Ring | What it means |
|---|---|
| Green | They get the docs in their language, either because they read the translation or because your docs are already written in it. |
| Amber | The translation exists and most of them still read the original. That is a discoverability problem, not a missing translation. |
| Red | Readers arrive from that region and effectively none of them read a translated page. This is the one to act on. |
| Grey | Docsbook has no translation language for that region yet, so there is nothing here for you to enable. |

The map opens framed on the countries you actually have readers in. Drag it to pan, and use the
controls in its corner to zoom in or to go back to that opening view — zooming spreads crowded
regions apart without growing the flags, which is what makes western Europe readable.

Hover a marker for that country's visitor count, the share of them on a translation, and the top
language they read in. The breakdown list to the left carries the same verdict as a figure on each
row — the share of that country's readers who landed on a translated page, in the same colour —
and pointing at a row names the verdict and lights that country on the map. Rows showing `—`
instead of a share are the three cases where no share exists: the docs are already in that
region's language, Docsbook has no language for it, or the window has nothing measured.

Two things the map deliberately will not say. It never reports your own language as a missing
translation: if your docs are in English then American readers count as served, and a workspace
whose docs are written in German gets the mirror image. And where the per-country language
breakdown is not available to your plan, markers read as unmeasured grey rather than red, so a
missing measurement can never look like a missing translation.

## One Language at a Time

The page above covers every language at once, which is not the question you act on. That one is always about a single language: keep paying for German, or not. So each language has a page of its own — click **Translations** in the sidebar, then pick the language from the tabs across the top of the page.

### At the top: is it on, and is it keeping up?

Beside the language's name sits everything you can *do* to it, on one line: the on/off **switch**, a state chip saying whether the language is level with your docs and when it was last written to, and a button that runs a translation now.

The switch is here, and not only in settings, so you can act on what the page just told you. Turning a language **on** still quotes the bill first, exactly as it does in settings — the same confirmation dialog, not a cheaper-looking second way to start spending. Turning one **off** asks nothing, because it costs nothing and deletes nothing.

The state chip opens onto everything behind that one word:

- **Coverage** — one percentage, over a bar split by the *kind* of gap. Pages that are translated and current, pages whose source has since changed, and pages never translated at all are three different colours, because they call for different responses. A page that fell behind is telling your reader something your docs no longer say; a page never translated simply falls back to your original.
- **Last update** — when this language was last written to, and which commit your docs are currently at.
- **What is running now** — a live progress bar while a run is in flight, naming who started it: **you**, someone else on the dashboard, switching the language on, or a commit Docsbook followed.
- **Recent runs** — the last dozen runs as a strip, coloured by how each one ended. One failed run is a blip; a strip that has not finished cleanly in a month is a problem, and a single "last run failed" cannot tell you which you have.
- **Why it stopped** — when a run ended short, the reason in plain words: budget exhausted, provider quota, an unreadable repository.

The run button holds the two ways to start one by hand: **Translate now**, which fills in what is missing or behind, and **Re-translate everything**, which discards what is stored and translates the whole thing again.

### Did it pay off, and what did it cost?

Two rows of figures, and neither reads correctly without the other — 180 readers is a good week or a waste depending on whether they cost you four dollars or four hundred.

The first row is **who it reached**. The number it is built around is one the overview cannot show you: **how many people from that language's countries visit your docs at all**, in whatever language they end up reading. On its own, "180 readers in German" tells you nothing — it could be your entire German-speaking audience or a rounding error. Against 1,240 visitors from German-speaking countries it is a decision, and the 1,060 who never landed on the translation are either the reason to keep it running or something to go look at. Beside it: how those readers convert against readers of your original pages, and how much of your documentation carries this language at all.

The second row is **what it cost to reach them** — what you have spent, what that saved against a human translator's rate, how much of the work was served from cache rather than sent to the model again, and how many of those readers completed a goal you defined.

Every figure in both rows explains itself: press the **?** beside its name for what it counts and what it does not.

Two things worth knowing about how the audience is counted:

- A language is measured against **all** its countries, not one. Portuguese is Brazil and Portugal, Spanish is sixteen countries, German is five.
- Readers of a language who are **not** in its countries — diaspora, travellers, anyone who simply prefers it — are reported separately rather than folded into the share. A language read entirely outside its own countries still has a real audience, and you can see it.

### Did the translation follow what you shipped?

Below the figures is the one part of the page that names something to go fix: your documentation's commits, newest first, each with a verdict on how its pages stand in this language.

It is asked per commit rather than per page because a commit is what you remember. "The pricing rewrite went out on Tuesday" is a thing you know; "one file under `pricing/` is behind" is a thing you would have to work out. A commit with nothing amber has been followed in full, and you can skip the row without opening it.

Open a commit to see every documentation page it touched, each marked **translated**, **behind**, **not translated**, **manual** (written or uploaded by a person, so its freshness is that person's call) or **removed** (a path your source has since renamed or deleted). Open a page to read the change itself — the patch, fetched from your repository at that moment.

The state is always how the page stands **now**, not how it stood on the day of that commit. What you can act on is whether your readers are being served the right thing today, and a commit since superseded by a newer one is exactly how a page ends up behind.

### Who actually read it

The page ends on the readers themselves — the same table as **Users**, narrowed to this language and opened on its widest set of columns: where each reader connected from, which translation they read, what they came through, how far they got, which goals they reached and what they are worth. By the time you reach it the totals above are already answered, and the question left is which of these people to go talk to.

A language you switch off keeps its page. Turning one off deletes nothing, so its pages, its cost and its past readers are all still there — shown as history, next to the country audience that keeps arriving whether or not there is a translation waiting for them. That pairing is what answers "should I turn this back on?".

## Keeping Translations Current

On the **Auto** translation mode, Docsbook follows your repository: when you push a commit that changes a documented page, the pages that fell behind are re-translated for every enabled language without you asking. Pages the commit did not touch cost nothing, and stale pages are re-done before never-translated ones — a translation that now says something your docs no longer say is worse for a reader than a page that falls back to the original.

It is a check, not an instant reaction. Docsbook looks for new commits about every 15 minutes, so expect a catch-up to begin within roughly that window rather than the second you push.

Following commits stays inside the fences you already set:

| Fence | Effect |
|---|---|
| Translation mode | Only **Auto** follows commits. On **Manual** and **External webhook** nothing starts by itself. |
| Enabled languages | Only languages you switched on. A language that is off is never translated. |
| Plan | Requires a plan that includes translation. |
| Budget and quota | The same AI spend budget and provider limits as any other run. When the budget runs out the run stops and says so, and resumes when it refreshes. |
| Runs in flight | Never starts a second run for a language that is already translating. |

To correct or replace a specific translation by hand, ask your AI agent to re-translate a page, or use the MCP translation tools (`upload_translation`, `approve_translation`, `delete_translation`). A translation you upload or approve is marked as hand-written, so later automatic runs leave it alone.

## Disabling a Language

Uncheck the language in the Translation tab → Save, or use the switch on that language's own page. No confirmation is asked, because nothing is destroyed.

Visitors on that language's URL are automatically redirected to the English version.

**Turning a language off never deletes what is already translated**, and turning it back on does not pay again for pages that have not changed — only new or edited pages are translated. Re-enabling a language you previously used is effectively instant and free. You can experiment with languages without risking a second bill.

---

> **Reach a global audience without hiring translators.**
> [Upgrade to Pro →](https://docsbook.io/connect)

See also: [How AI Translations work →](./ai-translations)
