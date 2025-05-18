cmake_minimum_required(VERSION 3.20)

project(project_include_guard VERSION 1.1.0)

include(${CMAKE_CURRENT_LIST_DIR}/project_include_guard.cmake)
include(${CMAKE_CURRENT_LIST_DIR}/list_file_include_guard.cmake)
project_include_guard()

option(${PROJECT_NAME}_BUILD_TESTS "Build tests" OFF)
if(${PROJECT_NAME}_BUILD_TESTS)
  message("Hello from project_include_guard")
  add_subdirectory(tests)
endif()
