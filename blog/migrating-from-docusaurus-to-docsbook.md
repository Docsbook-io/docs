---
title: "Migrating from Docusaurus to Docsbook, step by step"
description: "Move a Docusaurus site to Docsbook: keep your /docs URLs, convert admonitions and tabs, drop sidebars.js and the build, and redirect the pages that changed."
---

# Migrating from Docusaurus to Docsbook

Point Docsbook at the repository that holds your Docusaurus `docs/` folder, convert admonitions and tabs, and your pages keep their `/docs/…` URLs with no build step.

Docusaurus details below are from [docusaurus.io](https://docusaurus.io/docs) as of September 2026. If you are still deciding whether to move, read [Docusaurus alternatives in 2026](./docusaurus-vs-docsbook.md) first.

## How do I move from Docusaurus to Docsbook?

<!-- widget:stepper -->

### Connect the repository

[Start on Docsbook](https://docsbook.io/?start=1) and import the repository. Every `.md` and `.mdx` file outside `node_modules/` and `.github/` becomes a page, including a Docusaurus `blog/` folder, and the site goes live at `https://<owner>.docsbook.io/<repo>`.

### Convert admonitions and tabs

Docsbook does not compile MDX, so `:::note` shows up as text and tabs lose their switcher. Swap them for [widgets](../site/widgets.md) using the table below.

### Take React out of the pages

`import` lines and JSX components do not run on Docsbook. Replace them with a widget, plain Markdown, or a link to a live demo hosted elsewhere.

### Fix image paths

Docusaurus serves `static/img/diagram.png` at `/img/diagram.png`. Docsbook resolves images relative to the page's file, so write `../static/img/diagram.png` from a page in `docs/`.

### Redirect what moved

Pages whose Docusaurus URL came from a number prefix or a `slug` get a new URL on Docsbook. Rename them, or map the old path in `.docsbook/redirects.json`.

**On a [custom domain](../site/custom-domain.md)** the redirects file does not fire yet — it works on the site's `docsbook.io` address — so keep the old paths wherever you can.

### Move the domain and retire the build

Attach the domain in **Settings ▸ Domain & API**, then delete the deploy workflow. The repository stays; only the build goes.

![Settings ▸ Domain & API: the Custom Domain card with docs.helio.dev entered and a Save button](../images/admin/settings-domain.webp)

<!-- /widget -->

## What changes in the Markdown?

Plain Markdown and frontmatter `title` and `description` move as they are. MDX features and sidebar config need a Docsbook equivalent.

| Docusaurus | Docsbook |
|---|---|
| `:::note` … `:::` | A `callout` widget with `type=note`; `tip`, `info`, `warning` and `danger` keep their names |
| `:::note Custom title` | The same callout with a `### Custom title` heading inside |
| `<Tabs>` and `<TabItem label="npm">` with their imports | A `tabs` widget with one `### npm` heading per tab, or a `code-group` when the tabs only hold code |
| `sidebars.js`, `_category_.json`, `sidebar_position` | Not read: folders and file names order the sidebar |
| `slug` in front matter | Not read: the URL is the file path |
| `versioned_docs/` | No version switcher: keep the current version, or keep old ones as an ordinary folder |

An admonition before and after, readable on GitHub either way:

<!-- widget:code-group -->

#### Docusaurus

```markdown
:::warning
Rotate the API key before you deploy.
:::
```

#### Docsbook

```markdown
<!-- widget:callout type=warning -->

Rotate the API key before you deploy.

<!-- /widget -->
```

<!-- /widget -->

## Will my URLs change?

Most will not. Docusaurus serves `docs/intro.md` at `/docs/intro` by default, and so does Docsbook on your domain, because Docsbook's URL is the file path.

Two kinds of page do change:

- **Number prefixes** — Docusaurus serves `docs/01-intro.md` at `/docs/intro`; Docsbook serves it at `/docs/01-intro` and shows the prefix in the sidebar label.
- **Custom slugs** — a page with `slug: /start` in its front matter moves back to its file path.

Rename those files, or send the old path to the new one:

```json
{
  "version": 1,
  "redirects": [
    { "from": "docs/start", "to": "docs/getting-started" }
  ]
}
```

Both sides are page paths without `.md`, up to 500 entries. When the agent renames a page for you, it adds the redirect itself.

## Can the agent do the conversion?

Yes. Tell the Docsbook agent in one sentence, from Claude Code, Cursor or the panel chat ([Get discovered](../get-discovered.md)):

```text
Convert the Docusaurus admonitions and tabs in docs/ to Docsbook callouts and tabs, and remove the MDX imports.
```

It opens a [pull request](../agent/review.md); with **Auto-merge** off, the change waits for your approval. On a repository in your own GitHub account, install the Docsbook GitHub App with **Contents: Read and write** first.

After the move, the same agent keeps looking for the next win: [Find wins fast](../find-wins-fast.md).

## FAQ

<!-- widget:accordion -->

### What happens to my Docusaurus landing page?

`README.md` at the repository root becomes the home page, so give it your docs' introduction. React pages under `src/pages/` (`.js` or `.tsx`) are not published, because Docsbook publishes only Markdown files.

### Do I have to delete docusaurus.config.js?

No: Docsbook reads only Markdown, so config and theme files are ignored. Delete them once the domain points at Docsbook.

### Can I run both sites while I test?

Yes. Connecting the repository publishes a second site on a `docsbook.io` address and changes nothing in your Docusaurus deploy until you move the domain.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Docusaurus alternatives in 2026](./docusaurus-vs-docsbook.md) — When to stay, when to move {git-compare}
- [Widgets](../site/widgets.md) — Callouts, tabs, steppers and cards in plain Markdown {layers}
- [Custom domain](../site/custom-domain.md) — Serve the docs from your own domain {globe}
- [Find wins fast](../find-wins-fast.md) — What the agent fixes first after you move {zap}

<!-- /widget -->
