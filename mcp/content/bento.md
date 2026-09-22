---
title: "Bento card grid"
description: "Renders mixed-width feature cards on a twelve-column rail — each with a screenshot, badge, chips and icon. Available on all plans."
status: generated
version: "0.1"
---

# Bento card grid

<!-- widget:mcp access=read -->

## find_skill / find_widget usage

Available as a content widget on every plan. Call `list_content_widgets` or open Settings → Widgets to see the full contract and examples. This page covers how it differs from `cards` and `showcase`, and when to reach for it.

### What it is

A twelve-column rail of feature cards of different widths, each carrying a title, a short description, an optional badge, a screenshot, and either inline body or chip tags. It is the block a landing or feature page uses to show what the product looks like across several features at once.

### Difference from neighbours

- `cards` crops an image into a 6.5rem band beside an icon, which turns a dashboard screenshot into a grey smear. A bento card carries the full screenshot flush to the bottom edge.
- `showcase` IS its picture, with only a name and tagline under it — right for 'sites other people built', wrong for 'here is one feature, explained'.

Reach for `bento` when each item needs a paragraph AND a screenshot, and when relative importance should be visible in their width.

### Marker syntax

```markdown
<!-- widget:bento cols=3 -->
```

`cols` sets the default card width (1–4); the default of 3 means unmarked cards span 4 columns. Every card then controls its own width with `{span:N}`.

### Per-card markers

All per-card markers appear at the end of the list item, before the closing punctuation:

- `{span:N}` — card width out of 12 columns. Values outside 1–12 are ignored. A row adds up to 12.
- `{crop:center}` / `{crop:top}` / `{crop:bottom}` etc. — which part of the screenshot survives the frame. Default `top`.
- `{side}` — picture BESIDE the copy instead of under it. Useful for full-width `{span:12}` cards.
- `{badge:New}` / `{badge:Beta}` — small accent-coloured pill above the title, up to 32 characters.
- `{tags}` — nested bullet list renders as chips under the title instead of body prose. Each chip one or two words.
- `{icon-name}` — Lucide glyph above the title (e.g. `{rocket}`, `{chart-line}`).

Markers may appear in any order and are all optional. A card without a screenshot falls back to `{icon-name}` or plain text.

### Content structure

Each list item becomes one card. Indented markdown under the item renders as body text:

```markdown
<!-- widget:bento cols=3 -->

- **Analytics that speaks in revenue** — Set a call-to-action URL and an average deal size. {badge:Autonomous} {span:7}

  ![Analytics screen](https://docsbook.io/shot-analytics.png)

  Revenue, conversion rate, and bounce rate in one view.

- **Plugs into your stack** — GitHub, Slack, Google Calendar, any MCP server. {span:5}

  ![Integrations screen](https://docsbook.io/shot-integrations.png)

<!-- /widget -->
```

### Usage guidance

Three to five stages is the working range. Two reads as a comparison (wanted `cards`), seven turns each lane into a column too narrow to carry a label.

Cards in a row line their pictures up along the bottom however uneven the copy above them is, so descriptions do not need matching length.
