# CMake build control file for inner product testbench

cmake_minimum_required( VERSION 3.5 )

add_compile_options( -std=c++17 -Wall -Wextra -Werror )

# Release build by default
if( NOT CMAKE_BUILD_TYPE )
  set( CMAKE_BUILD_TYPE Release CACHE STRING "Default build type (Debug, Release, RelWithDebInfo)" FORCE )
endif()
set( CMAKE_CXX_FLAGS_RELEASE "-g -O3 -DNDEBUG -march=native" )
set( CMAKE_CXX_FLAGS_DEBUG "-g -O0 -fno-omit-frame-pointer -march=native" )

# We need Boost for HPX
find_package( Boost 1.65 REQUIRED COMPONENTS system program_options filesystem )

# Set up HPX
if (NOT DEFINED HPX_ROOT)
  message(FATAL_ERROR "please supply a path to the HPX install directory with -DHPX_ROOT=<some-path>")
endif()

add_library( HPX::HPX SHARED IMPORTED )
set_target_properties( HPX::HPX PROPERTIES
  IMPORTED_LOCATION ${HPX_ROOT}/lib/libhpx.so
  INTERFACE_LINK_LIBRARIES Boost::filesystem
  INTERFACE_INCLUDE_DIRECTORIES ${HPX_ROOT}/include
  INTERFACE_SYSTEM_INCLUDE_DIRECTORIES ${HPX_ROOT}/include
)

add_executable( dotproduct dotproduct.cpp )
target_compile_options( dotproduct PRIVATE -ffast-math )
target_link_libraries( dotproduct HPX::HPX Boost::program_options ${HPX_ROOT}/lib/libhpx_init.a )
add_executable( dotproductstandard dotproduct.cpp )
target_link_libraries( dotproductstandard HPX::HPX Boost::program_options ${HPX_ROOT}/lib/libhpx_init.a )

