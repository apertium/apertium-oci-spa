###############################################################################
## Makefile for Occitan--French
###############################################################################

LANG1=oci
LANG1b=oci@aran
LANG2=spa
PREFIX1=$(LANG1)-$(LANG2)
PREFIX1b=$(LANG1b)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)
PREFIX2b=$(LANG2)-$(LANG1b)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	bin/$(PREFIX1).automorf.bin	\
	bin/$(PREFIX1b).automorf.bin	\
	bin/$(PREFIX1).prob		\
	bin/$(PREFIX1).rlx.bin	\
	bin/$(PREFIX1).autobil.bin	\
	bin/$(PREFIX1b).autobil.bin	\
	bin/$(PREFIX1).autolex.bin	\
	bin/$(PREFIX1b).autolex.bin	\
	bin/$(PREFIX1).autogen.bin	\
	bin/$(PREFIX1).autopgen.bin	\
	build/$(PREFIX1).t1x	\
	build/$(PREFIX1b).t1x	\
	bin/$(PREFIX1).t1x.bin	\
	bin/$(PREFIX1).t2x.bin	\
	bin/$(PREFIX1).t3x.bin	\
	bin/$(PREFIX2).automorf.bin	\
	bin/$(PREFIX2).prob		\
	bin/$(PREFIX2).rlx.bin	\
	bin/$(PREFIX2).autobil.bin	\
	bin/$(PREFIX2b).autobil.bin	\
	bin/$(PREFIX2).autolex.bin	\
	bin/$(PREFIX2b).autolex.bin	\
	bin/$(PREFIX2).autogen.bin	\
	bin/$(PREFIX2b).autogen.bin	\
	bin/$(PREFIX2).autopgen.bin	\
	bin/$(PREFIX2b).autopgen.bin	\
	bin/$(PREFIX2).t1x.bin	\
	bin/$(PREFIX2).t2x.bin	\
	bin/$(PREFIX2).t3x.bin


# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Occitan analysis:
# -------------------

bin/$(PREFIX1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin bin/$(PREFIX1).autobil.bin
	lt-trim $^ $@

bin/$(PREFIX1b).automorf.bin: $(AP_SRC1)/$(LANG1b).automorf.bin bin/$(PREFIX1b).autobil.bin
	lt-trim $^ $@

# -------------------
# Occitan generation:
# ---------------------


bin/$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

bin/$(PREFIX2b).autogen.bin: $(AP_SRC1)/$(LANG1b).autogen.bin
	cp $< $@

# -------------------
# Spanish analysis:
# -------------------

bin/$(PREFIX2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.bin bin/$(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# Spanish generation:
# ---------------------


bin/$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Tagger models
###############################################################################

bin/$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

bin/$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

bin/$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

bin/$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

.deps/$(PREFIX2).dix: src/dictionaries/$(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1) alt.xsl src/dictionaries/$(BASENAME).$(PREFIX1).dix >$@

.deps/$(PREFIX2b).dix: src/dictionaries/$(BASENAME).$(PREFIX1).dix .deps/.d
	xsltproc --stringparam alt $(LANG1b) alt.xsl src/dictionaries/$(BASENAME).$(PREFIX1).dix >$@

bin/$(PREFIX1).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

bin/$(PREFIX1b).autobil.bin: .deps/$(PREFIX2b).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp lr $< $@

bin/$(PREFIX2).autobil.bin: .deps/$(PREFIX2).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

bin/$(PREFIX2b).autobil.bin: .deps/$(PREFIX2b).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

.deps/.$(PREFIX1).lrx: src/lexical-selection/$(BASENAME).$(PREFIX1).lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/.$(PREFIX1b).lrx: src/lexical-selection/$(BASENAME).$(PREFIX1b).lrx .deps/.d
	apertium-filter-rules oci@aran $< >$@

.deps/.$(PREFIX2).lrx: src/lexical-selection/$(BASENAME).$(PREFIX2).lrx .deps/.d
	apertium-filter-rules oci $< >$@

.deps/.$(PREFIX2b).lrx: src/lexical-selection/$(BASENAME).$(PREFIX2b).lrx .deps/.d
	apertium-filter-rules oci@aran $< >$@

bin/$(PREFIX1).autolex.bin: .deps/.$(PREFIX1).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX1b).autolex.bin: .deps/.$(PREFIX1b).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2).autolex.bin: .deps/.$(PREFIX2).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

bin/$(PREFIX2b).autolex.bin: .deps/.$(PREFIX2b).lrx
	apertium-validate-lrx $<
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################

build/$(PREFIX1).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x
	apertium-filter-rules oci src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x >$@

build/$(PREFIX1b).t1x: src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x
	apertium-filter-rules oci@aran src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x >$@

bin/$(PREFIX1).t1x.bin: build/$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1b).t1x.bin: build/$(PREFIX1b).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t2x.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX1).t3x.bin: src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


bin/$(PREFIX2).t1x.bin: src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t2x.bin: src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

bin/$(PREFIX2).t3x.bin: src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

bin/$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

bin/$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

bin/$(PREFIX2b).autopgen.bin: $(AP_SRC1)/$(LANG1b).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		src/lexical-selection/$(BASENAME).$(PREFIX1).lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX1b).lrx	\
		src/dictionaries/$(BASENAME).$(PREFIX1).dix	\
		src/lexical-selection/$(BASENAME).$(PREFIX2).lrx	\
		src/lexical-selection/$(BASENAME).$(PREFIX2b).lrx	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x	\
		src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x	\
		src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x	\
		src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x	\
		src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_oci_spadir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_oci_spa_DATA=	\
	$(TARGETS_COMMON)				\
	src/transfer/chunkers/$(BASENAME).$(PREFIX1).t1x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX1).t2x			\
	src/transfer/postchunks/$(BASENAME).$(PREFIX1).t3x			\
	src/transfer/chunkers/$(BASENAME).$(PREFIX2).t1x			\
	src/transfer/interchunks/$(BASENAME).$(PREFIX2).t2x			\
	src/transfer/postchunks/$(BASENAME).$(PREFIX2).t3x

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes bin build

###############################################################################
## Test
###############################################################################

test: all
	echo "ostal" | apertium -d . oci-spa | tee .test-mt
	@echo "casa" > .test-ref
	@diff .test-ref .test-mt
	echo "casa" | apertium -d . spa-oci | tee .test-mt
	@echo "ostal" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt

