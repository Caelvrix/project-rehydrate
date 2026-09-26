# Protocol

Project Rehydrate defines a small operating protocol for preserving continuity across long-running AI-assisted IT and technical work.

## Roles

### Human operator

The human remains the decision authority.

Responsibilities:

- verify critical facts;
- approve risky or destructive actions;
- identify when a checkpoint is needed;
- preserve secrets outside public context;
- correct stale or inaccurate canonical state.

### AI assistant

The assistant acts as a continuity-aware collaborator.

Responsibilities:

- prefer canonical state over conversational inference;
- avoid inventing missing history;
- distinguish verified state from assumptions;
- identify stale instructions;
- preserve exact next actions;
- surface contradictions before execution.

## State hierarchy

When sources disagree, use this priority order:

1. current verified system evidence;
2. canonical domain state;
3. canonical master routing file;
4. current conversation;
5. assistant memory or prior summaries.

A lower-priority source must not silently override a higher-priority source.

## REHYDRATE contract

A REHYDRATE operation should produce:

1. Project identity — what project is this?
2. Active workstream — which domain is currently in scope?
3. Last verified milestone — what was actually proven?
4. Current safe state — what can be asserted without speculation?
5. Unresolved items — what remains unknown, blocked, or contradictory?
6. Exact next action — what is the smallest safe next step?
7. Risk boundary — what must not be changed yet?

A rehydration is incomplete if it ends with a vague statement such as `continue implementation`.

## STATUS contract

STATUS should be short enough to scan quickly and should include active workstream, last verified milestone, safe state, unresolved items, exact next action, and continuity risk.

## CHECKPOINT contract

A checkpoint is not merely a summary. It is a persistence operation.

Minimum requirements:

- backup created before mutation;
- writes performed in small chunks;
- each chunk verified after write;
- stale next-actions explicitly superseded;
- key markers verified;
- final SHA256 or equivalent integrity hash recorded.

## Checkpoint frequency

Checkpoint when:

- a major architectural decision changes;
- a risky step has just been proven safe;
- a destructive step is about to begin;
- a workstream changes;
- the conversation is becoming very long;
- the operator is about to stop for the day;
- an investigation reaches a defensible conclusion;
- a temporary experiment becomes canonical.

Do not checkpoint every trivial message.

## Domain separation

A master context file should route to domain-specific state.

```text
00_Master_Context/README_FIRST.md
01_Data_Platform/CURRENT_STATE.md
02_Infrastructure/CURRENT_STATE.md
03_Security/CURRENT_STATE.md
04_Reporting/CURRENT_STATE.md
```

A single giant context file eventually becomes a dumping ground. Domain separation makes retrieval easier and reduces accidental cross-contamination.

## Safe-state language

Prefer evidence-based wording such as confirmed, observed, reconciled, read-only inspection complete, not yet validated, blocked, intentionally disabled, production untouched, and experimental only.

Avoid overstating certainty with words like fixed, complete, secure, production-ready, or proven unless the evidence actually supports them.

## Exact next action

The next action should be atomic.

Good:

 > Run a read-only query to confirm the candidate incremental key is unique over the last 30 days.

Bad:

 > Finish orchestration.

Atomic next actions reduce drift.