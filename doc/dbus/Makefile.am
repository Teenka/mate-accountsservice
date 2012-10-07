NULL =

SPEC_XML_FILES =			\
	MateAccountsService.xml		\
	org.freedesktop.MateAccounts.ref.xml	\
	org.freedesktop.MateAccounts.User.ref.xml		\
	$(NULL)

if DOCBOOK_DOCS_ENABLED

htmldocdir = $(docdir)/spec
htmldoc_DATA = MateAccountsService.html

MateAccountsService.html : $(SPEC_XML_FILES)
	$(XMLTO) $(XMLTO_FLAGS) xhtml-nochunks -m $(top_srcdir)/doc/dbus/config.xsl MateAccountsService.xml

endif # DOCBOOK_DOCS_ENABLED

org.freedesktop.MateAccounts.ref.xml : $(top_srcdir)/data/org.freedesktop.MateAccounts.xml spec-to-docbook.xsl
	$(XSLTPROC) $(top_srcdir)/doc/dbus/spec-to-docbook.xsl $< | tail -n +2 > $@
org.freedesktop.MateAccounts.User.ref.xml : $(top_srcdir)/data/org.freedesktop.MateAccounts.User.xml spec-to-docbook.xsl
	$(XSLTPROC) $(top_srcdir)/doc/dbus/spec-to-docbook.xsl $< | tail -n +2 > $@

EXTRA_DIST =				\
	spec-to-docbook.xsl		\
	MateAccountsService.xml.in		\
	config.xsl			\
	docbook.css			\
	dbus-introspect-docs.dtd	\
	$(SPEC_XML_FILES)
	$(NULL)

MAINTAINERCLEANFILES =		\
	*~			\
	Makefile.in		\
	$(NULL)

clean-local:
	rm -f *~ *.ref.xml
	rm -f MateAccountsService.html

check-local:
	xmllint --noout --noent --valid MateAccountsService.xml
