cmake_minimum_required(VERSION 3.19)

project(SdlWithCMake VERSION 1.0)

if (DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE $ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake CACHE STRING "")
endif()

find_package(sdl2 CONFIG REQUIRED)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED true)

file(GLOB_RECURSE SOURCES "src/*.cpp")

add_executable(
    SdlWithCMake
    ${SOURCES}
)

target_link_libraries(SdlWithCMake PRIVATE SDL2::SDL2 SDL2::SDL2main)

add_custom_command(
    TARGET SdlWithCMake POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${PROJECT_SOURCE_DIR}/resources $<TARGET_FILE_DIR:SdlWithCMake>/resources
)
