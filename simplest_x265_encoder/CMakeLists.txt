cmake_minimum_required(VERSION 2.9 FATAL_ERROR)
cmake_policy(VERSION 2.9)
project(simple_x265_encoder)

find_package(PkgConfig REQUIRED)

set(PKG_CONFIG_USE_CMAKE_PREFIX_PATH 1)

list(APPEND CMAKE_PREFIX_PATH /opt/workspace/cp/x265_install)

message(STATUS "Using CMAKE_PREFIX_PATH: \"${CMAKE_PREFIX_PATH}\"")

#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} /usr/lib/x86_64-linux-gnu)

message(STATUS "PKG_CONFIG_VERSION_STRING: ${PKG_CONFIG_VERSION_STRING}")

pkg_search_module(X265 REQUIRED x265)
message(STATUS "Using x265: ${X265_FOUND}")

find_package(Threads REQUIRED)



#pkg_check_modules(x265 REQUIRED IMPORTED_TARGET x265)
#pkg_search_module(SDL2 REQUIRED sdl2>=2.0.1)

message(STATUS "x ${X265_INCLUDE_DIRS} ${X265_LIBRARIES}")

add_executable(encoder simplest_x265_encoder.cpp)
target_link_libraries(encoder ${X265_LINK_LIBRARIES}  ${CMAKE_DL_LIBS} Threads::Threads numa)
target_include_directories(encoder PUBLIC ${X265_INCLUDE_DIRS})