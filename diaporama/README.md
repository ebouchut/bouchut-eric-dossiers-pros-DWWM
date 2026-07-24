# DWWM oral-defense slideshow — Slidev sources

[Slidev](https://sli.dev) sources of the oral-defense slideshow for the *Développeur Web et
Web Mobile* professional title (DWWM, RNCP37674). The jury-facing files are generated at the
repository root: `bouchut-eric-diaporama.pdf` and `bouchut-eric-diaporama.pptx`.

> The slides themselves are written in French (certification requirement); only this README
> and the build files are in English.

## Contents

| File | Purpose |
|---|---|
| `slides.md` | Slide deck source (French), one block per slide, presenter notes as HTML comments |
| `style.css` | Catppuccin Latte palette over the Slidev `default` theme |
| `public/images/` | Screenshots and diagrams referenced as `/images/...` |
| `package.json` | Slidev CLI + `playwright-chromium` (required by the exporters) |
| `Makefile` | Wrappers around the npm scripts |

## Requirements

- Node.js **>= 20** (any version pinned with `fnm` works).
- One-time setup (downloads the export browser, ~150 MB):

```bash
npm install
```

## Present (recommended for the defense)

```bash
make dev        # or: npm run dev
```

Then open <http://localhost:3030>. **Presenter mode** (notes + timer + next slide) is at
<http://localhost:3030/presenter/1> — press `o` for the slide overview, `d` for dark mode.

## Export the jury-facing files

```bash
make pdf        # => ../bouchut-eric-diaporama.pdf
make pptx       # => ../bouchut-eric-diaporama.pptx  (slides as images, NOT editable)
make html       # => dist/  (standalone SPA, gitignored)
make all        # all three
```

The PPTX export embeds each slide as an image: use the live `make dev` presentation (or the
PDF) rather than PowerPoint to actually present.
