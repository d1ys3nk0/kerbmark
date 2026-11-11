# Concurrent repository edits

Read before editing or staging changes in a shared checkout.

Before implementation, inspect the current branch, `git status --porcelain`, the index and untracked files. Identify the task's expected paths and compare them with existing changes. Unrelated changes in other files do not block work or require confirmation. Stop and coordinate only where the task needs to edit a file already containing changes outside the task or overwrite an existing untracked file; continue independent work. Never reset, stash or commit another writer's changes, or create a worktree to bypass an overlap.

Recheck overlap when scope expands and before writing or staging. If another session changed the same file, preserve its work and coordinate the shared edit; starting first does not establish exclusive ownership.

Commit only the task's own paths or hunks. Do not defer a finished commit until other sessions finish or include their work. Never use `git add .` or `git add -A`; stage explicit owned paths. If unrelated staged changes exist, use an isolated index and preserve the original index. Before committing, inspect the complete intended diff, ownership and secrets. Target-repository verification, review and publication requirements remain mandatory. Follow the repository’s approval and delivery workflow for external delivery.
