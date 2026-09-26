# Failure Modes

Project Rehydrate was shaped by failures, not by theory.

## 1. The giant handoff summary

**Symptom:** A single massive summary is generated at the end of a long session.

**Risk:** Important details are omitted, assumptions blend with verified facts, and the result becomes difficult to audit.

**Mitigation:** Maintain living domain state during the project and checkpoint incrementally.

## 2. Stale next actions

**Symptom:** An old next step remains in the master context after strategy changes.

**Risk:** A later session may faithfully execute the wrong plan.

**Mitigation:** Explicitly state that the new direction supersedes the old one.

## 3. Conversation becomes the database

**Symptom:** Important decisions exist only in chat history.

**Risk:** Continuity depends on one conversation remaining available and correctly interpreted.

**Mitigation:** Persist decisions externally in canonical files.

## 4. Assistant reconstructs missing history

**Symptom:** A future session fills gaps with plausible assumptions.

**Risk:** The answer sounds coherent while being operationally wrong.

**Mitigation:** Rehydrate from canonical state and ask for missing evidence.

## 5. Temporary artifact drift

**Symptom:** A local test file, exported model, notebook, or branch changes after the last checkpoint.

**Risk:** Canonical state describes an older reality.

**Mitigation:** Checkpoint after a disposable experiment becomes meaningful or before it becomes the new baseline.

## 6. Domain contamination

**Symptom:** Security, infrastructure, reporting, and application work are mixed into one context file.

**Risk:** Wrong assumptions bleed across workstreams.

**Mitigation:** Use a master router plus domain state files.

## 7. Overwriting instead of appending

**Symptom:** A large canonical state file is replaced during an update.

**Risk:** Historical decisions disappear.

**Mitigation:** Backup first. Prefer append for milestone history.

## 8. Trusting command execution without validation

**Symptom:** A command returns no error, so the result is assumed correct.

**Risk:** Files may be incomplete, malformed, or written to the wrong location.

**Mitigation:** Read back the affected section immediately.

## 9. Hash without semantic verification

**Symptom:** A hash is recorded before anyone checks whether the file content is correct.

**Risk:** A perfectly hashed mistake is still a mistake.

**Mitigation:** Verify content first, hash last.

## 10. Over-automation

**Symptom:** Continuity writes happen automatically without human review.

**Risk:** Incorrect assumptions become canonical faster.

**Mitigation:** Keep checkpointing deliberately observable until the process is mature.

## 11. No risk boundary

**Symptom:** A handoff records what to do next but not what must remain untouched.

**Mitigation:** Record explicit safety boundaries such as production untouched, read-only inspection only, mutation disabled, or experimental branch only.

## 12. Canonical file becomes a novel

**Symptom:** The context file grows until important state is buried.

**Mitigation:** Use master routing, domain separation, concise current-state sections, milestone history, and periodic cleanup with backups.