lib_LTLIBRARIES = libemanedleplayer.la

libemanedleplayer_la_CPPFLAGS=          \
 -I@top_srcdir@/include                 \
 $(AM_CFLAGS)                           \
 $(LIBXML2_CFLAGS)

libemanedleplayer_la_SOURCES=           \
 shimlayer.cc                           \
 dlepclientimpl.cc                      \
 dlepmodemservice.cc

EXTRA_DIST =                            \
 shimlayer.h                            \
 dlepclientimpl.h                       \
 dlepmodemservice.h


libemanedleplayer_la_LIBADD=            \
 $(LIBXML2_LIBS)                        \
 -lboost_system                         \
 -lboost_thread                         \
 -ldlep

libemanedleplayer_la_LDFLAGS=           \
 -avoid-version

clean-local:
	rm -f $(BUILT_SOURCES)
