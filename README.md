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

## What makes it different

Project Rehydrate is not just a handoff note. It introduces explicit operating rules:

- a source-of-truth hierarchy;
- exact safe-state language;
- atomic next actions;
- explicit risk boundaries;
- stale-instruction supersession;
- backup-before-mutation;
- small verified checkpoint writes;
- read-back validation;
- integrity hashing after semantic verification;
- recovery procedures when continuity has already broken.

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

- [Quickstart](QUICKSTART.md) — smallest useful implementation
- [Protocol](PROTOCOL.md) — operating contract
- [Reference Card](REFERENCE_CARD.md) — short day-to-day version
- [Checkpointing](CHECKPOINTING.md) — verified persistence workflow
- [Failure Modes](FAILURE_MODES.md) — how continuity breaks
- [Recovery Playbook](RECOVERY_PLAYBOOK.md) — what to do when it already broke
- [Adoption Guide](ADOPTION_GUIDE.md) — introduce the pattern without creating bureaucracy
- [FAQ](FAQ.md) — common questions
- [Examples](examples/) — sanitized sample context files
- [Roadmap](ROADMAP.md) — planned evolution
- [Governance](GOVERNANCE.md) — how the protocol itself changes
- [Security & Privacy](SECURITY.md) — information-hygiene guidance
- [Contributing](CONTRIBUTING.md) — how to help

## Thirty-second version

At the end of a meaningful work session, do not write only what you did.

Record:

```text
Last verified milestone:
Current safe state:
Unresolved:
Exact next action:
Do not do yet:
```

At the start of the next session, reload that state before doing substantial work.

That simple discipline is the seed of Project Rehydrate.

## Example

Instead of:

> Worked on ingestion. Continue tomorrow.

write:

> Read-only source inspection complete. Candidate incremental key validated over three historical windows. No production changes made. Scheduler remains disabled. Next action: run duplicate-key analysis before implementing merge logic.

The second note survives a new chat, a tired operator, a different assistant, and a week away from the project.

## What this is not

Project Rehydrate does **not** replace:

- Git;
- tickets;
- runbooks;
- architecture documentation;
- backups;
- secrets management;
- engineering judgment.

It is a continuity layer between those systems and the AI-assisted work happening around them.

## Status

**v0.1 preview**

This protocol is intentionally being published early. It has been shaped by repeated real-world continuity failures and recoveries, but it should still be treated as a field-tested working pattern rather than a finished standard.

Feedback, criticism, edge cases, and better patterns are welcome.

## Article draft

A long-form introduction is being prepared in [ARTICLE_DRAFT.md](ARTICLE_DRAFT.md).

## License

Project Rehydrate is available under the [MIT License](LICENSE).

## Philosophy

The goal is practical usefulness.

If this saves one engineer from reconstructing hours or days of lost context, it has done its job.