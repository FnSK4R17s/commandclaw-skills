---
name: github
description: Interact with GitHub repositories using the gh CLI. Use for creating PRs, managing issues, reviewing code, and repository operations.
---

# GitHub

Interact with GitHub via the `gh` CLI and `git`.

## Prerequisites

- `gh` CLI installed and authenticated
- `GH_TOKEN` environment variable set (preferred for non-interactive auth)

## Git Push Auth

When pushing to GitHub, avoid interactive username/password prompts:

```bash
# Use GH_TOKEN for non-interactive push
GIT_TERMINAL_PROMPT=0 git push -u origin <branch>
```

If that fails, use the askpass pattern:

```bash
cat >/tmp/git-askpass-gh.sh <<'EOF'
#!/usr/bin/env bash
case "$1" in
  *Username*) echo "x-access-token" ;;
  *Password*) echo "$GH_TOKEN" ;;
  *) echo "" ;;
esac
EOF
chmod 700 /tmp/git-askpass-gh.sh
GIT_ASKPASS=/tmp/git-askpass-gh.sh GIT_TERMINAL_PROMPT=0 git push -u origin <branch>
```

## Common Operations

### Create a PR

```bash
gh pr create --title "Title" --body "Description"
```

### List open issues

```bash
gh issue list --state open
```

### Review a PR

```bash
gh pr view <number>
gh pr diff <number>
gh pr review <number> --approve
```

### Clone a repo

```bash
gh repo clone owner/repo
```

## Rules

- Always create feature branches — never push directly to main.
- Write clear, concise commit messages.
- Include closing keywords in PR descriptions (`Fixes #123`).
- Never print token values in logs.
