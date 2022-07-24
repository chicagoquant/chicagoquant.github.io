
# Ninja

## Quickstart

```shell
cmake -S . -B build -G Ninja
cmake --build build
  -v        # verbose
  -j N      # parallel
  -t target

# may invoke with VERBOSE=1 cmake --build builds

```

### Minimal

```cmake
cmake_minimum_required(VERSION 3.15)

# set the project name and version
project(Tutorial VERSION 1.0)

...
```

### Diagnostics

- list cmake variables
```shell
cmake -LAH
```

- a function to print variables

```cmake
# optionally use a regular expression to print only a subset of variables with matching names
function(dump_cmake_variables)
    get_cmake_property(_variableNames VARIABLES)
    list (SORT _variableNames)
    foreach (_variableName ${_variableNames})
        if ((NOT DEFINED ARGV0) OR _variableName MATCHES ${ARGV0})
            message(STATUS "${_variableName}=${${_variableName}}")
        endif()
    endforeach()
endfunction()

dump_cmake_variables("Boost")
```

- to print environment variables seen by your script, insert this line in CMake file

```cmake
execute_process(COMMAND "${CMAKE_COMMAND}" "-E" "environment")
```

- list all imported targets

```
find_package(Python3 COMPONENTS Development Interpreter)
find_package(Boost COMPONENTS python)

get_property(blah DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}" PROPERTY IMPORTED_TARGETS)
# or 
get_directory)property(blah DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}" IMPORTED_TARGETS)

# a semicolon separated list
message(STATUS "Imported targets are --> ${blah}")
```


## List all targets

```shell
ninja -t targets all
```

## Ninja verbose

```shell
VERBOSE=1 ninja
ninja -v
ninja -d explain
```

## Misc ninja

```shell
ninja {all,test,install}
ninja path/to/module/{all,test,install}
```

# CMake

## Configure and Build

```shell
cmake -GNinja \
  -S source_dir \
  -B build_dir \
  -DCMAKE_INSTALL_PREFIX=install_dir \
  -DCMAKE_BUILD_TYPE=Debug \
  --debug-output / --trace

cmake --build build_dir --target {all,test,install}
```

## Useful variables

```shell
CMAKE_CXX_COMPILER=clang++
CMAKE_C_COMPILER=clang
CMAKE_CXX_CLANG_TIDY=clang-tidy

CMAKE_CXX_STANDARD=20
CMAKE_CXX_STANDARD=23

CMAKE_EXPORT_COMPILE_COMMANDS=on               # generates compile_commands.json

# these are set by CMake
CMAKE_SOURCE_DIR
CMAKE_BINARY_DIR
CMAKE_CURRENT_SOURCE_DIR
CMAKE_CURRENT_BINARY_DIR

# these are relative to most recent project() seen in CMakeLists
PROJECT_SOURCE_DIR
PROJECT_BINARY_DIR
```

## Sanitize

```shell
# sanitize thread
CMAKE_CXX_FLAGS += -fsanitize=thread
CMAKE_LD_FLAGS += -fsanitize=thread

# sanitize address
CMAKE_CXX_FLAGS += -fsanitize=address
CMAKE_CXX_FLAGS += -fsanitize-recover=all
CMAKE_CXX_FLAGS += -fno-omit-frame-pointer
CMAKE_CXX_FLAGS += -mno-omit-leaf-frame-pointer
CMAKE_LD_FLAGS += -fsanitize=address

CMAKE_LD_FLAGS += -static-libasan          # gcc

CMAKE_CXX_FLAGS += -D__SANITIZE_ADDRESS__  # clang
CMAKE_LD_FLAGS += -static-libsan           # clang

# sanitize undefined variable
CMAKE_CXX_FLAGS += -fsanitize=undefined
CMAKE_LD_FLAGS += -fsanitize=undefined

CMAKE_LD_FLAGS += -rtlib=compiler-rt -unwindlib=libgcc           # clang

```

## Commands

```cmake
add_executable(EXECUTABLE_NAME source1.cpp source2.cpp ...)

target_link_libraries(EXECUTABLE_NAME PUBLIC libname1 libname2 PRIVATE libname3 libname4)

install(TARGETS EXECUTABLE_NAME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)

project(PROJ_NAME)

add_compile_option(-Wblah)

include_directories(boost/latest/include)
target_include_directories(EXECUTABLE INTERFACE ...)

target_compile_features(EXECUTABLE PUBLIC cxx_std_23)

target_compile_definitions(EXECUTABLE PRIVATE -Dblah=bla)

add_dependencies(EXECUTABLE something)

add_subdirectory(subdir)

if (condition)
  return()
endif()

set(VARIABLE "value-str")

add_library(LIBRARY_NAME STATIC source1.cpp source2.cpp ...)
target_link_libraries(LIBNAME PUBLIC lib1 lib2 PRIVATE lib3 lib4)

find_package(PKGNAME REQUIRED)

add_custom_command(...)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

include(CTest)
enable_testing()

add_executable(test_NAME SRC source1.cpp source2.cpp)
target_link_libraries(test_NAME PUBLIC lib1 lib2 ... GTest::gtest_main)
target_compile_definitions(test_NAME PRIVATE extra_link_flags)
add_test(NAME test_NAME COMMAND test_NAME --param1 val1 --param2 val2 WORKING_DIRECTORY some_dir)

include(GoogleTest)
gtest_discover_tests(test_NAME)
```

