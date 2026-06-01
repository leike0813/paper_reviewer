## 1. OpenSpec

- [x] 1.1 Create `add-review-runtime` change.
- [x] 1.2 Add proposal, design, capability spec, and implementation tasks.

## 2. Runtime Script

- [x] 2.1 Implement `review_runtime.py init`.
- [x] 2.2 Implement `status`, `instructions`, `update`, `read`, and `export`.
- [x] 2.3 Validate required fields for `paper_profile`, `stage_summary`, `finding`, `decision`, and `open_question`.
- [x] 2.4 Upsert memory records by stable `record_id`.
- [x] 2.5 Block export when required confirmations are still pending.

## 3. Skill Instructions

- [x] 3.1 Document stages S0-S8 in `SKILL.md`.
- [x] 3.2 Document responsibilities among Agent, `reference_guide.py`, and `review_runtime.py`.
- [x] 3.3 Document memory rules and runtime command usage.

## 4. Verification

- [x] 4.1 Validate OpenSpec change.
- [x] 4.2 Run runtime init/status/instructions/update/read/export with a temporary sample manuscript.
- [x] 4.3 Verify invalid payloads fail.
- [x] 4.4 Verify export is blocked while confirmations remain.
- [x] 4.5 Compile scripts with `$HOME/.ar` uv runtime.
