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

## Creating Your First Project

Before creating a workspace, you need a repository with documentation files.

### Option 1: Create a New Repository

1. Go to [GitHub](https://github.com/new)
2. Create a new repository
3. Add a `README.md` file with your project description
4. Create a `docs/` folder with markdown files

### Option 2: Fork an Example Repository

You can fork one of our example repositories to get started quickly:

- **[docsbook-io/docs](https://github.com/docsbook-io/docs)** — Complete documentation example
- **[docsbook-io/blog](https://github.com/docsbook-io/blog)** — Blog example
- **[docsbook-io/api-docs](https://github.com/docsbook-io/api-docs)** — API documentation example

**To fork:**

1. Click on the repository link above
2. Click the **"Fork"** button
3. Choose where to fork it (your account)
4. Clone it to your local machine or edit directly on GitHub

## Creating a Workspace

### Step 1: Open the Site

1. Go to [docsbook.io](https://docsbook.io)
2. Click **"Create my docs site"** or **"Sign in"**

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

1. **Edit the file** in GitHub, locally, or with Claude Code
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

## Editing Documentation with GitHub Web Interface

The simplest way to edit documentation without any tools.

### Edit a File

1. Go to your repository on GitHub
2. Navigate to the file you want to edit
3. Click the **pencil icon** (Edit this file)
4. Make your changes in the editor
5. Click **Commit changes**
6. Add a commit message (e.g., "Update getting-started.md")
7. Click **Commit**

### Create a New File

1. Go to your repository
2. Click **Add file** → **Create new file**
3. Enter the file name (e.g., `docs/new-page.md`)
4. Type your markdown content
5. Click **Commit new file**

### Delete a File

1. Open the file in your repository
2. Click the **trash icon**
3. Click **Commit changes**

**Screenshot placeholder: GitHub web editor interface**

## Editing Documentation with Claude Code

Use Claude Code for faster editing and more advanced features.

### Setup

1. [Install Claude Code](https://claude.com/claude-code)
2. Open your documentation repository in Claude Code
3. Sign in with your GitHub account

### Edit Files

1. Click on a `.md` file in the sidebar
2. Make your changes
3. Claude Code will suggest improvements
4. Stage and commit your changes with git

### Use AI Assistance

You can ask Claude Code to:
- **Generate content** — "Write a guide for getting started"
- **Fix formatting** — "Add proper markdown headers"
- **Improve text** — "Make this section clearer"
- **Add examples** — "Add code examples to this section"

### Commit and Push

```bash
# Stage your changes
git add docs/

# Commit with a message
git commit -m "docs: update getting-started guide"

# Push to GitHub
git push
```

Your documentation site updates automatically!

**Screenshot placeholder: Claude Code editing interface**

## Manual Editing with VS Code

For advanced users who prefer local editing.

### Setup

1. [Install VS Code](https://code.visualstudio.com/)
2. [Install Git](https://git-scm.com/)
3. Clone your repository:

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
```

### Edit Files

1. Open the repository in VS Code
2. Edit `.md` files in the `docs/` folder
3. Use the built-in preview (Markdown Preview)
4. Save your changes

### Useful Extensions

- **Markdown All in One** — Better markdown editing
- **Prettier** — Auto-format on save
- **Spell Checker** — Check spelling
- **Code Spell Checker** — Check code comments

### Commit and Push

```bash
# Check what changed
git status

# Stage your changes
git add docs/

# Commit with a message
git commit -m "docs: update getting-started guide"

# Push to GitHub
git push
```

Your documentation site updates automatically!

### Live Preview

To see how your docs look locally:

```bash
# Install a local markdown server (optional)
npm install -g http-server
cd docs
http-server
```

Visit `http://localhost:8080` to see your files.

**Screenshot placeholder: VS Code with documentation files**

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
