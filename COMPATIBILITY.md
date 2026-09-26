# AI Platform Compatibility

Project Rehydrate is designed to be **AI-platform agnostic**.

It was developed and field-tested primarily with ChatGPT, but the protocol itself does not depend on ChatGPT-specific memory, project, connector, or automation features.

The durable part of the system is the external canonical state plus the operating discipline around it.

## Compatibility levels

### Level 1 — Manual

Requirements:

- the AI can read text pasted into a conversation.

How it works:

- the human opens the canonical files;
- relevant content is pasted into the AI session;
- REHYDRATE / STATUS / CHECKPOINT are performed manually.

This mode should work with almost any general-purpose AI assistant.

### Level 2 — File-assisted

Requirements:

- the AI can read uploaded files or project documents.

How it works:

- canonical files are uploaded or attached;
- the assistant reads the master router and domain state directly;
- the human still controls file updates.

This reduces copy/paste effort and transcription risk.

### Level 3 — Repository or workspace integrated

Requirements:

- the AI can read a repository, shared drive, workspace, or project folder.

How it works:

- the assistant can inspect canonical context directly;
- links between master and domain files can be followed;
- diffs and repository history can support verification.

This is usually the most convenient operating mode.

### Level 4 — Assisted write-back

Requirements:

- the AI can update files or repository content;
- human review remains available.

How it works:

- the assistant can perform checkpoint writes;
- backups, marker checks, and hashes can be executed through tools;
- the human reviews the resulting canonical state.

### Level 5 — Partially automated continuity

Possible capabilities:

- scheduled integrity checks;
- stale-marker detection;
- automated backups;
- context linting;
- consistency checks across domain files;
- notification when canonical state has not been checkpointed after significant work.

This level should be approached carefully. Automation should not silently convert AI inference into canonical truth.

## Platforms

The protocol should be adaptable to AI assistants such as:

- ChatGPT;
- Claude;
- Gemini;
- Microsoft Copilot;
- local or self-hosted language models;
- future AI assistants with equivalent text/file capabilities.

This is a design claim, not a claim that every feature has been tested on every platform.

## Provenance statement

Recommended wording when describing the project:

> Project Rehydrate is a vendor-neutral continuity protocol developed and field-tested primarily with ChatGPT. It externalizes project state so the workflow is not dependent on any one AI platform or model.

## What may differ by platform

Different AI systems may vary in:

- context-window size;
- persistent memory;
- file upload limits;
- direct filesystem access;
- repository connectors;
- write permissions;
- tool execution;
- automation support.

The protocol should degrade gracefully: when integration is unavailable, the human can always fall back to manual mode.

## Core portability rule

If an AI assistant can read the canonical state and follow explicit instructions, it can participate in Project Rehydrate.

The protocol should never require one vendor's hidden memory to function.