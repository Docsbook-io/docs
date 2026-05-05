# GitHub Integration

Let readers jump directly to edit any page on GitHub — making community contributions effortless.

## Settings

| Setting | What it does |
|---|---|
| Show "Edit on GitHub" | Adds an edit link at the bottom of every page |
| GitHub edit base URL | Base path for the edit link |

## How to Enable

1. Open your docs site.
2. Float Widget → **Design** → **Content** tab.
3. Turn on **Show "Edit on GitHub"**.
4. Set the **GitHub edit base URL** (see below).
5. Save.

## Setting the Edit Base URL

The edit base URL tells Docsbook where to send readers when they click "Edit on GitHub."

**Format:**
```
https://github.com/{username}/{repo}/edit/{branch}/{docs-folder}
```

**Examples:**

| Repository | Docs location | Edit base URL |
|---|---|---|
| `myname/my-repo` | Root of repo | `https://github.com/myname/my-repo/edit/main` |
| `myname/my-repo` | `/docs` folder | `https://github.com/myname/my-repo/edit/main/docs` |
| `myname/my-repo` | `master` branch | `https://github.com/myname/my-repo/edit/master` |

Docsbook automatically appends the current page path to this base URL.

If you leave this field empty, Docsbook uses a sensible default based on your repository.

## Why Enable It?

For **open-source projects**, the "Edit on GitHub" link is essential — it lets community members fix typos, clarify explanations, and improve examples with a single click.

For **team documentation**, it allows any team member to propose improvements without needing to know how Docsbook works — they just edit the file directly on GitHub.

---

> **Turn your readers into contributors.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
