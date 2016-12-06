cmake_minimum_required(VERSION 3.1)
project(game.libretro.vba-next)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_package(libretro-vba-next REQUIRED)

set(VBA-NEXT_CUSTOM_BINARY ${VBA-NEXT_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} VBA-NEXT "")