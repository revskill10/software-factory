---
name: tdd
description: Enforces test-first delivery through red-green-refactor, requiring a failing test to exist before any implementation change for the behavior under test. Use when implementing a task whose acceptance criteria are behavior-based, or when a change would otherwise ship without a test. Not for pure refactors with no behavior change, for docs-only work, or when a test cannot be written.
---

# TDD as Hard Constraint

## Purpose

Make the test the first evidence of any behavior, not an afterthought (P4). A failing test is the cheapest possible way to prove a change is needed and then prove it works. Tagged hard constraint `[H]` — it may not be waived by the agent, only by the named human owner recording an exception.

## Practices

1. **Red.** Write a test for the next behavior. It must fail before touching the implementation. A test that passes immediately is not proving anything — check what it actually asserts.
2. **Green.** Make it pass with the smallest implementation that does. Resist adding speculative code.
3. **Refactor.** Remove duplication and rename while the tests stay green.
4. **Repeat** one behavior at a time.

## Enforcement Note

Tier: **gating** `[H]`. The verification checklist is a binary gate: no green tests, no stage passes. The controller under `pipeline` reads this result from disk, not from a claim in the transcript.

## Constraints

- Failing test precedes the implementation change — same commit boundary is acceptable.
- No implementation without a named test, unless a human records a `// PROJ-ADR-NNN` exception via `decision-record`.
- Tests assert observable behavior, not internals; keep them stable across refactors.
- Do not delete or weaken a test to get green.

## Verification

- [ ] Each new behavior has a test written and observed failing first.
- [ ] All targeted tests are green.
- [ ] No test was deleted or weakened to pass.
- [ ] Refactor kept tests green.
- [ ] Any exception has a recorded ADR reference.

## Dependencies

- `code-review` — reviews test quality and coverage gaps.
- `quality-gates` — applies the binary gate to the verification checklist.
- `decision-record` — records any hard-constraint exception.
- `pipeline` — orchestrates the stage and collects packet results.
