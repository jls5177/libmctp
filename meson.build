project('libmctp', 
    'c',
    version: '0.0.1.dev0',
    license: 'MIT',
    meson_version: '>= 0.64.0',
    default_options: [
        'default_library=static',
        'buildtype=debugoptimized',
        'c_std=gnu17',
        'cpp_std=c++17',
    ],
)

cc = meson.get_compiler('c')

# C warning flags: Checks all required args once at the start of the build
Wno_unused_parameter = cc.get_supported_arguments('-Wno-unused-parameter')
Wno_sign_compare = cc.get_supported_arguments('-Wno-sign-compare')
Wno_type_limits = cc.get_supported_arguments('-Wno-type-limits')
Wno_ignored_qualifiers = cc.get_supported_arguments('-Wno-ignored-qualifiers')

src_files = [
    'alloc.c',
    'core.c',
    'log.c',
    'libmctp.h',
    'serial.c',
]

libmctp_c_args = [
  '-DMCTP_LOG_STDERR',
  '-DMCTP_HAVE_STDIO',
  '-DMCTP_DEFAULT_ALLOC'
]
#libmctp_c_args += ['-DMCTP_HAVE_FILEIO']

inc = include_directories('.')

libmctp_lib = library('libmctp',
    src_files,
    c_args: [
        libmctp_c_args, 
        cc.get_supported_arguments(
        '-Wnull-dereference',
        '-Wpointer-to-int-cast',
        '-Wformat=2',
        ),
        Wno_unused_parameter,
        Wno_sign_compare,
        Wno_type_limits,
        Wno_ignored_qualifiers,
  ],
  include_directories : inc,
  install : true,
)

# Expose the library as a dependency with correct include directory
libmctp_dep = declare_dependency(
    include_directories : inc,
    link_with : libmctp_lib,
)
