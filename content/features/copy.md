---
title: "Copy Page & Markdown Buttons"
description: "Let readers copy a full page as markdown or copy code blocks with one click — perfect for pasting context into ChatGPT, Claude, or other AI assistants."
---

# Copy Options

Give readers easy ways to copy your documentation content.

## Settings

| Setting | What it does |
|---|---|
| Copy page button | Adds a "Copy page" button — copies the full page as markdown |
| Copy markdown | Shows a markdown copy option on code blocks |
| Copy page menu items | Seven independent toggles — Copy Skills.md URL, View as Markdown, and one per AI client (ChatGPT, Claude, Cursor, Windsurf, VS Code MCP) — for what appears in the Copy page dropdown |

## How to Enable

1. Open your docs site.
2. Float Widget → **Design** → **Content** tab.
3. Toggle the desired copy options.
4. Save.

---

## Copy Page Button

Adds a button (usually near the top of the page) that copies the entire page content as raw markdown.

**Use cases:**
- Readers who want to paste page content into an AI prompt (e.g., ChatGPT, Claude) for further analysis.
- Teams that want to quickly copy documentation into internal tools.
- Technical writers who reference your docs while writing their own.

---

## Copy Page Menu

The "Copy page" button expands into a dropdown with more options: Copy page, Copy Skills.md URL, View as Markdown, and — by default — a set of one-click links that open the page directly in an AI client: **ChatGPT**, **Claude**, **Cursor**, **Windsurf**, and **Connect via VS Code MCP**.

Each of those seven items has its own toggle, so you can keep exactly the ones you want and hide the rest — e.g. keep the plain copy actions but drop just Windsurf, or keep only the base "Copy page" button and turn everything else off. The dropdown's chevron hides itself automatically once every item is off, since there'd be nothing left to open.

**All enabled by default.** Toggle them individually in Float Widget → **Design** → **Content** tab, on the "Copy page menu" card.

---

## Copy Markdown on Code Blocks

When enabled, every code block shows a small "copy" icon. Clicking it copies the raw code.

This is a standard developer experience feature. Most developers expect it — enabling it removes friction from your most technical readers.

**Tip:** This is tracked as an event in [Events Analytics](../../analytics/tracking/events), so you can see which code examples are copied most often.

---

> **Make your documentation worth copying.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
