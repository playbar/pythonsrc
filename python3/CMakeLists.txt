cmake_minimum_required(VERSION 3.4.1)
project(python3 LANGUAGES C)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fexceptions -Wno-unused-result -Wsign-compare \
 -DNDEBUG -g -fwrapv -O3 -Wall -Wextra -Wno-unused-result -Wno-unused-parameter
  -Wno-missing-field-initializers -Werror=implicit-function-declaration ")

add_definitions(-DHAVE_STD_ATOMIC)
add_definitions(-DPy_BUILD_CORE)

set(py_objects_src
        Objects/abstract.c
        Objects/accu.c
        Objects/boolobject.c
        Objects/bytearrayobject.c
        Objects/bytes_methods.c
        Objects/bytesobject.c
        Objects/call.c
        Objects/capsule.c
        Objects/cellobject.c
        Objects/classobject.c
        Objects/codeobject.c
        Objects/complexobject.c
        Objects/descrobject.c
        Objects/dictobject.c
        Objects/enumobject.c
        Objects/exceptions.c
        Objects/fileobject.c
        Objects/floatobject.c
        Objects/frameobject.c
        Objects/funcobject.c
        Objects/genobject.c
        Objects/iterobject.c
        Objects/listobject.c
        Objects/longobject.c
        Objects/memoryobject.c
        Objects/methodobject.c
        Objects/moduleobject.c
        Objects/namespaceobject.c
        Objects/object.c
        Objects/obmalloc.c
        Objects/odictobject.c
        Objects/rangeobject.c
        Objects/setobject.c
        Objects/sliceobject.c
        Objects/structseq.c
        Objects/tupleobject.c
        Objects/typeobject.c
        Objects/unicodectype.c
        Objects/unicodeobject.c
        Objects/weakrefobject.c
        )

set(py_parser_src
        Parser/acceler.c
        Parser/bitset.c
        Parser/firstsets.c
        Parser/grammar.c
        Parser/grammar1.c
        Parser/listnode.c
        Parser/metagrammar.c
        Parser/myreadline.c
        Parser/node.c
        Parser/parser.c
        Parser/parsetok.c
        Parser/pgen.c
        Parser/tokenizer.c
        )

set(py_modules_src
        Modules/main.c
        )

add_library( pythonlib STATIC
        ${py_modules_src}
        ${py_objects_src}
        ${py_parser_src}
       )

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


