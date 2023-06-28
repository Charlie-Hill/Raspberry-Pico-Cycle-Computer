cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(flashprint C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(PICO_BOARD pico_w)

pico_sdk_init()

add_executable(mainfile
    main.c
)

pico_enable_stdio_usb(mainfile 1)
pico_enable_stdio_uart(mainfile 0)

pico_add_extra_outputs(mainfile)

# target_include_directories(mainfile PRIVATE ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(mainfile pico_stdlib pico_cyw43_arch_none)
