# CMake build control file for inner product testbench

cmake_minimum_required( VERSION 3.5 )

add_compile_options( -std=c++17 -Wall -Wextra -Werror )

# Release build by default
if( NOT CMAKE_BUILD_TYPE )
  set( CMAKE_BUILD_TYPE Release CACHE STRING "Default build type (Debug, Release, RelWithDebInfo)" FORCE )
endif()
set( CMAKE_CXX_FLAGS_RELEASE "-g -O3 -DNDEBUG -march=native" )
set( CMAKE_CXX_FLAGS_DEBUG "-g -O0 -fno-omit-frame-pointer -march=native" )

add_executable( dotproduct dotproduct.cpp )
target_compile_options( dotproduct PRIVATE -ffast-math )
add_executable( dotproductstandard dotproduct.cpp )
