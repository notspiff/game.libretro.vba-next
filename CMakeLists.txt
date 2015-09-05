project(game.libretro.vba-next)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)
find_package(libretro-vba-next REQUIRED)

set(DEPLIBS vba-next)
set(VBA_NEXT_CUSTOM_BINARY ${VBA_NEXT_LIB}
                           game.libretro.vba-next${CMAKE_SHARED_LIBRARY_SUFFIX} vba-next)

build_addon(game.libretro.vba-next VBA_NEXT DEPLIBS)
