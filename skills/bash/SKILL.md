---
name: bash
description: Execute shell commands safely. Use for running scripts, installing packages, file system operations, and any task requiring shell access.
---

# Bash

Execute shell commands via the `bash` tool.

## Safety Rules

- Never run destructive commands (`rm -rf /`, `dd`, `mkfs`) without explicit user approval.
- Always use timeouts for long-running commands.
- Prefer `trash` over `rm` when available (recoverable > gone forever).
- Pipe large outputs through `head` or `tail` to avoid flooding context.
- Quote file paths that contain spaces.

## Patterns

### Run a command

```bash
bash("ls -la /path/to/dir")
```

### Chain commands

```bash
bash("cd /app && npm install && npm test")
```

### Check before acting

```bash
bash("which docker")  # verify tool exists before using it
```

### Capture output for analysis

```bash
bash("git log --oneline -20")
```

## Environment

- Working directory defaults to the vault path.
- Environment variables from the host are available.
- Commands run with the agent's user permissions.
