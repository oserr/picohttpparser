cmake_minimum_required(VERSION 3.25)
project(picohttpparser CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (NOT CMAKE_BUILD_TYPE OR (CMAKE_BUILD_TYPE STREQUAL ""))
  set(CMAKE_BUILD_TYPE "Debug")
endif()

string(TOLOWER "${CMAKE_BUILD_TYPE}" build_type)
message(STATUS "Building ${CMAKE_PROJECT_NAME} in ${build_type} mode")

#############################
# picohttpparser
#############################

add_library(picohttpparser STATIC
  picohttpparser.c
  picohttpparser.h)

if (build_type STREQUAL "debug")
  target_compile_options(picohttpparser PRIVATE -Wall -Wextra -Wpedantic -Og)
else()
  target_compile_definitions(picohttpparser PRIVATE NDEBUG)
  target_compile_options(picohttpparser PRIVATE -Wall -Wextra -Wpedantic -Ofast)
endif()

set_target_properties(picohttpparser PROPERTIES LINKER_LANGUAGE CXX)
target_compile_features(picohttpparser PUBLIC cxx_std_20)
