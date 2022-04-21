cmake_minimum_required(VERSION 3.10)

project(hello_world_with_formatter_ex)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CURRENT_SOURCE_DIR /Users/daniildanilov/lab06_timp) 

add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world_application/hello_world.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib)

find_library(formatter_ex NAMES libformatter_ex.a PATHS ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib)
find_library(formatter NAMES libformatter.a PATHS ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib)

target_link_libraries(hello_world /Users/daniildanilov/lab03_timp/formatter_lib/_build/libformatter.a)
target_link_libraries(hello_world /Users/daniildanilov/lab03_timp/formatter_ex_lib/_build/libformatter_ex.a)
