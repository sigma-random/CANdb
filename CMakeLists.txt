cmake_minimum_required(VERSION 3.0.0)

project(CANdb CXX C)

option(WITH_COVERAGE "Build with coverage" OFF)
option(WITH_TESTS "Build with test" ON)
option(WITH_TOOLS "Build example dbc tools" ON)

set(CMAKE_CXX_STANDARD 14)

find_package(Threads REQUIRED)
find_package(Boost REQUIRED)

add_subdirectory(3rdParty)

if(WITH_COVERAGE)
    set(CMAKE_CXX_FLAGS "-g -O0 -Wwrite-strings -fprofile-arcs -ftest-coverage")
    set(CMAKE_C_FLAGS="-g -O0 -Wall -W -fprofile-arcs -ftest-coverage")
    set(CMAKE_EXE_LINKER_FLAGS="-fprofile-arcs -ftest-coverage")
endif()

add_subdirectory(src)

if((WITH_TESTS OR WITH_COVERAGE))
    enable_testing()
    add_subdirectory(tests)
endif()

if(WITH_TOOLS)
    add_subdirectory(tools)
endif(WITH_TOOLS)
