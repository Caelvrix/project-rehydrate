# Maturity Model

Project Rehydrate can be adopted progressively.

## Level 0 — Chat-dependent

Characteristics:

- project state lives mainly in conversation;
- handoffs are ad-hoc;
- next actions are remembered rather than recorded.

Primary risk: reconstruction.

## Level 1 — External notes

Characteristics:

- one external context file exists;
- milestones and next steps are written down;
- no consistent structure yet.

Primary improvement: state survives the chat.

## Level 2 — Structured continuity

Characteristics:

- README_FIRST routing exists;
- domain files exist;
- REHYDRATE / STATUS / CHECKPOINT are used consistently;
- safe state and next action are explicit.

Primary improvement: repeatable handoff.

## Level 3 — Verified continuity

Characteristics:

- backup before mutation;
- small checkpoint chunks;
- read-back verification;
- marker checks;
- hashes after verification;
- stale directions explicitly superseded.

Primary improvement: continuity becomes auditable.

## Level 4 — Recoverable continuity

Characteristics:

- contradiction handling is documented;
- incomplete checkpoint recovery is tested;
- stale context is detected deliberately;
- another operator can recover without the original author.

Primary improvement: resilience.

## Level 5 — Assisted continuity

Characteristics:

- safe parts are automated;
- context linting and integrity checks exist;
- automation cannot silently promote unverified assumptions to canonical truth;
- humans retain authority over risky state changes.

Primary improvement: scale without losing control.

## Do not rush maturity

Higher maturity is not automatically better.

A solo developer may need only Level 2 or 3.

A regulated or high-risk engineering programme may benefit from Level 4 or 5.

The protocol should reduce cognitive load, not create compliance theater.