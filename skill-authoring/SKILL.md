---
name: skill-authoring
description: Authors and ships a SKILL.md in the factory format — compliant frontmatter, progressive-disclosure body, and a verified shipping checklist. Use when creating or editing any skill in a pack, or when a skill fails discovery because its description is vague. Not for authoring user code; that is the tdd and code-review skills.
---

# Skill Authoring

## Purpose

Define the anatomy every factory skill follows (P9, L6) and give it a checklist so that a shipped skill is discoverable and coherent, not just a file.

## Practices

1. **Frontmatter.**
   - `name` — lowercase, hyphens only, 64 characters or fewer.
   - `description` — third person; states what the skill does, when to use it, and what it is *not* for. 1024 characters or fewer. The description is what discovery matches on; write it to be found.
2. **Body, in order.** Purpose, Practices, Enforcement Note, Constraints, Verification (a checklist), Dependencies.
3. **Progressive disclosure.** Body under 500 lines. If it would exceed that, move the overflow to a `reference/` file one level deep and link to it.
4. **Scripts.** A skill that needs to run code should reference the script path and describe how to call it, not inline the source.
5. **Cross-reference.** Name the skills this one depends on or is depended on, using the shared pack vocabulary.

## Enforcement Note

Tier: **structural**. Authoring rules shape the pack; `factory-review` runs them as a gate when shipping.

## Constraints

- No skill body above the 500-line budget without an explicit `reference/` split.
- No description without negative scope — "not for" is what stops a skill being selected for the wrong task.
- No inline scripts; reference them.
- One skill, one layer. A skill that spans layers is two skills.

## Verification

- [ ] Frontmatter `name` and `description` pass the format rules.
- [ ] Body is under 500 lines.
- [ ] All six body sections are present.
- [ ] References, if any, are one level deep.
- [ ] Cross-references resolve.
- [ ] `factory-review` returns no frontmatter or structure findings.

## Dependencies

- `factory-review` — audits this skill's output.
- `quality-gates` — gates a pack that fails the authoring checks.
