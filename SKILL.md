---
name: alt-text-linter-skill
description: Audits and generates accessibility alt text for technical documentation based on WCAG standards and corporate style rules. Trigger when evaluating alt text, auditing Markdown image tags, or writing visual descriptions.
---

# Accessibility Alt Text & Visual Asset Validator

## Objective
Evaluate draft alt text against accessibility rules or generate compliant alt text for technical documentation visuals (screenshots, diagrams, logos, active buttons).

## Rules Engine

### 1. Tag Existence, Placeholders & Contextual Specificity
- **Missing Alt Attribute:** Every image tag must have an `alt` attribute. Missing tags break screen reader navigation.
- **Banned Placeholders & File Names:** Never use placeholder text (`"TODO"`, `"TBD"`, `"placeholder"`) or raw file names (`"screen1.png"`, `"diagram.svg"`).
- **Contextual Purpose over Generic Labels:** Never describe an image by merely stating what generic element it is without explaining its purpose or outcome in the context of the document.
  - **Failing (No Context):** `alt="A screenshot of a dialog box."`
  - **Passing (Tutorial Context):** `alt="A screenshot displaying the message your end-user receives on their device after a successful send."`
  - **Passing (Procedural Diagram Context):** `alt="A diagram comparing a successful SMS Verify notification flow with an unsuccessful attempt."`

### 2. Length Budgets
- **Hard Upper Limit (125 Characters):** Alt text must not exceed 125 characters. If more detail is required, move the explanation to a text caption or body paragraph and summarize the key takeaway in the alt text.
- **Minimum Context Limit (10 Characters):** Descriptive alt text for screenshots and diagrams must be at least 10 characters long.
- **Minimum Length Exceptions:** The 10-character lower limit does **NOT** apply to decorative images (`alt=""`), brand logos (`alt="Vero Finto"`), or functional action labels (e.g., `alt="Close"`, `alt="Submit"`).

  ### 3. Asset Type, Prefixes, and Hybrids
- **Allowed Prefixes:** Start descriptions of technical assets with specific asset types: `"A screenshot of..."` or `"A diagram of..."`.
- **Banned Prefixes:** Never start alt text with `"An image of..."` or `"A photo of..."`.
- **Hybrid Visual Tie-Breaker:** For UI screenshots containing charts, flowcharts, or architecture diagrams:
  - Check the **Markdown heading or body paragraph text immediately preceding the image** in the source file to determine reader intent. Non-rendered annotations (HTML/Markdown comments, front-matter, code comments) do not count as context, since they don't inform what a reader actually sees on the page.
  - Use `"A screenshot of..."` if that preceding text guides the user through UI navigation or button clicks.
  - Use `"A diagram of..."` if that preceding text explains data flow, metrics interpretation, or system architecture.
  - **Ambiguous Context Handling:** If no qualifying heading or paragraph indicates either reading, do not guess. Flag the tag as **NEEDS CONTEXT** and prompt the author to confirm which reading applies, rather than defaulting to either prefix.

### 4. Grammar
- **Punctuation:** Always use standard capitalization and end with a period or terminal punctuation.
- **Tone:** Plain English, no unexplained acronyms or industry jargon. No file names, copyright notices, or author attributions.

### 5. Special Asset Types and Functional Precedence
- **Decorative Images:** Use an explicit empty string (`alt=""`) with no spaces so screen readers skip non-functional visual elements.
- **Photographs (Banned):** Standalone photographs or stock photos are excluded from technical documentation. If a photo is detected, flag it for removal or query if it can be replaced with a screenshot or architecture diagram.
- **Active / Functional Images (Buttons, Links):** Describe the target action rather than the visual (e.g., `"Download PDF"`, `"Contact Support"`, `"Close"`).
- **Linked / Interactive Logos (Absolute Precedence):** If any logo—primary header or repeated footer—is wrapped in an active link (`<a>`), interactive action trumps identity and decorative exemptions. The alt text **must** describe the link destination (e.g., `alt="Vero Finto homepage"`).
- **Static Logos:** Use `alt="Vero Finto"` for primary header identification; use `alt=""` for repeated decorative static logos.
- **Text in Screenshots/Diagrams:** Do not dump all UI text. Summarize the *purpose* or *key outcome* of the visual (e.g., `"A screenshot displaying the confirmation message after a successful send"`).

## Output Format

When auditing existing Markdown or HTML image tags, return a structured linter output:

```markdown
### Alt Text Audit Result

- **Original Tag:** `<img src="headshot.jpg" alt="Photo of team founder at a desk">`
- **Status:** ACTION REQUIRED
- **Violations:**
  - Rule 5: Photographs are disallowed in developer documentation.
  - Rule 3: Uses banned prefix "Photo of".
- **Suggested Action:** Remove image or replace with an architecture diagram or UI screenshot.
```
