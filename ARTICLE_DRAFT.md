# When Your AI Forgets the Project: How We Built a Continuity Protocol for Long-Running IT Work

Long-running AI-assisted IT work has a strange failure mode: the project can be healthy while the conversation carrying its history becomes unreliable.

You open a new chat. A context window fills up. A browser session disappears. The assistant remembers the broad idea but not the exact safe state. An old instruction survives after the plan changed. Someone says, "continue where we left off," and both human and AI start reconstructing the past from fragments.

We kept running into this during real technical work.

Eventually we stopped treating it as a chat problem and started treating it as a continuity problem.

That became **Project Rehydrate**, published by **Caelvrix**.

## The idea in one paragraph

Project Rehydrate keeps a small external source of truth for long-running AI-assisted IT work. During meaningful work, verified milestones are checkpointed continuously into an external canonical store rather than waiting for the end of the conversation. Each checkpoint records the last verified milestone, current safe state, unresolved items, exact next action, and what must not be changed yet. At the start of a new session, the AI discovers the active branch and latest relevant checkpoint first, then reloads canonical project state before continuing.

The important shift is simple: **do not make the dying chat responsible for saving itself.**

Three commands make the workflow memorable:

- **REHYDRATE** — reload canonical project state.
- **STATUS** — show where the project safely stands.
- **CHECKPOINT** — persist the latest verified milestone.

That is the core protocol.

In our current field implementation, CHECKPOINT is no longer only a user-issued command. The operator can still say CHECKPOINT to force a hard stopping-point snapshot, but the assistant also records substantial verified milestones as work progresses. This reduces the amount of state that can be lost when a conversation ends unexpectedly.

## Why the name?

We use *rehydrate* because a new AI session should not have to reconstruct a project from conversational memory.

It should be reloaded from canonical state.

The name is shorthand. The problem it solves is simple: **keeping long-running AI-assisted IT work coherent across sessions.**

## Why chat history is not enough

Chat history is useful context, but it is a poor place to keep authoritative project state.

A technical project contains operational facts:

- what was actually proven;
- what is safe to assume now;
- what remains unresolved;
- what must not be touched;
- what exact action should happen next.

When those facts live only inside a long conversation, continuity becomes fragile.

## We learned this the painful way

Project Rehydrate did not appear fully formed.

We tried large handoff summaries. They became hard to audit.

We also learned not to wait until a chat is nearly full before saving state. In one real session, the interface warned that the conversation was full and allowed only one final message. Because verified milestones had already been committed incrementally, that last message only needed to request a checkpoint instead of reconstructing hours of work.

We left old next-actions in context. They survived after strategy changed.

We let several workstreams share too much continuity state. They started bleeding into each other.

We wrote large checkpoint blocks. Some became fragile or difficult to verify.

We trusted commands because they returned no error before checking what they actually wrote.

We learned that hashing a bad file only gives you a very reliable bad file.

We watched temporary working copies become newer than the canonical notes.

And we saw how easily an AI assistant could fill gaps with a plausible history when the real one was incomplete.

Each failure hardened the protocol.

The full list is documented in `FIELD_NOTES_AND_GROWING_PAINS.md` because we think the mistakes are as useful as the final framework.

## The newer field-tested pattern

The first version of Project Rehydrate assumed that a checkpoint would usually happen near the end of a work session. That was better than relying on chat history, but still left an obvious weakness: the conversation could fail before the checkpoint happened.

The newer pattern treats continuity as a **running transaction log of verified milestones**.

A practical Git-backed workflow now looks like this:

1. **Work in small verified stages.** Inspect, validate, change, reconcile.
2. **Checkpoint meaningful proof as it happens.** Do not wait for the user to remember to ask.
3. **Keep a compact latest-checkpoint surface plus a deeper continuity record.** A small file such as `LATEST_CHECKPOINT.md` tells a new session exactly where to resume; the deeper record preserves operational evidence, exact IDs, hashes, failures and historical safe stopping points.
4. **Commit small, reviewable chunks.** Avoid one giant context write that can fail, truncate or trigger connector/tool limits.
5. **Verify every write.** Capture the commit SHA or revision and read back when practical.
6. **If the write is blocked or fails, say so explicitly.** Never claim continuity is safe when the canonical write did not land.
7. **At REHYDRATE, discover before reading.** Identify repository, enumerate likely active branches, inspect recent relevant commits, then read the checkpoint/current-state files at the winning branch/ref.
8. **Resume from the last verified state, not the last conversational sentence.**

