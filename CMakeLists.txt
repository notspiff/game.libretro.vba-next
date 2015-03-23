project(game.libretro.vba-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make -f Makefile.libretro platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make -f Makefile.libretro ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make -f Makefile.libretro platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

include(ExternalProject)
externalproject_add(vba-next
                    GIT_REPOSITORY https://github.com/libretro/vba-next
                    GIT_TAG efc06a6
                    PREFIX vba-next
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(VBA-NEXT_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/vba-next/src/vba-next/vba_next_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                           game.libretro.vba-next${CMAKE_SHARED_LIBRARY_SUFFIX} vba-next)

build_addon(game.libretro.vba-next VBA-NEXT DEPLIBS)
add_dependencies(game.libretro.vba-next vba-next)

include(CPack)
