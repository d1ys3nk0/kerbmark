# Commit and dependency delivery conventions

Read when preparing commits or publishing shared dependencies. Follow the repository’s own approval and delivery workflow.

Use descriptive commit subjects of at most 50 characters, counting spaces and the complete prefix. Repositories with a maintained software, infrastructure or tooling codebase use semantic-version-compatible Conventional Commits, including documentation changes. Documents-only repositories use plain descriptive subjects. Determine the format from the owning repository's contents, not its directory or the current diff.

Keep commits scoped to completed atomic changes after required verification. Preserve other writers' work, including their staged changes; inspect the full intended diff before committing.

For implementation-only work on shared dependencies distributed as published releases, verify and commit shared changes locally; publication and dependent release-pin updates remain pending. Do not add consumer overrides to bridge an unpublished change. When publication is authorized, publish and confirm an immutable shared dependency release first, then update, verify, commit and deliver each consumer that needs the changed behavior. Assess each consumer independently; a shared release alone does not justify a bulk version bump. Respect narrower scope and separate deployment or infrastructure permissions.

Explicit [Git contract snapshots](../engineering/contract-snapshots.md) may instead pin a caller-selected local provider commit and be verified and committed without publication. This exception concerns contract snapshots, not unpublished package overrides; pushes and deployment retain separate authority.

## Message syntax

For codebase repositories, use [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

- Use `feat` for a new feature and `fix` for a bug fix. For other changes, use an accurate established type such as `docs`, `refactor`, `test`, `build`, `ci`, `perf`, `style`, or `chore`; an optional scope names the affected area.
- Describe the actual diff concisely. Commit each completed independently meaningful piece separately after its required checks instead of waiting for the whole task to finish or combining unrelated work.
- Mark breaking changes with `!` before the colon or a `BREAKING CHANGE: <explanation>` footer. Explain the break and migration in the body or footer, including when using `!`.
- Separate the optional body and footers with blank lines. Use the body for material intent or rationale and footers for applicable references or trailers.
