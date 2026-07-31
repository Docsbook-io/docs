---
title: "Content Options & Settings"
description: "Show or hide UI elements around your documentation content — scroll-to-top, prev/next buttons, breadcrumbs, and Ask AI placement options."
---

# Content Options

Control the UI elements that appear around your page content.

> Looking to change how the content itself renders — cards, accordions, steps, call-to-action blocks? That is [Content Widgets](../features/widgets.md), written in the markdown rather than toggled here.

## Settings

| Setting | What it does |
|---|---|
| Scroll to top button | Floating button that returns the reader to the top of the page |
| Prev / Next buttons | Navigation arrows at the bottom of each page |
| Breadcrumbs | Breadcrumb trail above the page title |
| Ask AI button | Preview / Chat switcher shown on the page (owners also get Editor) |
| Ask AI in outline | AI button shown in the right-side table of contents panel |
| Copy page menu items | Seven independent toggles for the Copy page dropdown — Skills.md URL, view as Markdown, and one per AI client (ChatGPT, Claude, Cursor, Windsurf, VS Code MCP) |

## How to Configure

1. Open your docs site.
2. Float Widget → **Design** → **Content** tab.
3. Toggle the desired options.
4. Save.

---

## Scroll to Top

A small floating arrow that appears after the reader scrolls down. One click returns them to the top of the page.

**Recommended for:** Long reference pages, API docs, or any page that exceeds one screen height.

---

## Prev / Next Buttons

Adds "← Previous" and "Next →" navigation arrows at the bottom of every page, linking to the adjacent pages in your sidebar order.

**Recommended for:** Tutorial-style docs where readers follow a sequence. Leave off for reference docs where pages are consulted independently.

---

## Breadcrumbs

Shows the current page location as a path above the heading:

```
Home > Guides > Custom Domain
```

[More about breadcrumbs in sidebar settings →](../../design/layout/sidebar)

---

## Copy Page Menu

The Copy page dropdown includes Copy Skills.md URL, View as Markdown, and one-click links that open the current page directly in ChatGPT, Claude, Cursor, Windsurf, or via VS Code MCP — seven items in total, each with its own toggle. Turn off any subset to keep the dropdown focused on just the items you want; once every item is off, the dropdown's chevron disappears entirely.

[More about the Copy page dropdown →](../features/copy#copy-page-menu)

---

## Ask AI Button

Shows the AI controls on the page. Requires the AI Agent to be enabled.

On the page itself this renders as a small segmented switcher. Readers see
**Preview** and **Chat** — Chat opens the AI assistant. Signed-in owners get a
third position, **Editor**, which arms block-level editing of the live page.

You can show it:
- On the page (the switcher, above the content)
- In the right outline panel (table of contents area)

Both can be on at the same time if you want maximum discoverability.

---

> **Give readers the navigation experience they deserve.**
> [Connect your GitHub repo →](https://docsbook.io/create)