In our own use this has been dramatically more reliable than the earlier end-of-session handoff model. An informal field estimate puts successful continuity recovery around **90% in the scenarios we have exercised**, but that is an experience report, not a controlled benchmark. The remaining failures are exactly why the protocol still requires verification and explicit failure handling.

## State is not enough: preserve the artifacts too

A continuity note can perfectly describe a script, report definition, notebook or model that still exists only on one workstation. That is documentation, not full recovery.

We now treat a checkpoint as incomplete for implementation work until the required artifact bytes are also recoverable from the canonical repository or another approved artifact store.

That introduced another subtle lesson: **a successful Git add is not proof that Git stored the same bytes you validated locally.** Text normalization, filters or line-ending conversion can change staged content.

For critical artifacts, our current pattern is:

1. copy only the approved recovery artifacts into a bounded canonical folder;
2. record expected hashes;
3. apply repository rules needed to preserve their bytes;
4. compare the working-tree object with the staged Git object before commit;
5. commit and push;
6. verify the remote revision;
7. only then mark the artifact as recoverable from Git.

The broader principle is the same one that shaped the rest of Project Rehydrate: **verify the state you actually persisted, not the state you intended to persist.**

## What a checkpoint actually looks like

Instead of writing:

> Worked on the migration. Continue tomorrow.

write:

> Read-only source validation complete. No production changes made. Candidate key is still unproven. Next action: run duplicate-key analysis. Do not implement merge logic yet.

The second note can survive:

- a new chat;
- a different AI assistant;
- a tired operator;
- a week away from the project;
- partial loss of conversational context.

That is the difference between an activity log and resumable state.

## Why the boring parts matter

The protocol intentionally favors boring things:

- plain Markdown;
- explicit safe-state language;
- exact next actions;
- separate domain files;
- explicit supersession of stale directions;
- backup before mutation;
- small checkpoint writes;
- continuous milestone checkpointing rather than end-of-chat rescue;
- branch-first rehydration;
- commit/read-back verification;
- explicit reporting when a checkpoint write fails;
- hashes only after semantic verification.

Boring state is easier to inspect, diff, correct, and trust.

## Is this only for ChatGPT?

No.

Project Rehydrate was developed and field-tested primarily with ChatGPT, but the continuity layer lives outside the AI platform.

The protocol is designed to be vendor-neutral.

It can be adapted to assistants such as ChatGPT, Claude, Gemini, Microsoft Copilot, local models, or future systems, as long as they can read the canonical state and follow explicit instructions.

We are deliberately careful about this claim: we are **not** saying every feature has been tested on every platform.

We are saying the protocol itself does not depend on one vendor's hidden memory.

At the simplest level, you can paste the relevant context into any capable assistant. At more integrated levels, the assistant may be able to read repositories, shared drives, project folders, and even write checkpoint updates under human review.

## Who is this for?

Not only software developers.

Project Rehydrate is intended for long-running AI-assisted work across IT and technical disciplines:

- systems administration;
- infrastructure and networking;
- cybersecurity and incident response;
- cloud operations;
- databases;
- data, BI and analytics;
- software and automation;
- ERP and business systems;
- IT governance and architecture;
- support and troubleshooting;
- technical research.

If your work has state, decisions, unresolved questions, risk boundaries, and a next action, continuity matters.

## What it does not replace

Project Rehydrate does not replace Git, ticketing, runbooks, architecture documentation, backups, secrets management, or technical judgment.

It is the continuity layer between those systems and the AI-assisted work happening around them.

## Why publish it?

Because many of us learned computing by being rescued by strangers.

Someone wrote the forum answer. Someone documented the obscure fix. Someone posted the script that saved an evening. Most of them never knew who would eventually need it.

Project Rehydrate is one attempt to put something useful back into that commons.

If it saves one IT professional from rebuilding hours or days of lost context, it has done its job.

Project Rehydrate is being published by **Caelvrix** as a **v0.1 preview** so people can test it, break it, improve it, and contribute real failure cases.