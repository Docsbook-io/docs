---
title: "Logos strip"
description: "Social-proof strip under a landing page hero — uploads logos for brands that have them, names for those that don't. Available on all plans."
status: generated
version: "0.1"
---

# Logos strip

<!-- widget:mcp access=read -->

## find_skill / find_widget usage

Available as a content widget on every plan. Call `list_content_widgets` or open Settings → Widgets to see the full contract and examples. This page covers when to use it versus similar widgets.

### What it is

A centered row of customer marks placed directly under a landing page's hero. When an item has an uploaded logo image, it renders the logo; otherwise it renders the customer's name set in the page type. A half-finished wall always looks deliberate.

### Difference from neighbours

- `showcase` is a gallery where every tile carries a screenshot — right for 'here is what their site looks like'.
- `cards` labels destinations within your own docs — a grid of doors.
- `logos` says 'these people use it' — a single row of marks, not a gallery.

### Marker syntax

```markdown
<!-- widget:logos size=md color -->
```

`size` = `sm`, `md` (default), or `lg`. `color` keeps brand colours instead of desaturating the row.

### Item format

```markdown
<!-- widget:logos -->

**Trusted by teams shipping fast**

- [Cursor](https://cursor.com)
- [ClickHouse](https://clickhouse.com)
- [Discord Developers](https://discord.com/developers)

[See every site →](./showcase.md)

<!-- /widget -->
```

Each item is `- [Name](url)`. With a logo image — `- [Name](url) ![Name](/logos/name.svg)` — the mark is the picture. Without an image, it is the name in the page type. An item with no link renders as a plain mark.

A leading paragraph that is only `**bold text**` becomes a small uppercase eyebrow above the row. A final paragraph containing only links becomes a trailing link.

### Logo file format

Use SVG or a transparent PNG for uploaded logos. Always provide `![alt text]` — the alt text is what a screen reader and search engine read, and it falls back to the item's name when empty.

### Design notes

Marks are desaturated by default and lift to full colour on hover, because a row of brand palettes competes with the headline above it. Reach for `color` only when the marks themselves are the point of the section.
