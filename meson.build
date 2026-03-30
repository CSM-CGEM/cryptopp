project(
    'cryptopp',
    'cpp',
    version: '8.9.0',
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

cpp = meson.get_compiler('cpp')

arch = host_machine.cpu_family()

cryptopp_inc = include_directories('.')

cryptopp_sources = files(
    'rsa.cpp',
    'sha.cpp', #
    'filters.cpp', #
    'base64.cpp', #
    'pssr.cpp', #

    # 'pch.cpp', # this file is basically a precompiled header, but it is not used in the CGEM library, so we can skip it.
    'nbtheory.cpp', #
    'algparam.cpp', #
    'fips140.cpp', #
    'pkcspad.cpp', #
    'emsa2.cpp', #
    'ripemd.cpp', #
    'whrlpool.cpp', #
    'misc.cpp', #
    'mqueue.cpp', #
    'cpu.cpp', #
    'integer.cpp', #
    'asn.cpp', #
    'pubkey.cpp', #
    'cryptlib.cpp', #
    'queue.cpp',
    'iterhash.cpp', #

    'osrng.cpp', #
    'algebra.cpp',
    'allocate.cpp',
    'ecp.cpp',
)

# | -- [cryptopp] Compiler definitions:  CRYPTOPP_DISABLE_ASM=1;_WIN32_WINNT=0x0A00
# | -- [cryptopp] Compiler options: /DWIN32 /D_WINDOWS /EHsc  /FIwinapifamily.h;/GR;/MP;/EHsc
if host_machine.system() == 'windows'
    add_project_arguments('-D_WIN32_WINNT=0x0A00', language: 'cpp')

    msvc = meson.get_compiler('cpp').get_id() == 'msvc'

    has_winapifamily = cpp.has_header('winapifamily.h')
    if msvc and has_winapifamily
        add_project_arguments('/FIwinapifamily.h', language: 'cpp')
    endif
endif

thread_dep = dependency('threads')

cryptopp_lib = library(
    'cryptopp',
    cryptopp_sources,
    include_directories: cryptopp_inc,
    dependencies: thread_dep,
)

cryptopp_dep = declare_dependency(
    link_with: cryptopp_lib,
    include_directories: cryptopp_inc,
    dependencies: thread_dep,
)
