# Your AI Project Forgot Everything. Ours Did Too — So We Built a Continuity Protocol.

Long-running AI-assisted engineering work has a strange failure mode: the project can be perfectly healthy while the conversation holding its history becomes unusable.

You change chats. A context window fills up. A browser session disappears. An assistant remembers the broad idea but not the exact safe state. A stale instruction survives three architecture changes. Someone says, "continue where we left off," and suddenly both human and AI are reconstructing the past from fragments.

We kept running into this problem during real technical work.

Eventually we stopped treating it as an annoyance and started treating it as an engineering problem.

That became **Project Rehydrate**.

## The core observation

Chat history is useful, but it is a poor place to keep authoritative project state.

A long-running project needs an external continuity layer that is:

- human-readable;
- easy for an AI assistant to reload;
- explicit about what is verified;
- explicit about what must not be touched;
- explicit about the exact next safe action.

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

Large context dumps were difficult to verify. Stale next actions survived longer than they should have. Temporary working copies drifted away from the canonical state. A successful command was occasionally mistaken for a successful outcome.

So the protocol became intentionally boring:

- plain Markdown;
- explicit supersession of stale directions;
- domain-specific state files;
- read-back verification;
- exact next actions;
- explicit safety boundaries;
- hashes only after semantic verification.

## A small example

Instead of writing:

 > Worked on ingestion. Continue tomorrow.

write:

 > Read-only source inspection complete. Candidate incremental key validated over three historical windows. No production changes made. Scheduler remains disabled. Next action: run duplicate-key analysis before implementing merge logic.

That second note can survive a week, a new chat, a different assistant, and a tired human brain.

## What Project Rehydrate is not

It is not a replacement for Git, ticketing, documentation, backups, or engineering judgment.

It is simply the continuity layer between all of those things and the AI conversation helping you work through them.

## Why publish this?

Because most of us learned computing by being rescued by strangers.

Someone wrote the forum answer. Someone documented the obscure fix. Someone posted the script that saved an evening. They often had no idea who would eventually need it.

Project Rehydrate is our attempt to put one useful thing back into that commons.

If it saves one engineer from rebuilding hours or days of lost context, it has done its job.

Project Rehydrate is being published as a v0.1 preview so that the rough edges can be found in the open.