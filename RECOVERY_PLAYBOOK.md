# Recovery Playbook

Use this playbook when continuity has already broken.

## Scenario 1 — The new chat does not know where you left off

Action:

1. Stop technical execution.
2. Read README_FIRST.md.
3. Read the routed domain state.
4. Compare the latest checkpoint with current system evidence.
5. State the safe state before making changes.

Do not ask the assistant to 'just continue' from memory.

## Scenario 2 — Two context files disagree

Action:

1. Do not silently choose one.
2. Identify the conflicting claims.
3. Check current system evidence if safe.
4. Determine which claim is newer and verified.
5. Correct canonical state explicitly.
6. Record what was superseded and why.

## Scenario 3 — A checkpoint was interrupted halfway through

Action:

1. Locate the pre-edit backup.
2. Compare backup and current file.
3. Identify the last fully verified chunk.
4. Remove or repair incomplete content deliberately.
5. Re-run marker checks.
6. Hash only after semantic verification.

## Scenario 4 — A temporary artifact may be newer than canonical state

Action:

1. Treat canonical state as potentially stale.
2. Inspect the temporary artifact read-only.
3. Identify differences.
4. Decide whether the experiment should become canonical.
5. Checkpoint the decision.

## Scenario 5 — An old next action was executed accidentally

Action:

1. Stop further mutation.
2. Record exactly what changed.
3. Assess whether rollback is needed.
4. Re-establish current verified state.
5. Update canonical context with the incident and corrected direction.

## Scenario 6 — The context file is too large to use comfortably

Action:

1. Back it up.
2. Keep milestone history intact.
3. create or refresh a concise current-state section;
4. split unrelated domains into separate files;
5. make README_FIRST.md route to them;
6. preserve explicit links to older history.

## Scenario 7 — You cannot tell whether a statement is fact or assumption

Action:

Mark it explicitly as one of:

- confirmed;
- observed;
- inferred;
- assumed;
- unresolved.

Then validate before relying on it for a risky step.

## Golden recovery rule

When continuity is uncertain, reduce scope.

Recover one fact, one file, one subsystem, or one decision at a time.