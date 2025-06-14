cmake_minimum_required(VERSION 3.20)

project(project_include_guard VERSION 1.2.4)

get_property(
  ${PROJECT_NAME}_INITIALIZED GLOBAL
  PROPERTY "${PROJECT_NAME}_INITIALIZED"
  SET)
if(${PROJECT_NAME}_INITIALIZED)
  project_include_guard()
endif()

include(${CMAKE_CURRENT_LIST_DIR}/list_file_include_guard.cmake)
include(${CMAKE_CURRENT_LIST_DIR}/project_include_guard.cmake)

option(${PROJECT_NAME}_BUILD_TESTS "Build tests" OFF)
if(${PROJECT_NAME}_BUILD_TESTS)
  message("Hello from project_include_guard")
  add_subdirectory(tests)
endif()
