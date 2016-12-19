%AC_COPYRIGHT([
 Copyright (c) 2015 - Adjacent Link LLC, Bridgewater, New Jersey
 All rights reserved.

 Redistribution and use in source and binary forms, with or without
 modification, are permitted provided that the following conditions
 are met:
 
 * Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.
 * Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in
   the documentation and/or other materials provided with the
   distribution.
 * Neither the name of Adjacent Link LLC nor the names of its
   contributors may be used to endorse or promote products derived
   from this software without specific prior written permission.
 
 THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
 "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
 LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
 FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
 COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
 INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
 BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
 LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
 CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
 LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN
 ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
 POSSIBILITY OF SUCH DAMAGE.

 See toplevel COPYING for more information.
])

AC_INIT([emanedleplayer],0.0.1_1.9,[emane at adjacent link dot com])

AC_CONFIG_SRCDIR([src])

AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE([1.9.6])

AC_PROG_CXX

AC_PROG_CXXCPP

AX_CXX_COMPILE_STDCXX_11([noext],[mandatory])

AC_PROG_INSTALL

AC_PROG_LIBTOOL

AC_LANG([C++])

AC_ARG_WITH(profile,
           [  --with-profile          add profiling support (off)])

AC_ARG_WITH(debug,
           [  --with-debug            add debug support (off)])

AC_ARG_WITH(dot,
           [  --with-dot              Use dot with doxygen (off)])

AC_ARG_WITH([verbose-logging],
           [  --without-verbose-logging  disable verbose logging support (on)],
           [],
           [with_verbose_logging=yes])


PKG_CHECK_MODULES([LIBXML2], libxml-2.0)
PKG_CHECK_MODULES([libuuid], uuid)

AC_CHECK_FILE(/etc/debian_version,[DEBIAN_VERSION=`cat /etc/debian_version | awk -F/ '{print $1}'`],)
AC_SUBST(DEBIAN_VERSION)


CPPFLAGS="${CPPFLAGS} -std=c++11 ${libuuid_CFLAGS} \
	-DBOOST_MPL_CFG_NO_PREPROCESSED_HEADERS \
	-DBOOST_MPL_LIMIT_VECTOR_SIZE=30 \
	-DBOOST_MPL_LIMIT_LIST_SIZE=30 \
	-DBOOST_TEST_DYN_LINK"

_cppflags=${CPPFLAGS}
_ldflags=${LDFLAGS}

# Checks for libraries.
if test "${ACE_CFLAGS}" != ""; then
   CPPFLAGS="${ACE_CFLAGS} ${CPPFLAGS}"
fi

if test "${ACE_LIBS}" != ""; then
   LDFLAGS="${ACE_LIBS} ${LDFLAGS}"
fi

AC_CHECK_HEADER(ace/OS_main.h,
 [AC_CHECK_LIB([ACE],main,[ACE_LIBS+=' -lACE'],[AC_MSG_ERROR("ACE not installed")])],
 [AC_MSG_ERROR("Missing ACE development headers")])

CPPFLAGS=${_cppflags}
LDFLAGS=${_ldflags}

AC_SUBST(ACE_CFLAGS)
AC_SUBST(ACE_LIBS)

# Checks for libraries.
if test "${EMANE_CFLAGS}" != ""; then
   CPPFLAGS="${EMANE_CFLAGS} ${CPPFLAGS}"
fi

AC_CHECK_HEADERS(emane/component.h,,[AC_MSG_ERROR("EMANE headers not installed")])
AC_CHECK_HEADERS(dlep/DlepClient.h,,[AC_MSG_ERROR("DLEP Client headers not installed")])

AC_SUBST(EMANE_CFLAGS)

AC_C_BIGENDIAN(AC_DEFINE([__BYTE_ORDER],__BIG_ENDIAN,[Big Endian]),AC_DEFINE([__BYTE_ORDER],__LITTLE_ENDIAN,[Little Endian]))
AC_DEFINE([__LITTLE_ENDIAN],1234,[for the places where it is not defined])
AC_DEFINE([__BIG_ENDIAN],4321,[for the places where it is not defined])

# compiler options
CXXFLAGS="-W -Wall"

# options for use with gprof
if test "$with_profile" = "yes"
then
CPPFLAGS="$CPPFLAGS -g -pg"
LDFLAGS="$LDFLAGS -g -pg"
fi

# options for use with debug
if test "$with_debug" = "yes"
then
CPPFLAGS="$CPPFLAGS -g3 -O0"
LDFLAGS="$LDFLAGS -g3 -O0"
else
CPPFLAGS="$CPPFLAGS -g0 -O3"
LDFLAGS="$LDFLAGS -g0 -O3"
fi

LANG=C
AC_SUBST(LANG)

# check for rpmbuild
AC_CHECK_PROG(HAVE_RPMBUILD, rpmbuild, true, false)
AM_CONDITIONAL(HAVE_RPMBUILD,$HAVE_RPMBUILD)

# check for deb
AC_CHECK_PROG(HAVE_DEB, dh_clean, true, false)
AM_CONDITIONAL(HAVE_DEB,$HAVE_DEB)

AC_OUTPUT(
 Makefile 
 src/Makefile
 include/Makefile
 src/xml/Makefile
)
