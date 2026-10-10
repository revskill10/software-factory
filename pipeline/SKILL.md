---
name: pipeline
description: Runs a factory pipeline as a controller that executes phases, writes structured evidence packets to disk, and recovers from crash state without memory. Use when orchestrating multi-stage delivery or when a run must survive interruption. Not for writing implementation code, for single-shot edits, or when no phase evidence needs auditing.
---

# Pipeline Controller

## Purpose

Orchestrate the lifecycle without touching implementation (P2, ADR-003). The controller's product is a durable, ordered evidence trail; the workers' product is code. Separation keeps the gate judgment unbiased.

## Practices

1. **Declare phases.** Ordered stages — Product, Architecture, Engineering, Review, QA, Documentation, Release (P7) or the five spec stages. Each names a human owner.
2. **Execute in order.** A phase starts only when its predecessor emitted `CYCLE_COMPLETE`.
3. **Emit evidence packets.** On phase close, write a structured record to `.factory/audit-trail/<seq>-<phase>.json`: phase, gate result, artifacts, check outputs, timestamp.
4. **Recover from disk.** On resume, read `.factory/audit-trail/` to find the last completed phase. Never resume from model memory.
5. **Route failures.** A failed gate sends the run back to that phase (budget 3), then to the human owner.

Controller MAY read, plan, emit packets, and escalate.
Controller MUST-NOT write, edit, or refactor implementation code.

## Enforcement Note

Tier: **mechanical**. The MUST-NOT list above is a hard constraint `[H]`. A controller that edits code forfeits its authority to judge that code — role separation is load-bearing, not etiquette.

## Constraints

- Evidence packets are append-only; a corrected run appends a new sequence, never overwrites.
- Packet schema is fixed: `phase`, `status`, `gate`, `artifacts`, `checks`, `ts`.
- No phase is skipped forward, including after a human override — an override is itself recorded as a packet.
- Resume never guesses: if the trail is unreadable, halt and escalate rather than infer.

## Verification

- [ ] Every completed phase has a `CYCLE_COMPLETE` packet on disk.
- [ ] A cold resume reproduces phase state from `.factory/audit-trail/` alone.
- [ ] Controller made no implementation edits.
- [ ] Failed gates routed backward, then escalated after budget 3.
- [ ] Human override, if any, is recorded as an evidence packet.

## Dependencies

- `spec-driven-development` — defines the phases and their gates.
- `quality-gates` — gate semantics and rework budget.
- `ensemble-team` — worker roles that implement under the controller.
- `factory-review` — audits controller/worker separation.
