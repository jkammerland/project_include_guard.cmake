add_subdirectory(A)
add_subdirectory(B)

include(include_guard1/HELLO.cmake)
include(include_guard2/HELLO.cmake)

include(list_file_include_guard1/HELLO.cmake)
include(list_file_include_guard2/HELLO.cmake)
