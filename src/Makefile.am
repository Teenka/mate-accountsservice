SUBDIRS = . libmateaccountsservice
INCLUDES = 			\
	-DLOCALSTATEDIR=\""$(localstatedir)"\" \
	-DDATADIR=\""$(datadir)"\" \
	$(DBUS_GLIB_CFLAGS) 	\
	$(GIO_CFLAGS)	 	\
	$(GLIB_CFLAGS)		\
	$(POLKIT_CFLAGS)	\
	$(WARN_CFLAGS)

BUILT_SOURCES = 		\
	daemon-glue.h		\
	user-glue.h

daemon-glue.h: $(top_srcdir)/data/org.freedesktop.MateAccounts.xml Makefile
	dbus-binding-tool --prefix=daemon --mode=glib-server --output=daemon-glue.h $(top_srcdir)/data/org.freedesktop.MateAccounts.xml

user-glue.h: $(top_srcdir)/data/org.freedesktop.MateAccounts.User.xml Makefile
	dbus-binding-tool --prefix=user --mode=glib-server --output=user-glue.h $(top_srcdir)/data/org.freedesktop.MateAccounts.User.xml

libexec_PROGRAMS = mateaccounts-daemon

mateaccounts_daemon_SOURCES = 	\
	$(enums_h_sources)	\
	$(BUILT_SOURCES)	\
	types.h			\
	daemon.h		\
	daemon.c		\
	user.h			\
	user.c			\
	util.h			\
	util.c			\
	main.c

mateaccounts_daemon_LDADD = 	\
	$(DBUS_GLIB_LIBS) 	\
	$(GIO_LIBS)		\
	$(GLIB_LIBS)		\
	$(POLKIT_LIBS)

CLEANFILES = $(BUILT_SOURCES)

install-data-hook:
	$(MKDIR_P) "$(DESTDIR)$(localstatedir)/lib/MateAccountsService/users"
	$(MKDIR_P) "$(DESTDIR)$(localstatedir)/lib/MateAccountsService/icons"
