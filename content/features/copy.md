---
title: "Let readers copy your docs page as markdown or code"
description: "Add a Copy page button, per-code-block copy icons, and one-click hand-off of the page into ChatGPT, Claude, Cursor, Windsurf or VS Code MCP."
---

# Copy page and copy markdown buttons

The Docsbook copy controls hand a reader the raw markdown of the page they are reading, either as a whole page or one code block at a time. A reader who copies a page into an AI assistant gets your exact wording instead of the assistant's summary of it.

## What each setting does

| Setting | What it does |
|---|---|
| Copy page button | Adds a **Copy page** button that copies the whole page as markdown |
| Copy markdown | Adds a copy icon to every code block |
| Copy page menu items | Seven independent toggles for what appears in the Copy page dropdown |

## Turn on the copy controls

1. Open your docs site while signed in.
2. Open Float Widget → **Design** → **Content** tab.
3. Turn on the copy options you want.
4. Click **Save**.

## What the Copy page button copies

The Copy page button sits in the action row above the page content. Clicking it puts the entire page on the clipboard as raw markdown — headings, tables and code included, with no site chrome.

Readers use it to paste a page into an AI prompt, to lift a procedure into an internal runbook, or to quote your docs while writing their own.

## What is in the Copy page dropdown

The Copy page button expands into a dropdown with seven items: Copy page, Copy Skills.md URL, View as Markdown, and one-click links that open the current page in **ChatGPT**, **Claude**, **Cursor**, **Windsurf**, or **Connect via VS Code MCP**.

Each of the seven has its own toggle, so you can keep the plain copy actions and drop a single AI client, or keep only the base Copy page button and turn everything else off. Once every item is off, the dropdown's chevron disappears, because there is nothing left to open.

All seven are on by default. Toggle them in Float Widget → **Design** → **Content** tab, on the **Copy page menu** card.

## Copy icons on code blocks

With **Copy markdown** on, every fenced code block shows a small copy icon that copies the raw code without the surrounding prose.

Each click is recorded as an event, so [Events analytics](../../analytics/tracking/events.md) shows which of your examples readers actually take away.

## Next steps

- [Content options](../setup/content-options.md) — the rest of the toggles on the same Design tab.
- [Content widgets](./widgets.md) — turn a region of markdown into cards, steps or an API playground.

<!-- widget:cta -->

## Make your pages worth copying

Every new project starts with $1 of balance, and the copy controls do not spend it.

[Create a project](https://docsbook.io/start)

<!-- /widget -->
