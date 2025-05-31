project(B VERSION 0.1.0)
include(A.cmake)

project_include_guard()
message("PROJECT B")
add_subdirectory(A)
