cmake_minimum_required(VERSION 3.11.1)

project(hello)

set(SOURCES src/hello.c)

add_library(${PROJECT_NAME} STATIC ${SOURCES})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/inc)

