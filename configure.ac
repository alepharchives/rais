AC_INIT([rais],[0.0.1],[tonyg@rabbitmq.com])
AC_CONFIG_SRCDIR(src/main.c)
AM_INIT_AUTOMAKE

AC_CONFIG_HEADER([config.h])

dnl On Mac OS X, include/link against macports for libevent
AC_MSG_CHECKING(for macports)
if test -d /opt/local
then
	AC_MSG_RESULT(yes)
	CFLAGS="-I/opt/local/include $CFLAGS"
	CPPFLAGS="-I/opt/local/include $CPPFLAGS"
	LDFLAGS="-L/opt/local/lib $LDFLAGS"
else
	AC_MSG_RESULT(no)
fi

dnl Program checks
AC_PROG_CC

dnl Library checks
AM_PROG_LIBTOOL
AC_CHECK_LIB(event,event_init,,[AC_MSG_ERROR([cannot link with libevent])])

dnl Header-file checks
AC_HEADER_STDC
AC_CHECK_HEADERS([event.h],,[AC_MSG_ERROR([cannot find event.h to include])])
AC_CHECK_HEADERS([tcadb.h],,[AC_MSG_ERROR([cannot find tokyocabinet's tcadb.h to include])])

dnl Only use -Wall if we have gcc
if test "x$GCC" = "xyes"; then
  if test -z "`echo "$CFLAGS" | grep "\-Wall" 2> /dev/null`" ; then
    CFLAGS="$CFLAGS -Wall"
  fi
fi

dnl Enable -m64 if we were asked to do so
AC_ARG_ENABLE(64-bit,
[  --enable-64-bit         produce 64-bit library],
[CFLAGS="$CFLAGS -m64"; LDFLAGS="$LDFLAGS -m64"],
)

AC_OUTPUT(
Makefile
src/Makefile
)
