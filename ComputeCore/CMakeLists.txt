add_library(ComputeCore
  src/fft_smoke.cpp
)
add_library(aq::ComputeCore ALIAS ComputeCore)
 
# Users of ComputeCore get #include <aq/compute/...>
target_include_directories(ComputeCore
  PUBLIC  ${CMAKE_CURRENT_SOURCE_DIR}/include
  PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src
)
 
# FFTW is an implementation detail: PRIVATE as long as no public header
# includes <fftw3.h>.
target_link_libraries(ComputeCore
  PRIVATE PkgConfig::FFTW3 PkgConfig::FFTW3F
)
 
# Warnings on our code only, not on third-party code
target_compile_options(ComputeCore PRIVATE -Wall -Wextra -Wpedantic)
 