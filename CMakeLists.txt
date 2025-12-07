cmake_minimum_required(VERSION 3.5.0)
project(StreamPilot C)

set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

file(DOWNLOAD https://raw.githubusercontent.com/nicbarker/clay/refs/heads/main/clay.h ${PROJECT_SOURCE_DIR}/external/clay/clay.h)

set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # don't build the supplied examples
set(BUILD_GAMES    OFF CACHE BOOL "" FORCE) # don't build the supplied example games

include(FetchContent)
set(FETCHCONTENT_QUIET FALSE)
FetchContent_Declare(
  SDL
  GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
  GIT_TAG release-3.2.28
  GIT_SHALLOW TRUE
  GIT_PROGRESS TRUE
  PATCH_COMMAND ${CMAKE_COMMAND} -E chdir <SOURCE_DIR> git checkout -q . && ${CMAKE_COMMAND} -E chdir <SOURCE_DIR> git apply ${PROJECT_SOURCE_DIR}/SDL_cocoametalview_resize.patch
)
FetchContent_MakeAvailable(SDL)


FetchContent_Declare(
  SDL_ttf
  GIT_REPOSITORY https://github.com/libsdl-org/SDL_ttf.git
  GIT_TAG release-3.2.2
  GIT_SHALLOW TRUE
  GIT_PROGRESS TRUE
)
FetchContent_MakeAvailable(SDL_ttf)


FetchContent_Declare(
  SDL_image
  GIT_REPOSITORY "https://github.com/libsdl-org/SDL_image.git"
  GIT_TAG release-3.2.4
  GIT_SHALLOW TRUE
  GIT_PROGRESS TRUE
)
FetchContent_MakeAvailable(SDL_image)


include_directories(external)

add_executable(${PROJECT_NAME} main.c)
target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3 SDL3_ttf::SDL3_ttf SDL3_image::SDL3_image)