## CMake Presets

```
CMakePresets.json
{ "version": 3, "configurePresets": [...]}
{ "name": "preset1", "generator": "Ninja", "binaryDir": "", "installDir", "cacheVariables": { "CMAKE_C_COMPILER": "clang", "CMAKE_CXX_COMPILER": "clang++", "CMAKE_BUILD_TYPE": "Debug" }}

$sourceDir
$presetName
$hostSystemName
$env{HOME}


CMakeUserPresets.json
```

# Tutorial

```text
#----------------------------------------------------
# cmake_minimum_required()
# project()
# add_executable()
cmake_minimum_required(VERSION 3.15)
project(tutorial)
add_executable(tutorial tutorial.cxx)


# CMAKE_CXX_STANDARD
# CMAKE_CXX_STANDARD_REQUIRED
# set()
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# project(... VERSION ...) automatically defines tutorial_VERSION_MAJOR tutorial_VERSION_MINOR
# configure_file()
project(tutorial VERSION 1.0)
configure_file(tutorialConfig.h.in tutorialConfig.h)
target_include_directories(tutorial PUBLIC "${PROJECT_BINARY_DIR}")

#----------------------------------------------------
# tutorialConfig.h.in
#define tutorial_VERSION_MAJOR @tutorial_VERSION_MAJOR@
#define tutorial_VERSION_MINOR @tutorial_VERSION_MINOR@

#include "tutorialConfig.h"
```

# Python in CMake

```
python3  -c 'import sysconfig; print(sysconfig.get_path("include"))'
python3  -c 'import sysconfig; print(sysconfig.get_path("stdlib"))'

Python3_EXECUTABLE = ... path to python exe ...
# or
Python3_ROOT = ... path to python install root ...
find_package(Python3 COMPONENTS Development Interpreter)
# will discover python3 based on hint Python3_ROOT and set variables
```

# Pytest in CMake

```
add_subdirectory(tests)

# tests/CMakeLists.txt
add_test(NAME test_blah1 COMMAND ${Python3_EXECUTABLE} -m pytest ${CMAKE_CURRENT_SOURCE_DIR})
set_tests_properties(test_blah1 PROPERTIES ENVIRONMENT "PYTHONPATH=${CMAKE_BINARY_DIR}/blah1:$ENV{PYTHONPATH}")

# tests/test_blah1.py

import pytest

def test_foobar():
    from hello_ext import greet
    assert greet() == "hello, world"
```

to run
```
cmake -GNinja -DCMAKE_INSTALL_PREFIX=$HOME/space
  -DPython3_EXECUTABLE=${PATH_TO_PYTHON}/bin/python3
  -DBoost_ROOT=${PATH_TO_BOOST_INSTALL}
  -DCMAKE_CXX_COMPILER=clang++
  -B $HOME/crap/build-blah
  $HOME/sources/blah

cmake --build $HOME/crap/build-blah --target all test install

cmake --build $HOME/crap/build-blah --target test

ctest --test-dir $HOME/crap/build-blah
```

# Boost in CMake

```
Boost_ROOT = ...
find_package(Boost COMPONENTS python)
```

- building boost

```
bootstrap.sh --with-python=path-to-python3-executable
# that would have build b2 executable, and produced project-config.jam

# define our own toolset gcc-crap in user-config.jam
# note 3 config files: site-config.jam, user-config.jam, project-config.jam
# user-config.jam can be put in ~/ or boost build path
cat tools/build/src/user-config.jam
using gcc
  : crap
  : ${MY_CUSTOM_CXX_PATH}
  : <cflags>"${MY_CUSTOM_CFLAGS}"
    <cxxflags>"${MY_CUSTOM_CXXFLAGS}"
  ;

./b2 
  -d2
  -j8
  --build-dir=my-junk-build     # build location
  --prefix=my-junk              # install location
  --with-system
  --with-log
  --with-filesystem
  --with-program_options
  --with-context
  --with-fiber
  --with-chrono
  --with-container
  --with-date_time
  --with-regex
  --with-thread
  --with-random
  --with-iostreams
  --with-serialization
  --with-coroutine
  --with-python
  -s ZLIB_INCLUDE=${ZLIB_ROOT_DIR}/include
  -s ZLIB_LIBRARY_PATH=${ZLIB_ROOT_DIR}/lib
  -s ZSTD_INCLUDE=${ZSTD_ROOT_DIR}/include
  -s ZSTD_LIBRARY_PATH=${ZSTD_ROOT_DIR}/lib64
  toolset=gcc-crap      # as defined in user-config.jam
  threading=multi
  runtime-link=shared
  link=static           # shared / static
  variant=release       # debug / release
  install               # optional target: stage / install
```

# Bazel

TBD
