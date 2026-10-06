# Git-backed continuity (optional deployment pattern)

Project Rehydrate is storage-agnostic. A private Git repository can serve as the canonical context store when an AI assistant has authorized repository read/write access. This is an optional extension, not a prerequisite for the five-minute workflow.

## Roles

- **Private Git repository:** authoritative README/map, domain current-state files, procedures and architecture decisions. Commit history provides provenance, not an independent backup.
- **AI connector:** retrieve the map and relevant domain files; propose bounded edits; write only through supported, authorized operations; read back and verify commits.
- **Independent backup:** versioned snapshots in a separate protected location such as an organization's SharePoint environment, with tested restoration. A sync mirror that replicates deletions is not sufficient.
- **Public methodology repository:** sanitized protocol and examples only. Never mix organization-specific internal context into public documentation.

## REHYDRATE

Use a **branch-first discovery sequence**. Do not assume the default branch or ask the operator to paste a checkpoint until repository discovery has failed.

1. Identify the repository and active workstream from the user's request.
2. Enumerate plausible active branches and inspect recent relevant commits.
3. Match the workstream, date and latest verified checkpoint to the most likely canonical branch/ref.
4. Retrieve the master README/router and the workstream current-state/checkpoint files from that branch.
5. Verify the branch HEAD and checkpoint revision before treating the recovered state as canonical.
6. Fetch only relevant dependencies and referenced implementation artifacts needed to continue safely.
7. Reconcile the latest verified checkpoint against newer evidence and distinguish CURRENT, PROVISIONAL and UNRESOLVED state.
8. Report the branch/ref, checkpoint revision, last verified milestone, safe state, blockers and exactly one next action. No operational mutation during rehydration.
9. If repository access is unavailable or discovery cannot establish a trustworthy ref, fall back to direct attachment of canonical files. Avoid giant terminal dumps and do not reconstruct missing operational history from chat.

## STATUS

Report the verified workstream state, blockers and next action, citing exact file paths/revisions where possible.

## CHECKPOINT

Inspect → Validate → Back up → Change → Validate → Reconcile → Record.

CHECKPOINT is both an explicit operator command and a **continuous continuity discipline**. The operator may issue CHECKPOINT to force a hard stopping-point snapshot, but assistants should also record substantial verified milestones during long work rather than waiting for the end of the chat.

- Before writing, read the latest target file and revision; detect concurrent edits rather than overwrite them.
- Change domain truth and the compact master quest log together where practical. Use a branch/PR where review is warranted.
- Make small, bounded commits rather than one giant context write.
- Verify the resulting content and commit SHA by readback.
- Record exact evidence that materially matters for recovery: branch/ref, operation IDs, hashes, validation results, failure states, untouched boundaries and the next safe action.
- Never claim a checkpoint is complete when a write or readback failed.
- If a repository connector blocks or rejects a write, keep the verified state in active context, report the failure explicitly, retry with a smaller bounded change when appropriate, and preserve a manual/local Git fallback path. Do not silently substitute an unverified checkpoint.
- Repository documentation updates do not authorize execution against production systems.

## RECOVER — historical knowledge archaeology

A fourth, complementary workflow can recover valuable engineering knowledge from old AI conversations. It is not a fourth prerequisite for everyday use of the three core commands.

1. Select an old conversation or a bounded topic. Extract concrete commands, object names, decisions, test results, failures, lessons and source chronology into a provisional recovery record.
2. Preserve provenance: source conversation/date, exact evidence where possible, extraction gaps, and whether each statement was observed, inferred or merely proposed.
3. Compare the extraction with the latest canonical domain file and newer evidence. Historical facts do not automatically become current configuration; explicitly mark SUPERSEDED, HISTORICAL, PROVISIONAL or UNRESOLVED where appropriate.
4. Have a human review material contradictions and sensitive details. Do not commit unredacted full chat dumps, credentials or confidential artifacts.
5. Commit validated additions to the owning domain in small, reviewable changes, keeping the master map concise. Record the revision and verify readback.
6. Preserve non-current archaeology in a clearly identified historical location when retention is approved. It must not silently override current truth.

**Recovery is evidence reconciliation, not transcript ingestion.** A conversation may preserve the reasoning and observations behind a decision, but only validated evidence can advance operational current state.

