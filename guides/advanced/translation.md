---
title: "How to Enable AI Translations"
description: "Step-by-step guide to enable AI-powered translations in Docsbook — pick target languages, let Claude translate, and serve indexed pages per locale."
---

# How to Translate Your Documentation

Automatically translate your documentation to any language.

**Required:** Pro (monthly, 7-day free trial) or Business (monthly, 14-day free trial)

## What Is Automatic Translation?

Docsbook can translate all your documentation to other languages **automatically**.

Select the target languages — AI does the rest.

**Example:**

```
Original documentation in English
                ↓
Select: Spanish, French, German
                ↓
All pages translated automatically
                ↓
Visitors see a language selection menu
```

## Supported Languages

Docsbook supports **15 languages** for automatic AI translation:

- English (EN)
- Español / Spanish (ES)
- Français / French (FR)
- Deutsch / German (DE)
- Português / Portuguese (PT)
- Italiano / Italian (IT)
- Русский / Russian (RU)
- 中文 / Chinese (ZH)
- 日本語 / Japanese (JA)
- 한국어 / Korean (KO)
- العربية / Arabic (AR)
- हिन्दी / Hindi (HI)
- Türkçe / Turkish (TR)
- Polski / Polish (PL)
- Nederlands / Dutch (NL)

## Enabling Translations

### Step 1: Check Your Plan

Translation is available on Pro and Business.

1. Open settings (Float Widget)
2. Check status — should show "Pro" or "Business"
3. If Free — [upgrade](./premium.md)

### Step 2: Open Translation Settings

1. Click Float Widget → Settings
2. Find **Translation Languages**

### Step 3: Select Languages

```
☑ English (default)
☐ Español
☐ Français
☐ Deutsch
☐ Italiano
☐ Português
☐ Русский
☐ 日本語
... and more
```

1. Check the languages you need
2. Click Save
3. Docsbook starts translating

### Step 4: Wait

Translation takes:
- **Small documentation (< 10 pages):** 1-2 minutes
- **Medium (10-50 pages):** 5-10 minutes
- **Large (> 50 pages):** 15-30 minutes

When done, translated versions appear on the site.

## How Is Translation Used?

### Language Selection Menu

Your site will have a language selector:

```
[EN ▼]  ← click to select another language
```

Clicking opens the list:

```
▼ English
  Español
  Français
  Deutsch
  Italiano
```

### URLs of Translated Pages

Translated pages are available at different paths:

```
English:  docs.example.com/page
Spanish:  docs.example.com/es/page
French:   docs.example.com/fr/page
German:   docs.example.com/de/page
```

### What Gets Translated?

- ✅ All text content
- ✅ Headings
- ✅ Image descriptions
- ✅ Tables
- ✅ Navigation (sidebar)
- ❌ Code blocks (stays as is)
- ❌ URLs and links (stay as is)
- ❌ Inline code (stays as is)

## Translation Quality

### How Does It Work?

Uses artificial intelligence (Claude from Anthropic) for translation.

**Quality:** Good for technical documentation

**What translates well:**
- Instructions and guides
- Technical explanations
- Lists and tables
- Simple language

**What may need editing:**
- Idioms and expressions
- Cultural references
- Specific slang

### Example Translation

```
Original English:
"Getting started is straightforward. Enter your URL to finish setup."

Translated Spanish:
"Comenzar es sencillo. Ingresa tu URL para completar la configuración."
```

## Updating Translations

### When Does Translation Update?

Enabling a language translates your whole site once. After that, pushing to GitHub does **not** re-translate anything on its own — readers keep seeing the last translation until it is re-run.

To update translations after an edit, ask your AI agent to re-translate the page, or re-run translation from the Translation tab. When a re-run is scoped to the pages a commit changed, those pages are translated first.

A large re-run is processed in chunks and resumes on its own until it finishes, so you do not need to keep an eye on it. The language row shows a progress counter while it runs, and marks the language **Stopped** with a reason if a run ended early.

### How to Update Manually?

If you want to override automatic translation:

1. Download translations
2. Edit the files
3. Upload back
4. Docsbook uses your version

(Contact support@docsbook.io for help)

## SEO & Translations

### Search Engines

Each language:
- Fully indexed by Google
- Separate pages in search
- Automatically adds hreflang tags

**Result:** Spanish speakers find your documentation in Spanish in Google.

### Traffic to Other Languages

Adding translations can:
- 📈 Increase visits
- 🌍 Expand audience
- 🔍 Improve SEO ranking

## Best Practices for Translation

### 1. Write Clearly

```
✅ Good (easy to translate):
"To install the package, run the command."

❌ Bad (hard to translate):
"Pip this bad boy and you're golden."
```

Plain English translates better.

### 2. Avoid Idioms

```
✅ Good:
"The setup process takes three steps."

❌ Bad:
"It's a piece of cake to set up."
```

Idioms often get lost in translation.

### 3. Use Structure

```
✅ Good structure translates better:
- Short paragraphs
- Clear headings
- Lists and tables
```

### 4. Keep Code Comments in English

```python
# Good — keep English
def setup():
    """Configure the system."""
    pass

# Bad — mixing languages
def setup():
    """Configurar el sistema."""
    pass
```

### 5. Use ISO Date Format

```
✅ ISO format: 2024-03-25
❌ Local: 25/03/2024
```

ISO format is consistent everywhere.

## Managing Translations

### Add a New Language

1. Open Settings
2. Click "Add language"
3. Select language
4. Save

Docsbook translates current pages to the new language.

### Remove a Language

1. Open Settings
2. Click ✕ next to the language
3. Save

Pages in that language stop being served — visitors on those URLs are redirected to the default language. Nothing is deleted: the translations are kept, so turning the language back on is instant and does not pay again for pages that have not changed.

### Change Default Language

Default is English. To change it:

1. Open Settings
2. Select from **Default Language**
3. Save

Visitors see this language first.

## URL Examples

### Structure of Translated Sites

**Without custom domain:**
```
docsbook.io/user/repo              — English
docsbook.io/user/repo/es           — Spanish
docsbook.io/user/repo/fr           — French
docsbook.io/user/repo/de/guides    — German (subpage)
```

**With custom domain:**
```
docs.example.com                    — English
docs.example.com/es                 — Spanish
docs.example.com/fr                 — French
docs.example.com/de/api/overview    — German (subpage)
```

## Analytics by Language

### Which Language Is Most Popular?

(Will be built-in soon)

For now you can track via Google Analytics:

1. Add GA code to the site
2. Filter by URL (`/es`, `/fr`, `/de`)
3. See traffic by language

Contact support@docsbook.io for help.

## Translation FAQ

**Q: Can AI translation be wrong?**

A: Yes, sometimes. Especially with technical terms or specific content. You can edit translations manually.

**Q: How long does translation take?**

A: 1 to 30 minutes depending on volume.

**Q: Can I edit translations manually?**

A: Yes, download translations, edit, upload back.

**Q: What if I need a rare language?**

A: Docsbook supports 15 languages today. If you need another one, contact support@docsbook.io.

**Q: Is translation free?**

A: Translations are included in Pro and Business, with a higher monthly limit on Business. No extra per-translation charges below those limits.

**Q: Will translation update when I update docs?**

A: Not on its own. A push to GitHub does not re-translate anything — readers keep seeing the last translation until you re-run it. Ask your AI agent to re-translate a page, or re-run translation from the Translation tab.

## What's Next?

- [Custom Domain](./custom-domain.md)
- [Pro and Business plans](./premium.md)
- [Managing Documentation](../getting-started/managing-docs.md)
