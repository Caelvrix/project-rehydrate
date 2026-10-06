# Checkpointing

Checkpointing is the heart of Project Rehydrate.

A good checkpoint lets a future session resume safely without reconstructing the project from memory.

Do not treat checkpointing as an end-of-session ceremony. In long or high-risk work, record **substantial verified milestones continuously**. An explicit CHECKPOINT command still means "create a hard stopping-point snapshot now", but normal work should already have left a recoverable trail before that moment.

## Why small writes matter

Large context writes are fragile. They can truncate, fail halfway through, hide formatting damage, make verification difficult, or overwrite good state with malformed content.

Prefer multiple small verified writes over one giant append.

## Recommended checkpoint sequence

Use this sequence for each meaningful milestone rather than waiting for one giant final handoff.

### Step 1 — Back up

Create a timestamped backup before editing canonical state.

```powershell
$Stamp = Get-Date -Format 'yyyyMMdd_HHmmss'
Copy-Item $State "$State.bak_$Stamp"
```

### Step 2 — Write one logical chunk

Each chunk should describe one concern:

- architecture decision;
- validation result;
- failure mode;
- current safe state;
- exact next action.

### Step 3 — Verify immediately

After each append:

```powershell
Get-Content $State -Tail 40
```

Do not assume the write succeeded merely because no error appeared.

### Step 4 — Repeat

Add the next logical block only after the previous block is visibly correct.

### Step 5 — Verify key markers

```powershell
Select-String -Path $State -SimpleMatch `
  'Current safe state',
  'Exact next action',
  'supersedes'
```

### Step 6 — Hash the final file

```powershell
Get-FileHash $State -Algorithm SHA256
```

The hash is not a security control by itself. It is a simple integrity checkpoint that makes later comparison easier.

## Append vs rewrite

Prefer **append** when recording historical milestones.

Prefer **targeted rewrite** when:

- the master routing file has become misleading;
- duplicate stale instructions are creating ambiguity;
- a concise current-state section must be replaced.

Never rewrite a large canonical file casually.

## Supersession rule

When a new checkpoint changes direction, state it explicitly.

> This checkpoint supersedes the previous instruction to resume deployment after UI cleanup. The new next action is schema reconciliation.

This protects future sessions from following the wrong instruction simply because it appears earlier in the file.

## Verification mindset

A checkpoint is only complete when:

- content exists;
- content is correct;
- important markers are findable;
- the final integrity value is recorded;
- the next action is unambiguous.

## If the Git write is blocked

A blocked checkpoint is not a completed checkpoint.

Use this order:

1. State clearly that the canonical write did not land.
2. Keep the verified milestone intact in the active working context.
3. Re-read the target file/revision before retrying.
4. Retry with a smaller bounded edit.
5. If the connector remains blocked, use an approved manual Git path or a compact emergency checkpoint file.
6. Verify the resulting commit/ref before declaring continuity safe.
7. Later reconcile emergency state into the normal domain/mega history.

For large continuity repositories, consider separating:
- a **small latest-checkpoint file** optimized for frequent writes and fast rehydration;
- normal domain current-state files;
- a **deeper forensic/mega log** updated at major gates rather than on every tiny event.

This reduces write size and contention without sacrificing detailed historical evidence.
