# Adoption Guide

Project Rehydrate works best when introduced gradually.

## Start small

Do not begin by documenting your entire estate.

Choose one long-running workstream that already suffers from continuity problems.

Examples:

- a data migration;
- an infrastructure rebuild;
- a security hardening programme;
- a reporting platform;
- a software refactor;
- an incident investigation;
- an AI-assisted research project.

Create only two files at first:

```text
00_Master_Context/README_FIRST.md
01_Main_Workstream/CURRENT_STATE.md
```

## First week

Use the protocol only at natural milestones.

Recommended triggers:

- start of a new AI conversation;
- end of a work session;
- major decision change;
- before a risky change;
- after proving something important.

Do not checkpoint every minor observation. Excessive checkpointing turns continuity into bureaucracy.

## What to measure

After several sessions, ask:

- Did a new session resume without repeating discovery work?
- Did we avoid following a stale next action?
- Could another person understand the safe state?
- Did the checkpoint expose unresolved assumptions?
- Did we know what not to touch?
- Was the next step small enough to execute confidently?

## Team use

For teams, agree on:

- the canonical root location;
- who may edit canonical state;
- naming conventions;
- checkpoint review expectations;
- whether hashes are required;
- how sensitive data is handled;
- when a domain file should be split.

## Avoid premature automation

The protocol should first become understandable manually.

Automating a bad continuity process only makes bad state propagate faster.

Automate only after the team can explain:

- what is canonical;
- what is evidence;
- what requires human approval;
- what makes a checkpoint valid;
- how stale state is detected.

## Migration from ad-hoc notes

If you already have scattered notes, do not copy everything into the new structure.

Instead:

1. identify the current active workstream;
2. capture the last verified milestone;
3. capture the current safe state;
4. capture unresolved items;
5. capture the exact next action;
6. route older material as references only.

Continuity quality matters more than historical completeness.