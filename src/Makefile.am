AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_maxdigest.la

libvmod_maxdigest_la_LDFLAGS = -module -export-dynamic -avoid-version -shared -lmhash

libvmod_maxdigest_la_SOURCES = \
	vmod_maxdigest.c

nodist_libvmod_maxdigest_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_maxdigest.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_maxdigest.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_maxdigest.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_maxdigest.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_maxdigest.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_maxdigest.man.rst \
	$(builddir)/vmod_maxdigest.rst
