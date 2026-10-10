---
name: decision-record
description: Manages the traceable decision chain — product decision, architecture decision record, code marker, and CI check — so any change can be traced from why to where to how. Use when a lasting design choice is made, when a gate waiver is recorded, or when a reviewer cannot tell why the code looks the way it does. Not for style choices that do not constrain future work.
---

# Decision Record

## Purpose

Make decisions durable and traceable (P6, G4). A decision that lives only in a conversation dies with it. The chain — PD to ADR to code marker to CI check — is what allows a future reviewer to understand and audit any change.

## Practices

1. **Product decision (PD).** The business-level choice, recorded with who made it and why.
2. **Architecture decision record (ADR).** Context, decision, and consequences, in a numbered file. States the trade-off accepted, not just the choice.
3. **Code marker.** Where the decision constrains code, add a `// PROJ-ADR-NNN` marker that references the ADR.
4. **CI check.** A zero-dependency check (e.g. `decisions.mjs`) confirms the marker exists and the ADR is present; it blocks on a missing link.
5. **Lane choice.** Minor decisions may bypass some gates; major decisions route through all of them. The lane is declared up front.

## Enforcement Note

Tier: **mechanical** for the CI check — a broken PD-ADR-marker chain fails the build. The ADR document itself is an artifact, not a gate; the chain that enforces it is.

## Constraints

- No decision with lasting consequence ships without a numbered ADR.
- An ADR is append-only once accepted; changes supersede it, they do not edit it.
- A waiver of a hard constraint is a recorded ADR, not a silent exception.
- The human who made the PD is named; agents accelerate, the person decides.

## Verification

- [ ] Every lasting decision has a numbered ADR.
- [ ] ADRs state context, decision, and accepted consequences.
- [ ] Code markers reference valid ADRs.
- [ ] The CI check passes on the current chain.
- [ ] Lane choice and waiver, if any, are recorded.

## Dependencies

- `quality-gates` — applies the mechanical tier to the chain check.
- `pipeline` — runs the check as a phase gate.
- `factory-review` — audits that decision markers resolve to real ADRs.
