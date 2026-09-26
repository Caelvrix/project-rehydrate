# README_FIRST

## Project

Example Data Platform

## Purpose

Build a governed reporting platform while preserving safe continuity across multiple engineering sessions.

## Active workstream

01_Data_Ingestion

## Current safe state

- development environment only;
- source access is read-only;
- first three source tables reconciled;
- incremental ingestion not yet enabled;
- production untouched.

## Exact next action

Run a read-only duplicate-key check on the candidate incremental key for SourceTable04.

## Do not do yet

- do not enable scheduled ingestion;
- do not change production;
- do not create merge logic until key uniqueness is validated.

## Domain routing

- Data ingestion: ../01_Data_Ingestion/CURRENT_STATE.md
- Reporting: ../02_Reporting/CURRENT_STATE.md
- Security: ../03_Security/CURRENT_STATE.md

## Continuity protocol

**REHYDRATE:** Read this file first, then the active domain file.

**STATUS:** Report the active workstream, last verified milestone, current safe state, unresolved items, and exact next action.

**CHECKPOINT:** Back up canonical files, write in small verified chunks, verify markers, then record final SHA256.