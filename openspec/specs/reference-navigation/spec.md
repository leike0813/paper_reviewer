# reference-navigation Specification

## Purpose
TBD - created by archiving change replace-reference-guide-with-index-navigation. Update Purpose after archive.
## Requirements
### Requirement: Reference identifiers and navigation

The script MUST expose stable reference ids and route domain/stage/section requests to candidate reference headings without generating review instructions.

#### Scenario: List identifiers

- **WHEN** an agent runs `reference_guide.py list`
- **THEN** the script lists domains, review stages, paper sections, and reference ids

#### Scenario: Navigate by route

- **WHEN** an agent runs `reference_guide.py nav --domain computational-algorithm-data-driven --review-stage macro --paper-section abstract`
- **THEN** the script returns candidate reference ids, paths, and exact headings only

### Requirement: Table of contents

The script MUST expose a table of contents for a chosen reference document.

#### Scenario: Show reference TOC

- **WHEN** an agent runs `reference_guide.py toc --ref computational-algorithm-data-driven`
- **THEN** the script returns the reference path and its Markdown headings with line numbers and levels

### Requirement: Raw heading disclosure

The script MUST return raw Markdown content for a requested heading without summarizing, rewriting, or restructuring it.

#### Scenario: Show raw section

- **WHEN** an agent runs `reference_guide.py show --ref computational-algorithm-data-driven --heading "5.2 摘要 Abstract"`
- **THEN** the script returns the original Markdown from that heading through its child headings and stops before the next same-level or higher-level heading

#### Scenario: Missing heading

- **WHEN** an agent requests a heading that does not exist
- **THEN** the script exits non-zero and returns a recoverable error with nearby heading candidates

#### Scenario: Duplicate heading

- **WHEN** an agent requests a heading text that appears more than once in the same reference
- **THEN** the script exits non-zero and returns all matching line numbers instead of guessing

### Requirement: Index validation

The script MUST validate every indexed reference file and heading.

#### Scenario: Check index

- **WHEN** an agent runs `reference_guide.py check`
- **THEN** the script verifies referenced files and headings exist and reports success only when the index is consistent

