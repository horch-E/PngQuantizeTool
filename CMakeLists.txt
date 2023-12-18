cmake_minimum_required(VERSION 3.26)
project(PngQuantizeTool)
set(CMAKE_CXX_STANDARD 17)

set(SOURCE_DIR imagequant/include)

include_directories(${SOURCE_DIR})

set(SOURCE main.cpp ${SOURCE_DIR}/lodepng.cpp)

link_directories(imagequant/lib)

add_executable(PngQuantizeTool ${SOURCE})

target_link_libraries(PngQuantizeTool libimagequant.a)

add_custom_command(TARGET PngQuantizeTool POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  "${CMAKE_CURRENT_SOURCE_DIR}/build/PngQuantizeTool.wasm"
        "${CMAKE_SOURCE_DIR}/static/PngQuantizeTool.wasm")
add_custom_command(TARGET PngQuantizeTool POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  "${CMAKE_CURRENT_SOURCE_DIR}/build/PngQuantizeTool.js"
        "${CMAKE_SOURCE_DIR}/static/PngQuantizeTool.js")