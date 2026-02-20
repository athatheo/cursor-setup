---
name: run-precommit-hooks
description: Run pre-commit hooks after code changes to ensure code quality. Use proactively after writing, modifying, or deleting code files. Agent should fix failures and retry up to 3 times.
---

# Run Pre-commit Hooks

## When to Run

Run pre-commit hooks **immediately after** completing any of these actions:
- Creating new files
- Editing existing files
- Deleting files
- Any batch of related code changes

## Execution

Use the `pre-commit-runner` subagent:

```
Task tool with subagent_type="pre-commit-runner"
```

Or run directly:
```bash
pre-commit run --all-files
```

## Failure Handling

If hooks fail:
1. Review the error output
2. Fix the issues (most hooks auto-fix, just re-stage files)
3. Re-run hooks
4. **Maximum 3 retry attempts** - if still failing after 3 tries, report the issues to the user

## Common Fixes

| Hook | Auto-fixes? | Manual Fix |
|------|-------------|------------|
| trailing-whitespace | Yes | Re-run |
| end-of-file-fixer | Yes | Re-run |
| ruff | Yes (--fix) | Re-run |
| ruff-format | Yes | Re-run |
| mypy | No | Fix type errors |

## Workflow

```
Code changes complete
       ↓
Run pre-commit hooks
       ↓
   Pass? → Done ✓
       ↓ No
   Fix issues
       ↓
   Retry < 3? → Re-run hooks
       ↓ No
Report to user with remaining errors
```
