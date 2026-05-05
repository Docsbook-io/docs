# Translating Documentation to Other Languages

Automatically translate your documentation to any language.

**Required:** Premium subscription ($29 one-time)

## What Is Automatic Translation?

Docsbook can translate all your documentation to other languages **automatically**.

Just select the languages — AI does the rest.

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

Docsbook can translate to **100+ languages**:

**Main languages:**
- English
- Español (Spanish)
- Français (French)
- Deutsch (German)
- Italiano (Italian)
- Português (Portuguese)
- Русский (Russian)
- 日本語 (Japanese)
- 中文 (Chinese)
- 한국어 (Korean)
- العربية (Arabic)
- ภาษาไทย (Thai)

Plus 80+ other languages.

## Enabling Translations

### Step 1: Check Premium

Translation is only available in the Premium subscription.

1. Open settings (Float Widget)
2. Check status — should show "Premium"
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

When done — translated versions appear on the site.

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
"Getting started is a breeze. Just plug in your URL and boom,
you're done!"

Translated Spanish:
"Comenzar es muy fácil. Solo ingresa tu URL y listo, ¡hemos terminado!"
```

## Updating Translations

### When Does Translation Update?

When you update documentation:

1. Edit file in English
2. Commit to GitHub
3. Docsbook notices changes
4. Translates updates to other languages
5. Done! Translated versions are updated

This happens automatically — you don't need to do anything.

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
"Just pip this bad boy and you're golden!"
```

Plain English translates better.

### 2. Avoid Idioms

```
✅ Good:
"The setup process is simple."

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

Pages in that language disappear from the site. History is saved and can be restored.

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

A: Docsbook supports 100+ languages. For a specific one — contact support@docsbook.io.

**Q: Is translation free?**

A: Included in Premium subscription. No extra charges.

**Q: Will translation update when I update docs?**

A: Yes, automatically on the next update.

## What's Next?

- [Custom Domain](./custom-domain.md)
- [Premium Features](./premium.md)
- [Managing Documentation](./managing-docs.md)
