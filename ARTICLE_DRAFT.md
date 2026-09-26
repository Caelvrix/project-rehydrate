# When Your AI Forgets the Project: How We Built a Continuity Protocol for Long-Running IT Work

Long-running AI-assisted IT work has a strange failure mode: the project can be healthy while the conversation carrying its history becomes unreliable.

You open a new chat. A context window fills up. A browser session disappears. The assistant remembers the broad idea but not the exact safe state. An old instruction survives after the plan changed. Someone says, "continue where we left off," and both human and AI start reconstructing the past from fragments.

We kept running into this during real technical work.

Eventually we stopped treating it as a chat problem and started treating it as a continuity problem.

That became **Project Rehydrate**.

## The idea in one paragraph

Project Rehydrate keeps a small external source of truth for long-running AI-assisted IT work. At the end of meaningful work, you record the last verified milestone, current safe state, unresolved items, exact next action, and what must not be changed yet. At the start of the next session, the AI reloads that canonical state before continuing.

Three commands make the workflow memorable:

- **REHYDRATE** — reload canonical project state.
- **STATUS** — show where the project safely stands.
- **CHECKPOINT** — persist the latest verified milestone.

That is the core protocol.

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

We left old next-actions in context. They survived after strategy changed.

We let several workstreams share too much continuity state. They started bleeding into each other.

We wrote large checkpoint blocks. Some became fragile or difficult to verify.

We trusted commands because they returned no error before checking what they actually wrote.

We learned that hashing a bad file only gives you a very reliable bad file.

We watched temporary working copies become newer than the canonical notes.

And we saw how easily an AI assistant could fill gaps with a plausible history when the real one was incomplete.

Each failure hardened the protocol.

The full list is documented in `FIELD_NOTES_AND_GROWING_PAINS.md` because we think the mistakes are as useful as the final framework.

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
- read-back verification;
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

Project Rehydrate is being published as a **v0.1 preview** so people can test it, break it, improve it, and contribute real failure cases.