# Governance

Project Rehydrate is deliberately lightweight, but the protocol itself still needs disciplined change control.

## Principles

1. Real-world evidence beats elegance.
2. Failure cases are first-class documentation.
3. Breaking changes must be visible.
4. Examples must remain sanitized.
5. The protocol should stay usable without proprietary tooling.
6. Human-readable state is a core requirement.

## Change categories

### Editorial

Typos, clearer wording, formatting, examples that do not alter protocol behavior.

### Additive

New guidance, templates, failure modes, or optional patterns.

### Behavioral

Changes to the meaning of REHYDRATE, STATUS, CHECKPOINT, state hierarchy, safety boundaries, or canonical-state handling.

Behavioral changes should be called out explicitly in the changelog.

## Versioning

Until v1.0, releases may evolve quickly. Preview versions should favor learning over compatibility, but changes should still be documented.

After v1.0, semantic versioning is recommended for protocol changes.

## Decision standard

A proposed change should answer:

- What real continuity problem does this solve?
- What failure prompted it?
- Does it make the protocol easier or safer to use?
- Can it be explained without vendor-specific assumptions?
- Does it preserve human agency and verification?