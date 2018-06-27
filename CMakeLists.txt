cmake_minimum_required(VERSION 3.0.0)
project(imgui_tail VERSION 0.1.0)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
set(CMAKE_VERBOSE_MAKEFILE 1)

include_directories(include)
include_directories(imgui)
include_directories(imgui/gl3w)
include_directories(/usr/include/libdrm)

find_package(PkgConfig REQUIRED)
find_library(glfw /usr/lib/x86_64-linux-gnu/)

execute_process(COMMAND pkg-config --static --libs glfw3 OUTPUT_VARIABLE var OUTPUT_STRIP_TRAILING_WHITESPACE)


file(GLOB SRC_IMGUI ${PROJECT_SOURCE_DIR}/imgui/*.cpp)
file(GLOB SRC_Gl3w ${PROJECT_SOURCE_DIR}/imgui/gl3w/GL/*.cpp)
file(GLOB SRC ${PROJECT_SOURCE_DIR}/src/*cpp)
file(GLOB HDR ${PROJECT_SOURCE_DIR}/include/*.h)

add_executable(imgui_tail main.cpp ${SRC_IMGUI} ${SRC_Gl3w})
target_link_libraries(imgui_tail GL ${var})