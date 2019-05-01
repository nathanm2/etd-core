# The minimum version of cmake required to build this project:
cmake_minimum_required(VERSION 3.5)
project(etd-core C CXX)

#-- ETD Core Library ----------------------------------------------------------

set(etd_core_hdrs
    etd/etd.h
    )

set(etd_core_srcs
    src/frame_decoder.c
    )

add_library(etd_core ${etd_core_srcs} ${etd_core_hdrs})

target_include_directories(etd_core PUBLIC include)

# All consumers of the shared library version of 'etd' need the
# 'USE_SHARED_ETD_CORE' defined.  Hence the interface definition.
#
# 'DEFINE_SYMBOL' is a target property set by CMake when building a shared
# library.  It defaults to 'etd_EXPORTS', but we'd prefer BUILD_SHARED_ETD_CORE.
if(${BUILD_SHARED_LIBS})
    target_compile_definitions(etd_core INTERFACE USE_SHARED_ETD_CORE)
    set_target_properties(etd_core PROPERTIES DEFINE_SYMBOL
        BUILD_SHARED_ETD_CORE)
endif()
