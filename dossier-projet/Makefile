# Build the DWWM project-dossier PDFs from the Markdown sources.
# Requires pandoc >= 3.1.7 and typst (see README.md).
#   make            builds both PDFs at the repository root
#   make clean      removes the generated PDFs

PANDOC   := pandoc
ENGINE   := typst
OUT_DIR  := ..
DP_PDF   := $(OUT_DIR)/bouchut-eric-dossier-projet.pdf
RES_PDF  := $(OUT_DIR)/bouchut-eric-resume.pdf

# Shared options: Typst engine, numbered table of contents, image search path.
DP_OPTS  := --pdf-engine=$(ENGINE) --metadata-file=metadata.yaml \
            --toc --number-sections --resource-path=.:images

RES_OPTS := --pdf-engine=$(ENGINE) --metadata-file=metadata-resume.yaml \
            --resource-path=.:images

.PHONY: all clean
all: $(DP_PDF) $(RES_PDF)

$(DP_PDF): dossier-projet.md metadata.yaml
	$(PANDOC) dossier-projet.md $(DP_OPTS) -o $@
	@echo "OK => $@"

$(RES_PDF): resume.md metadata-resume.yaml
	$(PANDOC) resume.md $(RES_OPTS) -o $@
	@echo "OK => $@"

clean:
	rm -f $(DP_PDF) $(RES_PDF)
