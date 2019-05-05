cmake_minimum_required(VERSION 3.4.1)
project(python3 LANGUAGES C)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fexceptions -Wno-unused-result -Wsign-compare \
 -DNDEBUG -g -fwrapv -O3 -Wall -Wextra -Wno-unused-result -Wno-unused-parameter
  -Wno-missing-field-initializers -Werror=implicit-function-declaration ")

add_definitions(-DHAVE_STD_ATOMIC)
add_definitions(-DPy_BUILD_CORE)

set(python_src
        Parser/acceler.c
        Modules/main.c
        )

add_library( pythonlib STATIC
        ${python_src})

target_include_directories(pythonlib PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/include)

#

set(python_main
       Programs/python.c)
add_executable(python ${python_main})
target_include_directories(python PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(python pythonlib)


