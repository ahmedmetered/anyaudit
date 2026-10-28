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

A multi-lens code review pipeline. One pass per lens, every finding verified
against the code before it reaches the report, and nothing changed without
the human saying so. The review lenses come from a 33-file reference library
(adapted from [code-review-skill](https://github.com/awesome-skills/code-
review-skill), MIT); the phase discipline is adapted from
[adamsreview](https://github.com/adamjgmiller/adamsreview) (MIT).

## Phases

### Phase 0: Scope

Establish what is under review: whole repository, a branch's diff, a pull
request's diff, or a single commit. For diffs, read the actual changed lines
and their surrounding context; for repositories, read enough of the codebase
to know what each file is for. Record the scope in the report header.

### Phase 1: Stack detection

Identify languages, frameworks, and architecture style from manifests and
code. This selects the lenses: `references/` holds per-stack review guides
(angular, react, vue, django, fastapi, go, java, kotlin, csharp, cpp, c, php,
nestjs, dart, css, typescript and more) plus cross-cutting lenses
(architecture, performance, code-quality, common-bugs, security-adjacent
checklists). Load only the lenses that match the detected stack, plus the
universal ones.

### Phase 2: Lens review

One pass per lens. Each lens produces findings with a stable ID (`AUD-n`),
the file and line range, the lens that found it, the code quoted as
evidence, and a severity proposal. A finding without quoted evidence does
not exist yet.

### Phase 3: Verification

Re-read the code for every finding and try to disprove it. Drop findings
that do not survive contact with the actual code, merge duplicates, and
assign final severity (critical / major / minor / nit). The verification
pass is the product: an unverified finding list is a guess list.

### Phase 4: Report

A `review.md` with: scope, stack detected, findings table (ID, severity,
location, evidence, why it matters, suggested fix), and the gate failures if
any were reported. Read-only: no code is changed in this phase.

### Phase 5: Fix loop (only on request)

For confirmed findings the candidate wants fixed: draft patches one finding
at a time, each as a minimal diff the human reviews and applies. Batch
related fixes, run the project's own tests where they exist, and never mix
an unrelated refactor into a fix.

## Rules

- Findings are verified or they are not reported. Recency of the tool does
  not make a guess true.
- Severity is argued from impact, not from how clever the finding sounds.
- The lens library guides attention; it does not replace reading the code.
- Style preferences are nits, not findings, unless the project's own
  conventions say otherwise.
