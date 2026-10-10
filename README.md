# Software Factory — Skill Packs

Version: 0.1.0 · Date: 2026-10-10 · Goal: goal-mv27ywej-ksk

Local skill packs implementing the six-layer architecture in `../software-factory.md`.
Each skill is a self-contained folder with a `SKILL.md` (YAML frontmatter + body under 500 lines).
Synthesized from 4 independent source families (deepkawal, jwilger, magnus919, artreimus);
patterns P1-P10 in `../reports/status/goal-mv27ywej-ksk-research-patterns.md`.

## Skills by layer

| Layer | Skill | Role |
|---|---|---|
| L1 Spec | `spec-driven-development` | five-stage lifecycle with binary gates |
| L1 Spec | `business-context` | business-context intake, separate from spec prose |
| L2 Orchestration | `pipeline` | controller, phases, evidence packets, crash recovery |
| L3 Role | `ensemble-team` | role panels and Full/Lean/Solo-plus presets |
| L4 Quality | `tdd` | red-green-refactor as hard constraint `[H]` |
| L4 Quality | `code-review` | findings-first severity-ordered review |
| L4 Quality | `quality-gates` | binary gates, rework budget, human escalation |
| L4 Quality | `factory-review` | audits a pack for authoring coherence |
| L5 Decision | `decision-record` | PD -> ADR -> code marker -> CI gate |
| L6 Authoring | `skill-authoring` | SKILL.md anatomy + shipping checklist |

## Shared vocabulary

- **Gate** — binary pass/fail at a stage. Fail routes backward to rework (budget 3 cycles), then human escalation. Never skips forward.
- **Evidence packet** — structured `CYCLE_COMPLETE` record written to `.factory/audit-trail/`. Durable on disk, never model memory.
- **Enforcement tier** — advisory -> structural -> gating -> mechanical. Only gating/mechanical tiers may block.
- **Human owner** — named person accountable at each declared gate. Agents accelerate; the person decides.

## Install

Copy a skill folder into your agent's skills directory, or:

```
npx skills add <repo> --skill <name>
```

## Usage order

`business-context` -> `spec-driven-development` -> `pipeline` (orchestrates) -> `ensemble-team` / `tdd` / `code-review` -> `quality-gates` -> `decision-record`. Run `factory-review` to audit a pack itself.
