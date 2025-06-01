project(A VERSION 1.100.0) # NEWER VERSION SHOULD PRODUCE WARNING
include(list_file_include_guard.cmake)
project_include_guard()
message("  PROJECT A")

message(FATAL_ERROR "PROJECT A, ERROR")
