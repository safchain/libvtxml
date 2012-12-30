AC_PREREQ([2.59])
AC_INIT([libvtxml],[0.5],[safchain@gmail.com])
AC_CONFIG_SRCDIR([src])

AM_INIT_AUTOMAKE

AC_CONFIG_HEADERS([config.h])
AC_PROG_CC
AC_PROG_RANLIB

CFLAGS="$CFLAGS -Wall -W -fno-strict-aliasing"
AC_ARG_ENABLE(debug,
[  --enable-debug		Enable some extra expensive checks for developers],
    if test x$enableval = xyes; then
        AC_DEFINE(DEBUG,, Build with extra debugging checks)
	elif test x$enableval = xalloc; then
		AC_DEFINE(DEBUG_ALLOC,, Build with extra allocation debugging checks)
	elif test x$enableval = xstack; then
		AC_DEFINE(DEBUG_STACK,, Build with extra stack debugging checks)
	elif test x$enableval = "xalloc,stack"; then
		AC_DEFINE(DEBUG_ALLOC,, Build with extra allocation debugging checks)
		AC_DEFINE(DEBUG_STACK,, Build with extra stack debugging checks)
    fi)

dnl checks
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h strings.h fcntl.h unistd.h limits.h])

AC_C_INLINE
AC_FUNC_FORK
AC_FUNC_REALLOC
AC_TYPE_PID_T
AC_TYPE_UID_T

AC_C_CONST

AC_FUNC_MALLOC
AC_TYPE_SIGNAL
AC_CHECK_FUNCS([memset strcasecmp strerror strncasecmp strtol strdup dup2 strstr])

AC_CONFIG_FILES([Makefile \
	src/Makefile])


AC_OUTPUT
