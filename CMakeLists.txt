cmake_minimum_required(VERSION 3.20)
project(udpchat CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
include(CompilerWarnings)

add_executable(udpchat src/main.cpp)
set_project_warnings(udpchat)

include(CTest)
if(BUILD_TESTING)
  add_subdirectory(tests)
endif()
