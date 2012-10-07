END_OF_LIST =

BUILT_SOURCES = $(END_OF_LIST)
CLEANFILES = $(END_OF_LIST)

AM_CPPFLAGS = \
        -I.                                                                   \
        -I..                                                                  \
        -DG_LOG_DOMAIN=\"MateAccountsService\"                                    \
        $(END_OF_LIST)

lib_LTLIBRARIES =                                                             \
        libmateaccountsservice.la                                                 \
        $(END_OF_LIST)

act-user-enum-types.h: act-user.h
	$(AM_V_GEN) (cd $(srcdir) && \
	         glib-mkenums \
	          --fhead "#ifndef __ACT_USER_ENUM_TYPES_H__\n#define __ACT_USER_ENUM_TYPES_H__\n\n#include <glib-object.h>\n\nG_BEGIN_DECLS\n" \
	          --fprod "/* enumerations from \"@filename@\" */\n" \
	          --vhead "GType @enum_name@_get_type (void);\n#define ACT_USER_TYPE_@ENUMSHORT@ (@enum_name@_get_type())\n"    \
	          --ftail "G_END_DECLS\n\n#endif /* __ACT_USER_ENUM_TYPES_H__ */" \
	          act-user.h) > $@

act-user-enum-types.c: act-user.h act-user-enum-types.h
	$(AM_V_GEN) (cd $(srcdir) && \
	         glib-mkenums \
	          --fhead "#include \"act-user.h\"\n" \
	          --fhead "#include \"act-user-enum-types.h\"\n" \
	          --fhead "#include <glib-object.h>" \
	          --fprod "\n/* enumerations from \"@filename@\" */" \
	          --vhead "GType\n@enum_name@_get_type (void)\n{\n  static GType etype = 0;\n  if (etype == 0) {\n    static const G@Type@Value values[] = {"    \
	          --vprod "      { @VALUENAME@, \"@VALUENAME@\", \"@valuenick@\" }," \
	          --vtail "      { 0, NULL, NULL }\n    };\n    etype = g_@type@_register_static (\"@EnumName@\", values);\n  }\n  return etype;\n}\n" \
	         act-user.h) > $@

BUILT_SOURCES += act-user-enum-types.c act-user-enum-types.h
CLEANFILES += $(BUILT_SOURCES)

libmateaccountsservicedir = $(includedir)/mateaccountsservice-1.0/act
libmateaccountsservice_HEADERS =                                                  \
        act-user.h                                                            \
        act-user-manager.h                                                    \
        act-user-enum-types.h                                                 \
        $(END_OF_LIST)

libmateaccountsservice_la_CFLAGS = $(LIBMATEACCOUNTSSERVICE_CFLAGS)
libmateaccountsservice_la_LDFLAGS =                                               \
        -export-symbols-regex '^[^_].*'                                       \
        -version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)                  \
        -no-undefined                                                         \
        $(END_OF_LIST)

libmateaccountsservice_la_LIBADD =                                                \
        $(LIBMATEACCOUNTSSERVICE_LIBS)                                            \
        -lcrypt                                                               \
        $(END_OF_LIST)

libmateaccountsservice_la_SOURCES =                                               \
        $(libmateaccountsservice_HEADERS)                                         \
        act-user-private.h                                                    \
        act-user.c                                                            \
        act-user-manager.c                                                    \
        $(BUILT_SOURCES)                                                      \
        $(END_OF_LIST)

pkgconfigdir = $(libdir)/pkgconfig
dist_pkgconfig_DATA = mateaccountsservice.pc

-include $(INTROSPECTION_MAKEFILE)

if HAVE_INTROSPECTION
girdir = $(datadir)/gir-1.0
gir_DATA = MateAccountsService-1.0.gir
typelibsdir = $(libdir)/girepository-1.0
typelibs_DATA = $(gir_DATA:.gir=.typelib)
INTROSPECTION_GIRS = $(gir_DATA)

MateAccountsService-1.0.gir:                                                      \
        $(INTROSPECTION_SCANNER)                                              \
        libmateaccountsservice.la                                                 \
        Makefile                                                              \
        $(END_OF_LIST)

MateAccountsService_1_0_gir_SCANNERFLAGS =                                        \
        --warn-all                                                            \
        --namespace=MateAccountsService                                           \
        --identifier-prefix Act                                               \
        $(libmateaccountsservice_la_CFLAGS)                                       \
        $(END_OF_LIST)

MateAccountsService_1_0_gir_INCLUDES = $(LIBMATEACCOUNTSSERVICE_GIR_INCLUDES)
MateAccountsService_1_0_gir_LIBS = libmateaccountsservice.la
MateAccountsService_1_0_gir_FILES =                                               \
        $(filter-out %-private.h, $(libmateaccountsservice_la_SOURCES))           \
        $(BUILT_SOURCES)                                                      \
        $(END_OF_LIST)

CLEANFILES += $(gir_DATA) $(typelibs_DATA)
endif

MAINTAINERCLEANFILES = Makefile.in
