# v0.1 Preview Release Checklist

This checklist is the final gate before Project Rehydrate becomes public.

## Repository clarity

- [x] README explains the problem within the first few lines.
- [x] 30-second summary exists.
- [x] 5-minute start guide exists.
- [x] REHYDRATE / STATUS / CHECKPOINT are defined consistently.
- [x] deeper material is linked rather than forced on first-time readers.
- [x] audience includes broad IT and technical roles, not only software engineering.

## Protocol quality

- [x] exact safe state is defined.
- [x] exact next action is defined.
- [x] stale instruction supersession is documented.
- [x] risk boundaries are documented.
- [x] micro-chunk checkpointing is documented.
- [x] read-back verification is documented.
- [x] hash-after-semantic-verification rule is documented.
- [x] recovery procedures exist.
- [x] failure modes and growing pains are preserved.

## Platform positioning

- [x] vendor-neutral design is stated.
- [x] ChatGPT provenance is disclosed.
- [x] no claim is made that every platform has been fully tested.
- [x] manual fallback mode is documented.

## Privacy and sanitization

- [x] examples are fictional and generic.
- [x] obvious employer-specific names removed.
- [x] obvious internal hostnames / project names removed.
- [x] credentials and secrets prohibited by project guidance.
- [x] public contribution guidance warns against sensitive data.

## Community readiness

- [x] CONTRIBUTING.md exists.
- [x] issue template for continuity failures exists.
- [x] issue template for improvements exists.
- [x] pull request template exists.
- [x] roadmap exists.
- [x] governance guidance exists.
- [x] MIT license exists.

## Launch content

- [x] long-form launch article drafted.
- [x] GitHub launch copy drafted.
- [x] DEV Community launch copy drafted.
- [x] Reddit launch copy drafted.
- [x] Hacker News launch copy drafted.

## Verified pre-publication checkpoint — 2026-09-26

- Organization handle: `Caelvrix` (renamed from the former organization handle).
- Repository: `Caelvrix/project-rehydrate`, default branch `main`.
- Visibility at checkpoint: PRIVATE.
- Publisher branding: Caelvrix in README, NOTICE, LICENSE, ARTICLE_DRAFT and launch copy.
- Profile logo: the approved black-and-crimson Caelvrix 2 artwork was shown uploaded in the organization settings screenshot; visual account-level confirmation only.
- A focused default-branch content search found no obvious legacy branding or internal identifiers, but this is not a full history/secrets audit.
- **Commit attribution decision RESOLVED:** Kaval explicitly accepts public attribution to `kwadolia`. Keep existing Git history; no anonymization or history rewrite. Profile visibility and commit-email review remain sensible optional hygiene checks, not a requirement to disguise authorship.
- Do not claim a domain, trademark, public social handle, or GitHub release has been created without separate verification.

### Exact next action

With attribution accepted, perform the last manual public-profile / email-hygiene check if desired, confirm repository visibility is PRIVATE, then change only `Caelvrix/project-rehydrate` to PUBLIC in GitHub Settings. Keep `Caelvrix/community-hub` PRIVATE. Verify public access before announcing.

### Do not do yet

- Do not publish launch posts or distribute release links until public visibility is independently verified.
- Do not make `Caelvrix/community-hub` public.
- Do not rewrite history without an agreed preservation and validation plan.

## Final manual actions

- [x] Open the repository in GitHub and visually inspect the README rendering (screenshots reviewed; latest diagram edit still merits visual confirmation).
- [ ] Confirm the Mermaid diagram renders correctly.
- [x] Confirm all README linked files exist (link targets checked via connector).
- [ ] Change repository visibility from Private to Public.
- [ ] Create a GitHub release/tag for `v0.1-preview` if desired.
- [ ] Publish the article and community posts after the repository is public.

## Release principle

Do not wait for perfection.

v0.1 is intentionally a preview. The goal is to expose the protocol to real practitioners and improve it from real feedback.