cmake_minimum_required(VERSION 3.11.1)

project(targetPrj)

set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)
set(CMAKE_CROSSCOMPILING 1)

set(GCC_PATH /tri/ti/css901/ccs/tools/compiler/gcc-arm-none-eabi-7-2017-q4-major/bin)

set(CMAKE_C_COMPILER ${GCC_PATH}/arm-none-eabi-gcc CACHE PATH "" FORCE)
set(CMAKE_C_OBJCOPY ${GCC_PATH}/arm-none-eabi-objcopy CACHE PATH "" FORCE)

set(SOURCES src/main.c src/tm4c123gh6pm_startup_ccs_gcc.c)

set(CMAKE_C_FLAGS "-mcpu=cortex-m4 -march=armv7e-m -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16 -DPART_TM4C123GH6PM -ffunction-sections -fdata-sections -Wall -specs=\"nosys.specs\"")

set(CMAKE_C_FLAGS_RELEASE "-Os")
set(CMAKE_C_FLAGS_DEBUG "-Og -g -gdwarf-3 -gstrict-dwarf")
set(CMAKE_EXE_LINKER_FLAGS "--entry ResetISR -Wl,-T\"../tm4c123gh6pm.lds\"")

add_subdirectory(libs/hello)

add_executable(${PROJECT_NAME}.elf ${SOURCES})
target_link_libraries(${PROJECT_NAME}.elf hello)

add_custom_target(${PROJECT_NAME}.bin ALL DEPENDS ${PROJECT_NAME}.elf)
add_custom_command(TARGET ${PROJECT_NAME}.bin
    COMMAND ${CMAKE_C_OBJCOPY} ARGS -O binary ${PROJECT_NAME}.elf ${PROJECT_NAME}.bin)
