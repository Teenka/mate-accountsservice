
dbusifdir   = $(datadir)/dbus-1/interfaces
dbusif_DATA = \
	org.freedesktop.MateAccounts.xml 		\
	org.freedesktop.MateAccounts.User.xml

dbusconfdir   = $(sysconfdir)/dbus-1/system.d
dbusconf_DATA = org.freedesktop.MateAccounts.conf

servicedir       = $(datadir)/dbus-1/system-services
service_in_files = org.freedesktop.MateAccounts.service.in
service_DATA     = $(service_in_files:.service.in=.service)

$(service_DATA): $(service_in_files) Makefile
	@sed -e "s|\@libexecdir\@|$(libexecdir)|" $< >$@

policydir       = $(datadir)/polkit-1/actions
policy_in_files = org.freedesktop.mateaccounts.policy.in
policy_DATA     = $(policy_in_files:.policy.in=.policy)

@INTLTOOL_POLICY_RULE@

if HAVE_SYSTEMD
systemdsystemunit_DATA = \
	mateaccounts-daemon.service

mateaccounts-daemon.service: mateaccounts-daemon.service.in
	@sed -e "s|\@libexecdir\@|$(libexecdir)|" $< >$@

endif

EXTRA_DIST = 			\
	$(dbusif_DATA)		\
	$(dbusconf_DATA)	\
	$(service_in_files)	\
	$(policy_in_files)      \
	mateaccounts-daemon.service.in

DISTCLEANFILES = 		\
	$(service_DATA)		\
	$(policy_DATA)

CLEANFILES = \
	mateaccounts-daemon.service
