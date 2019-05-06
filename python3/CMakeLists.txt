cmake_minimum_required(VERSION 3.4.1)
project(python3 LANGUAGES CXX C)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall \
   -std=c99 -Wextra -Wno-unused-result -Wno-unused-parameter -Wno-missing-field-initializers \
   -Werror=implicit-function-declaration ")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall \
    -std=c99 -Wextra -Wno-unused-result -Wno-unused-parameter -Wno-missing-field-initializers  \
    -Werror=implicit-function-declaration")

add_definitions(-DHAVE_STD_ATOMIC)
add_definitions(-DPy_BUILD_CORE)

set(py_modules_src
        Modules/main.c
        )

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
set(py_python_src
        Python/_warnings.c
        Python/asdl.c
        Python/ast.c
        Python/ast_opt.c
        Python/ast_unparse.c
        Python/bltinmodule.c
        Python/bootstrap_hash.c
        Python/ceval.c
        Python/codecs.c
        Python/compile.c
        Python/context.c
        Python/dtoa.c
        Python/dup2.c
        Python/dynamic_annotations.c
        Python/dynload_shlib.c
        Python/errors.c
        Python/fileutils.c
        Python/formatter_unicode.c
        Python/frozen.c
        Python/frozenmain.c
        Python/future.c
        Python/getargs.c
        Python/getcompiler.c
        Python/getcopyright.c
        Python/getopt.c
        Python/getplatform.c
        Python/getversion.c
        Python/graminit.c
        Python/hamt.c
        Python/import.c
        Python/importdl.c
        Python/marshal.c
        Python/modsupport.c
        Python/mysnprintf.c
        Python/mystrtoul.c
        Python/pathconfig.c
        Python/peephole.c
        Python/pyarena.c
        Python/pyctype.c
        Python/pyfpe.c
        Python/pyhash.c
        Python/pylifecycle.c
        Python/pymath.c
        Python/pystate.c
        Python/pystrcmp.c
        Python/pystrhex.c
        Python/pystrtod.c
        Python/Python-ast.c
        Python/pythonrun.c
        Python/pytime.c
        Python/structmember.c
        Python/symtable.c
        Python/sysmodule.c
        Python/thread.c
        Python/traceback.c
        )


add_library( pythonlib STATIC
        ${py_modules_src}
        ${py_objects_src}
        ${py_parser_src}
        ${py_python_src}
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


