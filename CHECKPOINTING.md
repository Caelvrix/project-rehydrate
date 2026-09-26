# Checkpointing

Checkpointing is the heart of Project Rehydrate.

A good checkpoint lets a future session resume safely without reconstructing the project from memory.

## Why small writes matter

Large context writes are fragile. They can truncate, fail halfway through, hide formatting damage, make verification difficult, or overwrite good state with malformed content.

Prefer multiple small verified writes over one giant append.

## Recommended checkpoint sequence

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