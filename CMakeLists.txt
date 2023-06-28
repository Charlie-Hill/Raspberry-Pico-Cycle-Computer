cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)
project(mainfile C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(PICO_BOARD pico_w)

pico_sdk_init()

# add a compilation subdirectory
add_subdirectory(lib/Config)
add_subdirectory(lib/e-Paper)
add_subdirectory(lib/Fonts)
add_subdirectory(lib/GUI)

# add a header directory
include_directories(./lib/Config)
include_directories(./lib/GUI)
include_directories(./lib/e-Paper)
include_directories(./lib/Fonts)


add_executable(mainfile
    main.c
)

# enable uart output, disable usb output
pico_enable_stdio_uart(mainfile 1)
pico_enable_stdio_usb(mainfile 1)

pico_add_extra_outputs(mainfile)

target_link_libraries(mainfile pico_stdlib pico_cyw43_arch_none hardware_adc ePaper GUI Fonts Config pico_stdlib hardware_spi)