This supports device-independent collaboration: a connected assistant can read the same authenticated repository from different sessions without repeatedly pasting large context files. Actual cloud or infrastructure execution still requires separate authorization and environment access.

## Security and recovery boundaries

Keep repositories private for organizational context; apply least privilege, organization approval, protected branches, MFA and access review. Do not commit credentials, keys, raw confidential exports or sensitive incident evidence. Scan candidates and nested archives before import; use a restrictive allowlist rather than uploading an entire unexamined ZIP. Git history retains mistakes even after a file is deleted; follow an incident response and history-cleaning process for exposed secrets. Test restoration from independent, versioned backups.

## Evidence status

This document describes a deployable pattern. A specific organization must separately validate connector permissions, initial import, rehydration, controlled checkpoint writes, backup scheduling and restoration before calling its migration complete.


## Artifact-continuity rule (field lesson, September 2026)

A checkpoint that names a script, notebook, model or other essential implementation artifact is **not recoverable** merely because Markdown records its old local path and hash. The artifact itself must be accessible from the canonical storage system (or an explicit, tested external artifact store) before the checkpoint is declared complete.

For a Git-canonical deployment, keep approved source and sanitized, reviewable working artifacts in a private repository with the documentation that depends on them. Maintain an artifact manifest recording path/ref, content hash or object ID, classification (reference/WIP/validated/deployed), runtime environment and authorization status, and exact recovery instructions. Check sensitive or generated material against a restrictive allowlist before publication; do not commit secrets, raw business data, credentials, unreviewed exports or notebook outputs.

At CHECKPOINT: commit the approved implementation and domain state together or as explicitly linked commits; independently fetch the committed artifact at the intended branch/ref and compare the retrieved content/hash, then update the master handoff with its actual status. A successful push, locally matching hash or descriptive checkpoint alone is insufficient. Do not imply local working folders and remote Git are synchronized without checking both.

At REHYDRATE: fetch the README, relevant domain state **and referenced executable source artifacts** from the canonical ref; verify availability and integrity before planning execution. Prefer fetching directly from the authorized repository rather than asking the operator to locate/re-upload a file already present there. If a referenced artifact is absent, mark the workstream **BLOCKED: ARTIFACT NOT RECOVERED** instead of reconstructing from chat or silently treating documentation as implementation.

An unfinished artifact may be committed privately as explicitly labeled WIP, with fail-closed defaults and deployment prohibitions; a source commit does not prove Fabric/cloud runtime validation or authorize a write. Never conflate source-recovered, syntactically checked, deployed, executed and independently reconciled.

**Workflow-efficiency guard:** one action at a time applies at meaningful inspect/validate/mutate/reconcile boundaries. It does not mean repeatedly reading already verified source in arbitrary small excerpts or editing each constant separately. Construct a coherent reviewed change and expose one controlled operational step at a time. When a user intentionally migrates the canonical store to Git, legacy local copies are recovery evidence, not mandatory rehydration dependencies. Independent, versioned backup still remains necessary; Git commit history alone is not backup.


## Write-failure resilience

Git-backed continuity needs a second path for the moments when the preferred repository connector refuses, rate-limits, conflicts or blocks a write.

Recommended resilience ladder:

1. **Retry smaller.** Split a large append into one verified milestone per commit.
2. **Refresh before retry.** Re-read the target file/ref and use the newest blob/revision to avoid stale-write conflicts.
3. **Write the owning domain first.** If a mega continuity file is large or repeatedly blocked, commit the smallest authoritative current-state file before attempting the larger forensic log.
4. **Use normal Git as the manual fallback.** A local clone with authenticated `git add`, `git commit`, `git push` can preserve continuity when an AI connector cannot perform the write. The same verification rules still apply.
5. **Maintain a compact emergency checkpoint surface.** A small file such as `LATEST_CHECKPOINT.md` can record branch/ref, last verified milestone, safe state, next action and links to deeper evidence. This reduces dependence on repeatedly rewriting a very large continuity file.
6. **Reconcile later.** Once the preferred write path is healthy, fold the emergency checkpoint into the normal domain/mega history and mark it reconciled.

The goal is not to make writes infallible. The goal is to ensure **one blocked write cannot make the whole project continuity-dependent on the chat window again**.
