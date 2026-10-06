# Changelog

## v0.1-preview

Initial public protocol draft.

Introduced:

- canonical project root;
- README_FIRST routing pattern;
- domain-specific state files;
- REHYDRATE / STATUS / CHECKPOINT commands;
- exact safe-state recording;
- atomic next-action recording;
- explicit supersession of stale instructions;
- small verified checkpoint writes;
- backup-before-mutation guidance;
- marker verification;
- final SHA256 integrity check;
- documented failure modes;
- sanitized example context files.

This release is intentionally labeled preview so the protocol can evolve through field use and community feedback.

## 2026-10-06 — continuous checkpointing field update

- Updated the published article to reflect continuous milestone checkpointing rather than end-of-session-only handoffs.
- Added branch-first REHYDRATE discovery and revision verification.
- Added explicit blocked-write handling and manual Git fallback guidance.
- Added the compact latest-checkpoint + deeper forensic-log pattern for resilient Git-backed continuity.
- Documented the approximately 90% continuity success observation as informal field experience, not a controlled benchmark.
