---
name: debugging-playbook
description: Use when asked to fix a bug, error, crash, or unexpected behavior with little upfront context (e.g. "fix this", "why is X broken", a stack trace, a failing test). Not for feature requests, refactors, or CI/PR review — see the PR review skill for those.
---

# Debugging Playbook

## When to use

- The user reports something broken: an error message, a stack trace, a
  failing test, or behavior that doesn't match expectations.
- The root cause isn't yet known.

## When not to use

- The task is a new feature, refactor, or design question — no bug to
  isolate yet.
- The user already knows the root cause and just wants the fix written.

## Steps

1. **Reproduce first.** Before touching code, find or write the smallest
   case that triggers the bug (a failing test, a repro script, a specific
   input). If you can't reproduce it, say so — don't guess at a fix.
2. **Read the actual error**, not just its headline. Trace it to the
   originating line, not the first frame that looks familiar.
3. **Isolate the cause** by narrowing, not by reading the whole codebase:
   bisect with `git log`/`git bisect` if the bug is a regression, add a
   targeted log/print or use a debugger, or comment out code paths to
   confirm which one is responsible.
4. **Form one root-cause hypothesis** and verify it before writing a fix.
   A fix based on a guess that happens to make symptoms go away is not a
   fix — confirm the mechanism.
5. **Fix the root cause**, not the symptom. Don't add a try/catch or a
   null check that hides the failure without addressing why it happened,
   unless the boundary genuinely calls for defensive handling (see
   `CLAUDE.md`'s rule on validating only at real system boundaries).
6. **Verify with the original repro** plus the existing test suite. Add a
   regression test for the specific case that broke, if the codebase has
   tests.
7. **Keep the fix minimal.** Don't refactor surrounding code while fixing
   a bug — file that separately if it's worth doing.
