﻿cmake_minimum_required (VERSION 3.8)

add_executable (nesemu "main.c"  "cpu.h" "types.h" "bus.h" "bus.c" "cartridge.h" "cpu.c" "cartridge.c" "opcodes.c" "log.c" "ppu.h" "ppu.c" "mapper.h" "mappers/mapper000.h" "mappers/mapper000.c" "mapper.c")

target_include_directories(nesemu PUBLIC ${SDL2_INCLUDE_DIRS})
target_link_libraries(nesemu PUBLIC ${SDL2_LIBRARIES})

if(MSVC)
target_compile_definitions(nesemu PUBLIC _CRT_SECURE_NO_WARNINGS)
endif()

add_custom_command(TARGET nesemu POST_BUILD
	COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_SOURCE_DIR}/roms $<TARGET_FILE_DIR:nesemu>/roms
)
