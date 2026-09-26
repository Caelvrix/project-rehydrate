# Project Rehydrate — 5 Minute Start

You do not need to adopt the full protocol to get value from it.

Start with two files and three commands.

## Step 1 — Create two files

```text
project-context/
├─ 00_Master_Context/
│  └─ README_FIRST.md
└─ 01_Main_Workstream/
   └─ CURRENT_STATE.md
```

## Step 2 — Put this in README_FIRST.md

```markdown
# Project Context

## Active workstream
01_Main_Workstream

## Current safe state
- Development only.
- Production untouched.
- Last verified test passed.

## Exact next action
Run one read-only validation before making changes.

## Do not do yet
- Do not change production.
- Do not enable automation.

## Route
Detailed state: ../01_Main_Workstream/CURRENT_STATE.md
```

## Step 3 — Put detail in CURRENT_STATE.md

```markdown
# Current State

## Last verified milestone
Describe what was actually proven.

## Current safe state
Describe what can safely be assumed now.

## Unresolved
List what is still unknown.

## Exact next action
Write one small, verifiable next action.

## Risk boundary
State what must not be changed yet.
```

## Step 4 — Use three commands

### REHYDRATE

At the start of a new AI session:

```text
REHYDRATE

Read README_FIRST.md first.
Then read the active workstream state.
Report:
- last verified milestone
- current safe state
- unresolved items
- exact next action
- risk boundary

Do not guess missing history.
```

### STATUS

When you need orientation:

```text
STATUS

Give me:
- active workstream
- last verified milestone
- safe state
- unresolved
- next action
- continuity risk
```

### CHECKPOINT

After a meaningful milestone:

```text
CHECKPOINT

Back up canonical files first.
Write the new milestone in small chunks.
Read each write back.
Explicitly supersede stale directions.
Verify key markers.
Hash the final files after semantic verification.
```

## Step 5 — Follow one rule

Do not record only **what you did**.

Record **where the project safely stands now**.

Bad:

> Worked on the migration. Continue tomorrow.

Better:

> Read-only source validation complete. No production changes made. Candidate key is still unproven. Next action: run duplicate-key analysis. Do not implement merge logic yet.

That is enough to start.

Everything else in Project Rehydrate adds resilience around this core.