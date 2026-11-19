include(FetchContent)
 
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG        v1.15.2
  GIT_SHALLOW    TRUE
)
set(INSTALL_GTEST OFF CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
 
add_executable(compute_tests
  test_fft_smoke.cpp
)
target_link_libraries(compute_tests
  PRIVATE aq::ComputeCore GTest::gtest_main
)
target_compile_options(compute_tests PRIVATE -Wall -Wextra -Wpedantic)
 
include(GoogleTest)
gtest_discover_tests(compute_tests)