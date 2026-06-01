## Why

The current reference guide script generates synthesized review instructions that can drift away from the source reference documents. The skill needs a stricter progressive-disclosure tool that helps agents navigate references and retrieve exact source sections without summarizing, rewriting, or inventing guidance.

## What Changes

- Replace generated `guide` behavior with explicit reference navigation commands.
- Add `nav`, `toc`, and `show` commands to locate candidate headings, inspect document tables of contents, and return raw Markdown sections.
- Reduce `reference_index.json` to stable reference ids and heading mappings.
- Update `SKILL.md` to use `nav -> toc -> show` and to treat returned reference text as writing criteria, not manuscript evidence.

## Capabilities

### New Capabilities

- `reference-navigation`: Provides index navigation and progressive raw-section disclosure for reference documents.

### Modified Capabilities

None.

## Impact

- Updates `paper-reviewer/scripts/reference_guide.py`.
- Updates `paper-reviewer/references/reference_index.json`.
- Updates `paper-reviewer/SKILL.md` reference usage instructions.
- No new dependencies.
