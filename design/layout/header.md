---
title: "Header Layout & Navigation"
description: "Customize the top navigation bar of your Docsbook site — header links, social icons, theme toggle, search button, and language switcher placement."
---

# Header Options

Control what appears in the top navigation bar of your documentation site.

## Settings

| Setting | What it does |
|---|---|
| Header layout preset | Arranges header blocks (theme, search, Ask AI, nav links) into one of 5 presets |
| Show header | Show or hide the entire top navigation bar |
| Header links | Custom text links in the header nav |
| Social links | Icon links for GitHub, Twitter, Discord |
| Theme toggle in header | Show the light/dark switcher in the header |
| Language selector in header | Show the language switcher in the header |
| Search button in header | Show a search icon/button in the header |

## How to Configure

1. Open your docs site.
2. Float Widget → **Design** → **Header** tab.
3. Fill in fields and toggle options.
4. Save.

## Editing the header from the page

You can also change the header where you can see it. On your docs site, press
**Editor** in the toolbar, then click the part you want to change:

| Click on | You can |
|---|---|
| The project name or logo | Change the name, logo, or icon |
| A header link | Change its text or URL, or turn it into a filled button |
| Search / Ask AI / language / theme | Hide it |
| A social icon | Point it somewhere else, or remove it |
| Empty space in the bar | Switch the layout preset |

Each action is sent to the AI chat as a request, which then applies it — so you
see what was asked and what changed, and you can undo it in the same
conversation.

---

## Header Layout Presets

The **Header Layout** card is the first card in the Header tab. It picks a preset arrangement for the blocks in your top navigation — theme toggle, search, Ask AI, and nav links — without changing which blocks are shown.

| Preset | Arrangement | Best for |
|---|---|---|
| **Classic** (default) | Theme, Ask AI and search grouped on the right | Universal default — works for most docs sites |
| **Search-centric** | Wide search bar centered in the header, Ask AI on the right | Content-heavy docs where search leads |
| **Search + Ask AI** | Wide search centered with the Ask AI button right beside it | Docs where asking the AI matters as much as searching |
| **Centered** | Logo left, nav links centered, utilities right | Landing-page style with 3–5 links |
| **Minimal** | Ask AI and search shown as bare icons | Maximum room for nav links and social icons |

Click a preset to apply it — one click sets all six underlying placement fields at once (theme side, search width, Ask AI placement, icon-only Ask AI, icon-only search, nav link position).

**Ask AI beside the search** only takes effect when the search bar is wide. With a compact search there is no centre cluster for the button to join, so it stays in the right-hand group.

**Layout ≠ visibility.** A preset only controls *where* a block sits, never *whether* it's shown. If you turn off a block using its own toggle (for example, **Theme toggle in header**), that block disappears and the rest of the header keeps following the same preset — the remaining blocks don't shift into its place or change arrangement.

---

## Header Links

Add custom navigation links that appear in the top bar — useful for linking to your product, blog, changelog, or support.

**Format:** Each link has a **label** and a **URL**.

Example:
| Label | URL |
|---|---|
| Product | `https://yourapp.com` |
| Changelog | `https://yourapp.com/changelog` |
| Support | `https://yourapp.com/support` |

---

## Social Links

Add icon links for your community and social presence.

Supported platforms:
- **GitHub** — links to your repository or organization
- **Twitter / X** — links to your Twitter profile
- **Discord** — links to your community server

Social links appear as small icons in the header. They help readers find your community without cluttering the navigation with text links.

---

## Theme & Language in Header

You can place the theme toggle and language switcher in the header instead of (or in addition to) the sidebar.

For finer control over *where in the header* the theme toggle and search sit relative to nav links, see [Header Layout Presets](#header-layout-presets) above.

**Recommendation:** Pick one location for each control to avoid duplication.

- Header placement: more visible, less click-depth for new visitors.
- Sidebar placement: saves header space, better for dense headers.

[Sidebar options →](./sidebar)
[Theming options →](../style/theming)

---

## Hiding the Header

Setting **Show header** to off removes the entire top navigation bar.

Only do this for embed or kiosk use cases where your docs are framed inside another product. For standalone documentation sites, always keep the header visible.

---

> **Design navigation that guides your readers.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
