set(JNETLIB_SOURCE
  "asyncdns.cpp"
  "asyncdns.h"
  "connection.cpp"
  "connection.h"
  "httpget.cpp"
  "httpget.h"
  "httpserv.cpp"
  "httpserv.h"
  "irc_util.h"
  "jnetlib.h"
  "listen.cpp"
  "listen.h"
  "netinc.h"
  "util.cpp"
  "util.h"
  "webserver.cpp"
  "webserver.h")

add_library(jnetlib-wdl ${JNETLIB_SOURCE})