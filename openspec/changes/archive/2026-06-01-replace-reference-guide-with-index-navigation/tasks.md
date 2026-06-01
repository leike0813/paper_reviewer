## 1. OpenSpec

- [x] 1.1 Create `replace-reference-guide-with-index-navigation` change.
- [x] 1.2 Add proposal, design, spec, and tasks.

## 2. Index

- [x] 2.1 Add stable `references` map with `ref_id`, labels, and paths.
- [x] 2.2 Remove instruction-generation fields from `reference_index.json`.
- [x] 2.3 Keep domain/stage/section heading mappings for navigation only.

## 3. Script

- [x] 3.1 Implement `list` with reference ids.
- [x] 3.2 Implement `nav`.
- [x] 3.3 Implement `toc`.
- [x] 3.4 Implement `show` raw heading extraction with child content.
- [x] 3.5 Deprecate `guide` without generating instructions.
- [x] 3.6 Keep `check` validation.

## 4. Skill Instructions

- [x] 4.1 Update `SKILL.md` reference discipline to `nav -> toc -> show`.
- [x] 4.2 Remove claims that `reference_guide.py` renders review instructions.

## 5. Verification

- [x] 5.1 Run OpenSpec validation.
- [x] 5.2 Run list/nav/toc/show/check.
- [x] 5.3 Verify show output excludes next same-level heading.
- [x] 5.4 Verify invalid ref and missing heading fail non-zero.
- [x] 5.5 Run py_compile.
