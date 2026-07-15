# DWWM oral-defense slideshow — source

Markdown source for the oral-defense slideshow (35-minute presentation) of the DWWM
professional title (RNCP37674). The deliverables are generated at the repository root:
`bouchut-eric-diaporama.pptx` (editable) and `bouchut-eric-diaporama.pdf` (jury handout).

> The slides are written in French (certification requirement); this README, the Makefile
> and the build files are in English. Speaker notes are embedded per slide (`::: notes`).

## Contents

| File | Purpose |
|---|---|
| `diaporama.md` | Slide source (French), with speaker notes |
| `reference.pptx` | Pandoc reference document styled with the **Catppuccin (Latte)** palette |
| `images/` | Figures reused from the project dossier (MCD, MPD, mockups) |
| `Makefile` | Slide generation |

## Requirements (macOS)

```bash
brew install pandoc          # tested with pandoc 3.10
```

- **LibreOffice** (for the PDF export) — the `soffice` binary is expected at
  `/Applications/LibreOffice.app/Contents/MacOS/soffice`.

## Regenerate

```bash
cd diaporama
make          # builds the .pptx then the .pdf at the repository root
make pptx     # builds only the editable .pptx
make clean    # removes the generated files
```

The `.pptx` is fully editable: open it in Keynote, PowerPoint, or LibreOffice Impress to
refine the design, then re-export to PDF (or run `make` again after editing `diaporama.md`).

## Theme

The `reference.pptx` embeds the **Catppuccin Latte** palette used by the learn-dev
application (`theme-catppuccin.css`): soft base background `#eff1f5`, text `#4c4f69`, mauve
accent `#8839ef`. To adjust the theme, edit the color scheme in
`ppt/theme/theme1.xml` inside `reference.pptx` (it is a ZIP archive).
