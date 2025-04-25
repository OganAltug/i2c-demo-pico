# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

cmake_minimum_required(VERSION 3.12)

# Pull in PICO SDK (must be before project)
include(pico_sdk_import.cmake)

project(pico_examples C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)


set(PICO_EXAMPLES_PATH ${PROJECT_SOURCE_DIR})


# Initialize the SDK
pico_sdk_init()


add_executable(voltmeter-i2c
        voltmeter-i2c.c
        )

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(voltmeter-i2c 0)
pico_enable_stdio_usb(voltmeter-i2c 1)

# Pull in our pico_stdlib which pulls in commonly used features
target_link_libraries(voltmeter-i2c pico_stdlib hardware_uart hardware_adc hardware_i2c)

# create map/bin/hex file etc.
pico_add_extra_outputs(voltmeter-i2c)

# add url via pico_set_program_url
#example_auto_set_url(voltmeter-i2c)
