## Why

The paper-reviewer skill already has a large set of domain writing guides, but reading them directly and broadly would waste context and can pull the agent away from the review task. A lightweight reference guidance layer is needed so the agent can ask for the smallest relevant guidance before each review pass.

## What Changes

- Add a reference guidance capability that routes by paper domain, review stage, and paper section.
- Add a concise `paper-reviewer/SKILL.md` skeleton that makes the guidance script the required entry point for reference use.
- Add a standard-library Python script that lists valid routing identifiers, emits Markdown guidance, and validates the reference index.
- Add a small maintained `reference_index.json` that maps domains, review stages, and paper sections to the existing reference documents and headings.
- No external dependency, database, or gate runtime is introduced.

## Capabilities

### New Capabilities

- `reference-guidance`: Provides controlled, on-demand reference routing so agents do not blindly read the full `references/` directory.

### Modified Capabilities

None.

## Impact

- Affected skill package files: `paper-reviewer/SKILL.md`, `paper-reviewer/scripts/reference_guide.py`, and `paper-reviewer/references/reference_index.json`.
- Affected workflow: agents must classify the manuscript domain first, then call the guidance script before reading long reference documents.
- Dependencies: none beyond Python standard library.
