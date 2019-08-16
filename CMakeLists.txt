cmake_minimum_required(VERSION 3.6)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

message(${CMAKE_CXX_COMPILER_ID})

add_definitions(-Werror=return-type)

add_subdirectory(python3)
add_subdirectory(pycpp)

MESSAGE("make files end")




#target_link_libraries()