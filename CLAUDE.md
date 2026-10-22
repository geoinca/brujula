# CLAUDE.md — brujula

## 1. Purpose
Analyze job offers and prepare applications (documents tailored to each offer).

## 2. Stack
- Python 3.12.0 (pyenv). Do not use the system Python (3.9.6).
- Dependencies: pip + venv (`.venv/`). uv is not used.
- Persistence: local SQLite in `data/` (not versioned).
- Quality: pytest, hypothesis, ruff (lint + format), mypy.

## 3. Structure
- `src/brujula/`: package code.
- `tests/`: tests mirroring the structure of `src/brujula/`.
- `data/`: local DB, ignored by git.

## 4. Conventions
- All code in English: identifiers and comments.
- PEP 8: snake_case (modules/functions), PascalCase (classes), UPPER_CASE (constants).
- Type hints are mandatory. Code must pass `ruff check`, `ruff format` and `mypy`.

## 5. Tests
- Files `tests/test_<module>.py`. Run with `python -m pytest`.
- Every behavior change includes or updates its test.
- A refactor that does not change behavior needs no new test, but existing tests must keep passing.

## 6. Working rules
- Commit only on the user's explicit order. Approving a diff does not authorize a commit.
- Do not expand scope: one phase at a time.
- Propose before executing and wait for the user's approval in each phase.
- Do not touch `.env*` or `data/`.

## 7. Safeguards
Safeguards are added here as new subsections (7.1, 7.2…), with date and reason.
Sections 1–6 are not modified to introduce them.
### 7.1 — Verify staged content before every commit
**Date:** 2026-10-22
**Reason:** A commit freezes what is in the staging area, not what is open in
the editor. On 2026-10-21 the staging area held an older version of a file
(added manually earlier) while the working tree held the intended one; a blind
commit would have recorded the wrong version. `git status` names *which* file
is staged but not *what* it contains.

**Rule:** Before every `git commit`, run `git diff --staged` and confirm the
staged content is exactly what should be recorded. If it is not, stop and fix
the staging before committing. `git status` alone is not sufficient.