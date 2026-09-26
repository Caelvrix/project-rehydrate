# When Your AI Forgets the Project: How We Built a Continuity Protocol for Long-Running IT Work

Long-running AI-assisted IT work has a strange failure mode: the project can be perfectly healthy while the conversation holding its history becomes unusable.

You change chats. A context window fills up. A browser session disappears. An assistant remembers the broad idea but not the exact safe state. A stale instruction survives three architecture changes. Someone says, "continue where we left off," and suddenly both human and AI are reconstructing the past from fragments.

We kept running into this problem during real technical work.

Eventually we stopped treating it as an annoyance and started treating it as an operational continuity problem.

That became **Project Rehydrate**.

## Why the name?

We use the word *rehydrate* because a new AI session should not have to reconstruct a project from conversational memory.

Instead, the session is reloaded from an external canonical project state: what was last proven, what is safe now, what remains unresolved, what must not be touched, and what exact action comes next.

The name is the shorthand. The problem it solves is simple: **keeping long-running AI-assisted IT work coherent across sessions.**

## The core observation

Chat history is useful, but it is a poor place to keep authoritative project state.

A long-running project needs an external continuity layer that is:

- human-readable;
- easy for an AI assistant to reload;
- explicit about what is verified;
- explicit about what must not be touched;
- explicit about the exact next safe action.

## This was not invented cleanly

Project Rehydrate grew out of repeated failures.

We tried large handoff summaries. They became hard to audit.

We let old next-actions remain in context. They survived after strategy changed.

We allowed multiple technical workstreams to share too much context. They started bleeding into each other.

We used large checkpoint writes. Some became fragile or difficult to verify.

We trusted successful commands before reading the result back.

We learned that hashing a bad file only gives you a very reliable bad file.

We watched temporary working copies drift beyond the canonical notes.

We saw how easily an AI assistant could reconstruct a plausible history when the real history was incomplete.

Those growing pains became the protocol.

The detailed record is preserved in `FIELD_NOTES_AND_GROWING_PAINS.md` because we believe the failures are as useful as the final pattern.

## Three commands

Project Rehydrate revolves around three simple operator commands.

### REHYDRATE

Reload canonical project context before substantial work.

The goal is not to summarize everything. The goal is to recover the exact operational state: what was proven, what is unresolved, what must remain untouched, and what the smallest safe next action is.

### STATUS

Give a compact orientation without rewriting the project history.

A good status answers: active workstream, last verified milestone, current safe state, unresolved items, next action, and continuity risk.

### CHECKPOINT

Persist a milestone back into canonical context.

This is not just 'write a summary.' A checkpoint is treated as a small controlled write operation: backup first, write in small chunks, read each chunk back, verify markers, then hash the final file.

## Why the boring parts matter

Some of the most useful rules came directly from things going wrong.

So the protocol became intentionally boring:

- plain Markdown;
- explicit supersession of stale directions;
- domain-specific state files;
- read-back verification;
- exact next actions;
- explicit safety boundaries;
- hashes only after semantic verification.

That boringness is a feature. Boring state is easier to audit.

## A small example

Instead of writing:

> Worked on ingestion. Continue tomorrow.

write:

> Read-only source inspection complete. Candidate incremental key validated over three historical windows. No production changes made. Scheduler remains disabled. Next action: run duplicate-key analysis before implementing merge logic.

That second note can survive a week, a new chat, a different assistant, and a tired human brain.

## Is this only for ChatGPT?

No.

Project Rehydrate was developed and field-tested primarily with ChatGPT, but it was deliberately designed so that the continuity layer lives outside the AI platform.

The protocol can be adapted to any assistant that can read the canonical state and follow explicit instructions.

That may include ChatGPT, Claude, Gemini, Microsoft Copilot, local models, or future assistants.

We are careful about the claim: we are **not** saying every feature has been tested on every AI platform.

We are saying the protocol is vendor-neutral by design.

At the simplest level, a human can paste the relevant canonical state into any capable assistant. At more integrated levels, the assistant may be able to read repositories, shared drives, project folders, or write back checkpoint updates under human review.

## Who is this for?

Not only software engineers.

The pattern is intended for anyone doing long-running AI-assisted technical work:

- sysadmins;
- network engineers;
- security teams;
- database administrators;
- cloud practitioners;
- data and BI professionals;
- developers;
- ERP administrators;
- IT managers;
- architects;
- support engineers;
- analysts;
- technical researchers.

If your work has state, decisions, unresolved questions, risk boundaries, and a next action, continuity matters.

## What Project Rehydrate is not

It is not a replacement for Git, ticketing, documentation, backups, runbooks, secrets management, or technical judgment.

It is simply the continuity layer between all of those things and the AI conversation helping you work through them.

## Why publish this?

Because most of us learned computing by being rescued by strangers.

Someone wrote the forum answer. Someone documented the obscure fix. Someone posted the script that saved an evening. They often had no idea who would eventually need it.

Project Rehydrate is our attempt to put one useful thing back into that commons.

If it saves one IT professional from rebuilding hours or days of lost context, it has done its job.

Project Rehydrate is being published as a v0.1 preview so that the rough edges can be found in the open.