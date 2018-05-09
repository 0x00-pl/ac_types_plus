# for cpp 17 support
cmake_minimum_required(VERSION 3.9)


message(${CMAKE_CURRENT_SOURCE_DIR})
message(${CMAKE_CURRENT_BINARY_DIR})

# running directory guard
if(${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_CURRENT_BINARY_DIR})
    message(FATAL_ERROR "do not run this. run in another directory or run make")
endif()

enable_testing()
PROJECT(AC_DATATYPE_PLUS)
include( CTest )

set(CTEST_PROJECT_NAME "AC_DATATYPE_PLUS")
set(CTEST_NIGHTLY_START_TIME "01:00:00 UTC")

set(CTEST_DROP_METHOD "http")
set(CTEST_DROP_SITE "127.0.0.1:8888")
set(CTEST_DROP_LOCATION "/")
set(CTEST_DROP_SITE_CDASH TRUE)


set(CMAKE_CXX_STANDARD 17)
set_property(GLOBAL PROPERTY CXX_STANDARD 17)
set(CMAKE_VERBOSE_MAKEFILE ON)

if(CMAKE_COMPILER_IS_GNUCC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -ftemplate-depth=4096 -fpermissive -g")
    link_libraries("stdc++fs" m)
endif()


set_property(GLOBAL PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}")

include_directories(include)
include_directories(cppitertools)

if(${TEST_EIGEN})
    add_subdirectory(eigen)
endif()

add_subdirectory(test)