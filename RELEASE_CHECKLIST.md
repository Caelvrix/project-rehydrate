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
- [x] Change repository visibility from Private to Public (GitHub connector verified PUBLIC on 2026-09-26).
- [x] Create a GitHub release/tag for `v0.1-preview` (verified published pre-release).
- [ ] Publish the article and community posts after the repository is public.

## Public launch verification — 2026-09-26

- `Caelvrix/project-rehydrate`: PUBLIC, default branch `main` (verified from live GitHub repository metadata).
- `Caelvrix/community-hub`: PRIVATE (verified separately).
- Commit attribution to `kwadolia` explicitly accepted by project owner.
- `v0.1-preview` release/tag: PUBLISHED and independently verified. Release URL: https://github.com/Caelvrix/project-rehydrate/releases/tag/v0.1-preview . GitHub release ID: 397169707; `prerelease=true`, `draft=false`, target `main`.
- External launch articles/posts: not yet published.

### Next exact action

Release verified. Publish the prepared article and community posts thoughtfully, using the canonical release URL. Then return to the Sales Performance POC. Keep the release tag as a fixed snapshot; later checklist updates to `main` do not alter that tag.

## Release principle

Do not wait for perfection.

v0.1 is intentionally a preview. The goal is to expose the protocol to real practitioners and improve it from real feedback.

## DEV publication checkpoint — 2026-09-26

- Publication: the first Caelvrix DEV article, **When Your AI Forgets the Project: How We Built a Continuity Protocol for Long-Running IT Work**.
- Canonical article URL supplied by Kaval: https://dev.to/caelvrix/when-your-ai-forgets-the-project-how-we-built-a-continuity-protocol-for-long-running-it-work-1l0
- Evidence: user screenshots show DEV's published article (not the earlier Unpublished Post draft), including the concluding **Try Project Rehydrate** section and its repository, five-minute guide and v0.1 release links. User provided the exact address.
- Verification limitation: an independent external fetch of the DEV article returned a cache miss; do not claim page content was independently fetched.
- Status: GitHub repo PUBLIC and v0.1 preview release independently verified earlier. DEV article publication supported by user-provided screenshot and URL.
- This section supersedes the older snapshot line above that states no external articles were published. That line is preserved solely as its dated historical state.

### Exact next action

Optionally add a Caelvrix cover image through DEV's Edit action, then distribute the published article to a small number of relevant communities using tailored, rule-compliant posts; do not claim submissions have occurred until confirmed. Preserve the article URL, any posts, feedback and resulting next actions in a later checkpoint. Then return to the Sales Performance POC.

### Do not do yet

- Do not change the existing `v0.1-preview` release tag or rewrite Git history.
- Do not publish any employer-specific infrastructure, data, screenshots or private context.
- Keep `Caelvrix/community-hub` PRIVATE.
