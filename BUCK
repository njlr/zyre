include_defs('//BUCKAROO_DEPS')

MACOS_PLATFORM_H = """
/* #undef HAVE_LINUX_WIRELESS_H */
#define HAVE_NET_IF_H
#define HAVE_NET_IF_MEDIA_H
#define HAVE_GETIFADDRS
#define HAVE_FREEIFADDRS
"""

genrule(
  name = 'macos-platform.h',
  out = 'platform.h',
  cmd = 'echo "' + MACOS_PLATFORM_H + '" > $OUT ',
)

cxx_library(
  name = 'zyre',
  header_namespace = '',
  exported_headers = subdir_glob([
    ('include', '*.h'),
  ]),
  platform_headers = [
    ('default', { 'platform.h': ':macos-platform.h' }),
    ('^macos.*', { 'platform.h': ':macos-platform.h' }),
  ],
  srcs = glob([
    'src/*.c',
  ],
  excludes = glob([
    'src/zyre_selftest.c',
  ])),
  visibility = [
    'PUBLIC',
  ],
  deps = BUCKAROO_DEPS,
)
