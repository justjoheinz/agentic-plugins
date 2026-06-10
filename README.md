# agentic-plugins

A Claude Code plugins marketplace by [justjoheinz](https://github.com/justjoheinz).

## Plugins

### ramsify

Redesign a web UI according to Dieter Rams' ten design principles: single accent color, IBM Plex Sans typography, 2px border-radius, no shadows, semantic button classes, icon discipline, and keyboard focus states.

**Source:** `plugins/ramsify`

### haskell-plugin

Haskell development support with HLS (Haskell Language Server) LSP integration and a skill for working with Haskell projects using GHC and Stack. Covers Stack/hpack, GHCi, RIO prelude, lenses, `hie.yaml` cradle configuration, HLint, Fourmolu, and common GHC flags.

**Source:** `plugins/haskell-plugin`

## Structure

```
agentic-plugins/
  .claude-plugin/
    marketplace.json
  plugins/
    ramsify/
      .claude-plugin/
        plugin.json
      skills/
        ramsify/
          SKILL.md
  LICENSE
  README.md
```

## License

MIT
