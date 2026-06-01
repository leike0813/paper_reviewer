# review-runtime Specification

## Purpose
TBD - created by archiving change add-review-runtime. Update Purpose after archive.
## Requirements
### Requirement: Runtime workspace initialization

The skill MUST provide a runtime script that initializes a review workspace for a UTF-8 manuscript source without modifying the source file.

#### Scenario: Initialize review run

- **WHEN** an agent runs `review_runtime.py init --source-path <path>` with an existing UTF-8 text file
- **THEN** the script creates `.paper-reviewer-runs/<paper_key>/<run_id>/manifest.json`, `memory.jsonl`, and `artifacts/`, then returns the run root

### Requirement: Stage status and blockers

The runtime MUST expose current stage, pending confirmations, memory statistics, and next action guidance.

#### Scenario: Initial status has confirmation blockers

- **WHEN** an agent checks status immediately after initialization
- **THEN** the runtime reports `S1_PROFILE_AND_SCOPE` with pending domain and scope confirmations

### Requirement: Stage instructions

The runtime MUST return complete stage instructions for each supported review stage.

#### Scenario: Request stage instructions

- **WHEN** an agent runs `review_runtime.py instructions --run-root <path> --stage S3_MACRO_REVIEW`
- **THEN** the script returns Markdown instructions describing responsibilities, required outputs, memory write expectations, and reference-guidance usage for that stage

### Requirement: Validated memory updates

The runtime MUST validate memory records before writing them.

#### Scenario: Reject invalid finding

- **WHEN** an agent attempts to write a `finding` record missing required fields or using an invalid severity
- **THEN** the script exits non-zero and does not write the invalid record

#### Scenario: Write valid finding

- **WHEN** an agent writes a valid `finding` record
- **THEN** the runtime upserts the record into `memory.jsonl` and includes it in later `read` summaries

### Requirement: Report export from memory

The runtime MUST render a review report artifact from structured memory only after required confirmations are cleared.

#### Scenario: Export blocked by pending confirmation

- **WHEN** report export is requested while pending confirmations remain
- **THEN** the script exits non-zero and does not create the report

#### Scenario: Export review report

- **WHEN** report export is requested after required confirmations are cleared and findings exist
- **THEN** the script writes `artifacts/review-report.md` using confirmed findings and retained candidate findings

