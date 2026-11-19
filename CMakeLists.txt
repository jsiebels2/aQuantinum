cmake_minimum_required(VERSION 3.24)
project(aQuantinum LANGUAGES CXX)
 
# ---- Language standard -------------------------------------------------------
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
 
# ---- Default to Release (Debug FFT code is 10-50x slower) --------------------
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS Debug Release RelWithDebInfo)
endif()
 
# compile_commands.json for clangd / IntelliSense
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
 
# ---- Options -----------------------------------------------------------------
option(AQ_BUILD_TESTS "Build C++ unit tests" ON)
option(AQ_ENABLE_CUDA "Build the CUDA/cuFFT backend" OFF)   # not used yet
 
# ---- System dependencies (installed via apt, located with pkg-config) --------
find_package(PkgConfig REQUIRED)
pkg_check_modules(FFTW3  REQUIRED IMPORTED_TARGET fftw3)    # double precision
pkg_check_modules(FFTW3F REQUIRED IMPORTED_TARGET fftw3f)   # single precision
 
# ---- Modules -----------------------------------------------------------------
add_subdirectory(ComputeCore)
# add_subdirectory(DisplayLayer)      # step 3
# add_subdirectory(DecoherenceMode)   # step 4
# add_subdirectory(App)               # once there is something to wire up
 
if(AQ_BUILD_TESTS)
  enable_testing()
  add_subdirectory(tests)
endif()
 