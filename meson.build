project(
    'cryptopp',
    'cpp',
    version: '8.9.0,
    default_options: [
        'cpp_std=c++20',
        'buildtype=release',
        'b_ndebug=if-release',
        'b_vscrt=from_buildtype',
        'default_library=static',
    ],
    meson_version: '>=1.3',
)

# Note this is a minimal build for the CGEM library, not the full cryptopp library.

add_project_arguments('-DCRYPTOPP_DISABLE_ASM', language: 'cpp')

cryptopp_inc = include_directories('.')

cryptopp_sources = files(
    'rsa.cpp',
    'sha.cpp',
    'filters.cpp',
    'base64.cpp',
    'pssr.cpp',
)

cryptopp_lib = library(
    'cryptopp',
    cryptopp_sources,
    include_directories: cryptopp_inc,
)

cryptopp_dep = declare_dependency(
    link_with: cryptopp_lib,
    include_directories: cryptopp_inc,
)
