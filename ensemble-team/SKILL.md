---
name: ensemble-team
description: Organizes delivery into a panel of role agents — PM, architect, developer, reviewer, QA, domain expert — with named presets sized to the task. Use when a feature needs cross-role review before ticket work or when one agent is both authoring and judging its own output. Not for trivial changes, solo fast-lane fixes, or replacing the human owner.
---

# Ensemble Team

## Purpose

Put distinct roles across the work so no single agent authors and approves the same change (P3, P7). Cross-review happens *before* ticket work begins, not after code exists. Each stage keeps a human owner — the panel informs them; it does not replace them.

## Practices

1. **Choose a preset.**
   - **Full** (~9): PM, architect, dev, reviewer, QA, domain expert + supporting; for high-risk or regulated work.
   - **Lean** (~5-6): PM/architect combined, dev, reviewer, QA; default for most features.
   - **Solo-plus** (~3): one implementer plus two reviewers; for contained changes.
2. **Research each expert.** In fresh roles, gather the role's actual concerns for *this* task — do not recite a memorized role list.
3. **Cross-review the plan** before ticket work. Reviewer and QA challenge the design while it is cheap to change.
4. **Hand off to tickets.** Only after panel agreement does work move to `spec-driven-development` tasks.

## Enforcement Note

Tier: **structural**. Panel cross-review is required before ticket work for non-trivial changes. It shapes the process but does not itself block a merge; blocking authority stays with `quality-gates`.

## Constraints

- No role both authors and approves the same artifact.
- The accountable human owner is named outside the panel.
- A panel round is bounded (roughly 5-50K tokens); escalate to the human rather than looping indefinitely.
- Roles are chosen per task; do not fill seats for the sake of a full preset.

## Verification

- [ ] Preset selected and justified by task risk.
- [ ] Each role's concerns are task-specific, not boilerplate.
- [ ] Cross-review of the plan completed before ticket work.
- [ ] No role authored and approved the same artifact.
- [ ] Human owner named and distinct from all agent roles.

## Dependencies

- `pipeline` — controller orchestrates panel phases.
- `spec-driven-development` — consumes the panel-agreed plan.
- `code-review` and `tdd` — reviewer and QA roles apply these.
- `quality-gates` — decides whether the panel's output passes.
