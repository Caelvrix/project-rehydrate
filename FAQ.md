# Frequently Asked Questions

## Is this just documentation?

Not quite.

Documentation explains a system. Project Rehydrate focuses on **operational continuity**: what was last proven, what state is safe, what remains unresolved, what must not be touched, and what exact action should happen next.

## Why not rely on AI memory?

Memory can be useful, but it is not a sufficiently auditable source of truth for long-running technical work. Canonical external state can be inspected, versioned, corrected, and verified by humans.

## Why Markdown?

Because it is portable, diffable, human-readable, easy for models to parse, and does not require a proprietary platform.

## Do I need Git?

No, but Git is highly recommended. Project Rehydrate can work with ordinary files, shared drives, document systems, or repositories as long as the canonical source is clear.

## Why hashes?

A final hash helps show whether a checkpointed file changed later. It does not prove the content is correct and it does not provide confidentiality.

## Why small checkpoint chunks?

Because large writes are harder to verify and easier to partially corrupt or misunderstand. Small writes make human review practical.

## Isn't the master file eventually going to become huge?

It should not contain all domain detail. Its job is routing and current orientation. Detailed history belongs in domain state files.

## Can this be automated?

Partly. Marker checks, backups, hashes, and linting can be automated. Decisions about truth, risk, and whether a change is safe should remain visible to humans.

## Is this tied to a particular AI provider?

No. The protocol is intentionally model- and vendor-neutral. It was developed and field-tested primarily with ChatGPT, but the continuity layer is external to the AI platform. See [COMPATIBILITY.md](COMPATIBILITY.md) for supported operating modes and portability guidance.

## Can I rename REHYDRATE, STATUS, and CHECKPOINT?

Yes. The names are conventions, not magic commands. Consistency matters more than terminology.

## What if my work is not software engineering?

That is expected. Project Rehydrate is intended for long-running AI-assisted IT and technical work across infrastructure, networking, security, cloud, databases, data, BI, ERP, support, architecture, software, governance, research, and other technical domains. Adapt the domain files accordingly.

## Does this replace tickets, Git, runbooks, or architecture docs?

No. It connects them by preserving the exact continuity state required to resume work safely.

## What should never go into public context files?

Secrets, credentials, private keys, access tokens, sensitive personal data, confidential customer information, and proprietary material you are not allowed to publish.