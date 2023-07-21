set(GIFLIB_SOURCE
  "config.h"
  "dgif_lib.c"
  "egif_lib.c"
  "gifalloc.c"
  "gif_hash.c"
  "gif_hash.h"
  "gif_lib.h"
  "gif_lib_private.h")

add_library(giflib-wdl ${GIFLIB_SOURCE})