# Quickstart

This is the smallest useful implementation of Project Rehydrate.

## 1. Create a canonical context root

```text
project-context/
├─ 00_Master_Context/
│  └─ README_FIRST.md
└─ 01_Main_Workstream/
   └─ CURRENT_STATE.md
```

## 2. Put routing in README_FIRST.md

The master file should answer:

- What is this project?
- What workstreams exist?
- Which workstream is active?
- What is the current safe state?
- What is the exact next action?
- Which detailed file contains authoritative domain truth?

Do not duplicate every technical detail into the master file. The master file routes. Domain files explain.

## 3. Use three commands consistently

### REHYDRATE

Use at the beginning of a new session or after a long interruption.

The assistant should:

1. read the master context first;
2. identify the active workstream;
3. read the routed domain state;
4. reconcile the canonical files with the current conversation;
5. state the current safe state;
6. identify unresolved items;
7. state the exact next safe action;
8. ask for missing evidence instead of guessing.

### STATUS

A useful STATUS response contains:

- active workstream;
- last verified milestone;
- current safe state;
- unresolved items;
- exact next action;
- continuity risk, if any.

### CHECKPOINT

Use after a meaningful milestone, before risky changes, or before changing chats.

A checkpoint should:

1. back up the canonical file;
2. append or update in small chunks;
3. verify each write;
4. check key markers;
5. compute a final file hash;
6. record the exact next action.

## 4. Record safe state, not just progress

Bad:

 > Worked on database ingestion. Need to continue tomorrow.

Good:

 > Source inspection complete. No production changes made. Incremental key validated against three historical windows. Next action: run a read-only duplicate-key check before creating merge logic.

The second statement is resumable.

## 5. Explicitly supersede old directions

When the plan changes, write:

 > This direction supersedes the earlier instruction to ...

Do not rely on chronology alone.

## 6. Keep context files boring

Canonical continuity files should favor plain Markdown, exact names, verified timestamps, clear decisions, unresolved questions, and reproducible commands where appropriate.

## 7. Rehydrate before changing anything important

If the task could alter infrastructure, code, data, security, or architecture, do not continue from memory alone. Rehydrate first.