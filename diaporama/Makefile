# Build the DWWM oral-defense slideshow from its Markdown source.
# Requires pandoc and LibreOffice (soffice). See README.md.
#   make          builds the .pptx and the .pdf at the repository root
#   make pptx     builds only the editable .pptx
#   make clean    removes the generated files

PANDOC  := pandoc
SOFFICE := /Applications/LibreOffice.app/Contents/MacOS/soffice
OUT_DIR := ..
PPTX    := $(OUT_DIR)/bouchut-eric-diaporama.pptx
PDF     := $(OUT_DIR)/bouchut-eric-diaporama.pdf

.PHONY: all pptx pdf clean
all: pdf

$(PPTX): diaporama.md reference.pptx
	$(PANDOC) diaporama.md --reference-doc=reference.pptx --slide-level=2 -o $(PPTX)
	@echo "OK => $(PPTX)"

pptx: $(PPTX)

pdf: $(PPTX)
	$(SOFFICE) --headless --convert-to pdf --outdir $(OUT_DIR) $(PPTX)
	@echo "OK => $(PDF)"

clean:
	rm -f $(PPTX) $(PDF)
