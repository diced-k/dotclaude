# dotclaude

A collection of reusable `.claude/commands` for use across projects.

## Conventions

- All command files and commit messages must be written in English
- Commands use `$ARGUMENTS` for user input
- Short flags preferred (e.g. `-f`, `-p`) over long options

## Markdown style

Follow these rules for all `.md` files:

- `commands/*.md` files must start with a plain-text description on line 1 (no `#` heading), as required by the `.claude/commands` spec
- Do not skip heading levels (`##` → `###`)
- Add blank lines before and after headings, lists, and code blocks
- End the file with a single trailing newline
