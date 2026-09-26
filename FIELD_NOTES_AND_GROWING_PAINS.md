# Field Notes and Growing Pains

Project Rehydrate did not begin as a neat framework.

It emerged from repeated continuity failures during long-running AI-assisted technical work. The protocol changed because things broke, became ambiguous, or proved too fragile in practice.

This document records those growing pains so that the finished pattern does not hide the lessons that created it.

## 1. We trusted the conversation for too long

At first, project continuity lived mainly in chat history.

That worked until conversations became long, multiple workstreams overlapped, and important decisions were buried several hundred messages back.

### Lesson

Conversation is useful context, but it is a poor canonical project store.

### Change introduced

We moved authoritative project state into external human-readable files.

---

## 2. Giant end-of-chat summaries became unreliable

Our first instinct was to preserve continuity by generating one large handoff summary at the end of a long session.

That looked efficient, but it created several problems:

- small operational details were easy to omit;
- verified facts and inferred conclusions could blend together;
- the summary became too large to review carefully;
- one malformed or truncated write could damage the whole handoff;
- future sessions had to trust a large block that was difficult to audit.

### Lesson

A giant summary is not the same as a verified checkpoint.

### Change introduced

We moved to living domain-state files and incremental checkpointing.

---

## 3. Old next-actions survived after the plan changed

Long projects accumulate instructions.

A statement such as "after this, resume scheduler work" may be correct on Monday and wrong by Thursday after a strategy change.

We found that chronology alone was not enough. An older instruction could remain visible and still sound valid.

### Lesson

Stale instructions must be explicitly superseded.

### Change introduced

Checkpoints now contain language such as:

> This direction supersedes the previous next-action statement.

That makes the governing instruction unambiguous.

---

## 4. Context from different workstreams became jumbled

When infrastructure, reporting, data, security, and application work all lived in one continuity stream, unrelated details began to contaminate each other.

The problem was not only file size. It was reasoning scope.

### Lesson

Long-running projects need domain boundaries.

### Change introduced

We adopted:

- one master routing file;
- separate domain state files;
- an explicit active workstream.

The master file points. The domain files explain.

---

## 5. The assistant sometimes reconstructed instead of reloaded

When exact history was missing, a plausible reconstruction could sound convincing even when it was operationally unsafe.

This is especially dangerous in technical work because the wrong assumption may still produce syntactically correct commands.

### Lesson

Fluent reconstruction is not continuity.

### Change introduced

REHYDRATE now requires canonical-state reading first and requires missing evidence to be surfaced instead of guessed.

---

## 6. Temporary working copies drifted away from canonical state

Experiments often happen in disposable files, test branches, exported models, scratch notebooks, or temporary folders.

Sometimes those artifacts become newer than the canonical documentation.

### Lesson

A checkpoint can become stale even when nobody edited the checkpoint file.

### Change introduced

Temporary artifacts are treated as an explicit continuity risk. Before promotion, the operator must reconcile the working artifact with canonical state.

---

## 7. Large checkpoint writes failed or became difficult to verify

One of the most important practical lessons came from writing long Markdown blocks through shell commands.

Large writes could:

- fail;
- truncate;
- become malformed;
- hide quoting problems;
- make it hard to know which portion actually persisted.

### Lesson

Smaller writes are slower but safer.

### Change introduced

We adopted **micro-chunk checkpointing**:

1. back up first;
2. write one small logical section;
3. read it back immediately;
4. only then write the next section;
5. verify key markers at the end;
6. compute the final hash last.

This became one of the defining operational practices of Project Rehydrate.

---

## 8. A successful command was mistaken for a successful outcome

A shell command can return without an error while still producing the wrong file, wrong location, incomplete content, or unexpected formatting.

### Lesson

Command success is not semantic success.

### Change introduced

Every important write is followed by read-back verification.

---

## 9. Hashing too early created false confidence

A checksum can prove that a file has not changed since it was hashed.

It cannot prove that the file was correct when the hash was created.

### Lesson

A perfectly hashed mistake is still a mistake.

### Change introduced

Semantic verification happens first. Hashing happens last.

---

## 10. The master context started becoming a dumping ground

As continuity improved, the temptation grew to put every important detail into the master file.

That recreated the original problem in a different format.

### Lesson

A master context should be a router and orientation surface, not the entire project history.

### Change introduced

Detailed truth remains in domain files while the master context carries:

- project identity;
- active workstream;
- safe-state summary;
- exact next action;
- routing links;
- superseding direction.

---

## 11. 'What we did' was less useful than 'what is safe now'

Early notes emphasized activity:

> We tested X, changed Y, discussed Z.

But a future operator usually needs a different answer:

> What can I safely assume right now?

### Lesson

Progress history and operational state are not the same thing.

### Change introduced

Project Rehydrate gives special weight to:

- last verified milestone;
- current safe state;
- unresolved items;
- exact next action;
- explicit risk boundary.

---

## 12. Vague next-actions caused drift

Statements such as:

- finish the migration;
- continue setup;
- resume orchestration;
- keep testing;

sound actionable but are not.

### Lesson

The next action should be atomic enough that another operator can execute it without inventing intermediate steps.

### Change introduced

We prefer actions such as:

> Run one read-only duplicate-key query over the last 30 days.

---

## 13. Safety boundaries needed to be written, not implied

Even when everybody knew production was sensitive, that assumption was sometimes left unstated.

### Lesson

Risk boundaries must survive the people who originally understood them.

### Change introduced

Continuity state now records explicit boundaries such as:

- production untouched;
- read-only inspection only;
- scheduler disabled;
- experimental branch only;
- no destructive mutation approved.

---

## 14. We resisted automating the process too early

Once the workflow became repeatable, automation was tempting.

But automatic checkpointing can promote wrong assumptions into canonical truth faster than a human can notice them.

### Lesson

Automate verification before automating authority.

### Change introduced

Backups, marker checks, hashes, and linting are good automation candidates.

Decisions about what is true, safe, or canonical should remain reviewable by humans.

---

## 15. Continuity itself needs maintenance

A continuity system can drift too.

Routing files become stale. Old sections accumulate. Domain boundaries stop matching reality.

### Lesson

The continuity layer is part of the system and needs periodic cleanup.

### Change introduced

Project Rehydrate treats cleanup as a controlled operation:

- back up first;
- preserve historical evidence;
- refresh concise current-state sections;
- split domains when needed;
- explicitly supersede stale routing.

---

## What these failures changed

The current protocol is deliberately more cautious than our first attempts.

That caution was earned.

The most important design rules now exist because an earlier, simpler approach failed in practice.

We intend to keep adding to this file as the protocol encounters new failure modes.