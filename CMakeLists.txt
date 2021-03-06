project(inputstream.mpd)

cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)
find_package(kodiplatform REQUIRED)
find_package(p8-platform REQUIRED)


set(MPD_SOURCES src/Main.cpp)

list(APPEND DEPLIBS ${p8-platform_LIBRARIES})
if(WIN32)
  list(APPEND DEPLIBS ws2_32)
endif()

include_directories(${INCLUDES}
                    ${kodiplatform_INCLUDE_DIRS}
                    ${p8-platform_INCLUDE_DIRS}
                    ${KODI_INCLUDE_DIR}
                    lib/libbento4/Core)
                    
add_subdirectory(lib/libbento4)
list(APPEND DEPLIBS bento4)
					
build_addon(inputstream.mpd MPD DEPLIBS)

include(CPack)
