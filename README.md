# Localization Playground

A simple web tool that helps translators check their work when the text contains **placeholders** — special markers that get replaced with a file name, a number, or a word depending on a particular situation.

🔗 **[Open the tool](https://securefolderfs-community.github.io/LocalizationTester/)**

---

## What problem does this solve?

Some localizable strings in SecureFolderFS aren't just plain text. They contain logic — for example, a single string might need to say:

- *"Copying document.pdf"* — when there's only one file
- *"Copying 3/10 items"* — when there are multiple files
- *"Copying 7 items"* — when the total number of items is unknown

All three of those come from the same string with placeholders in it. This tool lets you paste that string, fill in some test values, and instantly see what the final text looks like — without needing to run the app.

---

## How to use it

**1. Paste the original string**

Copy the string from the translation file and paste it into the **Original** box on the left. You'll see a live preview appear at the bottom.

**2. Paste your translation**

Type or paste your translated version into the **Translation** box on the right. Try to keep the `{placeholders}` exactly as they appear in the original — only translate the surrounding words.

> [!TIP]
> It's often easier to copy the original string and translate it from there.

**3. Fill in the parameters**

The tool automatically detects the placeholders in the string and shows them as input fields in the **Parameters** section. Fill them in with realistic values — for example, set a filename or a number — and both previews will update instantly.

**4. Check the previews**

- ✅ If the preview shows normal text, everything looks good.
- 🔴 If the preview turns red, something in the format is broken. The error message will tell you what went wrong.

---

## Example

The default string already loaded in the tool is:

```
Copying {Total:choose(0):{Achieved} {Achieved:plural:item|items|items}|{Total:choose(1):{State}|{Achieved}/{Total} {Total:plural:item|items|items}}}
```

While intimidating at first, the logic is straightforward:

| `Total` | `Achieved`     | `State`      | Result               |
|---------|----------------|--------------|----------------------|
| 0       | 7              | *(anything)* | Copying 7 items      |
| 1       | *(any number)* | document.pdf | Copying document.pdf |
| 10      | 3              | *(anything)* | Copying 3/10 items   |

Try changing the values in the Parameters section and watch the previews update in real-time.

> [!NOTE]
> In this case, the 'State' is a universal parameter that represents the file name.

---

## Tips for translators

- **Don't change the placeholders.** The logic inside `{curly braces}` is not translatable. Move them around in the sentence, but don't rename, remove, or modify it.
- **Word order can change freely.** If your language puts the number after the word, move the placeholder to match.
- **Plural forms vary by language.** If the original uses `item|items|items`, your language might need different forms. Ask a developer if you're unsure — getting plural forms wrong is exactly what this tool helps catch.
- **Test edge cases.** Try `0`, `1`, and larger numbers like `12` for any numeric parameter. These often trigger different wording.
- **Some languages require more plural forms.** Plural forms are separated by `|` characters in the format string. Test the translation by adjusting the parameters and adding or removing plural forms as needed.

---

## Powered by SmartFormat

[SmartFormat.NET](https://github.com/axuno/SmartFormat) — for more information about the different formatting rules, check out the project's Wiki page. What you see in the preview is exactly what users will see in the app.