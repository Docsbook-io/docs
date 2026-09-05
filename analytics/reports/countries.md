---
title: "Where your readers are, and which of them read a translation"
description: "How Docsbook resolves a reader's country and the language they read in, how accurate each is, and how to find the markets you attract and then lose at the language barrier."
tldr: "Country comes from the edge network's IP lookup, attached server-side — accurate at country level, unreliable below it. Language is not the reader's browser preference: it is the translated route they actually landed on, so the report measures which translation was read, never which one was wanted."
---

# Countries and languages

Two questions look like one and are not. "Where are my readers?" is answered by
an IP lookup and is reliable at country level. "What language do they want?" is
not answered anywhere in this product, and this page is careful to say so —
what is measured instead is which translation of your documentation readers
actually ended up on, which is a supply figure, not a demand figure.

The useful report is the pair: a country that sends you readers and gets none
of them onto a translated page is a market you already attract and lose at the
language barrier.

## What you get

Three readouts, in two places:

| Readout | Where | What it lists |
|---|---|---|
| **Countries** tab | Analytics → Audience | Your top 15 countries by distinct readers, each with visitors, views and revenue, and each usable as a dashboard filter |
| **Languages** tab | Analytics → Audience | The same visits by which translation they read |
| **Countries list + reader map** | Translations panel | Your top 30 countries, each paired with the share of that country's readers who landed on a translated page, coloured by how well they are served |

Reading them costs nothing against your project's balance. The Countries and
Languages tabs are available on every plan; the per-language page and the
zoomable visitor map are paid.

## How country is determined

**At the edge, from the IP, server-side.** The network that serves your
documentation resolves the request's IP to a country code and attaches it to
the pageview before it is stored, along with the region, city and coordinate it
resolved. Nothing in the browser is asked, and no location permission is ever
requested.

Where the lookup produces nothing, the field is **left out entirely** rather
than written as empty. That distinction is load-bearing: an explicitly empty
field reads as present-but-blank to the query layer, which would make "we don't
know" indistinguishable from a real value. A pageview with no country is still
a pageview and still counts everywhere else.

Coordinates are written **all or nothing** — a latitude with a missing
longitude would place a reader in the Gulf of Guinea — and are range-checked
before they are stored.

Region, city and coordinate are captured but used by **one** surface, the
zoomable visitor map. The Countries readouts use the country code and nothing
finer.

## How language is determined

**From the locale prefix of the URL the reader landed on. That is the only
source.** Docsbook supports 15 language codes; when the first segment of the
path is one of them, and it is a language you have enabled, that is the visit's
language. When there is no prefix, the visit has no language and is counted as
having read your original.

What it is **not**:

- Not `Accept-Language`. Docsbook never reads that header, anywhere.
- Not `navigator.language`.
- Not a stored reader preference.

Docsbook also does not redirect readers by language or geo-route them, so a
reader reaches a translation by choosing it — from the language picker, a link,
or a search result. That is what makes the figure honest and also what limits
it: **it measures which translation was read, not which one was wanted.** A
reader who would have preferred German, never found the German version, and
read the English one is counted as an English reader.

The two Languages readouts differ in one respect worth knowing:

- The **Translations** panel's Languages list shows *translation traffic only*
  — your own default language is excluded, because a site's own language is not
  a translation.
- The **Analytics → Audience → Languages** tab includes everything, and files
  visits with no locale prefix under **Unknown**.

## How the reports are built

### The Countries tab (Analytics → Audience)

One country per visit — the **first non-empty country in that visit's events** —
which makes the dimension single-valued, so its visitor counts partition the
window and add up to the total. Visits are cut on a 30-minute inactivity gap.
Bots and your own team are excluded, as they are everywhere on that page. The
list is the top 15, ranked server-side by visitors so switching the metric
reorders a list rather than fetching a different one. Rows with no country
resolved appear as **Unknown**; there is no "Other" bucket, and rows past the
limit are simply not returned.

There is **no minimum-sample suppression** on these rows: a country with one
reader is shown as a country with one reader. The response is stamped as an
estimate, because a visitor is a hashed IP.

### The countries list and reader map (Translations)

Top 30 countries, ranked by distinct readers, each carrying both its visitor
count and its pageview count. Beside each is the share of that country's
readers who landed on a translated page, clamped so it can never exceed 100% —
a reader who sampled two languages counts once per language in the raw figures
and must not therefore appear as 150% served.

**One caution when comparing screens.** The percentage shown in this list is a
share of the **top-30 subtotal**, while the shares on the Analytics breakdown
cards are of the whole window. Two correct numbers about the same country can
differ for that reason alone.

Each country is a marker on the map — its flag in a ring, sized by how many
readers it sent — and the ring carries the comparison:

| Ring | Rule | Reading |
|---|---|---|
| Green | Your docs are already written in that region's language, **or** at least **75%** of its readers read the translation | Served |
| Amber | Between **25%** and **75%** read the translation | The translation exists and most of them still read the original — a discoverability problem, not a missing translation |
| Red | Under **25%** | Readers arrive and effectively none of them reach a translated page |
| Grey | Docsbook has no language for that region, or the share could not be measured for the window | Nothing to enable, or nothing measured — never "nothing there" |

