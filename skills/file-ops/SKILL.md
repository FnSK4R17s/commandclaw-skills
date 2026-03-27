---
name: file-ops
description: Read, write, and manage files in the workspace. Use for creating, editing, searching, and organizing files and directories.
---

# File Operations

Read and write files using the `file_read` and `file_write` tools.

## Reading Files

```
file_read("path/to/file.md")
```

- Always read a file before modifying it.
- For large files, note that output may be truncated.

## Writing Files

```
file_write("path/to/file.md", "content here")
```

- Creates parent directories automatically.
- Overwrites existing content — read first if you need to preserve parts.

## Memory Files

Use `memory_read` and `memory_write` for vault memory files specifically:

```
memory_read("2026-03-27.md")          # Read a daily note
memory_write("2026-03-27.md", "...")  # Write and git-commit
```

Memory writes are automatically committed to Git for audit trail.

## Patterns

### Search for files

```bash
bash("find . -name '*.md' -type f")
```

### Search file contents

```bash
bash("grep -r 'pattern' --include='*.md' .")
```

### Create a directory structure

```bash
bash("mkdir -p path/to/new/dir")
```

## Rules

- Never read or write files outside the allowed workspace directories.
- Prefer editing existing files over creating new ones.
- Use markdown for all vault files — it's forgiving and human-readable.
