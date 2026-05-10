# Skill: github-pr-workflow

---
name: github-pr-workflow
description: "Branch → commit → push → open PR → CI → merge. Uses gh CLI. Short, conventional-commit-friendly."
tags: [github, pr, git, workflow]
version: 1.0.0
---

# github-pr-workflow

Use when pushing a change to a GitHub repo you don't own directly, or when the repo requires PRs for merges.

## When NOT to use
- Solo repo where you push directly to main (use plain `git push`)
- Emergency hotfix where PR review is waived (document the bypass)

## Steps

### 1. Branch from a clean base

```bash
git fetch origin
git checkout -b <topic-branch> origin/main
```

Branch name convention: `fix/<short-desc>`, `feat/<short-desc>`, or `chore/<short-desc>`.

### 2. Commit in logical chunks

Conventional commits:

```bash
git add <only the relevant files>
git commit -m "fix: handle null results from X endpoint"
```

Rules:
- One logical change per commit
- First line ≤ 72 chars, imperative mood
- Never `git add .` without checking `git status` first

### 3. Push and open PR

```bash
git push -u origin <topic-branch>
gh pr create \
  --title "<type>: <short description>" \
  --body "<what changed, why, how tested>" \
  --base main
```

PR body template:

```markdown
## What
Short description of the change.

## Why
Link to issue or problem statement.

## How tested
Commands run, test output, manual verification.

## Blast radius
What else this could affect, and why I think it's safe.
```

### 4. Wait for CI

```bash
gh pr checks --watch
```

If CI fails, read the log, fix, push. Don't merge with red checks.

### 5. Merge

```bash
gh pr merge --squash --delete-branch
```

Squash unless the repo convention is rebase. Delete the branch after merge.

## Pitfalls

- **Branching from stale main.** Always `git fetch && git checkout -b ... origin/main`.
- **Pushing to main by accident.** Check `git branch --show-current` before `git push`.
- **Force-pushing shared branches.** Never. Open a fixup PR instead.
- **Merging with red CI.** Don't override unless you have explicit authorization and a written reason.
- **Adding secrets to the PR body.** PR bodies are public on public repos.

## Verification

- [ ] Branch created from fresh `origin/main`
- [ ] PR opened with title, body, base set
- [ ] CI is green
- [ ] Branch deleted after merge
