# DWWM Project Dossier — sources

Markdown sources for the **Dossier Projet** (project dossier) and the **Résumé** (one-page
summary) for the *Développeur Web et Web Mobile* professional title (DWWM, RNCP37674). The
jury-facing PDFs are generated at the repository root: `bouchut-eric-dossier-projet.pdf` and
`bouchut-eric-resume.pdf`.

## Contents

| File | Purpose |
|---|---|
| `dossier-projet.md` | Project dossier source (French) |
| `resume.md` | One-page summary source (French) |
| `metadata.yaml` | Pandoc metadata for the dossier (title, margins, language) |
| `metadata-resume.yaml` | Pandoc metadata for the summary |
| `images/` | Screenshots and diagrams (MCD, MPD, mockups) |
| `Makefile` | PDF generation |

> The documents themselves are written in French (certification requirement); only this
> README and the build files are in English.

## Requirements (macOS)

```bash
brew install pandoc typst
```

- `pandoc` >= 3.1.7 (the Typst engine is required) — tested with pandoc 3.10.
- `typst` — tested with typst 0.15.

## Regenerate the PDFs

```bash
cd dossier-projet
make          # builds both PDFs at the repository root
make clean    # removes the generated PDFs
```

Equivalent manual command:

```bash
pandoc dossier-projet.md --pdf-engine=typst --metadata-file=metadata.yaml \
  --toc --number-sections --resource-path=.:images \
  -o ../bouchut-eric-dossier-projet.pdf
```
