---
name: tinymist
description: Use tinymist to compile, preview, and format Typst documents. Covers compile options (PDF/SVG/PNG/HTML), live browser preview, and LSP features.
---

# Tinymist Skill

[Tinymist](https://github.com/Myriad-Dreamin/tinymist) is a full-featured Typst language server and toolchain. It bundles its own Typst compiler and adds LSP, preview, formatting, and linting on top.

Install: `brew install tinymist`

---

## Compile

```bash
tinymist compile path/to/file.typ
```

Output format is selected by the output file extension (defaults to PDF):

| Output format | Example flag |
|---------------|--------------|
| PDF (default) | `tinymist compile file.typ` |
| SVG | `tinymist compile file.typ output.svg` |
| PNG | `tinymist compile file.typ output.png` |
| HTML | `tinymist compile file.typ output.html` |
| Markdown | `tinymist compile file.typ output.md` |
| Plain text | `tinymist compile file.typ output.txt` |

---

## Live preview

```bash
tinymist preview path/to/file.typ
```

Opens a live browser preview at `http://127.0.0.1:23635`. The preview hot-reloads on every file save.

Useful flags:
- `--port <PORT>` — change the preview server port (default: `23635`)
- `--partial-rendering` — only re-render changed pages (faster for large documents)

---

## When to compile vs. preview

| Situation | Use |
|-----------|-----|
| Generating a final PDF/SVG/PNG artifact | `tinymist compile` |
| Iterating on layout, content, or styling | `tinymist preview` |
| CI / automated build pipeline | `tinymist compile` |

---

## LSP features (automatic — no action needed)

When the plugin is installed, `tinymist lsp` starts automatically and provides:

- Semantic syntax highlighting
- Go-to-definition and find-references
- Hover documentation
- Inlay hints
- Typstyle-based code formatting (on save)
- Linting / diagnostics

These work in any editor with LSP support. No manual invocation is needed.

---

## Troubleshooting

**`command not found: tinymist`**
Install via Homebrew: `brew install tinymist`. Confirm with `tinymist probe`.

**Preview opens but shows a blank page**
Check the terminal output for compile errors. Run `tinymist compile file.typ` manually to see full diagnostics.

**Compile errors are silent in the hook**
The auto-compile hook uses `|| true` to avoid blocking Claude. If output is unexpected, run `tinymist compile path/to/file.typ` directly in the terminal to see full error output.
