# Org-wide Development Rules

This file is synced to other repositories (see `sync.yml`). Keep it
generic — nothing project-specific belongs here.

## Minimalism (YAGNI)

- Build only what the current task requires. Don't add abstractions,
  config options, or extension points for hypothetical future needs.
- Prefer editing existing files over creating new ones. Prefer a few
  duplicated lines over a premature abstraction shared by only two callers.
- No half-finished implementations, feature flags, or backwards-compat
  shims "just in case" — change the code directly instead.
- Don't add error handling, retries, or validation for cases that can't
  happen. Validate only at real system boundaries (user input, external
  APIs, network calls).
- Before adding a third-party package, check whether the standard library
  or an existing dependency already covers it. A new dependency must earn
  its place — justify it in the PR description.
- Don't wrap a library in your own abstraction unless you're using it in
  more than one place or hiding a real implementation detail. A thin
  pass-through wrapper is bloat, not architecture.
- Delete dead code instead of commenting it out or gating it behind a flag.

## Code Review Expectations

- A bug fix should not carry unrelated refactors, renames, or cleanup.
- Three similar lines are better than a helper function used once.
- If you can't explain why a piece of code exists in terms of the current
  task, remove it.

## Comments

- Default to no comments. Only write one when the *why* isn't obvious
  from the code itself (a non-obvious constraint, a workaround for a
  specific bug, a subtle invariant).
- Never describe *what* the code does — that's what naming is for.

## Workflow Playbooks

Repo-specific and task-specific workflows live under `.claude/skills/`.
Add a new skill there instead of growing this file — this file stays
limited to rules that apply to every repository.
