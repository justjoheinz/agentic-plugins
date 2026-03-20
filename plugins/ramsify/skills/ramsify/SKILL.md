---
name: ramsify
description:
  Guide for redesigning a web UI according to Dieter Rams' ten design principles.
  Use this when asked to ramsify, redesign, or clean up a project's UI.
---

Redesign the current project's UI according to Dieter Rams' ten principles, applied to web interfaces. Work through each area below in sequence. Read the relevant files before making changes. Preserve all functionality.

---

## 1. Audit first

Read the main stylesheet, layout file, and a representative sample of components. Identify:
- All color values in use (especially saturated accent colors beyond one)
- Icon usage inside labeled buttons
- Font declarations
- Border-radius and shadow values
- Layout spacers implemented as `&nbsp;`, empty elements, or fixed pixel hacks
- Section/card titles and their typographic treatment
- Interactive element states (focus, active, hover)

Report the findings as a short list before making any changes. Ask for confirmation to proceed.

---

## 2. Color palette — one accent, neutral everything else

**Principle: Good design is as little design as possible. Omit every component that is not necessary.**

Apply this palette (adapt values to suit the project's existing neutral tone):

| Role | Light | Dark |
|---|---|---|
| Page background | `#F5F4EF` warm off-white | `#1A1A1A` |
| Card / surface | `#FFFFFF` | `#242424` |
| Modal | `#FFFFFF` | `#242424` |
| Inset / info box | `#EFEFEB` | `#2E2E2E` |
| Primary text | `#1A1A1A` | `#E8E7E0` |
| Secondary text | `#6A6A66` | `#8A8A82` |
| Border | `#D4D3CC` | `#383836` |
| Input underline | `#9E9E98` | `#555550` |
| **Single accent** | `#E8420A` Braun orange | same |
| Accent subtle bg | `#FFF5F2` | `#2A1A14` |
| Nav / footer bg | `#1A1A1A` anthracite | `#111111` |
| Face-down card | `#3C3C3C` flat dark | same |

Rules:
- The accent color appears in exactly one semantic role per interaction surface: the primary action button, focus rings, selected states. Never for identity, status labels, or decoration.
- Status colors (error, warning, success) use desaturated values: green `#4A7C4A`, red `#C0301A`. They are not the accent.
- Remove all second accent colors (teal, indigo, purple, blue used as button colors).

---

## 3. Typography

**Principle: Good design makes a product understandable.**

- Load **IBM Plex Sans** via `next/font/google` (or equivalent for the stack) with weights 400, 500, 600. Apply via CSS variable `--font-ibm-plex-sans`.
- Override any framework-injected font (e.g., Materialize's Roboto) explicitly on `body, input, button, select, textarea`.
- Introduce a `.section-label` utility class for all card/panel headings:
  ```css
  .section-label {
    display: block;
    font-size: 0.6875rem;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--color-text-secondary);
    margin-bottom: 1rem;
  }
  ```
  Replace large framework card-title headings with this class. Section labels are instrument markings, not headings.
- Use `font-weight: 500` for labels, `400` for body, `600` only for numerical data that must read at a glance.

---

## 4. Shape language

**Principle: Good design is thorough down to the last detail.**

- Border-radius: `2px` everywhere. Remove all `4px`, `8px`, `rounded-*` values.
- Shadows: remove all `box-shadow` from cards and surfaces. Replace with `1px solid var(--color-border)`.
- No gradients. Flat fills only.

---

## 5. Semantic button classes

Replace framework color utilities on buttons with three semantic classes:

```css
/* Primary — dark fill */
.btn-primary { background: #1A1A1A; color: #F5F4EF; border-radius: 2px; box-shadow: none; }
.btn-primary:hover { background: #333333; }
.btn-primary:disabled { background: var(--color-border); color: var(--color-text-secondary); }

/* Accent — single action per screen (e.g. Reveal) */
.btn-accent { background: var(--color-accent); color: #fff; border-radius: 2px; box-shadow: none; }
.btn-accent:hover { background: #C93608; }
.btn-accent:disabled { background: var(--color-border); color: var(--color-text-secondary); }

/* Secondary — bordered, transparent */
.btn-secondary { background: transparent; border: 1px solid var(--color-border); color: var(--color-text-primary); border-radius: 2px; box-shadow: none; }
.btn-secondary:hover { background: var(--color-bg-info-box); }
```

Apply: primary actions → `.btn-primary`, the single highest-priority action per screen → `.btn-accent`, secondary/cancel actions → `.btn-secondary`.

---

## 6. Icons in buttons

**Principle: Good design is honest.**

Remove Material/Heroicon/FontAwesome icons from any button that already has a text label. The text is the affordance. Icons alongside labels are decoration.

Keep icons only when:
- The icon IS the entire label (theme toggle, play/pause controls)
- The icon provides non-redundant state information (copied ✓, connection status dot)
- The interface is so space-constrained that text is not shown (icon-only nav items)

---

## 7. Focus and active states — kill all teal

Framework defaults (Materialize, Bootstrap, Tailwind) inject teal, blue, or purple focus rings. Remove all of them:

```css
*:focus { outline: none; }
*:focus-visible { outline: 2px solid var(--color-accent); outline-offset: 2px; }

/* Accent button: white ring to stay visible on orange */
.btn-accent:focus-visible { outline: 2px solid #fff; outline-offset: 2px; }

/* Active state: mechanical depression, no color */
.interactive-element:active { transform: translateY(0); background-color: var(--color-bg-info-box); }
```

Checkboxes, radio buttons, and select elements styled by the framework should have their checked/selected color overridden to `var(--color-accent)`.

---

## 8. Interactive card grids (e.g. card selectors)

Replace card-in-a-div patterns with plain `<button>` elements:

```css
.card-btn {
  appearance: none;
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: 2px;
  aspect-ratio: 3 / 4;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  font-weight: 500;
  cursor: pointer;
  transition: transform 0.15s, border-color 0.15s;
}
.card-btn:hover:not(:disabled) { transform: translateY(-2px); border-color: var(--color-border-input); }
.card-btn:active:not(:disabled) { transform: translateY(0); }
.card-btn.selected { border: 2px solid var(--color-accent); background: var(--color-accent-subtle); color: var(--color-accent); transform: translateY(-2px); }
.card-btn:disabled { opacity: 0.35; cursor: not-allowed; }
```

Use a fixed column grid (`repeat(N, 1fr)`) rather than `auto-fit` — systematic, not fluid.

---

## 9. List / collection overrides

Framework list components draw a box border around the entire list. Use only horizontal rules:

```css
.collection { border: none; border-top: 1px solid var(--color-border); }
.collection .collection-item { border-bottom: 1px solid var(--color-border); border-left: none; border-right: none; border-radius: 0; }
```

For indicating the "current" or "selected" row: use a left-border rail in `--color-text-primary` plus a visible background tint (`--color-bg-info-box`). Do not use the accent color for identity.

```css
.list-item-current {
  background-color: var(--color-bg-info-box) !important;
  border-left: 3px solid var(--color-text-primary) !important;
  padding-left: calc(1rem - 3px) !important;
}
```

---

## 10. Layout spacers

Replace all `&nbsp;`, zero-width spaces, and invisible placeholder elements used to prevent layout shift. Use `min-height` on the container instead:

```css
.status-line { min-height: 1.5rem; font-size: 0.875rem; color: var(--color-text-secondary); }
```

---

## 11. Input focus

Override the framework's default focus underline color:

```css
.input-field input:focus:not([readonly]) {
  border-bottom-color: var(--color-accent) !important;
  box-shadow: 0 1px 0 0 var(--color-accent) !important;
}
.input-field input:focus:not([readonly]) + label { color: var(--color-accent) !important; }
```

---

## Verification checklist

After applying changes, confirm:

- [ ] One accent color visible in the entire UI (`#E8420A` or equivalent)
- [ ] No teal, indigo, purple, or blue on interactive elements
- [ ] No icons inside labeled buttons
- [ ] Section headers rendered as small uppercase tracking labels
- [ ] Cards have border, no shadow
- [ ] All border-radius values are `2px`
- [ ] No gradients
- [ ] Focus ring is orange (or white on orange bg) and appears only on keyboard navigation
- [ ] Active state depresses without color change
- [ ] Current-user / selected-row identified by left border rail + neutral tint, not accent color
- [ ] Font is IBM Plex Sans (or geometric grotesque equivalent) throughout
- [ ] No `&nbsp;` spacer elements
