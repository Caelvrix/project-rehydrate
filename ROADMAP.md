# Roadmap

Project Rehydrate is being developed in public as a practical continuity protocol for long-running AI-assisted IT and technical work.

## v0.1 — Foundation

Status: **preview**

Goals:

- define the REHYDRATE / STATUS / CHECKPOINT operating model;
- provide a minimal canonical folder structure;
- document safe-state and exact-next-action patterns;
- document common continuity failure modes;
- provide sanitized examples;
- gather practitioner feedback.

## v0.2 — Recovery and drift control

Planned areas:

- stale-context detection checklist;
- explicit contradiction handling;
- recovery after incomplete checkpoints;
- canonical-file cleanup guidance;
- project handoff between humans and assistants;
- examples from infrastructure, data, application, and security work.

## v0.3 — Tooling patterns

Possible areas:

- optional validation scripts;
- marker checks;
- hash manifests;
- lightweight context linting;
- templates for repository-backed continuity;
- Git integration patterns that preserve human review.

## v1.0 — Stable protocol

v1.0 should only be declared after repeated successful use across multiple independent projects and after recovery has been tested deliberately, not just during normal operation.

Suggested readiness criteria:

- multiple successful cross-session rehydrations;
- successful recovery from stale or contradictory context;
- successful recovery from a deliberately incomplete checkpoint;
- proof that another engineer can follow the protocol without its original authors present;
- stable terminology and examples;
- documented limitations.