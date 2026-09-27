# Alt text linter skill (`alt-text-validator-skill`)
![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)
![Made with VS Code](https://img.shields.io/badge/Made%20with-VS%20Code-blue?logo=visual-studio-code)

An AI-driven accessibility linter and specification designed for technical documentation repositories and docs-as-code workflows. Codified as a vendor-agnostic Agent Skill (`SKILL.md`), this tool enforces WCAG 2.1/2.2 Non-Text Content (1.1.1) compliance, character budgets, prefix conventions, and functional visual precedence across technical documentation assets.

---

## Quick start guide

### To test this linter:
1. Open an LLM workspace (such as Claude, ChatGPT, or Gemini).
2. Attach the `SKILL.md` file to a new chat window.
3. Copy and paste the text from `skill-prompt.md` into the chat window.
4. Review the structured linter audit report.

### To use this linter in production:

#### Option A: Local workspace integration (VS Code / Cursor / Claude Desktop)
1. Store the file in your repository at `.claude/skills/alt-text-validator/SKILL.md`.
2. Supported AI tools will automatically reference the rules when auditing Markdown image tags or writing image descriptions.

#### Option B: Claude projects / workspace knowledge
1. Create a workspace project (e.g., *Docs Accessibility Review*).
2. Upload `SKILL.md` into the **Project Knowledge** section.
3. Set the project system prompt: *"Enforce the accessibility rules defined in SKILL.md whenever reviewing or generating image alt text."*

#### Option C: CI/CD pipeline translation
Use the deterministic rule logic in `SKILL.md` to author static prose checks in tools like **Vale** or **Spectral** for automated PR checks.

---

## Key features and rule architecture

* **Contextual outcome validation:** Replaces generic labels ("A screenshot of a dialog box") with explicit, user-facing outcomes.
* **Bounded character budgets:** Enforces a 125-character cap and a 10-character floor, with built-in exemptions for action labels, brand logos, and decorative assets.
* **Hybrid asset tie-breaking:** Resolves UI vs. diagram ambiguities using preceding Markdown context while ignoring non-rendered comments or frontmatter.
* **Interactive element precedence:** Prioritizes link actions over static brand identity for clickable assets (e.g., active logos require navigation targets).
* **Tri-state verdict engine:** Returns explicit `PASS`, `ACTION REQUIRED`, or `NEEDS CONTEXT` audit outcomes to eliminate ambiguous AI inferences.

---

## Files in this repository

| File name | Purpose |
| :--- | :--- |
| **`SKILL.md`** | Core AI Agent Skill definition and rules engine. |
| **`README.md`** | Project overview and usage documentation. |
| **`skill-prompt.md`** | Final test prompt for skill. |
| **`LICENSE`** | CC BY-NC-ND 4.0 International License. |

---

## License

This repo and its assets are licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](https://creativecommons.org/licenses/by-nc-nd/4.0/).

You may share this work with attribution for non-commercial purposes, but you may not remix or reuse it in derivative works.