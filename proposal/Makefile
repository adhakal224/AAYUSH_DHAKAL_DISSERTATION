.SUFFIXES: .png .bb .jpg .pdf
TEXFILES:=$(wildcard *.tex)
AUXDIR:=./tmp/

FIGDIR:=./figs/
TARGET=proposal
DEPS= phd.bib $(TEXFILES) jacobsn.sty
BIBTEX_OPTS=-quiet -include-directory=$(AUXDIR)
LATEXF=-quiet -interaction=nonstopmode -aux-directory=$(AUXDIR) -include-directory=$(FIGDIR)
LATEXF=-aux-directory=$(AUXDIR) -include-directory=$(FIGDIR)
PDFF= $(LATEXF) 

define build-pdf 
	@echo building pdf
	pdflatex $(PDFF) $(TARGET) 
endef

define build-dvi
  @echo building dvi
	latex $(PDFF) $(TARGET) 
endef

define run-bibtex 
  @echo running bibtex
	bibtex $(BIBTEX_OPTS) $(patsubst %.tex,%,$(TARGET))
endef

pdf: $(DEPS) 
	@echo Run 'make all' to rebuild bibtex and references. 
	@$(build-pdf)

all: $(TARGET).pdf

open: $(TARGET).pdf
	cygstart $(TARGET).pdf

dvi: $(TARGET).dvi

$(TARGET).dvi: $(JPG_PDF) $(PNG_PDF) $(DEPS)
	@$(build-dvi)
	@$(run-bibtex)
	@$(build-dvi)
	@$(build-dvi)

$(TARGET).pdf: $(JPG_PDF) $(PNG_PDF) $(DEPS)
	@$(build-pdf)
	@$(run-bibtex)
	@$(build-pdf)
	@$(build-pdf)

bib: $(DEPS) 
	@$(run-bibtex)

#.jpg.pdf:
#	convert "$<" -colorspace RGB -density 400 "$@" 
#.png.pdf:
#	convert "$<" -colorspace RGB -density 400 "$@" 

clean:
	rm -f *.dvi
	rm -f *.pdf
	rm -f *.ps
	rm -f *.blg
	rm -f *.log
	rm -f *.lot
	rm -f *.aux
	rm -f *.toc
	rm -f *.lof
	rm -f *.bbl
	rm -f $(AUXDIR)*.aux

