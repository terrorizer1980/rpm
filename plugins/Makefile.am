# Makefile for rpm library.

include $(top_srcdir)/rpm.am
AM_CFLAGS = @RPMCFLAGS@

AM_CPPFLAGS = -I$(top_builddir) -I$(top_srcdir) -I$(top_builddir)/include/
AM_CPPFLAGS += -I$(top_srcdir)/misc
AM_CPPFLAGS += -DLOCALEDIR="\"$(localedir)\""
AM_CPPFLAGS += -DSYSCONFDIR="\"$(sysconfdir)\""
AM_CPPFLAGS += -DLOCALSTATEDIR="\"$(localstatedir)\""
AM_CPPFLAGS += -DLIBRPMALIAS_FILENAME="\"rpmpopt-${VERSION}\""

AM_LDFLAGS = -avoid-version -module -shared

pluginsdir = $(libdir)/rpm-plugins

plugins_LTLIBRARIES =

if SELINUX
selinux_la_SOURCES = selinux.c
selinux_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la @WITH_SELINUX_LIB@
plugins_LTLIBRARIES += selinux.la
endif

if DBUS
systemd_inhibit_la_SOURCES = systemd_inhibit.c
systemd_inhibit_la_CPPFLAGS = $(AM_CPPFLAGS) @DBUS_CFLAGS@
systemd_inhibit_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la @DBUS_LIBS@
plugins_LTLIBRARIES += systemd_inhibit.la

dbus_announce_la_SOURCES = dbus_announce.c
dbus_announce_la_CPPFLAGS = $(AM_CPPFLAGS) @DBUS_CFLAGS@
dbus_announce_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la @DBUS_LIBS@
plugins_LTLIBRARIES += dbus_announce.la

dbus_confdir=$(sysconfdir)/dbus-1/system.d/
dbus_conf_DATA = org.rpm.conf
EXTRA_DIST = org.rpm.conf
endif

prioreset_la_SOURCES = prioreset.c
prioreset_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la
plugins_LTLIBRARIES += prioreset.la

syslog_la_SOURCES = syslog.c
syslog_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la
plugins_LTLIBRARIES += syslog.la

if IMA
ima_la_sources = ima.c
ima_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la
plugins_LTLIBRARIES += ima.la
endif

if FAPOLICYD
fapolicyd_la_sources = fapolicyd.c
fapolicyd_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la
plugins_LTLIBRARIES += fapolicyd.la
endif

if FSVERITY_IOCTL
fsverity_la_sources = fsverity.c
fsverity_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la
plugins_LTLIBRARIES += fsverity.la
endif

if AUDIT
audit_la_sources = audit.c
audit_la_LIBADD = $(top_builddir)/lib/librpm.la $(top_builddir)/rpmio/librpmio.la @WITH_AUDIT_LIB@
plugins_LTLIBRARIES += audit.la
endif
