# Skills

Each subdirectory here is one skill: a self-contained playbook for a
specific, recurring task (debugging a category of failure, running a
release checklist, a repo-specific workflow). Skills keep `CLAUDE.md`
from accumulating task-specific instructions it doesn't always need.

## Structure

```
.claude/skills/
  <skill-name>/
    SKILL.md        # required: instructions Claude loads when invoked
```

## Adding a skill

1. Copy `_template/SKILL.md` into a new `<skill-name>/` directory.
2. Fill in the frontmatter `description` — this is what triggers the
   skill, so make it specific about when to use it (and when not to).
3. Keep the instructions minimal: only what's needed to complete the
   task, no speculative options.
