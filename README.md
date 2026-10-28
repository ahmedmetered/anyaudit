# anyaudit

Multi-lens code review from the AI agent you already have.

Point it at a repository, a branch diff, a pull request, or a commit. It
detects the stack, reviews the code through the lenses that match (33
reference files: per-language guides for TypeScript, React, Vue, Python,
Django, FastAPI, Go, Java, Kotlin, C#, C++, C, PHP, NestJS, Dart, CSS and
cross-cutting guides for architecture, performance, code quality, and common
bugs), then **verifies every finding against the code before reporting**.
Optional fix loop drafts minimal patches for confirmed findings.

Adapted from [code-review-skill](https://github.com/awesome-skills/code-
review-skill) (MIT) by awesome-skills, with the phase discipline of
[adamsreview](https://github.com/adamjgmiller/adamsreview) (MIT) by Adam
Miller, repackaged as an agent-native skill: no plugin manager, no specific
CLI.

## Install

Copy `skill/` into your agent's skills folder (ZCode, Claude Code, Codex,
Cursor - any agent that reads `SKILL.md` files), or clone this repository
into it; the root `SKILL.md` makes it discoverable either way.

## Use

- "Review this repository"
- "Audit the diff on this branch"
- "Review PR #12 and draft fixes for the confirmed findings"

## The verification rule

Most AI review output is a list of guesses. anyaudit's Phase 3 re-reads the
code for every finding and drops what does not survive; the report only
carries findings with quoted evidence. Read-only by default; patches are
drafted only when you ask, one finding at a time, for your review.

## Files

```
skill/SKILL.md           the pipeline: scope, stack detection, lenses, verify, report, fix loop
skill/references/        33 lens files + checklists + review templates
```

## Credits and license

MIT. Review lens library adapted from
[code-review-skill](https://github.com/awesome-skills/code-review-skill) by
awesome-skills; phase discipline adapted from
[adamsreview](https://github.com/adamjgmiller/adamsreview) by Adam Miller.
Independent project; not affiliated with or endorsed by Anthropic or any
agent vendor.
