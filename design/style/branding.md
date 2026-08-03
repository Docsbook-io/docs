---
title: "Branding — Colors, Fonts, Logos"
description: "Match your documentation to your product — custom name, accent color, logo, fonts, and remove the Powered by Docsbook badge on Pro plans."
---

# Branding

Make your documentation feel like your product — not a generic template.

## Settings

| Field | What it does |
|---|---|
| Custom name | Display name shown in the browser tab and header |
| Call To Action URL | The page your docs should drive readers to — see below |
| Accent color | Primary brand color applied to buttons, links, and highlights |
| Heading font | Google Font used for headings (h1–h6) |
| Content font | Google Font used for body text — falls back to the heading font |
| Hide "Powered by Docsbook" | Remove the footer badge *(Pro)* |

## How to Apply

1. Open your docs site.
2. Float Widget → **Design** → **Branding** tab.
3. Fill in the fields.
4. Click **Save**.

Changes apply instantly — no rebuild needed.

## Call To Action URL

The one page your documentation exists to send people to: your pricing page, a demo booking, signup. Set it once and three things start using it:

- **Your AI chat** points readers there when they are evaluating, comparing, or asking about plans — and stays out of the way when the question is plain troubleshooting.
- **Content generation** treats it as the goal of the site, so pages end on a next step instead of a dead end, and the AI can add it to your header as a button.
- **Analytics** counts conversations that end on this domain as reaching the goal, which is what turns the Conversations card from "readers left the docs" into "readers reached the page that sells".

Enter a full `https://` address. Matching is by domain, so every path on it counts and query strings or UTM tags are fine. Leave it empty if you have nothing to sell yet — nothing breaks, you just lose the goal column in analytics.

If you set it while creating your first documentation, it is already filled in here.

## Accent Color

The accent color is a hex code (e.g., `#5B47E0`). It affects:
- Active states in the sidebar
- Toggle switches
- Buttons
- Links

Pick a color that matches your product's primary brand color. Avoid very light colors — they won't meet contrast requirements on white backgrounds.

---

## Fonts

Pick your typography from 1500+ Google Fonts. Headings and body text are set
separately, so you can pair a distinctive display face with a highly readable
body face.

**Fields:** `Headings`, `Content`

**How to set:**

1. Float Widget → **Design** → **Font** card.
2. Pick a font under **Headings** — this styles h1–h6.
3. Optionally pick a different font under **Content** — this styles body text.
4. Save.

Leaving **Content** empty means body text uses the heading font, so a single
pick still styles the whole page. Each picker has a search box and previews
every family in the font itself. **Reset** clears a field.

The fonts load from Google Fonts automatically — nothing to install or host.

---

## Custom Icons

Set a custom favicon and header icon for your documentation site.

**Field:** `Icon URL`

**How to set:**

1. Float Widget → **Design** → **Branding** tab.
2. Paste a public URL to your icon image into the **Icon URL** field.
3. Save.

**Requirements:**
- Use a square image — PNG or SVG recommended.
- Ideal size: 64×64 px (PNG) or any size (SVG).
- The URL must be publicly accessible (no auth required).

**Where it appears:**
- Browser favicon (tab icon)
- Header logo area in your docs sidebar

---

## Hide "Powered by Docsbook" *(Business)*

By default, a small "Powered by Docsbook" badge appears at the bottom of the sidebar.

Turning this off gives your documentation a fully white-label appearance.

> **Business feature.** Requires a Business plan.
> [Upgrade to Business →](https://docsbook.io/connect)

---

> **Start building your brand.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
