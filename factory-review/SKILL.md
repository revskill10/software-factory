---
name: factory-review
description: Audits a skill pack for authoring coherence — frontmatter quality, progressive disclosure, pack-level cross-references, and alignment with the six-layer architecture. Use before shipping a pack, when adding or changing a skill, or when a pack has drifted from its architecture. Not for reviewing feature code under test.
---

# Factory Review

## Purpose

The review skill aimed at the factory itself, not at user code. It catches the failure modes of bad skill authoring: vague descriptions, packs that do not reference each other, and skills that contradict the architecture they claim to implement.

## Practices

1. **Frontmatter check.** `name` is lowercase-hyphens, 64 characters or fewer; `description` is third-person, states what the skill does and when to use it, and includes negative scope, 1024 characters or fewer.
2. **Progressive disclosure.** Body under 500 lines; references one level deep; no embedded scripts.
3. **Pack coherence.** Every skill cross-references the skills it depends on, using the shared vocabulary (gate, evidence packet, tier, human owner).
4. **Architecture alignment.** Each skill maps to exactly one layer; check it does not encroach on another layer's role.
5. **Vocabulary consistency.** Shared terms used identically across the pack.

## Enforcement Note

Tier: **gating** when run as a gate before shipping; **structural** when run ad hoc. Findings here are defects in the pack, not in any user code.

## Constraints

- Do not approve — report findings to the pack's human owner.
- A finding must name the skill and line, state the defect, and suggest the smallest correction.
- Do not rewrite the pack in the review; produce a findings list.

## Verification

- [ ] Every skill's frontmatter passes the frontmatter check.
- [ ] No skill body exceeds the 500-line budget.
- [ ] Cross-references between skills resolve.
- [ ] Each skill maps to a single declared layer.
- [ ] Shared vocabulary is consistent.

## Dependencies

- `skill-authoring` — defines the anatomy being audited.
- `quality-gates` — decides the gate outcome for a pack that has findings.
- `pipeline` — records the review in an evidence packet.
