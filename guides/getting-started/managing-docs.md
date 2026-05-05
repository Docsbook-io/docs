# Managing Documentation

How to work with documentation after creating your site.

## Float Widget — Managing Your Site

When you're logged in and viewing your own site, a management widget appears in the bottom-right corner.

```
┌──────────────────────┐
│ 👤 Your Name         │
│                      │
│ ✨ Premium / Free    │
│                      │
│ ⚙️ Settings          │
│ 🚪 Sign Out          │
└──────────────────────┘
```

### Click avatar or settings

A menu with management options will open.

## What Can You Configure?

### 1. Basic Settings

- **Workspace Name** — shown in your profile
- **Subscription Status** — Free or Premium
- **Site Language** — default language

### 2. Domain

(Premium only)

- If you have a custom domain — specify it here
- Instead of `docsbook.io/user/repo` you'll have `docs.example.com`

See in detail: [Custom Domain Setup](./custom-domain.md)

### 3. Appearance

Display options:

- **Hide "Powered by Docsbook"** (Premium)
  - Removes the badge at the bottom of the page
  - Makes the site completely yours

- **Theme** (coming soon)
  - Light / Dark theme
  - Will be added in the future

### 4. Languages & Translation

(Premium only)

- Enable automatic translation
- Select languages
- Documentation translates automatically

See in detail: [Document Translation](./translation.md)

### 5. Dangerous Actions

⚠️ **Delete Workspace**

Click "Delete Workspace" to:
- Delete all settings
- Disable the documentation site
- **This cannot be undone!**

Your GitHub repository won't be deleted, only the documentation site.

## How to Update Documentation?

### Method 1: GitHub Web Interface

1. Open your repository on github.com
2. Edit a markdown file
3. Click "Commit changes"
4. Updates appear on your Docsbook site

### Method 2: Git Locally

```bash
# 1. Clone the repository
git clone https://github.com/username/repo.git
cd repo

# 2. Edit files
nano docs/getting-started.md

# 3. Stage changes
git add docs/

# 4. Make a commit
git commit -m "Update documentation"

# 5. Push to GitHub
git push origin main
```

Updates appear on the site automatically!

### Method 3: Add a New Page

1. Create a new `.md` file in your repository
2. Write content
3. Commit
4. The file appears in the site menu

**Example:**

```bash
# Create new file
echo "# API Reference" > docs/api/reference.md

# Add content
echo "Your API documentation..." >> docs/api/reference.md

# Commit
git add docs/api/reference.md
git commit -m "Add API reference"
git push origin main
```

### Method 4: Delete a Page

1. Delete the file from the GitHub repository
2. Commit the deletion
3. The page disappears from the site

## Checking Synchronization

### Why hasn't my site updated?

**Updates are not instant, check:**

1. **Verify the commit in GitHub**
   - Open github.com → your repo
   - Do you see the new commit?
   - If not — update locally

2. **Refresh the page**
   - Press Ctrl+F5 (or Cmd+Shift+R on Mac)
   - This clears the browser cache

3. **Wait 1-2 minutes**
   - Sync is not instant
   - Docsbook periodically checks GitHub

4. **Check internet**
   - Make sure you have internet
   - Check if the repository is open

### Synchronization Issues?

**Files don't appear in menu:**
- Make sure files are `.md`
- Check names — only Latin letters, numbers, hyphens

**Some files updated, others didn't:**
- Could be browser cache
- Clear cache with Ctrl+F5

**Old version everywhere:**
- Wait 5 minutes
- Clear browser cache

## Structuring Documentation

### How to organize files?

The sidebar is built from the folder structure. Organize logically:

**Option 1: By Categories**
```
docs/
├── README.md
├── getting-started.md
├── api/
│   ├── overview.md
│   ├── auth.md
│   └── endpoints.md
└── guides/
    ├── deployment.md
    └── troubleshooting.md
```

**Option 2: By Detail Level**
```
docs/
├── README.md
├── 1-basics.md
├── 2-intermediate.md
├── 3-advanced.md
└── faq.md
```

**We recommend Option 1** — clearer structure.

## Links Between Pages

### How to create links within documentation?

```markdown
[See API](./api/overview.md)
[Start here](./getting-started.md)
[FAQ](../faq.md)
```

These links automatically convert to proper site page links.

### Links to Headings

```markdown
[Go to installation](#installation)
```

For this to work, another part of the file must have this heading:

```markdown
## Installation

Installation instructions...
```

## Images & Media

### How to add pictures?

1. **Add image to folder** (e.g., `docs/images/screenshot.png`)
2. **Upload to GitHub**
3. **Reference in markdown:**

```markdown
![Description](./images/screenshot.png)
```

### Where to store images?

Create a folder:

```
docs/
├── README.md
├── images/
│   ├── screenshot.png
│   ├── architecture.jpg
│   └── diagram.gif
└── guides/
```

### Formats

Supported:
- PNG (best)
- JPG (for photos)
- GIF (animation)
- WebP (modern format)

## Who Can See My Documentation?

### Open Access

Your documentation site is **open to everyone** — even if the repo is private.

**Who sees it:**
- ✅ Everyone on the internet
- ✅ Search engine bots (Google, Bing)
- ✅ People without a GitHub account

This is good — your documentation is accessible everywhere!

### Only You See Settings

The management widget is only visible to you when logged in.

Other people see only:
- Your documentation site
- Beautiful design
- Content
- **They don't see:** control buttons, settings, options

## Collaborative Documentation

### How to work together?

If multiple people work on documentation:

1. **Add them to the GitHub repository** — they can edit
2. **Anyone can update documentation** — by submitting pull requests
3. **Docsbook auto-updates the site** — as soon as changes merge to main

### Workflow

```
Colleague 1         Colleague 2         Docsbook Site
    ↓                   ↓                    ↓
Edits          →   Pull Request    →   Updates
Documentation      (Code Review)       Automatically
```

## Documentation Versioning

⚠️ Not yet supported, but planned.

Currently only the **latest version** is stored.

If you need different versions:
- Use Git branches (`docs/v1`, `docs/v2`)
- Or create separate repositories

## Analytics

### How do I know who's reading my documentation?

(Will be built-in soon)

For now you can:
1. Set up Google Analytics
2. Track traffic on your domain
3. See which pages are popular

Contact [support@docsbook.io](mailto:support@docsbook.io) for setup help.

## Next Steps

- [Setting Up a Custom Domain](./custom-domain.md)
- [Premium Features](./premium.md)
- [Frequently Asked Questions](../faq.md)
