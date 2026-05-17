# Licensing

This project uses two licenses depending on the type of content. This file is the canonical reference for what is covered by what.

## Quick reference

| Directory / file type | License | What you can do |
|----------------------|---------|----------------|
| `data/` (CSV, YAML, JSON) | Apache License 2.0 | Reuse in commercial products. Include attribution. Patent grant included. |
| `project/` (when populated — Python code, configs, scripts) | Apache License 2.0 | Reuse in commercial products. Include attribution. Patent grant included. |
| `scripts/` (build and render utilities) | Apache License 2.0 | Reuse in commercial products. Include attribution. |
| `.github/`, `docker-compose.yml`, dotfiles | Apache License 2.0 | Reuse freely. |
| `docs/` (Markdown documentation) | CC BY-SA 4.0 | Reuse with attribution. **Derivative works must share-alike.** |
| `site/` (Astro site source — when published) | CC BY-SA 4.0 for content, Apache 2.0 for build code | See below |
| `README.md`, `STATUS.md`, `CHANGELOG.md`, `WHAT_THIS_IS_NOT.md`, `CONTRIBUTING.md`, this file | CC BY-SA 4.0 | Reuse with attribution. Derivatives must share-alike. |

## Why two licenses?

**Apache 2.0 for code and structured data.** This is the most permissive license that still includes an explicit patent grant. It is the license enterprises are most comfortable adopting code under. The controls catalog is structured data designed to be ingested into other systems (GRC tools, compliance pipelines, documentation generators), so it gets the same treatment as code.

**CC BY-SA 4.0 for prose.** Creative Commons licenses are designed for written works. The share-alike clause matters here: if you translate this documentation into French, German, or Spanish — or extend it with additional commentary — the derivative work must also be openly licensed. This protects the documentation ecosystem from being absorbed into closed-source compliance products.

## Practical examples

### "I want to use the controls catalog in my company's GRC tool."

Apache 2.0 covers this. You can import `data/controls.csv`, integrate it into your tooling, modify it, and ship it as part of a commercial product. Include the Apache 2.0 license text and attribution to this project.

### "I want to translate the documentation into French and host it on my website."

CC BY-SA 4.0 covers this. You can translate the docs and republish them. Two requirements: (1) attribute the original (link back to this project) and (2) license your translation under CC BY-SA 4.0 as well — you cannot make it proprietary.

### "I want to include this project's threat model in a consulting deliverable I am selling to a client."

For the threat model text (`docs/02-architecture/threat-model.md`): CC BY-SA 4.0 applies. You can include it in your deliverable. You must attribute the source. Your deliverable, to the extent it incorporates this content, must also be available under CC BY-SA 4.0 — or you must reframe the content substantially enough that it constitutes original work.

For the controls catalog you might reference alongside it: Apache 2.0 applies. No share-alike requirement on your deliverable, but attribution is still required.

### "I want to extract individual control rows for a slide deck."

Either license permits this for short excerpts (fair use / fair dealing applies in most jurisdictions). Attribution is good practice. For substantial extraction, follow the license that covers the source file.

### "I want to use this for internal training within my company."

Both licenses permit this freely. No external distribution = no public license obligations triggered. Attribution is still encouraged.

## Files outside this scheme

Two categories of file are not covered by either license:

- **References to external standards** (ISO 42001 clause numbers, NIST AI RMF subcategories, etc.) — these belong to their respective standards bodies. This project references them under fair use for the purpose of mapping, but does not republish their text.
- **External logos or branding** — none should appear in this repo. If they do, file an issue.

## License files

The full text of each license is in the repository:

- `LICENSE` — Apache License 2.0 (default for code and data)
- `LICENSE-docs.txt` — CC BY-SA 4.0 (for documentation)

If `LICENSE-docs.txt` has not been added yet, the canonical text is at: https://creativecommons.org/licenses/by-sa/4.0/legalcode

## Attribution

If you reuse content from this project, please attribute as:

> Manzambi, J. (2026). *EU AI Act Blueprint*. https://github.com/josephManzambi/eu-ai-act-blueprint

This attribution is sufficient under both licenses.
