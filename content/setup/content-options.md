---
title: "Show or hide the controls around your page content"
description: "Toggle the scroll-to-top button, prev/next arrows, breadcrumbs, the Ask AI button and the Copy page dropdown on your Docsbook documentation site."
---

# Content options

Content options are the Docsbook toggles that control the interface *around* your page — the navigation and action controls, not the words. All of them live on one tab and apply to every page on the site.

> Looking to change how the content itself renders — cards, accordions, steps, call-to-action blocks? That is [Content widgets](../features/widgets.md), written in the markdown rather than toggled here.

## What each option does

| Setting | What it does |
|---|---|
| Scroll to top button | Floating button that returns the reader to the top of the page |
| Prev / Next buttons | Navigation arrows at the bottom of each page |
| Breadcrumbs | Breadcrumb trail above the page title |
| Ask AI button | Chat button shown on the page (owners also get Editor) |
| Ask AI in outline | AI button shown in the right-side table of contents panel |
| Copy page menu items | Seven independent toggles for the Copy page dropdown |

## Change a content option

1. Open your docs site while signed in.
2. Open Float Widget → **Design** → **Content** tab.
3. Toggle the options you want.
4. Click **Save**.

## Scroll to top

A small floating arrow appears once the reader scrolls down. One click returns them to the top of the page.

Turn it on for long reference pages, API tables, or any page taller than one screen.

## Prev / Next buttons

Adds **← Previous** and **Next →** arrows at the bottom of every page, linking to the adjacent pages in your sidebar order.

Turn them on for docs read in sequence, such as a tutorial series. Leave them off for reference docs, where each page is consulted on its own and the arrows suggest an order that does not exist.

## Breadcrumbs

Shows the current page's location as a path above the heading:

```text
Home > Guides > Custom domain
```

Breadcrumbs read the same folder structure the sidebar does, so they follow your repository layout with nothing to configure. See [Sidebar settings](../../design/layout/sidebar.md) for the related navigation controls.

## Copy page menu

The Copy page dropdown holds seven items: Copy page, Copy Skills.md URL, View as Markdown, and one-click links that open the current page in ChatGPT, Claude, Cursor, Windsurf, or via VS Code MCP. Each has its own toggle.

Turn off any subset to keep the dropdown down to the items you want. Once every item is off, the dropdown's chevron disappears, because there is nothing left to open. See [the Copy page dropdown](../features/copy.md#what-is-in-the-copy-page-dropdown) for what each item hands the reader.

## Ask AI button

Shows the AI controls on the page. It requires the AI agent to be enabled.

On the page this renders as an **Ask AI** button in the action row above the content, next to **Copy page**. Pressing it opens the question box at the bottom of the page, already pointed at the page being read; pressing it again puts the box away.

You can show it in two places:

- On the page, in the action row above the content
- In the right outline panel, beside the table of contents

Both can be on at once. Unlike the other options on this tab, this one leads somewhere that spends money: every answer the assistant writes is billed against the project's balance, while the button itself costs nothing until a reader asks something.

## Next steps

- [Content widgets](../features/widgets.md) — the reference for blocks written in the markdown itself.
- [Copy page and copy markdown buttons](../features/copy.md) — what the Copy page dropdown hands a reader.
- [Sidebar settings](../../design/layout/sidebar.md) — the navigation tree these controls sit around.

<!-- widget:cta -->

## Set up the controls your readers need

Every new project starts with $1 of balance, and these toggles do not spend it.

[Create a project](https://docsbook.io/start)

<!-- /widget -->
