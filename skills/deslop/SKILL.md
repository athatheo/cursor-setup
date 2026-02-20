---
name: deslop
description: Remove AI-generated code slop and clean up code style. Use when the user asks to deslop, clean up AI-generated code, remove unnecessary comments, simplify defensive patterns, or fix style inconsistencies introduced by AI.
---

# Remove AI Code Slop

Check the diff against `main` and remove AI-generated slop introduced in the branch.

## Workflow

1. Run `git diff main...HEAD` to identify all changes on the branch.
2. For each changed file, read the surrounding code to understand local style.
3. Remove slop patterns (see Focus Areas below).
4. Verify behavior is unchanged after each edit.
5. Summarize what was cleaned up (1-3 sentences).

## Focus Areas

- **Unnecessary comments**: Remove comments that restate the code, explain obvious logic, or are inconsistent with the local commenting style.
- **Defensive overkill**: Remove try/catch blocks, null checks, or guard clauses that are abnormal for trusted internal code paths.
- **`any` casts**: Remove casts to `any` (or equivalent) used only to bypass type issues. Fix the actual type instead.
- **Deep nesting**: Flatten deeply nested conditionals with early returns or guard clauses.
- **Style drift**: Fix patterns that are inconsistent with the file and surrounding codebase (naming, formatting, structure).

## Guardrails

- Keep behavior unchanged unless fixing a clear bug.
- Prefer minimal, focused edits over broad rewrites.
- Do not introduce new abstractions or refactor beyond slop removal.
- When uncertain whether something is slop, leave it alone.
