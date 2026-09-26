# Why External State Matters

AI-assisted work often feels continuous even when the underlying context is not.

A model may remember themes, terminology, or prior decisions while still missing the one operational detail that matters: which file is canonical, whether a scheduler is enabled, which environment is safe to change, or whether a test result was actually reconciled.

That gap is dangerous because fluent reconstruction can look like continuity.

## The illusion of continuity

Humans experience a conversation as one story.

Engineering systems do not.

A technical project consists of state:

- files;
- commits;
- configuration;
- data;
- environment boundaries;
- decisions;
- exceptions;
- unresolved questions;
- evidence.

If the AI conversation remembers only the story but not the state, it can continue coherently in the wrong direction.

## External state changes the failure mode

Without canonical external state:

- the assistant may reconstruct;
- the human may misremember;
- stale instructions may remain invisible;
- a handoff depends on chat availability.

With canonical external state:

- claims can be inspected;
- changes can be diffed;
- stale instructions can be superseded;
- another person can audit the handoff;
- the next session can recover from files instead of inference.

## Why plain text

Plain text is intentionally unglamorous.

It is:

- portable;
- searchable;
- diffable;
- readable without a special application;
- easy to version;
- easy for many AI systems to parse;
- resilient over long time periods.

Project Rehydrate does not require Markdown specifically, but Markdown is a practical default.

## Why this still needs humans

External state is not automatically correct.

A stale canonical file can be more dangerous than no file at all if everyone trusts it blindly.

That is why the protocol includes:

- read-back verification;
- explicit evidence language;
- supersession;
- exact next actions;
- risk boundaries;
- recovery procedures.

The objective is not to replace memory with files.

The objective is to make continuity auditable.