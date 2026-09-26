# Prompt Patterns

Project Rehydrate is intentionally model-neutral. These prompts are examples, not required syntax.

## REHYDRATE prompt

Use when starting a new AI session or after a significant interruption.

```text
REHYDRATE

Read the canonical master context first.
Identify the active workstream.
Read the routed domain state.
Reconcile those files with the current conversation.
Report:
1. project identity
2. active workstream
3. last verified milestone
4. current safe state
5. unresolved items
6. exact next safe action
7. explicit risk boundary

Do not guess missing history.
If canonical state is stale or contradictory, stop and surface the conflict.
```

## STATUS prompt

```text
STATUS

Give a concise continuity status with:
- active workstream
- last verified milestone
- current safe state
- unresolved items
- exact next action
- continuity risk
```

## CHECKPOINT prompt

```text
CHECKPOINT

Persist the current verified milestone to canonical context.
Back up before mutation.
Write in small logical chunks.
Verify each write by reading it back.
Explicitly supersede stale directions.
Verify key markers.
Record the exact next action.
Hash the final canonical files after semantic verification.
```

## Conservative recovery prompt

Use when you suspect context drift.

```text
Continuity may be stale.
Do not continue implementation yet.
Read canonical context and identify contradictions between:
- current verified evidence
- domain state
- master routing
- current chat
- remembered history

Return only:
- confirmed facts
- conflicts
- unknowns
- safest next read-only action
```

## Handoff prompt

Use when another person or assistant will take over.

```text
Prepare a handoff from canonical state, not memory.
Include:
- project purpose
- current workstream
- last verified milestone
- current safe state
- unresolved questions
- risk boundary
- exact next action
- files the next operator must read first

Keep historical detail in linked domain files instead of duplicating it all here.
```

## Prompt design rule

A continuity prompt should ask for state recovery, not confidence.

Bad:

 > You remember where we were, right? Continue.

Better:

 > Rehydrate from canonical state. If anything is missing, say what evidence is required before continuing.