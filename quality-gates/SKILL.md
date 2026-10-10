---
name: quality-gates
description: Applies binary quality gates at each factory stage, defining pass/fail criteria, rework loops, escalation to a human owner, and the enforcement tiers that decide which rules may block. Use when a stage must be judged, when a gate result is being recorded, or when a rule's blocking authority is unclear. Not for writing the code being gated.
---

# Quality Gates

## Purpose

Make a stage's completion a binary decision, not a judgment call (P1, P8). Gates are the only forward motion in a factory: a failed gate returns to rework, and after the budget it escalates to a human. Enforcement tiers decide which rules have blocking power.

## Practices

1. **Declare each gate's criteria** before the stage runs: what pass looks like, checkable.
2. **Classify each rule by tier:**
   - **advisory** — reported, never blocks
   - **structural** — shapes the process, does not block a merge
   - **gating** — may block a stage
   - **mechanical** — automatic, always blocks on fail
3. **Evaluate.** All gating and mechanical criteria must pass. Advisory notes attach to the packet without blocking.
4. **On fail**, route backward to rework at that stage.
5. **After 3 rework cycles**, escalate to the named human owner with the evidence.

## Enforcement Note

Tier: **gating/mechanical** — this is the skill that decides whether anything may block. Only rules tagged gating or mechanical may block; advisory and structural rules may not. An agent that silently promotes an advisory rule to blocking has broken the tier contract.

## Constraints

- Gates are binary: pass or fail. No "mostly pass".
- Never skip a gate forward; a waiver is an ADR via `decision-record`, recorded on disk.
- Rework budget is 3 by default; per-project config may change it, and the change is itself recorded.
- Escalation goes to a named human, not to "the team".

## Verification

- [ ] Each stage's gate criteria were declared before the stage.
- [ ] Each rule has a declared tier.
- [ ] No advisory/structural rule blocked a stage.
- [ ] Failed gates reran the stage, budget honored.
- [ ] Escalation after budget 3 reached a named human.

## Dependencies

- `tdd`, `code-review` — produce the check outputs a gate evaluates.
- `decision-record` — records waivers and tier changes.
- `pipeline` — records gate results in evidence packets.
- `factory-review` — audits that tiers were honored.
