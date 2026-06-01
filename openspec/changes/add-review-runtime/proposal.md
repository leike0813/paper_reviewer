## Why

The paper-reviewer skill has reference guidance, but it still lacks a recoverable execution model. A lightweight runtime is needed so long reviews can proceed stage by stage, keep finding-level memory, and resume without relying on conversation context alone.

## What Changes

- Add a JSON-workspace runtime for paper review runs.
- Add a single `review_runtime.py` entry point for initializing runs, checking status, getting stage instructions, writing memory records, reading summaries, and exporting review reports.
- Extend `SKILL.md` with execution stages, responsibilities, confirmation points, and runtime/memory rules.
- Keep `reference_guide.py` independent and default to no long reference reads.
- Do not add SQLite, external dependencies, PDF/Word parsing, or reference联网核验 in this change.

## Capabilities

### New Capabilities

- `review-runtime`: Provides a lightweight staged runtime and finding-level memory system for recoverable manuscript review.

### Modified Capabilities

None.

## Impact

- Adds `paper-reviewer/scripts/review_runtime.py`.
- Updates `paper-reviewer/SKILL.md` with runtime workflow and script responsibilities.
- Adds internal runtime artifacts under `.paper-reviewer-runs/<paper_key>/<run_id>/` when the script is used.
- Uses only Python standard library.
