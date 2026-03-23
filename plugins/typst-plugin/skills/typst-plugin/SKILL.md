---
name: typst-plugin
description: Guide for working with Typst projects via tinymist. The hook auto-compiles on every edit; see the tinymist skill for preview, formatting, and advanced compile options.
---

# Typst Auto-Compile Plugin

This plugin installs a PostToolUse hook that automatically runs `tinymist compile <file>`
after every `Edit` or `Write` on a `.typ` file.

## Requirements

- `tinymist` must be installed and on `$PATH` (`brew install tinymist`)
  - tinymist bundles its own Typst compiler — no separate `typst` install needed
- `jq` must be installed and on `$PATH`

## Manual compilation

To compile a Typst file explicitly:

```bash
tinymist compile path/to/file.typ
```

For preview, format options, and the live preview server, see the **tinymist** skill.

## Troubleshooting

If compilation fails silently, run manually to see the full error output.
The hook suppresses errors (via `|| true`) to avoid blocking Claude — check
the status message in the sidebar for failures.
