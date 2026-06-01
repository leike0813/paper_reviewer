## 1. OpenSpec Artifacts

- [x] 1.1 Create proposal for `reference-guidance`.
- [x] 1.2 Create design for the lightweight routing approach.
- [x] 1.3 Create capability spec for the guidance entry point and reading discipline.
- [x] 1.4 Create implementation task checklist.

## 2. Skill Package Skeleton

- [x] 2.1 Add `paper-reviewer/SKILL.md` with mission, non-goals, and reference reading discipline.
- [x] 2.2 Document the guidance script commands and when agents must call them.

## 3. Reference Guidance Implementation

- [x] 3.1 Add `paper-reviewer/references/reference_index.json` with domain, review-stage, and paper-section routing data.
- [x] 3.2 Add `paper-reviewer/scripts/reference_guide.py` with `list`, `guide`, and `check` commands.
- [x] 3.3 Make `guide` fail recoverably for missing or invalid identifiers.
- [x] 3.4 Expand `reference_index.json` with reusable instruction policy fields.
- [x] 3.5 Change `guide` output from pointer-first routing to complete review-pass instructions.
- [x] 3.6 Demote file and heading references to optional fallback suggestions only.

## 4. Verification

- [x] 4.1 Run index consistency validation.
- [x] 4.2 Run representative guide calls for computational, engineering, and medical routes.
- [x] 4.3 Run invalid input checks.
- [x] 4.4 Run `openspec validate initialize-project-skeleton`.
- [x] 4.5 Verify guide output no longer contains `Minimal reading pointers`.
