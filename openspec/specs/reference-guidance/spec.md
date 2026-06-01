# reference-guidance Specification

## Purpose
TBD - created by archiving change initialize-project-skeleton. Update Purpose after archive.
## Requirements
### Requirement: Reference guidance entry point

The skill MUST provide a single script entry point that lists valid routing identifiers, returns complete Markdown review instructions for a requested route, and validates the reference index.

#### Scenario: List available routing identifiers

- **WHEN** an agent runs the reference guidance script with the `list` command
- **THEN** the script returns the available domain, review-stage, and paper-section identifiers in Markdown

#### Scenario: Validate the reference index

- **WHEN** an agent runs the reference guidance script with the `check` command
- **THEN** the script verifies referenced files, referenced headings, and duplicate identifiers, then exits successfully only when the index is consistent

### Requirement: Complete guidance before reference reading

The skill MUST instruct agents to use the reference guidance script output as the default operating instructions for a review pass instead of reading long files under `paper-reviewer/references`.

#### Scenario: Agent prepares a focused review pass

- **WHEN** an agent has identified a manuscript domain, review stage, and paper section
- **THEN** the agent calls the `guide` command and receives task boundaries, checklists, judgement standards, output requirements, and prohibitions sufficient for ordinary review work

#### Scenario: Missing or invalid route

- **WHEN** an agent calls the `guide` command with a missing or invalid domain, review-stage, or paper-section identifier
- **THEN** the script returns a recoverable Markdown error with candidate identifiers and exits with a non-zero status

### Requirement: Optional reference suggestions

The guidance output MUST place file and heading references only in an optional reading section that explicitly says they are not the default next step.

#### Scenario: Valid guide request

- **WHEN** an agent requests guidance for a valid domain, review stage, and paper section
- **THEN** the script returns the current route, task boundary, six to twelve checks, judgement standards, output requirements, prohibitions, and optional reading suggestions marked as fallback-only

