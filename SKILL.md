---
name: anyaudit
description: >-
  Run a multi-lens code review on a repository, branch, pull request diff, or
  commit: detect the stack, review through architecture, quality, performance,
  bug-checklist, and stack-specific lenses from a 33-file reference library,
  verify every finding against the code before reporting, and optionally
  draft patches for confirmed findings. Use when the user asks to review
  code, audit a repo or diff, find bugs, or check a pull request.
---

# anyaudit

This file is the discovery entrypoint when the whole repository is cloned
into a skills folder. The canonical skill lives one level down.

**Read [skill/SKILL.md](skill/SKILL.md) and follow it as the pipeline.** The
lens library is in `skill/references/`.
