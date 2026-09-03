---
title: "Find the countries you attract but do not translate for"
description: "The countries report pairs each country your documentation readers come from with the share of them who actually landed on a page in a translated language."
---

# Countries & Language Analytics

The countries report of your Docsbook documentation site names where your readers are and which language they read in. Its point is the pairing: a country that sends you readers and gets none of them onto a translated page is a market you already attract and lose at the language barrier. Reading it costs nothing against your project's balance.

---

## Countries

The Countries list shows the top 30 countries by visit count, with each country's share of total traffic — and, beside
each, the share of that country's readers who landed on a page in a translated language, coloured
green, amber or red by the same rule the map uses.

**How to open:** Float Widget → **Translations** → the **Countries** tab of the breakdown card.

**Use this to:**
- Decide which languages are worth translating into.
- Understand if your docs attract the global audience your product needs.
- Validate marketing campaigns targeting specific regions.

---

## Countries breakdown

Full table view: country name, flag, visit count, and percentage of total visitors.

| Column | What it shows |
|---|---|
| Country | Visitor's country (detected from IP) |
| Visits | Total page views from that country |
| % share | That country's portion of all traffic |

The breakdown covers up to 30 countries. Countries below the threshold are grouped as "Other."

---

## Which regions arrive that you are not translating for?

Country counts and language counts each answer half a question. The reader map is the half that only
exists in both together: for every country your readers came from, how many of them actually
landed on a page in a translated language.

**How to open:** Float Widget → **Translations**, beside the breakdown card.

Each country of origin is one marker: that country's flag inside a ring, with the ring's colour
carrying the comparison. Marker size follows how many visitors the country sent.

| Ring | What it means |
|---|---|
| Green | They get the docs in their language, either reading the translation or because your docs are already written in it. |
| Amber | The translation exists and most of them still read the original. Discoverability, not a missing translation. |
| Red | Readers arrive from that region and effectively none of them read a translated page. |
| Grey | Docsbook has no translation language for that region yet, so there is nothing here for you to enable. |

Drag the map to pan it; the controls in its corner zoom in and out, and return it to the view it
opened on (framed on the countries you have readers in). Hover a marker for that country's visitor
count, the share of them on a translation, and the top language they read in — or point at a row
in the **Countries** list, which shows the same share in the same colour and lights that country
on the map.

**Use this to:**
- Find the regions worth translating for next — the red ones, ranked by how many readers they send.
- Confirm that enabled translations are actually reaching their intended audience.
- Discover unexpected markets (e.g., French speakers outside France).

Two things the map will not say. Your own language is never reported as a missing translation: if
your docs are in English then American readers count as served, and a workspace whose docs are
written in German gets the mirror image. And where the per-country language breakdown could not be
measured for the window, markers read as unmeasured grey rather than red, so a missing measurement
can never look like a missing translation.

> Colour needs at least one translation language enabled to say anything useful.
> See [translation settings](../../translation/settings.md).


---

## Languages

The Languages list splits traffic by translation language — how many visitors read each language version of your docs.

| Column | What it shows |
|---|---|
| Language | Translation language |
| Visits | Page views in that language |
| % share | Portion of total translated traffic |

**How to open:** Float Widget → **Translations** → the **Languages** tab of the breakdown card.

This shows only non-English traffic (the default language is not tracked as a separate language switch).

---

## One language at a time

Every section above covers all countries and all languages at once. To judge a single language — how much of its own audience it actually reaches, and what it has cost — open **Translations** and pick that language from the sidebar.

[What a language's page shows](../../translation/settings.md#one-language-at-a-time)

## Related

- [Translation settings](../../translation/settings.md) — enabling a language for a region this report flags red
- [How AI translations work](../../translation/ai-translations.md) — what a translation run does and what it leaves alone
- [Analytics overview](../tracking/overview.md) — the Countries and Languages tabs inside the main panel
