cmake_minimum_required(VERSION 3.19)

project(SdlWithCMake VERSION 1.0)

include(FetchContent)

set(BUILD_SHARED_LIBS OFF)
FetchContent_Declare(
    SDL2
    GIT_REPOSITORY https://github.com/libsdl-org/SDL
    GIT_TAG release-2.28.1
)
FetchContent_MakeAvailable(SDL2)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED true)

include_directories(include)

file(GLOB_RECURSE SOURCES "src/*.cpp")

add_executable(
    SdlWithCMake
    ${SOURCES}
)
target_link_libraries(
    SdlWithCMake
    SDL2::SDL2 SDL2::SDL2main
)

add_custom_command(
    TARGET SdlWithCMake POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${PROJECT_SOURCE_DIR}/resources $<TARGET_FILE_DIR:SdlWithCMake>/resources
)
