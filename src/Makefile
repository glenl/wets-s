#++
# PROJECT:
#   wets-s
#
# ABSTRACT:
#   A WETS service based on the WETS executable model.
#
# REQUIRED TOOLS:
#   atangle
#   pikchr
#   asciidoctor and various gems
#     asciidoctor-diagram
#     asciidoctor-rouge
#
#--
AUTHOR = "Glen Larsen"
VERSION = "1.0a"
REVISIONDATE = "09 Jan 2026"
PROJECT = wets-s

DOCDIR = ../doc
CODEDIR = ../code
IMAGEDIR = ../images

vpath %.pdf $(DOCDIR)
vpath %.html $(DOCDIR)
vpath %.test $(TESTDIR)
vpath %.uxf $(IMAGEDIR)

DOCSRC = \
	$(PROJECT)-ref.adoc \
	$(NULL)

DOCSRCS = \
	$(PROJECT)-ref.adoc \
	overview.adoc \
	wets-s.adoc \
	nats.adoc \
	wdriver.adoc \
	$(NULL)

REQUIRED_DIRS =\
	$(DOCDIR)\
	$(CODEDIR)\
	$(NULL)

_MKDIRS := $(shell for d in $(REQUIRED_DIRS) ;\
		 do\
			 [ -d $$d ] || mkdir -p $$d ;\
		 done)

PDF =\
	$(DOCDIR)/$(patsubst %.adoc,%.pdf,$(DOCSRC))\
	$(NULL)

TCLSRC	=\
	$(patsubst %.adoc,%.tcl,$(DOCSRC))\
	$(NULL)


IMAGES =\
	$(NULL)

ATANGLEOPTS =\
	$(NULL)

CLEANFILES =\
	$(IMAGES)\
	$(PDF)\
	$(NULL)

ADOCTOR_OPTS =\
	-d book\
	-a source-highlighter=rouge\
	-a author=$(AUTHOR)\
	-a revnumber=$(VERSION)\
	-a revdate=$(REVISIONDATE)\
	-r asciidoctor-diagram\
	$(NULL)

$(DOCDIR)/%.pdf : %.adoc
	asciidoctor-pdf $(ADOCTOR_OPTS)\
		-a imagesdir=$(IMAGEDIR)\
		--theme ./wetsim-theme.yml\
		-o $@ $<

$(DOCDIR)/%-doc.html : %.adoc
	asciidoctor $(ADOCTOR_OPTS)\
		-a imagesdir=../src/images -o $@ $<

.PHONY : all doc code clean

all : doc code

doc :  $(PDF) # $(HTML)

$(PDF) : $(DOCSRC) $(DOCSRCS) wetsim-theme.yml

code : $(CODEDIR)/wdriver.tcl $(CODEDIR)/wets-s.tcl

clean :
	$(RM) $(CLEANFILES)

$(CODEDIR)/%.tcl : %.adoc
	atangle $(ATANGLEOPTS) -root $(notdir $@) -output $@ $<
	chmod u+x $@
