# Build the DWWM oral-defense slideshow with Slidev.
# Requires Node.js >= 20 and `npm install` (once). See README.md.
#   make dev      live presentation with presenter mode (http://localhost:3030)
#   make pdf      export ../bouchut-eric-diaporama.pdf
#   make pptx     export ../bouchut-eric-diaporama.pptx (slides as images, not editable)
#   make html     build the static SPA into dist/
#   make all      pdf + pptx + html
#   make clean    remove the generated files

OUT_DIR := ..
PDF     := $(OUT_DIR)/bouchut-eric-diaporama.pdf
PPTX    := $(OUT_DIR)/bouchut-eric-diaporama.pptx

# The deck depends on its sources and on the local theme (styles, layouts, layers).
SOURCES := slides.md package.json $(wildcard theme/*.vue theme/*.ts theme/*.json theme/styles/* theme/layouts/*)

.PHONY: all dev pdf pptx html clean
all: pdf pptx html

dev:
	npm run dev

pdf: $(PDF)
$(PDF): $(SOURCES)
	npm run export:pdf
	@echo "OK => $(PDF)"

pptx: $(PPTX)
$(PPTX): $(SOURCES)
	npm run export:pptx
	@echo "OK => $(PPTX)"

html: $(SOURCES)
	npm run build
	@echo "OK => dist/"

clean:
	rm -rf $(PDF) $(PPTX) dist
