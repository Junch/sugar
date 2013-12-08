# Copyright (c) 2013, Ruslan Baratov
# All rights reserved.

# Example of using sugar_add_ios_gtest command to run gtest with ios simulator

cmake_minimum_required(VERSION 2.8.8)
project(03-example-ios-gtest CXX)

if(NOT XCODE_VERSION)
  sugar_fatal_error("Xcode only")
endif()

include("$ENV{SUGAR_ROOT}/cmake/Sugar")
include(sugar_add_ios_gtest)
include(sugar_set_xcode_ios_sdkroot)

# Install gtest ios using this project:
#     * 'https://github.com/hunter-packages/gtest'
# Note that it is just example, you don't need to install gtest manually
# if you're using "hunter" package manager (github.com/ruslo/hunter)
set(GTEST_ROOT "${CMAKE_CURRENT_LIST_DIR}/Install/")
find_package(GTest REQUIRED)

include_directories("${GTEST_INCLUDE_DIRS}")
add_executable(simple_test MACOSX_BUNDLE simple_test.cpp)
target_link_libraries(simple_test ${GTEST_BOTH_LIBRARIES})

set(MACOSX_BUNDLE_GUI_IDENTIFIER "com.example.sugar.ios.gtest")

sugar_set_xcode_ios_sdkroot(TARGET simple_test)

enable_testing()
sugar_add_ios_gtest(SimpleTestName simple_test)