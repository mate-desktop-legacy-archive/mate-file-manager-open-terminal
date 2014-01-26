AC_INIT([mate-file-manager-open-terminal], [1.6.1], [https://github.com/mate-desktop/mate-file-manager-open-terminal])

AM_INIT_AUTOMAKE([1.9 no-dist-gzip dist-xz])

AC_CONFIG_HEADERS(config.h)
AC_CONFIG_MACRO_DIR([m4])

CAJA_REQUIRED=1.1.0
EEL_REQUIRED=2.6.0
LIBMATE_DESKTOP_REQUIRED=1.1.0
GLIB_REQUIRED=2.4.0
GLIB_GSETTINGS

AC_PROG_CC
AM_PROG_LIBTOOL

dnl Check for pkgconfig first
AC_CHECK_PROG(HAVE_PKGCONFIG, pkg-config, yes, no)
AC_PATH_PROG(PKG_CONFIG, pkg-config, no)

dnl Give error and exit if we don't have pkgconfig
if test "x$HAVE_PKGCONFIG" = "xno"; then
  AC_MSG_ERROR(you need to have pkgconfig installed !)
fi

PKG_CHECK_MODULES(CAJA, libcaja-extension >= $CAJA_REQUIRED glib-2.0 >= $GLIB_REQUIRED)
PKG_CHECK_MODULES(MATEDESKTOP, mate-desktop-2.0 >= $LIBMATE_DESKTOP_REQUIRED)

PKG_CHECK_MODULES(GLIB_RECENT, glib-2.0 >= 2.13.3,
                  AC_DEFINE(HAVE_GLIB_DESKTOP_DIR_API, 1, [g_get_user_special_dir() support]),
		  AC_MSG_NOTICE([not using g_get_user_special_dir()]))


dnl make MATE_CFLAGS and MATE_LIBS available
AC_SUBST(CAJA_CFLAGS)
AC_SUBST(CAJA_LIBS)

AC_SUBST(MATEDESKTOP_CFLAGS)
AC_SUBST(MATEDESKTOP_LIBS)

# Get caja extensions directory
AC_ARG_WITH(cajadir,
    AS_HELP_STRING([--with-cajadir=DIR],[Installation path for Caja extension @<:@auto@:>@]),
    [ac_with_cajadir=$withval],
    [ac_with_cajadir=""])
if test "${ac_with_cajadir}" = ""; then
    ac_with_cajadir=`$PKG_CONFIG --variable=extensiondir libcaja-extension`
fi
AC_MSG_NOTICE([Installing caja plugins in ${ac_with_cajadir}])
AC_SUBST([CAJA_EXTENSION_DIR],[${ac_with_cajadir}])

dnl intltool stuff
AC_PROG_INTLTOOL(0.18)
dnl AM_WITH_NLS
GETTEXT_PACKAGE=caja-open-terminal
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE, "$GETTEXT_PACKAGE", [gettext package])
AM_GLIB_GNU_GETTEXT

AC_OUTPUT([
  Makefile 
  src/Makefile
  po/Makefile.in 
])

