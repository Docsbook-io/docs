---
title: "Content widgets: rich blocks written in plain markdown"
description: "Reference for every Docsbook content widget — cards, tabs, accordion, stepper, pricing, api, cta, cta-form and recommendations — and the markers each reads."
---

# Content widgets

A Docsbook content widget renders part of your page as a rich UI block — a grid of cards, a collapsible FAQ, numbered steps — without leaving markdown behind.

You mark the region with two HTML comments. They are invisible in every markdown reader, so the same file still reads correctly on GitHub, in your editor, and in any other tool. Only Docsbook re-shapes it.

```markdown
<!-- widget:cards -->

- [Search](./search.md) — Let readers find a page by keyword {search}
- [Page feedback](./feedback.md) — Ask whether the page helped {thumbs-up}

<!-- /widget -->
```

Widgets render on the server, so the output is plain HTML: indexable by search engines, readable by AI crawlers, and working with JavaScript disabled.

## The rules

- Each marker sits on its own line, with a blank line between it and the content.
- Widgets do not nest. An inner marker leaves the outer region as plain markdown.
- Nothing is ever hidden. An unknown widget name or a missing closing marker degrades to ordinary markdown — your content still appears.
- A widget you have switched off in your project settings behaves the same way: the markers stay in your file, and the region publishes as ordinary markdown. See [Turning a widget off](#turning-a-widget-off).
- Write the region so it reads correctly as plain markdown first. The widget is a presentation upgrade, not a data format.
- Some widgets take layout switches on the opening marker: `<!-- widget:cards cols=2 horizontal -->`. Switches go **on** the marker, never inside the region — the marker is already invisible, so your content stays plain markdown. A switch a widget does not recognise is ignored; the block still renders.

## Available widgets

<!-- widget:accordion -->

### cards — a grid of linked cards

Turns link lists into a responsive grid. Best on index and hub pages that send readers somewhere else.

- Each heading becomes a small uppercase label above its grid. Headings are optional.
- `- [Title](/href) — Description.` gives a card with a title and a description.
- End an item with `{icon-name}` to add an icon, e.g. `{rocket}`, `{book-open}`. Names come from the Lucide set. An unknown name is dropped silently — the braces never reach the page.
- Put an `![alt](url)` image in the item to use a real picture instead of an icon — it fills the same area the icon would. Better than an icon when the card is about a specific thing you have a picture of.
- An item without a link renders as a non-clickable card.

```markdown
<!-- widget:cards -->

## Start here

- [Search](./search.md) — Let readers find a page by keyword {search}
- [Page feedback](./feedback.md) — Ask whether the page helped {thumbs-up}

<!-- /widget -->
```

**Give a card a body.** Leave a blank line after the item and indent more markdown under it — paragraphs, a short list, a snippet. It renders under the description. Worth it when the card has something to explain; a card that only labels a destination reads better as one line.

**Give a card its own action.** If the last indented line contains nothing but links, it becomes the card's call-to-action row. A sentence that merely *contains* a link stays ordinary text.

**Choose the layout.** `cols=1`, `cols=2`, `cols=3` or `cols=4` fixes the number of columns; `horizontal` puts the icon beside the text instead of above it, for a compact row. Both go on the opening marker and can be combined. Without `cols` the grid fits as many cards per row as the page width allows, which is usually what you want. Narrow screens always get fewer columns.

```markdown
<!-- widget:cards cols=2 -->

- [Full-text search](./search.md) — Match a reader's keyword against your pages {search}

  Indexes every markdown file the site publishes and rebuilds itself when the
  repository changes. Nothing to reindex by hand.

  [Read the guide](./search.md)

- [Page feedback](./feedback.md) — Ask whether the page helped {thumbs-up}

  One click from the reader, no form and no email address. Results land per
  page, so you can sort by the pages rated worst.

  [Read the guide](./feedback.md)

<!-- /widget -->
```

### tabs — parallel versions behind one switch

Turns headed sections into a tab strip with one visible panel. Use it when the same instruction exists in several parallel versions and the reader needs exactly one of them: a package manager, an operating system, a language SDK, a hosted-versus-self-hosted path.

- Each heading becomes one tab; everything under it until the next heading of the same level becomes that tab's panel.
- The first tab is the one that opens, so put the variant most readers want first.
- A heading may end with `{icon-name}`, e.g. `### macOS {apple}`. Give every tab an icon or none of them — a strip where only some tabs have one reads as broken.
- Any markdown works inside a panel, including tables and code blocks with syntax highlighting.
- Content before the first heading renders above the strip as an intro. Use it for the one sentence true of every tab.
- Keep labels to one or two words. The strip scrolls sideways rather than wrapping, so a sentence-length label pushes the other tabs out of sight.
- Up to 8 tabs are switchable. A 9th section and beyond render below the strip as ordinary headings — nothing is lost, but a set that long wanted a list of headings.
- The panels are all in the page source and the switching is CSS-only, so every variant stays readable with JavaScript off and visible to crawlers.

Do not use it to hide content the reader needs all of. That is `accordion` on scanned reference material, and plain headings for a sequence.

### accordion — collapsible rows

Turns headed sections into rows the reader expands. Best for material people scan rather than read: FAQs, troubleshooting, per-option details.

- Each heading becomes one row; everything under it until the next heading of the same level becomes the row's body.
- Any markdown works inside a row, including code blocks and tables.
- Every row starts collapsed, so write headings that say enough to choose from without opening.
- Content before the first heading renders above the accordion as an intro.

### stepper — numbered steps

Turns headed sections into a connected, top-to-bottom sequence. Use it when the order matters — installation, setup, a multi-stage tutorial. If the order does not matter, use `accordion` instead.

- Each heading becomes one step, numbered in document order.
- Adding or removing a step renumbers the rest automatically.

### pricing — plans a reader can choose between

Turns plans into a row of comparable cards, or a plan table into a comparison matrix. Use it where a reader has to *choose* between tiers rather than read about them.

The widget picks its shape from what you wrote: headings present gives one card per plan, a region that is one plain table instead is re-rendered as a matrix. Write whichever shape the page already is.

**Plan shape.** Each heading is a plan name.

- The first paragraph under the heading is the price, rendered large: `**$20** / month` emphasises the number and keeps the unit beside it. Write `Free` or `Contact sales` the same way when there is no figure.
- The second paragraph is one line on who the plan is for. It sits between the price and the list, which is the narrowest part of the card.
- A list becomes what the plan includes, each item ticked. An item written struck through — `~~Priority support~~` — gets a dash and renders muted, which shows what a cheaper plan leaves out without a second list.
- A paragraph that is only `**bold text**` directly under the heading becomes that plan's badge and marks it featured: a ring around the card and a solid button. Use it on at most one plan.
- The plan's last link-only paragraph becomes its buttons, exactly as in `cta`. The featured plan's first button is solid and the rest are ghosts, so the block has one loud thing in it.

**Matrix shape.** The first column names the feature and every other column is a plan. A cell whose whole text is `yes`, `no`, `✓`, `—`, `included` or `none` becomes a tick or a dash, with the word kept in the markup for screen readers. A cell holding anything else — `3 seats`, `Unlimited`, a footnote — is left exactly as written. An empty cell stays empty: silence is not a "no".

`cols=1|2|3|4` on the opening marker fixes the grid at that many columns. The default fits as many cards as the page allows.

Never write a price, plan name, limit or service commitment into this widget that you did not read from the source. It is the one widget whose content is a commercial promise.

### api — an interactive endpoint playground

Turns REST endpoint sections into a form the reader can send a real request from, with their own key and parameters.

- A heading that is a method and a path — `## POST /api/v1/chat` — becomes one endpoint block.
- The first table under it with a `Field` (or `Name` / `Parameter`) column becomes the request form, one input per row. `Type`, `Required` and `Description` columns are used when present.
- Templated path segments like `/project/update/{projectId}` always get their own input.
- An Authorization input is always added. The reader's key is sent from their own browser and never reaches Docsbook.
- Documenting `Authorization` as a row in the table is fine: that row is claimed by the header input above, keeping your description, instead of rendering a second time as a field that would put the key in the URL.
- A `###` subsection containing a code block — `### Example`, `### Response` — moves into a samples pane beside the form, keeping its title. Any other subsection, such as an `### Errors` table, stays in the document flow below.

### cta — a compact call to action

A small bordered block closing a page with the one thing the reader should do next.

- The first heading becomes the block's title. It renders as a styled line rather than a real heading, so it stays out of your page outline.
- A leading paragraph that is only `**bold text**` becomes a small uppercase eyebrow.
- A paragraph containing only links becomes the buttons: the first is solid, the rest outlined. A sentence that merely contains a link stays prose.
- Use one per page and at most two links. A second block competes with the first and both convert worse.

```markdown
<!-- widget:cta -->

## Publish your docs from GitHub

Connect a repository and your markdown is live.

[Create a project](https://docsbook.io/start) · [See pricing](https://docsbook.io/pricing)

<!-- /widget -->
```

### cta-form — a call to action with an input

The same block, with the primary action rendered as a one-field form. What the reader types is carried into the target URL, so they can start without retyping it on the next page.

- The first link's URL is the form target, and its link text labels the button.
- Name the field with an empty query parameter: `?email=` submits what the reader typed as `email`. Without a query string the field is named `email`.
- A parameter that already has a value rides along unchanged — `?email=&ref=docs` keeps `ref=docs` on the submitted URL, which is useful for attribution.
- Set the placeholder with the link's markdown title: `[Join](https://example.io/signup?email= "you@company.com")`.
- The keyboard follows the field name: `email` gets an email keyboard, `url` / `site` / `domain` a URL one.
- A target that cannot take a form, such as `mailto:` or an in-page anchor, degrades to a plain button.

Point it only at a URL that actually reads the parameter. A page that ignores it silently drops what the reader typed, which is worse than a plain button.

### recommendations — a ranked list of things to fix

Turns a list of findings into a grid of cards, each carrying a severity badge and a link to act on. Use it for concrete, prioritized findings about your own documentation — audit results, content-health issues, any "here is what to fix, ranked" list. For a plain list of destinations use `cards` instead.

- Each heading becomes a small uppercase group label above its list. Headings are optional — omit them for a single ungrouped list.
- Each list item becomes one recommendation. `- [Title](/href) — Explanation. {severity}`: the link text is the headline, the text after the dash is why it matters and what to do.
- End every item with a severity marker — `{urgent}`, `{worth-doing}` or `{later}`. An item with no recognised marker renders as `{worth-doing}` rather than losing its severity.
- An item without a link renders as a non-clickable recommendation. Write one only when there is genuinely nowhere to send the reader.
- Paragraphs between a heading and its list pass through as ordinary intro prose.

```markdown
<!-- widget:recommendations -->

- [You are paying to keep the same page twice](/docs/quickstart) — "Quickstart" and "Getting started" are 96% the same and neither links to the other. Keep one, merge the other into it. {urgent}
- [214 people found "Webhooks" the hard way](/docs/webhooks) — No page links to it, yet it still gets visits. Add a link from "Integrations". {worth-doing}
- [Nobody reads "Migration notes"](/docs/migration-notes) — Zero visits although 2 pages link to it. Reword the link text. {later}

<!-- /widget -->
```

<!-- /widget -->

## Adding a widget without editing markdown

You do not have to type the markers by hand. In the live editor, select a block and pick **turn into a widget** from the action panel — the menu lists the widgets that fit that block, and the markers are written into your source for you. See [Editing on the page](../../guides/getting-started/managing-docs.md).

The **Widgets** section of your project settings shows the same set as a gallery, each one with a picture of what it renders and a page describing the markdown it expects. **Apply to a page** on any of them closes the settings and turns on editing over your docs, with that widget offered first on whichever block you pick.

## Turning a widget off

Every widget is on for every project. If one does not suit your documentation, switch it off in **Settings → Widgets** and Docsbook stops rendering it across the whole site.

Switching a widget off never edits your files. The `<!-- widget:… -->` comments stay exactly where an author put them, every word between them still publishes, and the region appears as ordinary markdown — the same thing that happens to a misspelled widget name. Switch it back on and every page that used it returns to the rich block, with nothing to re-write.

Two consequences worth knowing:

- The live editor stops offering a switched-off widget, and so does the assistant when it writes a page for you. Neither can hand you markers that would not render.
- Pages already translated into another language keep the widget until their next translation pass. Only the original picks the change up immediately.

## Related

- [Content options](../setup/content-options.md) — the toggles that control the UI around your content, rather than the content itself.
- [Copy page and copy markdown buttons](./copy.md) — the action row the `cta` widget sits below.
- [Editing on the page](../../guides/getting-started/managing-docs.md) — apply a widget to a block without typing the markers.
