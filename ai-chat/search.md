---
title: "Turn on full-text search on your documentation site"
description: "Put a search box in your Docsbook header or sidebar, pick which one your readers get, and see exactly what the search index covers."
---

# Turn on full-text search

Docsbook indexes every markdown page in your repository and can expose that index in two places: a search button in the header, and a search box in the left sidebar. Reader search costs nothing from your project balance — it queries an index Docsbook already built.

## Turn on the header search button

1. Open your docs site while signed in.
2. Open Float Widget → **Design** → **Header** tab.
3. Turn on **Search button**.
4. Click **Save**.

The button appears in the top bar of every page.

## Turn on sidebar search

1. Open your docs site while signed in.
2. Open Float Widget → **Design** → **Left Sidebar** tab.
3. Turn on **Search in sidebar**.
4. Click **Save**.

The box appears above the navigation tree in the left panel.

## Choose where the search box belongs

Both placements can run at the same time. Enabling one is usually enough.

| Placement | Best for | Trade-off |
|---|---|---|
| Header | First-time visitors, who look at the top bar first | Competes for space with your header links |
| Sidebar | Readers who already navigate by the tree | Hidden on narrow screens where the sidebar collapses |

If your header already carries several links, use sidebar search instead of adding another control to the top bar.

## What Docsbook search indexes

Docsbook full-text search covers every markdown file the site publishes, and the index is rebuilt when your repository changes on GitHub. There is nothing to reindex by hand.

Search matches:

- Page titles
- Headings
- Body text
- Code blocks, ranked below prose

Keyword search runs against that index and never calls an AI model, so it does not draw on your project balance. Semantic search — matching by meaning rather than by keyword — does call a model, and is billed against the balance like any other AI usage.

## Next steps

- [See what readers searched for](../../analytics/tracking/overview.md) — the queries that returned nothing tell you which page to write next.
- [Content options](../setup/content-options.md) — the other controls in the same Design panel.

<!-- widget:cta -->

## Put search in front of your readers

Every new project starts with $1 of balance, and reader search does not spend it.

[Create a project](https://docsbook.io/start)

<!-- /widget -->
