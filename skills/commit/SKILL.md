---
name: commit
description: Stage, commit, and push all changes as semantically grouped commits with clear titles.
disable-model-invocation: true
---

You are committing the user's changes. Follow these steps exactly:

## 1. Survey changes

Run `git status` and `git diff` (both staged and unstaged) to understand all modifications. Also run `git log --oneline -5` to see recent commit style.

## 2. Group changes into semantic commits

Analyze the changes and split them into logical, self-contained commits. Examples of good groupings:
- A refactor separated from a new feature
- Test updates separated from implementation changes
- Config/dependency changes separated from code changes
- Documentation changes on their own

If all changes are part of one cohesive unit, a single commit is fine. Don't over-split.

## 3. Create commits

For each semantic group:
1. Stage only the relevant files using `git add <file1> <file2> ...` (never `git add -A` or `git add .` unless everything belongs in one commit)
2. Commit with a concise, descriptive message. Use imperative mood (e.g., "Add user validation" not "Added user validation"). Keep the subject line under 72 characters.
3. Pass the message via heredoc:
   ```
   git commit -m "$(cat <<'EOF'
   Your commit message here
   EOF
   )"
   ```

## 4. Push

After all commits are created, push to the remote:
```
git push
```
If there is no upstream branch set, use `git push -u origin HEAD`.

## Rules

- **No attribution**: Never add `Co-authored-by`, `Signed-off-by`, or any other trailer attributing Claude/AI. Never use `--author` to set Claude as author. The commits must appear as the user's own work.
- **No hooks bypass**: Never use `--no-verify`. If a hook fails, fix the issue.
- **No amending**: Always create new commits. Never amend existing commits.
- **No skipping**: Do not skip or ignore any changed files — every modification must be included in exactly one commit.
- **Warn about secrets**: If you see files that likely contain secrets (`.env`, credentials, tokens), warn the user and skip those files.
