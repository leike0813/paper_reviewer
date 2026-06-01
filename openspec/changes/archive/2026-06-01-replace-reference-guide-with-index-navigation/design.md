## Context

The reference files are large, but their heading structure is stable. The script should not compress or reorganize their content. Its role is to expose just enough index information for the agent to decide which exact original section to read.

## Goals / Non-Goals

**Goals:**

- Preserve source wording when content is returned.
- Support navigation by domain, review stage, and paper section.
- Support document-level table of contents inspection.
- Support exact heading extraction with child headings included.

**Non-Goals:**

- Do not generate review instructions.
- Do not summarize, paraphrase, or merge reference content.
- Do not infer manuscript findings.

## Decisions

- Use `ref_id` as the public reference identifier.
  - Rationale: agents should not need to remember long file names.

- Use `show --heading <exact-heading>` for raw section extraction.
  - Rationale: exact headings avoid fuzzy matching surprises and keep output traceable.

- Keep `guide` as a deprecated compatibility command.
  - Rationale: existing instructions may still call it, but it must no longer generate guidance.

## Risks / Trade-offs

- Exact heading matching can be strict -> mitigated by `toc` and clear error candidates.
- Returning full child content can be longer than expected -> mitigated by requiring explicit `show`.
- Duplicate heading text can be ambiguous -> mitigated by failing with candidate line numbers.
