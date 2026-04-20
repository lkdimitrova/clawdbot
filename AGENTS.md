# Global Agent Rules

You are a coding agent spawned by **Sparky** (OpenClaw orchestrator) on behalf of Mira.

These are cross-repo defaults. The repo's own `AGENTS.md` appears above these and may override or extend them with repo-specific rules (branch targets, test commands, invariants).

## Test-Driven Development (Mandatory)

Every change follows TDD.

### RED → GREEN → REFACTOR
1. **RED** — Write a failing test first. Confirm it fails for the right reason.
2. **GREEN** — Write the minimum code to make the test pass.
3. **REFACTOR** — Clean up. Tests still pass.

### Rules
- **Never write production code without a failing test.**
- **One behavior per test.** If a test name has "and" in it, split it.
- **Run tests after every change.** Don't batch — the feedback loop IS the point.
- **Test failures mean the CODE is broken first.** A stale test is the LAST hypothesis. Dig into the code, trace the logic, find the real bug.
- **Cover edge cases.** Null/empty inputs, boundary values, error conditions, concurrent access.
- **Tests are documentation.** Name them so someone reading the test file understands the feature without reading the implementation.

### Common test runners
- **Python (pytest):** `pytest -v --tb=short`
- **TypeScript/JS (Vitest):** `npx vitest run`
- **TypeScript/JS (Jest):** `npx jest`
- **E2E (Playwright):** `npx playwright test` — only when explicitly requested; expensive.

If the repo uses a different runner, check `package.json` or `pyproject.toml`. Repo-level `AGENTS.md` may set specific commands.

### What counts as a test
- Unit tests for pure logic and utilities
- Integration tests for API endpoints and DB queries
- Component tests for UI components
- E2E only when explicitly requested

## Code Quality

- **Clean code.** Readable > clever. Short functions. Clear names.
- **No dead code.** No commented-out blocks, no unused imports.
- **Type everything.** TypeScript strict mode. Python type hints on public function signatures.
- **Handle errors meaningfully.** No bare `except:` or empty `catch {}`. Log or propagate.

## Git Discipline

- **Atomic commits.** One logical change per commit, tests pass.
- **Conventional commits.** `type(scope): description` — e.g. `feat(auth): add token refresh`, `fix(api): handle null project_id`, `test(tasks): cover empty sprint edge case`.
- **Commit after each GREEN step.** Don't accumulate massive diffs.
- **Push when done.** Open a PR against the repo's integration branch (enforced by the runtime `gh` wrapper — `--base main` is rejected).

## PR Description

Include:
1. **What** — one-sentence summary
2. **Why** — context / motivation
3. **How** — key implementation decisions
4. **Testing** — what tests were added or changed, how to verify

## Skills Library

A comprehensive skills library is available at `~/antigravity-awesome-skills/skills/`. Before starting work, check if a relevant skill exists:

```bash
ls ~/antigravity-awesome-skills/skills/ | grep -i <keyword>
```

If a matching skill exists, read its `SKILL.md` and follow its patterns. Common ones:
- `tdd-workflow` / `tdd-workflows-tdd-cycle` — TDD methodology
- `nextjs-best-practices` / `nextjs-app-router-patterns` — Next.js patterns
- `typescript-expert` — TypeScript patterns
- `python-testing-patterns` / `javascript-testing-patterns` — testing patterns
- `postgres-best-practices` — DB queries + schema
- `clean-code` — readability, naming, function design
- `github-actions-templates` — CI/CD workflows

## Don't

- Don't modify files outside your task scope.
- Don't install new dependencies without justification in the PR.
- Don't skip tests "to save time".
- Don't leave TODO comments — either do it or note it in the PR description.
- Don't hardcode secrets, URLs, or environment-specific values.
