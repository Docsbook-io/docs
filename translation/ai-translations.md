# AI Translations

How Docsbook automatically translates your documentation using Claude AI.

## How It Works

1. You enable a language in [Translation Settings](./settings).
2. Docsbook fetches your markdown files from GitHub.
3. Each file is sent to **Claude** (by Anthropic) for translation.
4. Translated pages are cached for fast delivery.
5. When you push updates to GitHub, only changed pages are re-translated.

No manual work. No translation files to maintain. No YAML keys.

## What Gets Translated

| Translated | Not translated |
|---|---|
| Body text | Code blocks |
| Headings | Inline code (`like this`) |
| Tables | URLs and links |
| Image alt text | File paths |
| Sidebar navigation labels | Technical identifiers |
| Page titles and meta descriptions | — |

Code is intentionally left in the original language — it should stay consistent regardless of the reader's locale.

## Translation Cache

Translations are cached per page per language, keyed to the file's content hash on GitHub.

- First visit after a content change triggers re-translation (a few seconds).
- All subsequent visits serve the cached version instantly.
- Cached translations persist even if you temporarily disable a language.

This means re-enabling a language that was previously active is instant — no re-translation needed.

## Translation Quality

Claude produces high-quality technical documentation translations.

**Works best for:**
- Step-by-step guides
- API documentation
- FAQs
- Configuration references

**May need manual review for:**
- Brand-specific terminology
- Cultural references or idioms
- Highly domain-specific jargon

## Writing Tips for Better AI Translation

Clear source content produces better translations. Follow these guidelines:

- **Use short, direct sentences.** Long compound sentences lose nuance in translation.
- **Avoid idioms.** "It's a piece of cake" doesn't translate literally. Say "It's simple."
- **Use ISO date format.** Write `2024-03-25`, not "March 25th" — dates are interpreted differently across locales.
- **Keep code comments in English.** They're excluded from translation but should be readable by all developers.
- **Use consistent terminology.** If you call something a "workspace" in one place, don't call it a "project" in another.

---

> **Go global without the translation overhead.**
> [Enable translations →](https://docsbook.io/connect)

See also: [Translation Settings →](./settings)
