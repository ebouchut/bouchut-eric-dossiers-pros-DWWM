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
| `theme/` | Local `slidev-theme-learn-dev` theme: Catppuccin Latte tokens, layouts, page-number footer (see [theme/README.md](theme/README.md)) |
| `public/images/` | Screenshots and diagrams referenced as `/images/...` |
| `package.json` | Slidev CLI + `playwright-chromium` (required by the exporters) |
| `Makefile` | Wrappers around the npm scripts |

The deck uses the local theme by path (`theme: ./theme` in the headmatter) — a local
Slidev theme does not need to be published to npm. All colors go through the CSS design
tokens declared in [theme/styles/tokens.css](theme/styles/tokens.css).

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

## Publish to GitHub Pages

The slideshow is published online by the [`pages.yml`](../.github/workflows/pages.yml)
GitHub Actions workflow: it builds the SPA with the project-page base path
(`--base /bouchut-eric-dossiers-pros-DWWM/`) and deploys it to GitHub Pages.

- **URL:** <https://www.ericbouchut.com/bouchut-eric-dossiers-pros-DWWM/>
  (alias: <https://ebouchut.github.io/bouchut-eric-dossiers-pros-DWWM/>)
- **Trigger:** every push to `main` touching `diaporama/**`, or manually from the
  *Actions* tab (*workflow_dispatch*).
- **One-time setup:** repository *Settings > Pages > Build and deployment >
  Source: GitHub Actions*.

> Note: the published SPA embeds the presenter notes (anyone with the URL can read them
> through the `/presenter` and `/overview` views).