Your own language is never reported as a missing translation, and an unmeasured
window reads grey rather than red, so a gap in measurement can never look like
a gap in coverage.

### The zoomable visitor map

Three levels, chosen by zoom: countries, then regions, then individual readers.
Where a marker is drawn depends on what the event actually carried:

- A row that names a **region or a city** and has a coordinate is drawn at that
  coordinate.
- Everything else is drawn at its country's **centroid**, from a static table of
  125 country codes, and is labelled approximate.
- A country-wide row is refused the exact placement **even when it has a
  coordinate**, because the average coordinate of a whole country is a point in
  the middle of it — for the United States, a field in Kansas.
- A country the table does not know is **counted but not drawn**, and the map
  says how many such readers there are rather than dropping them silently. An
  unknown code is never resolved to `0, 0`: "we do not know where this is" and
  "they are in the ocean" have to be different answers.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Trust IP geolocation at country level and not below it | MaxMind states its products "can identify users at the country level with 99.8% accuracy", against "around an 80% accuracy at the state/region level" and "a 66% accuracy for cities (within a 50km radius of that city)" for US addresses | [MaxMind: geolocation accuracy](https://support.maxmind.com/hc/en-us/articles/4407630607131-Geolocation-Accuracy) |
| Never present a located IP as a located person | Where a visitor uses "an anonymizing proxy like a VPN", the provider can geolocate the server but "will not be able geolocate the end-user"; business VPNs mean "the end-user may be anywhere within a region" | [MaxMind: geolocation accuracy](https://support.maxmind.com/hc/en-us/articles/4407630607131-Geolocation-Accuracy) |
| Do not infer a reader's language from `Accept-Language` | The W3C is explicit that it is "not a good idea to use the HTTP Accept-Language header alone to determine the locale of the user": "Many users never change the defaults … They are set when the user agent is installed", and "People borrow machines from friends, they rent them from internet cafes" | [W3C: Accept-Language for locale settings](https://www.w3.org/International/questions/qa-accept-lang-locales) |
| Expect the header to be missing or generic anyway | RFC 9110 states "A user agent SHOULD NOT generate an Accept-Language field when the user has not indicated a preference for linguistic content", and treats linguistic preferences as a fingerprinting surface | [RFC 9110 §12.5.4](https://datatracker.ietf.org/doc/html/rfc9110#section-12.5.4) |
| Draw an approximate location as approximate | The average coordinate of a country is a real number that describes nobody; labelling it as a centroid is the difference between a map and a map that invents cities | Mechanism, this page |

## Limits and open questions

- **The language figure is supply, not demand.** It answers "which translation
  did readers end up on", and cannot answer "which translation do readers
  want". Any product surface that describes this list as browser preference is
  describing something Docsbook does not collect.
- **A country is a network, not a person.** A corporate VPN places every
  employee wherever the tunnel terminates; a mobile network can be a hundred
  kilometres out; a hashed IP merges everyone behind one NAT into a single
  reader. Read country rows as a ranking, never as a headcount.
- **Sub-country geography is thin.** Most stored pageviews carry no coordinate
  at all, so the visitor map is mostly country centroids with a minority of
  precise placements. That is stated on the map rather than smoothed over.
- **No minimum sample is enforced on these rows.** A country with three
  readers is shown next to one with three thousand, and the percentage beside
  the small one moves by whole points per reader.
- **The colour scale needs at least one translation language enabled** to say
  anything useful. With none enabled every country is grey, correctly.
- **Thirty days is the whole history.** There is no seasonal or year-over-year
  reading of a market from this data.
- **Under question: "unserved market" is a hypothesis, not a finding.** What is
  verifiable is that readers from country X arrived and did not land on a
  translated page. What is not verifiable is why — no translation existed, one
  existed and was not findable, or those readers read English by preference.
  The colour scale distinguishes the first two by whether the language is
  enabled at all; it cannot distinguish the third from either. Treat a red
  country as a question to test with one translation, not as a measured loss.

## How to open them

- **Countries and Languages tabs** — Float Widget → **Analytics** → the
  **Audience** card, then pick the tab.
- **Countries list and reader map** — Float Widget → **Translations**. Hover a
  marker for that country's readers, the share on a translation and the top
  language they read in; hovering a row in the list lights the same country on
  the map. Drag to pan; the corner controls zoom and reset the view to the
  countries you actually have readers in.
- **One language at a time** — open **Translations** and pick a language from
  the sidebar to see how much of its own audience it reaches and what it cost.

## Related

- [How measurement works](../how-measurement-works.md) — visitor identity, bot filtering and why every count here is an estimate
- [Analytics overview](../tracking/overview.md) — the Audience card these tabs live in, and filtering the dashboard by a country
- [Translation settings](../../translation/settings.md) — enabling a language for a region this report flags red
- [How AI translations work](../../translation/ai-translations.md) — what a translation run does, and what it costs
- [Tracked events](../tracking/events.md) — `docs.language_switch`, the one event that records a reader changing language deliberately
