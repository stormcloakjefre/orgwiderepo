---
name: pr-review-checklist
description: Use before opening a pull request, or when asked to review a diff/PR for quality. Applies the minimalism rules in CLAUDE.md as a concrete checklist. Not for triaging bugs (see debugging-playbook) or for CI/merge mechanics on an already-open PR.
---

# PR / Code Review Checklist

## When to use

- About to open a PR: run this checklist against your own diff first.
- Asked to review someone else's PR or diff for quality.

## When not to use

- Debugging a reported failure — use `debugging-playbook` instead.
- Driving an already-open PR through CI/merge — that's operational, not a
  quality review.

## Checklist

Work through the diff (`git diff` against the PR's base) and check each:

1. **Scope** — does every changed file serve the PR's stated purpose? A
   bug fix carrying an unrelated rename or refactor should be split out.
2. **Minimalism** — any new dependency, wrapper, abstraction, or config
   option that isn't required by this change? Cut it (see `CLAUDE.md`).
   Three similar lines beats a helper used once.
3. **Dead code** — anything commented out, gated behind an unused flag,
   or a half-finished branch? Delete or finish it.
4. **Comments** — do any explain *what* the code does instead of *why*?
   Remove the former; keep only non-obvious rationale.
5. **Error handling** — is validation only at real system boundaries
   (user input, external APIs), or is there defensive code for cases
   that can't happen? Trim the latter.
6. **Tests** — does the change have coverage proportional to its risk?
   A behavior change with no test is a red flag; a config/docs-only
   change doesn't need one.
7. **Naming** — do names make comments unnecessary? Confusing names are
   a correctness risk, not just style.

## Output

- If reviewing your own diff before opening a PR: fix what you find,
  don't just note it.
- If reviewing someone else's PR: report findings with file:line
  references, ranked by severity, distinguishing "must fix" from "nit."
