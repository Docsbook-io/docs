---
title: "Add an Edit on GitHub link to every documentation page"
description: "Turn on the reader-facing Edit on GitHub link, set the edit base URL for your repository layout, and let readers open a pull request on a typo."
---

# Add an Edit on GitHub link

The **Edit on GitHub** link appears at the bottom of every page on your Docsbook site and opens that page's source file in the GitHub editor. A reader who spots a typo can fix it and open a pull request without knowing anything about Docsbook.

> Looking for something else? This page covers the reader-facing edit link. To connect a GitHub account, or to move a Docsbook-hosted project into a repository you own, open the project picker in the AI chat header and use **Connected repository** — see [Quick start](../../quick-start.md).

## What the two settings do

| Setting | What it does |
|---|---|
| Show "Edit on GitHub" | Adds the edit link at the bottom of every page |
| GitHub edit base URL | The base path the link is built from |

## Turn on the edit link

1. Open your docs site while signed in.
2. Open Float Widget → **Design** → **Content** tab.
3. Turn on **Show "Edit on GitHub"**.
4. Set the **GitHub edit base URL** — see the next section.
5. Click **Save**.

## Set the GitHub edit base URL

The edit base URL tells Docsbook where to send a reader who clicks the link. Docsbook appends the current page's path to it.

```text
https://github.com/YOUR_USERNAME/YOUR_REPO/edit/YOUR_BRANCH/YOUR_DOCS_FOLDER
```

Pick the row that matches where your markdown lives:

| Repository | Docs location | Edit base URL |
|---|---|---|
| `myname/my-repo` | Root of the repository | `https://github.com/myname/my-repo/edit/main` |
| `myname/my-repo` | `/docs` folder | `https://github.com/myname/my-repo/edit/main/docs` |
| `myname/my-repo` | `master` branch | `https://github.com/myname/my-repo/edit/master` |

Leave the field empty and Docsbook builds the link from the repository you connected.

## When to turn it on

For an **open-source project**, the edit link is the cheapest contribution path you can offer: a reader fixes a wrong flag or a stale version number in the browser, and you get a pull request instead of an issue.

For **internal team docs**, it lets anyone on the team propose a wording change without learning the Docsbook interface — they edit the file on GitHub and the site follows.

The edit link calls no AI model, so it does not draw on your project balance.

## Next steps

- [Content options](./content-options.md) — the other toggles on the same Design tab.
- [Manage your documentation site](../../guides/getting-started/managing-docs.md) — how an edit on GitHub reaches your live site.

<!-- widget:cta -->

## Turn your readers into contributors

Every new project starts with $1 of balance, and the edit link does not spend it.

[Create a project](https://docsbook.io/start)

<!-- /widget -->
