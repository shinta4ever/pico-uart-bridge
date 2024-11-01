cmake_minimum_required(VERSION 3.13...3.27)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(uart_bridge)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

add_executable(uart_bridge uart-bridge.c usb-descriptors.c)
target_compile_definitions(uart_bridge PRIVATE
  PICO_DEFAULT_UART_TX_PIN=16
  PICO_DEFAULT_UART_RX_PIN=17
  )
target_include_directories(uart_bridge PUBLIC
	./
	pico-sdk/lib/tinyusb/src)

target_link_libraries(uart_bridge
	hardware_flash
	pico_multicore
	pico_stdlib
	tinyusb_device)

pico_add_extra_outputs(uart_bridge)
