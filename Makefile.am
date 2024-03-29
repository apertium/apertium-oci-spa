###############################################################################
## Makefile for Occitan--French
###############################################################################

LANG1=oci
LANG1b=oci@gascon
LANG2=spa
PREFIX1=$(LANG1)-$(LANG2)
PREFIX1b=$(LANG1b)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)
PREFIX2b=$(LANG2)-$(LANG1b)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	$(PREFIX1).automorf.bin	\
	$(PREFIX1b).automorf.bin	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).autobil.bin	\
	$(PREFIX1b).autobil.bin	\
	$(PREFIX1).autolex.bin	\
	$(PREFIX1b).autolex.bin	\
	$(PREFIX1).autogen.bin	\
	$(PREFIX1).autopgen.bin	\
	$(PREFIX1).t1x.bin	\
	$(PREFIX1).t2x.bin	\
	$(PREFIX1).t3x.bin	\
	$(PREFIX2).automorf.bin	\
	$(PREFIX2).prob		\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2b).autobil.bin	\
	$(PREFIX2).autolex.bin	\
	$(PREFIX2b).autolex.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2b).autogen.bin	\
	$(PREFIX2).autopgen.bin	\
	$(PREFIX2b).autopgen.bin	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t2x.bin	\
	$(PREFIX2).t3x.bin


# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Occitan analysis:
# -------------------

$(PREFIX1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin $(PREFIX1).autobil.bin
	lt-trim $^ $@

$(PREFIX1b).automorf.bin: $(AP_SRC1)/$(LANG1b).automorf.bin $(PREFIX1b).autobil.bin
	lt-trim $^ $@

# -------------------
# Occitan generation:
# ---------------------


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

$(PREFIX2b).autogen.bin: $(AP_SRC1)/$(LANG1b).autogen.bin
	cp $< $@

# -------------------
# French analysis:
# -------------------

$(PREFIX2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# French generation:
# ---------------------


$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

.deps/$(PREFIX2).dix: $(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1) alt.xsl $(BASENAME).$(PREFIX1).dix >$@

.deps/$(PREFIX2b).dix: $(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1b) alt.xsl $(BASENAME).$(PREFIX1).dix >$@

$(PREFIX1).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX1b).autobil.bin: .deps/$(PREFIX2b).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX2b).autobil.bin: .deps/$(PREFIX2b).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1).autolex.bin: $(BASENAME).$(PREFIX1).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX1b).autolex.bin: $(BASENAME).$(PREFIX1b).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2).autolex.bin: $(BASENAME).$(PREFIX2).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

$(PREFIX2b).autolex.bin: $(BASENAME).$(PREFIX2b).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

$(PREFIX2b).autopgen.bin: $(AP_SRC1)/$(LANG1b).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1b).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX2b).lrx	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_oci_spadir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_oci_spa_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t3x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "house" | apertium -d . oci-fra | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	echo "house" | apertium -d . fra-oci | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt

