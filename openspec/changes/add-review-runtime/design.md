## Context

Paper review is multi-step and often longer than a single model context. The skill needs durable state, but a full database gate would be too heavy for this project at this stage. The current reference guidance layer already reduces reference-file reads; the next layer should track review progress and findings without replacing the agent's semantic work.

## Goals / Non-Goals

**Goals:**

- Use a lightweight JSON workspace with a manifest and JSONL memory.
- Track review stages, confirmation blockers, stage summaries, and finding-level records.
- Keep scripts deterministic: validate schemas, update state, summarize memory, and render report drafts.
- Keep the agent responsible for manuscript understanding, review judgement, severity, and final wording.

**Non-Goals:**

- Do not implement PDF/Word parsing.
- Do not implement联网 reference verification.
- Do not introduce SQLite or a strict next-action gate.
- Do not store long manuscript excerpts or long reference guide content in memory.

## Decisions

- Use `.paper-reviewer-runs/<paper_key>/<run_id>/` as the runtime root.
  - Rationale: it is easy to inspect, copy, and resume.
  - Alternative considered: a shared `.memory` file; rejected because run state and artifacts should be grouped.

- Use `manifest.json` for state and `memory.jsonl` for records.
  - Rationale: manifest is easy to overwrite atomically, while JSONL supports incremental review findings.
  - Alternative considered: SQLite; rejected as unnecessary for current complexity.

- Use key confirmation blockers only.
  - Rationale: domain/scope and final export decisions are high-impact; requiring confirmation after every stage would slow review without improving reliability.

- Use finding-level memory.
  - Rationale: final reports need traceable issues with location, evidence, impact, and suggested revision.

## Risks / Trade-offs

- JSONL can accumulate superseded records -> mitigated by upserting records by `record_id`.
- The runtime cannot judge whether findings are academically correct -> mitigated by keeping judgement with the agent and using schema validation only.
- Initial source support is UTF-8 text only -> mitigated by explicitly scoping complex parsing to future intake work.
