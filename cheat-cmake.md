
# Ninja

## List all targets

```
ninja -t targets all
```

## Ninja verbose

```
VERBOSE=1 ninja
ninja -v
ninja -d explain
```

## Misc ninja

```
ninja {all,test,install}
ninja path/to/module/{all,test,install}
```

# CMake

## Configure and Build

```
cmake -GNinja \
  -S source_dir \
  -B build_dir \
  -DCMAKE_INSTALL_PREFIX=install_dir \
  -DCMAKE_BUILD_TYPE=Debug \
  --debug-output / --trace

cmake --build build_dir --target {all,test,install}
```

## Useful variables

```
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
```

## Sanitize

```
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

```
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