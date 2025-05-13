cmake_minimum_required(VERSION 3.20)

project(project_include_guard VERSION 1.0.0)

include(${CMAKE_CURRENT_LIST_DIR}/project_include_guard.cmake)
project_include_guard()

if(${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_SOURCE_DIR})
  message("Hello from project_include_guard")
  add_subdirectory(tests)
endif()
