cmake_minimum_required(VERSION 3.11.1)

project(basePrj)

add_subdirectory(libs/hello)

set(SOURCES src/main.c)

add_executable(${PROJECT_NAME} ${SOURCES})
target_link_libraries(${PROJECT_NAME} hello)

