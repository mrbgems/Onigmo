noinst_PROGRAMS = encode listcap names posix simple sql syntax scan crnl

libname = $(top_builddir)/libonigmo.la
LDADD   = $(libname)
AM_CPPFLAGS = -I$(top_srcdir) -I$(includedir)

encode_SOURCES  = encode.c
listcap_SOURCES = listcap.c
names_SOURCES   = names.c
posix_SOURCES   = posix.c
# Link posix against every member of the static archive, without libtool, so
# the executable defines regcomp and regexec itself. Otherwise AddressSanitizer's
# libc interceptors handle the calls and forward them to glibc on Onigmo's
# struct, which can deadlock.
libonigmo-all.o: $(top_builddir)/.libs/libonigmo.a
	$(LD) -r --whole-archive $< -o $@

posix_LINK  = $(CCLD) $(AM_CFLAGS) $(CFLAGS) $(AM_LDFLAGS) $(LDFLAGS) -o $@
posix_LDADD = libonigmo-all.o
simple_SOURCES  = simple.c
sql_SOURCES     = sql.c
syntax_SOURCES  = syntax.c
scan_SOURCES    = scan.c
crnl_SOURCES    = crnl.c


sampledir = $(top_builddir)/sample

test: encode$(EXEEXT) listcap$(EXEEXT) names$(EXEEXT) posix$(EXEEXT) simple$(EXEEXT) sql$(EXEEXT) syntax$(EXEEXT) scan$(EXEEXT) crnl$(EXEEXT)
	$(sampledir)/encode
	$(sampledir)/listcap
	$(sampledir)/names
	$(sampledir)/posix
	$(sampledir)/simple
	$(sampledir)/sql
	$(sampledir)/syntax
	$(sampledir)/scan
	$(sampledir)/crnl
