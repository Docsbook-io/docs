---
title: "Sidebar Layout & Configuration"
description: "Configure the left navigation panel in Docsbook — sidebar search, breadcrumbs, language switcher, page/folder icons, subheader folder tabs, and how readers move between documentation pages."
---

# Sidebar Control

Configure what appears in the left navigation panel of your documentation.

## Settings

| Setting | What it does |
|---|---|
| Language switcher in sidebar | Show the language selector inside the left sidebar |
| Search in sidebar | Show a search box inside the left sidebar |
| Breadcrumbs | Show a breadcrumb trail above page content |
| Sidebar icons | Show a [lucide](https://lucide.dev/icons) icon next to a specific page or folder |
| Subheader folder icons | Show a lucide icon on a folder's tab in the subheader |

## How to Configure

1. Open your docs site.
2. Float Widget → **Design** → **Left Sidebar** tab.
3. Toggle the desired options.
4. Save.

---

## Language Switcher

Shows a language selector inside the sidebar so readers can switch translation languages.

**When to use:** Enable this when your header is already crowded with other elements.

> Note: Enable *either* the sidebar switcher *or* the [header language selector](./header#header-options) — not both. Showing it in two places creates redundancy.

Requires at least one translation language to be enabled.
[Set up translations →](../../translation/settings)

---

## Search in Sidebar

Adds a search input box directly inside the left sidebar panel.

This is an alternative to the header search button. Some readers prefer sidebar search because it doesn't cover page content.

[More about search options →](../../content/features/search)

---

## Breadcrumbs

Shows the current page location as a trail above the page title:

```
Home > Guides > Custom Domain
```

Breadcrumbs help readers in large documentation sites understand where they are and navigate up a level quickly.

**Recommended:** Keep breadcrumbs on for docs with more than 20 pages or multiple nested sections.

---

## Sidebar Icons

Add an icon next to any individual page or folder in the left sidebar, so readers can scan the tree visually instead of by label alone.

**How to Configure**

1. Open your docs site.
2. Float Widget → **Design** → **Left Sidebar** tab.
3. In the **Sidebar Icons** card, search for the page or folder you want to mark, then pick a [lucide](https://lucide.dev/icons) icon for it (e.g. `rocket`, `book-open`).
4. Repeat for any other pages or folders.
5. Save.

The picker only offers icon names from the current lucide icon set — searching by name (e.g. "rocket", "book", "folder") narrows the results. An icon assignment applies to one page or one folder; assign a folder's icon separately from any pages inside it.

**When to use:** Icons help readers spot key sections (getting started, API reference, FAQ) at a glance in a long or deeply nested sidebar. For a small docs site with only a handful of top-level pages, icons are optional.

---

## Subheader Folders

Turn any top-level repository folder into its own tab in the subheader — the row of tabs shown below the main header, on docs pages. Each enabled folder can also carry a lucide icon on its tab.

**How to Configure**

1. Open your docs site.
2. Float Widget → **Design** → **Header** tab.
3. In the **Subheader Folders** card, toggle on any top-level folder you want shown as a subheader tab.
4. Optionally, click the icon button next to an enabled folder to pick a lucide icon for its tab (or **Remove icon** to clear one already set).
5. Save.

A folder shown in the subheader can also be hidden from — or kept in — the left sidebar independently; see the **Folder Visibility** card next to Subheader Folders for that toggle.

---

> **Build the navigation experience your readers need.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
