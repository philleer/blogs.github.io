SRC = $(wildcard *.tex)

PDFS = $(SRC:.tex=.pdf)

PROJECT_DIR := $(shell pwd)
OUTPUT_DIR := $(join ${PROJECT_DIR}, /preview)
RESULTS := $(join ${OUTPUT_DIR}, /${PDFS})

TMP_LOG += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.log))
TMP_AUX += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.aux))
TMP_BBL += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.bbl))
TMP_BLG += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.blg))
TMP_GZ += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.synctex.gz))
TMP_OUT += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.out))
TMP_TOC += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.toc))
TMP_LOF += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.lof))
TMP_IDX += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.idx))
TMP_ILG += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.ilg))
TMP_IND += $(foreach dir, $(OUTPUT_DIR), $(wildcard $(dir)/*.ind))
TMP_FILES = ${TMP_LOG} ${TMP_AUX} ${TMP_BBL} ${TMP_BLG} ${TMP_GZ} ${TMP_OUT} ${TMP_TOC} ${TMP_LOF} ${TMP_IDX} ${TMP_ILG} ${TMP_IND}

${OUTPUT_DIR}:
	mkdir -p $@

all:	${OUTPUT_DIR} clean pdf

en: 	clean xelatex resume.tex

zh_CN:	clean xelatex resume-zh_CN.tex

pdf:	clean $(PDFS)

%.pdf:  %.tex
	xelatex -output-directory=${OUTPUT_DIR} $<

ifeq ($(OS),Windows_NT) # on Windows
  RM = cmd //C del
else # on Unix/Linux
  RM = rm -f
endif

clean:
	$(RM) ${TMP_FILES} ${RESULTS}
	$(RM) *.log *.aux *.bbl *.blg *.synctex.gz *.out *.toc *.lof *.idx *.ilg *.ind *.pdf
