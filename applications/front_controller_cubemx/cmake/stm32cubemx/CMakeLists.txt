cmake_minimum_required(VERSION 3.22)
# Enable CMake support for ASM and C languages
enable_language(C ASM)
# STM32CubeMX generated symbols (macros)
set(MX_Defines_Syms 
	USE_PWR_LDO_SUPPLY 
	USE_HAL_DRIVER 
	STM32H753xx 
	STM32_THREAD_SAFE_STRATEGY=4
    $<$<CONFIG:Debug>:DEBUG>
)

# STM32CubeMX generated include paths
set(MX_Include_Dirs
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Inc
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Inc/Legacy
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/include
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS_V2
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/CMSIS/Device/ST/STM32H7xx/Include
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/CMSIS/Include
)

# STM32CubeMX generated application sources
set(MX_Application_Src
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/main.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/gpio.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/freertos.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/adc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/dac.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/eth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/fdcan.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/i2c.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/rng.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/rtc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/sdmmc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/spi.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/usart.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/stm32h7xx_it.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/stm32h7xx_hal_msp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/stm32h7xx_hal_timebase_tim.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/sysmem.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/syscalls.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../startup_stm32h753xx.s
)

# STM32 HAL/LL Drivers
set(STM32_Drivers_Src
    ${CMAKE_CURRENT_SOURCE_DIR}/../../Src/system_stm32h7xx.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_tim.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_tim_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_adc.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_adc_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rcc.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rcc_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_flash.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_flash_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_gpio.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_hsem.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dma.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dma_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_mdma.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_pwr.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_pwr_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_cortex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_i2c.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_i2c_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_exti.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dac.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_dac_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_eth.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_eth_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_fdcan.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rng.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rng_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rtc.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_rtc_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_ll_sdmmc.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_ll_delayblock.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_sd.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_sd_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_mmc.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_mmc_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_spi.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_spi_ex.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_uart.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Drivers/STM32H7xx_HAL_Driver/Src/stm32h7xx_hal_uart_ex.c
)

# Drivers Midllewares


set(FreeRTOS_Src
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/croutine.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/event_groups.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/list.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/queue.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/stream_buffer.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/tasks.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/timers.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS_V2/cmsis_os2.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/portable/MemMang/heap_4.c
    C:/Users/Ryland/repos/ucr-firmware-monorepo/external/STM32CubeH7/Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/port.c
)

# Link directories setup
set(MX_LINK_DIRS

)
# Project static libraries
set(MX_LINK_LIBS 
    STM32_Drivers
    ${TOOLCHAIN_LINK_LIBRARIES}
    FreeRTOS	
)
# Interface library for includes and symbols
add_library(stm32cubemx INTERFACE)
target_include_directories(stm32cubemx INTERFACE ${MX_Include_Dirs})
target_compile_definitions(stm32cubemx INTERFACE ${MX_Defines_Syms})

# Create STM32_Drivers static library
add_library(STM32_Drivers OBJECT)
target_sources(STM32_Drivers PRIVATE ${STM32_Drivers_Src})
target_link_libraries(STM32_Drivers PUBLIC stm32cubemx)


# Create FreeRTOS static library
add_library(FreeRTOS OBJECT)
target_sources(FreeRTOS PRIVATE ${FreeRTOS_Src})
target_link_libraries(FreeRTOS PUBLIC stm32cubemx)

# Add STM32CubeMX generated application sources to the project
target_sources(${CMAKE_PROJECT_NAME} PRIVATE ${MX_Application_Src})

# Link directories setup
target_link_directories(${CMAKE_PROJECT_NAME} PRIVATE ${MX_LINK_DIRS})

# Add libraries to the project
target_link_libraries(${CMAKE_PROJECT_NAME} ${MX_LINK_LIBS})

# Add the map file to the list of files to be removed with 'clean' target
set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES ADDITIONAL_CLEAN_FILES ${CMAKE_PROJECT_NAME}.map)

# Validate that STM32CubeMX code is compatible with C standard
if((CMAKE_C_STANDARD EQUAL 90) OR (CMAKE_C_STANDARD EQUAL 99))
    message(ERROR "Generated code requires C11 or higher")
endif()
