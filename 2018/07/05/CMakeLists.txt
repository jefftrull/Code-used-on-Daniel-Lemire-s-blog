# CMake build control file for inner product testbench

cmake_minimum_required( VERSION 3.5 )

add_compile_options( -std=c++17 -Wall -Wextra -Werror )
set( CMAKE_CXX_FLAGS_RELEASE "-O3 -DNDEBUG -march=native" )

add_executable( dotproduct dotproduct.cpp )
target_compile_options( dotproduct PRIVATE -ffast-math )
add_executable( dotproductstandard dotproduct.cpp )
