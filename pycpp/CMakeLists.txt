# demo

cmake_minimum_required(VERSION 3.6)
project(algorithm LANGUAGES CXX C)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -fpermissive -fvisibility=hidden -std=c++17" )
set(CMAKE_CXX_STANDARD 17)

add_definitions(-Werror=return-type)

add_executable(test1
        test1.cpp)

target_include_directories(test1 PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/../python3/Include
        ${CMAKE_CURRENT_SOURCE_DIR}/../python3
)