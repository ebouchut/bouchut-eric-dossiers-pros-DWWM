# slidev-theme-learn-dev

Local (unpublished) [Slidev](https://sli.dev) theme for the learn-dev slide decks:
Catppuccin **Latte** palette, token-based styling, and a page-number footer.

## Usage

Reference it by **path** in the deck headmatter — a local theme needs no npm publishing:

```yaml
---
theme: ./theme
---
```

## Contents

| File | Purpose |
|---|---|
| `styles/tokens.css` | Design tokens: raw palette (`--latte-*`) + semantic aliases (`--ld-*`) |
| `styles/base.css` | Component styling built exclusively on the semantic tokens |
| `styles/layouts.css` | Layout typography, copied from `@slidev/theme-default` (MIT) |
| `layouts/cover.vue`, `layouts/section.vue` | Copied from `@slidev/theme-default` (MIT) for rendering parity |
| `global-top.vue` | Page-number footer (`current / total`, hidden on the cover) |
| `package.json` | Theme metadata + default fonts (same as `@slidev/theme-default`) |

## Dark mode

The theme ships **both Catppuccin flavors**: Latte (light) and Mocha (dark). Slidev
toggles the `dark` class on `<html>` (`colorSchema: auto` follows the system preference;
press `d` to toggle manually — the choice is pinned in `localStorage` under
`slidev-color-schema` until toggled back). Only the **semantic tokens** are remapped under
`html.dark`; every rule built on them adapts for free. Mermaid diagrams keep their light
color scheme and sit on a light chip in dark mode. **Exports (PDF/PPTX) always render in
light mode** — Slidev forces it unless `--dark` is passed.

## Layout coverage

All [built-in Slidev layouts](https://sli.dev/builtin/layouts) render with the theme
tokens. See [example.md](example.md) for one slide per layout
(`npm exec slidev theme/example.md` to browse it).

| Layouts | Styling |
|---|---|
| `cover`, `intro`, `section` | Gradient wash, bold mauve `h1`, mauve regular subtitle (`h2`) |
| `quote` | Gradient, centered large italic text framed by French guillemets |
| `fact`, `statement`, `end` | Gradient; `end` is centered and shows no page number |
| `two-cols`, `two-cols-header` | Column gap (`two-cols` renders the `two-columns` class) |
| `default`, `center`, `full`, `image`, `image-left`, `image-right`, `iframe-left`, `iframe-right` | Inherit the base token styling (background, text, headings) |
| `iframe`, `none` | Intentionally unstyled (no `.slidev-layout` root to hook into) |

## Design rules

- Layouts and components reference **semantic tokens only** (`--ld-*`); the raw palette
  (`--latte-*`) is mapped to semantics in one place, so swapping the palette is a
  one-block change.
- Tokens are declared on `:root` on purpose: global layers (like the footer) live
  **outside** `.slidev-layout` and would not resolve tokens scoped to it.
- All other layouts (`default`, `two-cols`, `full`, `center`…) come from the Slidev
  client built-ins.
