# Creating a Documentation Site

A complete guide to creating your first documentation in Docsbook.

## Requirements

What you need to get started:

1. **GitHub account** — to sign in
2. **Public repository** — where your documentation lives
3. **Markdown files** (`.md`) — your documentation

## Preparing the Repository

### Folder Structure

Docsbook works with any structure, but we recommend organizing it like this:

```
my-project/
├── README.md              ← Home page
├── docs/                  ← Documentation folder
│   ├── getting-started.md
│   ├── installation.md
│   ├── api/
│   │   ├── overview.md
│   │   ├── auth.md
│   │   └── endpoints.md
│   └── guides/
│       ├── deployment.md
│       └── faq.md
└── src/                   ← Project code (ignored)
```

### File Formats

**Supported:**
- `.md` — main format (recommended)
- `.markdown` — alternative

**Not supported:**
- `.rst` (ReStructuredText)
- `.txt` (text files)
- `.html` (HTML files)

### Naming Rules

- **Lowercase** — better for URLs
- **With hyphens** — `getting-started.md` instead of `Getting_Started.md`
- **Descriptive names** — reflect the content

**Examples:**
- ✅ `getting-started.md`
- ✅ `api-overview.md`
- ✅ `faq.md`
- ❌ `doc1.md`
- ❌ `README (1).md`

### README.md

**README.md** is the home page of your documentation. It will be displayed when visitors first arrive at your site.

**Recommended content:**
- Brief project description
- Key features
- Links to other sections
- How to get started

**Example:**

```markdown
# My Project

A brief description of what this is.

## Features

- Feature 1
- Feature 2
- Feature 3

## Quick Start

[Start here](./getting-started.md)

## Documentation

- [Installation](./installation.md)
- [API](./api/overview.md)
- [FAQ](./faq.md)
```

## Creating a Workspace

### Step 1: Open the Site

1. Go to [docsbook.io](https://docsbook.io)
2. Click **"Create my docs site"**

### Step 2: Sign in with GitHub

1. Click **"Sign in with GitHub"**
2. Enter your GitHub credentials
3. Allow Docsbook access

Docsbook will request permissions to:
- Read your public repositories
- Access your profile (name, avatar, email)

### Step 3: Select a Repository

After signing in you'll see a list of your public repositories.

1. Find the desired repository
2. Click on it
3. Docsbook will create the Workspace

### Step 4: View Your Site

Done! Your site is available at:

```
docsbook.io/{your-github-name}/{repo-name}
```

## Your Site Structure

### Sidebar

The sidebar is built from the file structure automatically:

```
Files in GitHub:         Shown in menu:
├── README.md            ├─ Home
├── getting-started.md   ├─ Getting Started
├── api/
│   └── overview.md      └─ API
        └─ Overview
```

### Navigation

Click on a filename in the sidebar → navigate to that page.

**Links within content also work:**

```markdown
[See API](./api/overview.md)
```

Automatically converted to a link to the page in Docsbook.

## Updating Documentation

### How to Update?

1. **Edit the file** in GitHub or locally
2. **Commit the changes** to the repository
3. **Visit the documentation site** (refresh the page)
4. **See the updates** automatically!

No additional steps needed — it syncs itself.

### Examples of Changes

**Add a new page:**
```
Create a new file guides/deployment.md → it will appear in the menu
```

**Delete a page:**
```
Delete the file from GitHub → the page disappears from the site
```

**Change text:**
```
Edit the text → updates on the site
```

**Rename a file:**
```
Rename the file → URL and menu update
```

## Markdown Content

### Basic Formatting

```markdown
# Heading 1
## Heading 2
### Heading 3

Regular text.

**Bold text** and *italic*.

`inline code`
```

### Lists

```markdown
- Item 1
- Item 2
  - Sub-item
  - Sub-item

1. First
2. Second
3. Third
```

### Code

Code blocks with syntax highlighting:

````markdown
```javascript
function hello() {
  console.log("Hello");
}
```

```python
def hello():
    print("Hello")
```

```bash
echo "Hello"
```
````

300+ programming languages supported.

### Links

```markdown
[Link text](https://example.com)
[Link to another page](./other-page.md)
[Anchor to heading](#heading)
```

### Images

```markdown
![Image description](./images/screenshot.png)
![External image](https://example.com/image.png)
```

PNG, JPG, GIF supported.

### Tables

```markdown
| Column 1 | Column 2 |
|----------|----------|
| Value    | Value    |
| Value    | Value    |
```

### Blocks

```markdown
> Quote or important information

---

Horizontal line above
```

## Best Practices

### 1. Clear Structure

```
✅ Good:
docs/
├── 01-getting-started.md
├── 02-installation.md
├── 03-usage.md
└── faq.md

❌ Bad:
docs/
├── doc1.md
├── doc2.md
├── readme.md
```

### 2. Short Headings

```
✅ "Getting Started"
❌ "How to Get Started with Our Amazing Project"
```

### 3. Short Paragraphs

```
✅ 3-5 sentences per paragraph
❌ Huge blocks of text without breaks
```

### 4. Code Examples

```
✅ Include examples and code
❌ Description only, no examples
```

### 5. Keep It Current

Update documentation together with code.

```
✅ Documentation + new feature = commit to GitHub
❌ Code updated, but documentation is out of sync
```

## Pre-publication Checklist

Before publishing your documentation:

1. **Check structure** — is the folder hierarchy logical?
2. **Check links** — do all links work?
3. **Check formatting** — is code highlighted?
4. **Check spelling** — any typos?
5. **Check images** — are pictures displayed?

## Next Steps

- [Managing Documentation](./managing-docs.md)
- [Setting Up a Custom Domain](./custom-domain.md)
- [Premium Features](./premium.md)
