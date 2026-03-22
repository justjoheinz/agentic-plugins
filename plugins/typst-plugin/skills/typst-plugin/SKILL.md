---
name: typst-plugin
description: Guide for working with Typst projects. The hook auto-compiles on every edit; use this skill for manual compilation or troubleshooting.
---

# Typst Auto-Compile Plugin

This plugin installs a PostToolUse hook that automatically runs `typst compile <file>`
after every `Edit` or `Write` on a `.typ` file.

## Requirements

- `typst` must be installed and on `$PATH`
- `jq` must be installed and on `$PATH`

## Manual compilation

To compile a Typst file explicitly:

```bash
typst compile path/to/file.typ
```

## Troubleshooting

If compilation fails silently, run manually to see the full error output.
The hook suppresses errors (via `|| true`) to avoid blocking Claude — check
the status message in the sidebar for failures.
