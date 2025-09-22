cmake_minimum_required(VERSION 3.22)

# Set a variable to hold the project name
set(CMAKE_PROJECT_NAME barebones_test)

# Include toolchain file
include("gcc-arm-none-eabi.cmake")

# Set actual project name and languages
project(${CMAKE_PROJECT_NAME}
        LANGUAGES C CXX ASM)

# C standard options
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)


# --- TARGET: application executable ---
add_executable(${CMAKE_PROJECT_NAME})
set(Application_Src
    ${CMAKE_SOURCE_DIR}/src/main.c
    #${CMAKE_SOURCE_DIR}/Src/gpio.c
    #${CMAKE_SOURCE_DIR}/Src/memorymap.c
    #${CMAKE_SOURCE_DIR}/Src/stm32h7xx_it.c
    #${CMAKE_SOURCE_DIR}/Src/stm32h7xx_hal_msp.c
    #${CMAKE_SOURCE_DIR}/Src/sysmem.c
    #${CMAKE_SOURCE_DIR}/Src/syscalls.c
    #${CMAKE_SOURCE_DIR}/startup_stm32h753xx.s
    #${CMAKE_SOURCE_DIR}/Src/system_stm32h7xx.c
)
target_sources(${CMAKE_PROJECT_NAME} PRIVATE ${Application_Src})
# -----------------------------------


# --- TARGET: STM32_Drivers static library ---
add_library(STM32_Drivers OBJECT)
set(STM32_Drivers_Src
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_cortex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rcc.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rcc_ex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_flash.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_flash_ex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_gpio.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_hsem.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dma.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dma_ex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_mdma.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_pwr.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_pwr_ex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_i2c.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_i2c_ex.c
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_exti.c
)
target_sources(STM32_Drivers PRIVATE ${STM32_Drivers_Src})
# -----------------------------------


# --- TARGET: Interface library for includes and symbols --- This effectively lets you use '#include "header.h"' without the full file path
add_library(stm32cubemx INTERFACE)
set(MX_Include_Dirs
    ${CMAKE_SOURCE_DIR}/Inc
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc/Legacy
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/CMSIS/Include
)
target_include_directories(stm32cubemx INTERFACE ${MX_Include_Dirs})
set(MX_Defines_Syms 
	USE_PWR_LDO_SUPPLY 
	USE_HAL_DRIVER 
	STM32H753xx 
	STM32_THREAD_SAFE_STRATEGY=2
    $<$<CONFIG:Debug>:DEBUG>
)
target_compile_definitions(stm32cubemx INTERFACE ${MX_Defines_Syms})
# -----------------------------------

# "STM32_Drivers" library depends on "stm32cubemx" library
target_link_libraries(STM32_Drivers PUBLIC stm32cubemx)

# Our actual executable target depends on "STM32_Drivers" library
target_link_libraries(${CMAKE_PROJECT_NAME} STM32_Drivers)


# Add the map file to the list of files to be removed with 'clean' target
set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES ADDITIONAL_CLEAN_FILES ${CMAKE_PROJECT_NAME}.map)

