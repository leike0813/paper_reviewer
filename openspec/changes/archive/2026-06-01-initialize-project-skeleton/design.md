## Context

The `paper-reviewer/references` directory contains more than twenty thousand lines of guidance across a general framework, taxonomy, and nine domain-specific writing guides. The skill needs those references, but loading them without routing creates unnecessary token use and increases the chance that irrelevant guidance pollutes the review context.

## Goals / Non-Goals

**Goals:**

- Keep `SKILL.md` concise while making reference use disciplined and repeatable.
- Render complete review-pass instructions by three explicit dimensions: manuscript domain, review stage, and paper section.
- Make the script output sufficient for ordinary review passes without opening long reference files.
- Validate that the index points to real reference files and headings.

**Non-Goals:**

- Do not parse or review user manuscripts in this change.
- Do not build a database, gate runtime, or persistent review memory.
- Do not automatically classify manuscripts with keyword heuristics.
- Do not generate summaries that replace the source reference guides.

## Decisions

- Use a lightweight instruction-rendering script instead of a gate runtime.
  - Rationale: the problem is controlling review guidance and context use, not multi-stage state management.
  - Alternative considered: a database-backed gate like `paper-condenser`; rejected as too heavy for a first infrastructure layer.

- Keep domain classification as an agent responsibility.
  - Rationale: domain classification is semantic and context-sensitive; a keyword script would be brittle.
  - Alternative considered: script-side keyword classification; rejected because false positives would route the agent to misleading guidance.

- Use `reference_index.json` as the routing truth source.
  - Rationale: the index is small, reviewable, and stores both routing metadata and executable review guidance.
  - Alternative considered: runtime heading parsing only; rejected because it would not encode review-stage or paper-section intent.

- Emit Markdown by default.
  - Rationale: the caller is an agent, and the output should be directly readable without another rendering step.
  - Alternative considered: JSON-only output; rejected because the user requested Markdown as the primary contract.

- Treat file and heading suggestions as optional fallback material.
  - Rationale: the goal is to reduce reference reading, so the primary output must be complete instructions rather than a pointer list.
  - Alternative considered: minimal reading pointers as the main output; rejected because it nudges agents to open more files.

## Risks / Trade-offs

- Index drift from source headings -> mitigated by `reference_guide.py check`, which verifies files and headings used by optional reading suggestions.
- Rendered instructions may be too sparse for unusual papers -> mitigated by a clearly marked optional reading section for concrete blockers only.
- Agents may still over-read references -> mitigated by making `SKILL.md` explicitly state that script output is the default instruction source and optional readings are not a next step.
- Markdown output is less machine-typed than JSON -> mitigated by keeping command identifiers validated and failure modes structured in the rendered message.
