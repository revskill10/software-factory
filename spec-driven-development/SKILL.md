---
name: spec-driven-development
description: Drives feature work through a fixed five-stage lifecycle (requirements, design, tasks, implement, verify) where every stage closes on a binary quality gate. Use when starting non-trivial feature work or when scope drift, skipped tests, or undocumented decisions appear. Not for one-line fixes, style-only edits, or work already past the implement stage.
---

# Spec-Driven Development

## Purpose

Turn an ambiguous request into a machine-checkable spec, then implement against it with a gate at every stage. Gate failure routes backward to rework — never forward. This is the L1 spec layer; it feeds `pipeline`, which orchestrates the stages.

## Practices

1. **Requirements.** Write what is in scope, out of scope, and the acceptance criteria as checkable statements. Negative scope is mandatory (what this will *not* do).
2. **Design.** Record the approach and the decisions it forces. Any decision with lasting consequence goes to `decision-record` (ADR), not into prose.
3. **Tasks.** Break the design into ordered, individually verifiable tasks. Each task names its own check.
4. **Implement.** Run tasks under `tdd` (failing test first). Evidence is written to disk as you go.
5. **Verify.** Re-run every acceptance criterion as a binary check. All pass or the stage fails.

Artifacts live under `docs/specs/<feature>/`. Business context is a separate input — see `business-context`, do not bury it in spec prose.

## Enforcement Note

Tier: **gating**. The implement stage may not start until the tasks stage passes its gate. A failing gate returns to that stage's rework loop (budget 3 cycles), then escalates to the human owner. Skipping a gate forward is a defect, not a shortcut.

## Constraints

- Acceptance criteria must be binary: each is pass or fail, never "mostly".
- Every stage emits an evidence packet (see `pipeline`); no stage is "done" by assertion.
- One-line fixes use the fast-lane escape hatch — do not run five stages for a typo.
- Spec artifacts are append-only once a gate passes; edits reopen the gate.

## Verification

- [ ] Requirements state explicit negative scope.
- [ ] Every lasting design decision has an ADR reference.
- [ ] Each task is independently verifiable.
- [ ] All acceptance criteria are binary and currently pass.
- [ ] Evidence packets exist for each completed stage.

## Dependencies

- `business-context` — separate intake, run before requirements.
- `pipeline` — orchestrates stages and writes evidence packets.
- `tdd` — hard constraint during implement.
- `quality-gates` — gate semantics, rework budget, escalation.
- `decision-record` — ADR lifecycle for design decisions.
