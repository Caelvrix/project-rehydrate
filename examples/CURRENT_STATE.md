# Data Ingestion — Current State

## Last verified milestone

2026-01-15 — SourceTable03 reconciliation complete.

Verified:

- source row count matched persisted row count;
- primary key contained zero nulls;
- no duplicate primary keys found;
- source access remained read-only;
- no production changes were made.

## Current investigation

SourceTable04 candidate incremental field: ModifiedTimestamp.

Observed:

- field is populated on sampled recent rows;
- update behavior appears plausible;
- uniqueness has not been proven;
- delete behavior is unknown.

## Unresolved

1. Is ModifiedTimestamp sufficiently reliable for incremental extraction?
2. Can multiple rows share the same timestamp?
3. How are deletes represented?
4. Is there a stable tie-breaker key?

## Exact next action

Run a read-only duplicate-key analysis over the last 30 days using ModifiedTimestamp and PrimaryKey.

Do not implement merge logic until the result is reviewed.

## Safety boundary

- DEV only.
- Source system read-only.
- Scheduler disabled.
- Production untouched.