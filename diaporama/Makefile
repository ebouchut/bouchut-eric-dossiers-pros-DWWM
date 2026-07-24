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

.PHONY: all dev pdf pptx html clean
all: pdf pptx html

dev:
	npm run dev

pdf: $(PDF)
$(PDF): slides.md style.css package.json
	npm run export:pdf
	@echo "OK => $(PDF)"

pptx: $(PPTX)
$(PPTX): slides.md style.css package.json
	npm run export:pptx
	@echo "OK => $(PPTX)"

html: slides.md style.css package.json
	npm run build
	@echo "OK => dist/"

clean:
	rm -rf $(PDF) $(PPTX) dist
