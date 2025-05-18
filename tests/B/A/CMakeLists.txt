project(A VERSION 1.2) # NEWER VERSION SHOULD PRODUCE WARNING
project_include_guard()
message("  PROJECT A")

message(FATAL_ERROR "PROJECT A, ERROR")
