# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Claude Code plugin marketplace. Each plugin lives under `plugins/<name>/` and is registered in the root `.claude-plugin/marketplace.json`. Plugins can ship any combination of:

- **Skills** — `skills/<name>/SKILL.md` (frontmatter + markdown, loaded into Claude's context)
- **Hooks** — `hooks/hooks.json` (PostToolUse / PreToolUse shell commands)
- **LSP** — `.lsp.json` at the plugin root (language server definitions)
- **Metadata** — `.claude-plugin/plugin.json` (name, version, description, keywords)

## Adding a new plugin

1. Create `plugins/<name>/` with `.claude-plugin/plugin.json`
2. Add skills, hooks, and/or `.lsp.json` as needed
3. Register the plugin in `.claude-plugin/marketplace.json` (add an entry to the `plugins` array)
4. Update `README.md` to document the new plugin

## Plugin file conventions

- `plugin.json` version follows semver; bump the minor version for new features, patch for fixes
- `marketplace.json` descriptions must stay in sync with `plugin.json` descriptions
- LSP definitions belong at the plugin root (`.lsp.json`), not inside `.claude-plugin/`
- Skill filenames: `skills/<skill-name>/SKILL.md` — the directory name becomes the skill name
- Hook commands must be safe to fail silently (`|| true`) so they never block Claude

## Commit messages

- Prefix with a JIRA key, `Merge`, or `noticket:` (enforced by pre-commit hook)
- Do not add a `Co-Authored-By:` trailer
