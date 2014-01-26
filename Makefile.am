ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAG}

DISTCHECK_CONFIGURE_FLAGS = --with-cajadir='$${libdir}/caja/extensions-2.0-distcheck'

gsettings_schemas_in_files = org.mate.caja-open-terminal.gschema.xml.in
gsettings_SCHEMAS = $(gsettings_schemas_in_files:.gschema.xml.in=.gschema.xml)

@INTLTOOL_XML_NOMERGE_RULE@

@GSETTINGS_RULES@

convertdir = $(datadir)/MateConf/gsettings
convert_DATA = caja-open-terminal.convert

SUBDIRS = \
	po \
	src

EXTRA_DIST = \
	intltool-extract.in \
	intltool-update.in \
	intltool-merge.in \
	$(convert_DATA) \
	$(gsettings_schemas_in_files)

DISTCLEANFILES = \
	intltool-extract \
	intltool-update \
	intltool-merge \
	po/.intltool-merge-cache \
	org.mate.caja-open-terminal.gschema.xml
