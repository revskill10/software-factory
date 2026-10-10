---
name: business-context
description: Captures the business context surrounding a build — stakeholders, constraints, success measures, and domain terms — as an input separate from the specification itself. Use when kickoff begins or when domain rationale is missing from a spec. Not for code style, architecture decisions already covered by an ADR, or spec acceptance criteria.
---

# Business Context Intake

## Purpose

Hold the *why* behind a build apart from the *what*. A spec states acceptance criteria; business context states who is affected, what constraints bind, and what success measures. Keeping them separate (P10) prevents prose bloat and lets either evolve independently. Feeds `spec-driven-development`.

## Practices

1. **Stakeholders.** Who requests, who uses, who is accountable at the gate.
2. **Constraints.** Budget, deadline, compliance, platform, and performance limits — each stated as a bound, not an aspiration.
3. **Success measures.** How the business knows this worked, distinct from the spec's binary acceptance criteria.
4. **Domain terms.** A short glossary so reviewers and specs share vocabulary.
5. **Out of scope.** Business-level exclusions, separate from the spec's technical negative scope.

Store under `docs/specs/<feature>/business-context.md`.

## Enforcement Note

Tier: **advisory**. Missing context degrades spec quality but does not block a stage. Escalate to the human owner when a constraint is discovered late enough to invalidate an accepted spec.

## Constraints

- One document per feature, updated by append — accepted context is not rewritten silently.
- Each constraint names its source (who imposed it), so it can be renegotiated.
- Success measures are business outcomes, not test assertions.
- Do not duplicate spec acceptance criteria here.

## Verification

- [ ] Stakeholders and the accountable human owner are named.
- [ ] Every constraint states a bound and a source.
- [ ] Success measures are business outcomes, not tests.
- [ ] Glossary covers domain terms used in the spec.
- [ ] Business-level out-of-scope is explicit.

## Dependencies

- `spec-driven-development` — consumes this as a separate input at requirements time.
- `factory-review` — audits that specs and context stayed separated.
