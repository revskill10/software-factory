---
name: code-review
description: Performs a findings-first code review that reads the repo's own contracts before judging changes, then emits severity-ordered findings each with file, line, impact, and the smallest fix. Use when a diff or merge request needs review or when a gate produced a rework cycle. Not for approving work, for the author's self-review, or when there is no diff to review.
---

# Findings-First Code Review

## Purpose

Review by evidence, not by impression (P5). Read the repository's contracts first, then walk the diff for defects, and report findings in the order that matters to risk. No-findings is a valid result but must state residual risk; it is not a rubber stamp.

## Practices

1. **Read the contracts.** `AGENTS.md`, `DESIGN.md`, specs, and decision records before looking at the diff — what this repo considers "right" varies.
2. **Walk the diff.** Findings ordered by severity:
   1. correctness
   2. security and permission boundaries
   3. missing tests
   4. stale or missing documentation
   5. broken architecture boundaries
   6. hidden prompt-only enforcement (rules that exist only in prose, not in the tooling)
   7. UI regressions where applicable
4. **For each finding:** file + line, the impact, and the smallest fix.
5. **No findings:** state the residual risk and what was checked.

## Enforcement Note

Tier: **gating** when run as a gate, **structural** otherwise. Only the reviewer role may run this; the author does not self-review. Every valid finding becomes an artifact — a code fix, a test, a doc update, or a new or updated skill-rule — tracked to closure.

## Constraints

- Findings are specific: a named location, not "code could be cleaner".
- Do not approve — the reviewer reports; the gate and human owner decide.
- Do not invent findings to fill a quota.
- Do not waive a finding without a recorded ADR.

## Verification

- [ ] Repo contracts read before the diff.
- [ ] Findings are severity-ordered, each with file+line, impact, and smallest fix.
- [ ] No-findings states residual risk and coverage.
- [ ] Every accepted finding has a tracked remediation.
- [ ] Author did not self-review.

## Dependencies

- `quality-gates` — decides pass/fail from the findings.
- `tdd` — supplies the "missing tests" finding class.
- `decision-record` — records a finding waived by exception.
- `pipeline` — collects the review into the phase's evidence packet.
