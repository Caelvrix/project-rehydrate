# Project Rehydrate

**A continuity protocol for long-running AI-assisted engineering work.**

Project Rehydrate exists for a simple reason: long technical projects outlive individual chat sessions, browser tabs, model context windows, and human memory.

The protocol externalizes project state into a small set of canonical files so that an AI assistant and a human operator can reliably resume work without guessing what happened before.

## Why it exists

Long-running AI-assisted projects often fail in predictable ways:

- decisions are scattered across many conversations;
- stale instructions survive after the plan changes;
- the assistant loses the exact safe state of a system;
- temporary files diverge from the actual project state;
- later sessions re-discover decisions that were already made;
- large handoff summaries become difficult to audit;
- missing history gets reconstructed instead of reloaded;
- destructive work can resume from an incorrect assumption.

Project Rehydrate treats continuity as an engineering problem, not a memory feature.

## Core idea

Keep one canonical project context outside the conversation.

A minimal implementation looks like this:

```text
project-context/
├─ 00_Master_Context/
│  └─ README_FIRST.md
├─ 01_Domain_A/
│  └─ CURRENT_STATE.md
└─ 02_Domain_B/
   └─ CURRENT_STATE.md
```

The three operator commands are:

- **REHYDRATE** — load canonical context before substantial work.
- **STATUS** — report the current safe state, unresolved items, and exact next action.
- **CHECKPOINT** — persist a verified milestone back into canonical context.

## Design principles

1. External state beats conversational memory.
2. Canonical truth must be human-readable.
3. Every handoff needs an exact safe state.
4. Every checkpoint needs an exact next action.
5. Back up before mutation.
6. Write checkpoints in small verifiable chunks.
7. Supersede stale instructions explicitly.
8. Separate project domains so one workstream does not contaminate another.
9. Treat AI memory as helpful context, never as the sole source of truth.
10. Human verification remains mandatory before destructive or production changes.

## Start here

1. Read [QUICKSTART.md](QUICKSTART.md)
2. Read [PROTOCOL.md](PROTOCOL.md)
3. Review [CHECKPOINTING.md](CHECKPOINTING.md)
4. Review [FAILURE_MODES.md](FAILURE_MODES.md)
5. Use the sanitized examples in [examples/](examples/)

## Status

**v0.1 preview**

This protocol is intentionally being published early. It has been shaped by repeated real-world continuity failures and recoveries, but it should still be treated as a field-tested working pattern rather than a finished standard.

Feedback, criticism, edge cases, and better patterns are welcome.

## Philosophy

The goal is practical usefulness.

If this saves one engineer from reconstructing hours or days of lost context, it has done its job.