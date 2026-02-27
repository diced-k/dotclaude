Create well-formatted commits with conventional commit messages.

## Usage

```
/commit
/commit feature/my-branch
/commit -f
/commit -p
/commit -f -p feature/my-branch
```

## Options

- `-f`: Force commit without running pre-commit hooks (passes `--no-verify` to git)
- `-p`: Push to remote after committing (runs `git push -u origin <branch>`)

## Arguments

`$ARGUMENTS` may contain a combination of `-f` flag and an optional branch name.

- Parse `-f` and `-p` flags from `$ARGUMENTS` if present
- Remaining argument is treated as a branch name
- If a branch name is given: run `git checkout <branch>` (create with `-b` if it does not exist)
- If no branch name: stay on the current branch

## Steps

1. Parse `$ARGUMENTS` for the `-f` and `-p` flags and optional branch name
2. If a branch name is provided, switch to that branch
3. Run `git status` and `git diff --staged` to review changes
4. If files are already staged, show them to the user and ask whether to commit only staged files or add more
5. If no files are staged, `git add` relevant files (exclude secrets like .env, credentials, etc.)
6. Analyze the diff to determine if multiple distinct logical changes are present
7. If multiple concerns are detected, suggest splitting into separate atomic commits
8. Craft a commit message following the rules below
9. Confirm the commit message with the user before committing
10. Execute the commit (with `--no-verify` if `-f` was given)
11. If `-p` was given, push to remote with `git push -u origin <current-branch>`

## Commit message rules

- Use Conventional Commits format: `type(scope): summary`
- type: one of feat, fix, refactor, docs, test, chore, ci, style, perf
- scope: optional. The module or component being changed
- summary: concise, imperative mood in English (e.g. add, fix, update)
- Present tense, imperative mood: write messages as commands (e.g. "add feature" not "added feature")
- Keep the first line under 72 characters
- Add a body separated by a blank line if further detail is needed

## Best practices

- **Check before you commit**: make sure linting passes, the build succeeds, and docs are up to date
- **Atomic commits**: one commit should represent one logical change
- **Break up large diffs**: when changes span multiple concerns, make separate commits

## When to split commits

Look for these signals that a diff should become multiple commits:

- **Unrelated areas**: changes touching separate parts of the codebase
- **Mixed intent**: features, bug fixes, and refactors bundled together
- **Different file types**: source code changes mixed with documentation or config updates
- **Independent units**: changes that are easier to review or revert on their own
- **Sheer volume**: a large diff that would be clearer as smaller pieces

## Important

- Do not create empty commits
- Always review the diff to ensure the message accurately reflects the changes
