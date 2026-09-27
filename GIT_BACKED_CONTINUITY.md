# Git-backed continuity (optional deployment pattern)

Project Rehydrate is storage-agnostic. A private Git repository can serve as the canonical context store when an AI assistant has authorized repository read/write access. This is an optional extension, not a prerequisite for the five-minute workflow.

## Roles

- **Private Git repository:** authoritative README/map, domain current-state files, procedures and architecture decisions. Commit history provides provenance, not an independent backup.
- **AI connector:** retrieve the map and relevant domain files; propose bounded edits; write only through supported, authorized operations; read back and verify commits.
- **Independent backup:** versioned snapshots in a separate protected location such as an organization's SharePoint environment, with tested restoration. A sync mirror that replicates deletions is not sufficient.
- **Public methodology repository:** sanitized protocol and examples only. Never mix organization-specific internal context into public documentation.

## REHYDRATE

1. Identify the active workstream from the user's request; use the master README as the routing map.
2. Retrieve the canonical README at a known repository and revision.
3. Fetch only the relevant domain current-state files and required dependencies.
4. Reconcile the latest verified checkpoint against any newer evidence and distinguish CURRENT, PROVISIONAL and UNRESOLVED state.
5. Report the last verified milestone, safe state, blockers, and exactly one next action. No changes during rehydration.
6. If repository access is unavailable, fall back to direct attachment of canonical Markdown files. Avoid giant terminal dumps.

## STATUS

Report the verified workstream state, blockers and next action, citing exact file paths/revisions where possible.

## CHECKPOINT

Inspect → Validate → Back up → Change → Validate → Reconcile → Record.

- Before writing, read the latest target file and revision; detect concurrent edits rather than overwrite them.
- Change domain truth and the compact master quest log together. Use a branch/PR where review is warranted.
- Make small, bounded edits. Verify the resulting content and commit SHA by readback.
- Record the next safe action and update backup/recovery evidence. Never claim a checkpoint is complete when a write or readback failed.
- Repository documentation updates do not authorize execution against production systems.

## Security and recovery boundaries

Keep repositories private for organizational context; apply least privilege, organization approval, protected branches, MFA and access review. Do not commit credentials, keys, raw confidential exports or sensitive incident evidence. Scan candidates and nested archives before import; use a restrictive allowlist rather than uploading an entire unexamined ZIP. Git history retains mistakes even after a file is deleted; follow an incident response and history-cleaning process for exposed secrets. Test restoration from independent, versioned backups.

## Evidence status

This document describes a deployable pattern. A specific organization must separately validate connector permissions, initial import, rehydration, controlled checkpoint writes, backup scheduling and restoration before calling its migration complete.
