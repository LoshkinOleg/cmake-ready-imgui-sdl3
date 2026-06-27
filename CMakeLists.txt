cmake_minimum_required(VERSION 3.20)

project(imgui
    VERSION 1.92.8
    DESCRIPTION "Dear ImGui with SDL3 backend, CMake-ready"
    LANGUAGES CXX
)

option(IMGUI_BUILD_SDL3_RENDERER  "Build the SDL3 renderer backend"     ON)
option(IMGUI_BUILD_DEMO           "Include imgui_demo.cpp"              ON)

if(NOT TARGET SDL3::SDL3)
    find_package(SDL3 QUIET CONFIG)
    if(NOT SDL3_FOUND)
        message(FATAL_ERROR
            "imgui requires SDL3::SDL3 to be available. "
            "FetchContent SDL3 in your parent project before this one, "
            "or install it system-wide."
        )
    endif()
endif()

set(IMGUI_SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    backends/imgui_impl_sdl3.cpp
)

if(IMGUI_BUILD_DEMO)
    list(APPEND IMGUI_SOURCES imgui_demo.cpp)
endif()

if(IMGUI_BUILD_SDL3_RENDERER)
    list(APPEND IMGUI_SOURCES backends/imgui_impl_sdlrenderer3.cpp)
endif()

add_library(imgui STATIC ${IMGUI_SOURCES})
add_library(imgui::imgui ALIAS imgui)

target_include_directories(imgui PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/backends>
)

target_compile_features(imgui PUBLIC cxx_std_17)
target_link_libraries(imgui PUBLIC SDL3::SDL3)

if(IMGUI_BUILD_SDL3_OPENGL3)
    find_package(OpenGL REQUIRED)
    target_link_libraries(imgui PUBLIC OpenGL::GL)
endif()

set(IMGUI_USER_CONFIG "" CACHE STRING "Path to custom imconfig.h replacement")
if(IMGUI_USER_CONFIG)
    target_compile_definitions(imgui PUBLIC IMGUI_USER_CONFIG="${IMGUI_USER_CONFIG}")
endif()