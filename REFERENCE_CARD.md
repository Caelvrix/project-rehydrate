# Project Rehydrate Reference Card

Use this page when you already understand the protocol and need the short operational version.

## REHYDRATE

Use when starting a new chat, returning after a long pause, switching operators, or before risky technical work.

Expected output:

- project identity;
- active workstream;
- last verified milestone;
- current safe state;
- unresolved items;
- exact next safe action;
- explicit risk boundary.

Rule: **do not reconstruct missing history from memory when canonical state exists.**

## STATUS

Use when you need orientation without a full reload.

Recommended shape:

```text
Active workstream:
Last verified milestone:
Safe state:
Unresolved:
Next action:
Continuity risk:
```

## CHECKPOINT

Use after a meaningful milestone, before a risky mutation, before changing chats, or when context is becoming difficult to trust.

Sequence:

1. Back up canonical files.
2. Write one small logical chunk.
3. Read it back.
4. Repeat as needed.
5. Explicitly supersede stale directions.
6. Verify key markers.
7. Hash the final state.
8. Record the exact next action.

## State priority

When sources disagree:

1. current verified system evidence;
2. canonical domain state;
3. canonical master routing file;
4. current conversation;
5. assistant memory or old summaries.

## Good safe-state language

Prefer:

- confirmed;
- observed;
- reconciled;
- read-only inspection complete;
- not yet validated;
- blocked;
- intentionally disabled;
- production untouched;
- experimental only.

## Bad next actions

Avoid:

- continue setup;
- finish integration;
- resume migration;
- keep testing.

Prefer atomic actions:

- run a read-only duplicate-key query;
- inspect one configuration file;
- reconcile one source table;
- validate one relationship;
- confirm one backup hash.

## Stop conditions

Stop and rehydrate if:

- you cannot state what was last proven;
- two files disagree about the next action;
- a temporary artifact may be newer than canonical state;
- the assistant is filling gaps with assumptions;
- production scope is unclear;
- the operator says 'where were we?' and the answer depends on memory.