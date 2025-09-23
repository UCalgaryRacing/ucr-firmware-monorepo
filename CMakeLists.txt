cmake_minimum_required(VERSION 3.22)

# Include toolchain file
include("gcc-arm-none-eabi.cmake")

# Set actual project name and languages
project(ucr-firmware-monorepo
        LANGUAGES C CXX ASM)

# C standard options
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

add_subdirectory(applications)
add_subdirectory(external)

