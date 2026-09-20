---
title: "Configure the footer of your Docsbook documentation site"
description: "Add a footer under your documentation: columns of links, a copyright and legal block, a call-to-action button, social icons and a light/dark picker."
tldr: "Docsbook's site footer is off by default and only appears once you switch it on and fill in at least one block — a link column, copyright text, a CTA button, your logo, or social icons."
---

# Footer Options

The footer is the band under every page of your Docsbook documentation site. It is where the things a reader looks for at the *end* of a page belong: your terms and privacy links, the legal entity behind the product, a way back to your pricing page, your community accounts.

It is **off by default**, so nothing on your site changes until you turn it on. Every setting here is a display choice — a footer costs nothing against your project balance.

## Footer settings

| Setting | What it does |
|---|---|
| Site Footer | Turns the footer on or off |
| Footer layout | Arranges the footer's blocks into one of 3 layouts |
| Footer links | Columns of links — up to 6 columns of 15 links each |
| Show the site logo | Shows your logo and project name in the footer |
| Copyright / legal text | Free text under the logo: copyright line, company, address |
| Call-to-action button | An optional button — its label, and where it points |
| Social icons in the footer | Shows the accounts you set under [Social links](./header.md#social-links) |
| Light / dark / system picker | A three-way theme picker in the footer |

## How to configure the footer

1. Open your docs site.
2. Float Widget → **Customize** → **Footer** tab.
3. Fill in the cards and save.

You can also just ask the AI chat — "add a footer with Terms and Privacy at the bottom" — or drive it from an MCP client with `update_ui_settings` (the switches) and `update_navigation` (the link columns).

---

<!-- widget:callout type=note -->

## Turning it on is not quite enough

The footer renders once it is switched on **and** has something in it: a link column, the copyright text, a call-to-action label, your logo, or social icons you have actually set.

This is deliberate. Switching it on and filling it in are two different cards, so "on, nothing in it yet" is the normal state for as long as it takes to type the first column — and a rule with nothing above it drawn across the bottom of every page looks like a site that broke, not like a setting you have not finished. Fill in any one block and the footer appears.

<!-- /widget -->

---

## Footer layouts

| Layout | Arrangement | Best for |
|---|---|---|
| **Columns** (default) | Brand block on the left, link columns on the right | A product site's footer — the widest shape, room for 3–4 columns |
| **Centered** | Logo, text, links and socials stacked down the middle | Smaller projects with one or two columns of links |
| **Minimal** | A single row: text on the left, links and socials on the right | Docs that want a closing line and nothing more |

**Layout ≠ visibility**, exactly as in the [header](./header.md#header-layout-presets). A layout decides only *where* a block sits. Turning a block off with its own toggle removes that block and leaves every other block where the layout put it.

---

## Footer links

Each column has a heading and a list of links. A link can be:

- an in-site path — `/pricing`, `/guides/setup`
- an absolute URL — `https://yourapp.com/blog`
- a mail or phone destination — `mailto:support@yourapp.com`, `tel:+15551234567`

Example:

| Column | Links |
|---|---|
| Product | Pricing · Changelog · Status |
| Company | About · Careers · Contact |
| Legal | Terms of service · Privacy policy · Security |

Links to your own site open in the same tab; external links open in a new one.

A few rules the editor applies for you when you save:

- Blank rows are dropped, so you can leave a half-typed row behind without it blocking the save.
- A column left with no usable links is dropped along with its heading — a heading with nothing under it is just a stray word.
- Up to **6 columns** of **15 links**.

Social profiles do **not** go in a column. They are the [social links](./header.md#social-links) your header already uses, drawn as icons — see below.

---

## The brand block

Beside the columns sits your brand block: your logo and project name, a free-text line under it, and an optional button.

**Copyright / legal text** is plain text and keeps its line breaks, which is what you want for the usual three-line block:

```
Copyright © 2026 — All rights reserved
Example Inc.
1 Example Street, Springfield
```

**The call-to-action button** needs a label to appear at all. Leave its URL blank and it points at your project's own [Call To Action URL](../style/branding.md#call-to-action-url) — the destination you already told Docsbook readers should end up at — so you do not have to type it twice. The button picks up your [accent color](../style/branding.md#accent-color) when you have one set.

---

## Social icons and the theme picker

**Social icons** in the footer are the same accounts as in the header. The footer's setting is only *whether* to show them — you set *which* on the [Social links](./header.md#social-links) card, in one place, so the two never disagree.

**The light / dark / system picker** is a three-way control, which is the difference from the sidebar's toggle: next to a copyright line, "follow my system" is usually the option a reader wants, and a two-state switch cannot offer it.

---

## The "Powered by Docsbook" badge

The badge at the foot of your pages is not a footer setting. When you enable a footer, the badge **moves into it** — it appears once, in the footer's bottom bar, instead of once above it. Turning a footer on never removes it and never shows it twice.

---

## Translations

Footer link labels and the copyright text are shown exactly as you wrote them in every language. Unlike sidebar labels and header links, they are not currently sent for translation.

<!-- widget:cards plain cols=2 -->

## Related

- [Header options](./header.md) — the other end of the frame, and where social links are set {panel-top}
- [Sidebar layout and configuration](./sidebar.md) {panel-left}
- [Branding — name, logo, colors, fonts](../style/branding.md) — the logo and accent the footer uses {palette}
- [Theming — light, dark, system](../style/theming.md) — what the footer's theme picker switches {moon}

<!-- /widget -->
