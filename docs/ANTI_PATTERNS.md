# Anti-Patterns

These patterns make Project Rehydrate weaker even when the files look organized.

## 1. The ceremonial checkpoint

A checkpoint is created because the process says so, but nobody verifies the content.

Result: bad state becomes official.

Better: read back every important write and confirm the exact next action.

## 2. The everything file

Every command, thought, screenshot reference, decision, and historical event is dumped into one giant Markdown file.

Result: retrieval becomes harder and stale state hides inside volume.

Better: master routing plus domain-specific state.

## 3. The vague safety statement

Example:

 > Be careful with production.

Better:

 > Production remains read-only. No configuration changes are approved. Next action is inspection only.

## 4. The heroic next step

Example:

 > Finish migration.

This is not an action. It is a project.

Better: define the smallest verifiable next operation.

## 5. The invisible assumption

A conclusion is written as fact even though it came from inference.

Better: label it as inferred or unresolved until evidence exists.

## 6. The auto-canonical assistant

An automated process writes directly into canonical context without human review.

Result: a hallucination can become official state.

Better: automate evidence collection and checks before automating authority.

## 7. The eternal history dump

Old milestones are preserved but no concise current-state section exists.

Result: the next operator must perform archaeology before every task.

Better: preserve history while maintaining a compact current orientation.

## 8. The secret-filled context file

Convenience leads to credentials or sensitive data being copied into continuity notes.

Better: store references to secret locations, never the secrets themselves.

## 9. The model-specific dependency

The workflow only works because one AI product remembers a custom behavior.

Better: encode the important behavior in files and prompts that can survive a model or provider change.

## 10. The untested recovery plan

A team documents normal checkpointing but never tests what happens when state is contradictory or incomplete.

Better: deliberately simulate one broken handoff before calling the protocol mature.