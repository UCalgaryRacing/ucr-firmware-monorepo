cmake_minimum_required(VERSION 3.22)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

    set(CMAKE_BUILD_TYPE "Debug")

# Set the project name
set(CMAKE_PROJECT_NAME front_controller)

# Include toolchain file
include("cmake/gcc-arm-none-eabi.cmake")


# STM32Cube generated symbols (macros)
set(MX_Defines_Syms 
	USE_PWR_LDO_SUPPLY 
	USE_HAL_DRIVER 
	STM32H753xx 
	STM32_THREAD_SAFE_STRATEGY=2
    $<$<CONFIG:Debug>:DEBUG>
)

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)


project(${CMAKE_PROJECT_NAME})


# Enable CMake support for ASM and C languages
enable_language(C ASM)

# Create an executable object type
add_executable(${CMAKE_PROJECT_NAME})


# Application sources
set(Application_Src
    ${CMAKE_SOURCE_DIR}/Src/main.c
    ${CMAKE_SOURCE_DIR}/Src/gpio.c
    ${CMAKE_SOURCE_DIR}/Src/memorymap.c
    ${CMAKE_SOURCE_DIR}/Src/stm32h7xx_it.c
    ${CMAKE_SOURCE_DIR}/Src/stm32h7xx_hal_msp.c
    ${CMAKE_SOURCE_DIR}/Src/sysmem.c
    ${CMAKE_SOURCE_DIR}/Src/syscalls.c
    ${CMAKE_SOURCE_DIR}/startup_stm32h753xx.s
    ${CMAKE_SOURCE_DIR}/Src/system_stm32h7xx.c
)
target_sources(${CMAKE_PROJECT_NAME} PRIVATE ${Application_Src})


# Create STM32_Drivers static library
add_library(STM32_Drivers OBJECT)

# STM32 HAL/LL Drivers
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

# Interface library for includes and symbols
add_library(stm32cubemx INTERFACE)

# STM32CubeMX generated include paths
set(MX_Include_Dirs
    ${CMAKE_SOURCE_DIR}/Inc
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc/Legacy
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
    ${CMAKE_SOURCE_DIR}/../../external/STM32CubeH7/Drivers/CMSIS/Include
)
target_include_directories(stm32cubemx INTERFACE ${MX_Include_Dirs})

target_compile_definitions(stm32cubemx INTERFACE ${MX_Defines_Syms}) # defined near top of file

target_link_libraries(STM32_Drivers PUBLIC stm32cubemx)

target_link_libraries(${CMAKE_PROJECT_NAME} STM32_Drivers)


# Add the map file to the list of files to be removed with 'clean' target
set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES ADDITIONAL_CLEAN_FILES ${CMAKE_PROJECT_NAME}.map)

# Validate that STM32CubeMX code is compatible with C standard
if((CMAKE_C_STANDARD EQUAL 90) OR (CMAKE_C_STANDARD EQUAL 99))
    message(ERROR "Generated code requires C11 or higher")
endif()
