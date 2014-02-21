project(gameclient.vba-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(xbmc REQUIRED)

include(ExternalProject)

externalproject_add(vba-next
                    GIT_REPOSITORY https://github.com/libretro/vba-next
                    GIT_TAG efc06a6
                    PREFIX vba-next
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -f Makefile.libretro
                    BUILD_IN_SOURCE 1)

set(VBA-NEXT_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/vba-next/src/vba-next/vba_next_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                           vba_next_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} vba-next)

build_addon(gameclient.vba-next VBA-NEXT DEPLIBS)
add_dependencies(gameclient.vba-next vba-next)
