cmake_minimum_required(VERSION 3.21)

project(vcpkg_test)

# vcpkgを利用するようにする
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE $ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake CACHE STRING "")
endif()

option(CMAKE_BUILD_SHARED False)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_COMPILER_FORCED True)

#find_package(Boost 1.79.0 REQUIRED)

add_library(vcpkg_test
    source/library.cpp
)

target_include_directories(vcpkg_test PUBLIC
    include
)

install(
    TARGETS vcpkg_test
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
)

install(
    DIRECTORY ${CMAKE_SOURCE_DIR}/include/
    DESTINATION include
)