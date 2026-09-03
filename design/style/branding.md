---
title: "Match your documentation site to your product brand"
description: "Set the name, accent color, fonts and icon of your Docsbook site, and declare the page it drives readers to so analytics can report what it earned."
---

# Branding

Branding is where a Docsbook documentation site takes your product's name, logo, accent color and fonts. Two of the fields on this page are not cosmetic: **Call To Action URL** and **Average Product Price** are what let analytics report conversions and revenue at all.

## Branding settings

| Field | What it does |
|---|---|
| Custom name | Display name shown in the browser tab and header |
| Call To Action URL | The page your docs should drive readers to — see below |
| Average Product Price | What one conversion is worth, so analytics can report revenue — see below |
| Accent color | Primary brand color applied to buttons, links, and highlights |
| Heading font | Google Font used for headings (h1–h6) |
| Content font | Google Font used for body text — falls back to the heading font |

## How to apply branding

1. Open your docs site.
2. Float Widget → **Design** → **Branding** tab.
3. Fill in the fields.
4. Click **Save**.

Changes apply instantly — no rebuild needed.

## Call To Action URL

Your **Call To Action URL** is the one page your documentation exists to send people to: your pricing page, a demo booking, signup. Set it once and three things start using it:

- **Your AI chat** points readers there when they are evaluating, comparing, or asking about plans — and stays out of the way when the question is plain troubleshooting.
- **Content generation** treats it as the goal of the site, so pages end on a next step instead of a dead end, and the AI can add it to your header as a button.
- **Analytics** counts a reader who leaves for this domain as a conversion. That is what turns the Conversations card from "readers left the docs" into "readers reached the page that sells", and it is what the Conversion rate figure at the top of the analytics panel measures.

Enter a full `https://` address. Matching is by domain, so every path on it counts and query strings or UTM tags are fine. Leave it empty if you have nothing to sell yet — nothing breaks, you lose the goal column in analytics.

If you set it while creating your first documentation, it is already filled in here.

## Average Product Price

Your **Average Product Price** is what one conversion is worth to you on average — a plan price, a typical order value, whatever a reader who reaches your call-to-action page is worth once they buy.

Set it and the analytics panel starts reporting **Revenue** and **Revenue per visitor**: the readers who clicked through to your Call To Action URL, multiplied by this number.

Enter it in dollars — `299` or `29.90`, with or without the `$`. It pairs with the Call To Action URL above, and both are needed: one says which click counts, the other says what it is worth. Set only one and the revenue figures stay switched off, saying which half is still missing.

Leave it empty to turn revenue reporting off again. There is no way to enter `0` — a zero average price would leave the figures looking switched on while reporting `$0` forever, which is worse than an honest blank.

## Accent color

The accent color of a Docsbook site is a hex code (e.g., `#5B47E0`). It affects:
- Active states in the sidebar
- Toggle switches
- Buttons
- Links

Pick a color that matches your product's primary brand color. Avoid very light colors — they won't meet contrast requirements on white backgrounds.

---

## Fonts

Pick the typography of your documentation site from 1500+ Google Fonts. Headings and body text are set
separately, so you can pair a distinctive display face with a highly readable
body face.

**Fields:** `Headings`, `Content`

**How to set fonts:**

1. Float Widget → **Design** → **Font** card.
2. Pick a font under **Headings** — this styles h1–h6.
3. Optionally pick a different font under **Content** — this styles body text.
4. Save.

Leaving **Content** empty means body text uses the heading font, so a single
pick still styles the whole page. Each picker has a search box and previews
every family in the font itself. **Reset** clears a field.

The fonts load from Google Fonts automatically — nothing to install or host.

---

## Custom icons

Set a custom favicon and header icon for your documentation site.

**Field:** `Icon URL`

**How to set an icon:**

1. Float Widget → **Design** → **Branding** tab.
2. Paste a public URL to your icon image into the **Icon URL** field.
3. Save.

**Icon requirements:**
- Use a square image — PNG or SVG recommended.
- Ideal size: 64×64 px (PNG) or any size (SVG).
- The URL must be publicly accessible (no auth required).

**Where the icon appears:**
- Browser favicon (tab icon)
- Header logo area in your docs sidebar

## Related

- [Theming — light, dark, system](./theming.md) — the theme your accent color is drawn on
- [Header layout and navigation](../layout/header.md) — where the name, logo and icon appear
- [Analytics overview](../../analytics/README.md) — the Revenue and Conversion figures these two fields switch on
