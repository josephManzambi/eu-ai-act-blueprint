# Contributing

Thanks for your interest in contributing to the EU AI Act Blueprint.

This project is in active early development (v0.1.x). The contributing guidelines below cover what's possible today; more detailed guidance will be added as the project matures.

## Ways to contribute

### Report issues

If you spot a typo, a broken link, an inconsistency between documents, or a factual error in the controls catalog or threat model, please [open an issue](https://github.com/josephManzambi/eu-ai-act-blueprint/issues/new). Include:

- Which file the issue is in (path or URL)
- What's wrong
- What you think the correct version should be, if you have a view

### Propose a new control or framework mapping

Read [`docs/03-controls/methodology.md`](docs/03-controls/methodology.md) first — especially §8 ("How to critique or extend the catalog"). The methodology lays out the productive forms of disagreement: split, merge, missing control, wrong mapping, scope wrong.

Open an issue describing the proposed change in those terms. Pull requests for catalog changes should:

- Update `data/controls.csv` (and validate against `data/controls-schema.json`)
- Add a row to `CHANGELOG.md`
- Reference the relevant article in the AI Act or amending regulation

### Propose a translation

The project is currently English-only. French translations are planned for Phase 6 (see [`STATUS.md`](STATUS.md)). If you want to translate documentation into French, Spanish, German, Italian, or any other language earlier, open an issue first to coordinate.

Translation conventions when they exist will be documented here.

### Improve the threat model

The threat model (`docs/02-architecture/threat-model.md`) covers STRIDE, ATLAS, and LINDDUN applied to the reference CV-screening system. Contributions welcome:

- Additional threat scenarios that map to existing controls
- Refinements to mitigation strategies
- New ATLAS techniques as the framework evolves

## Pull request checklist

Before submitting a PR:

- [ ] CI workflow passes locally (controls.csv schema validation)
- [ ] `CHANGELOG.md` has a new entry describing the change
- [ ] If you modified `controls.csv`, the row count matches the count in `README.md` and `docs/03-controls/methodology.md` §6.1
- [ ] If you modified dates, they are consistent with `data/timeline.yaml`
- [ ] If you added a new control, its `implementation_evidence` path either exists or is referenced in [`STATUS.md`](STATUS.md) as planned
- [ ] No personal information (real emails, internal URLs, customer names) appears in your changes

## Code of conduct

Be respectful and constructive. Disagreements about technical or interpretive choices are welcome; personal attacks are not. The methodology document deliberately invites critique — please make critique productive.

## License

By contributing, you agree that your contributions will be licensed under the same terms as the project:

- Code, data, and configuration: Apache License 2.0
- Documentation prose: CC BY-SA 4.0

See [`LICENSING.md`](LICENSING.md) for details.

## Maintainer

[Joseph Manzambi](https://manzambi.com). This project is currently maintained by one person; response times to issues and PRs are best-effort. See [`WHAT_THIS_IS_NOT.md`](WHAT_THIS_IS_NOT.md) for honest expectations about maintenance.
