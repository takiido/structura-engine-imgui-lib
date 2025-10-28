cmake_minimum_required(VERSION 3.20)
project(imgui LANGUAGES CXX)

set(IMGUI_SOURCES
    src/imgui.cpp
    src/imgui_draw.cpp
    src/imgui_tables.cpp
    src/imgui_widgets.cpp
)

set(IMGUI_BACKEND_SOURCES
    backends/src/imgui_impl_sdl3.cpp
    backends/src/imgui_impl_opengl3.cpp
    backends/src/imgui_impl_sdlrenderer3.cpp
)

find_package(OpenGL REQUIRED)

add_library(imgui STATIC
    ${IMGUI_SOURCES}
    ${IMGUI_BACKEND_SOURCES}
)

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/backends/include
)

# Link libraries
target_link_libraries(imgui PUBLIC
    SDL3::SDL3
    OpenGL::GL
    ${CMAKE_DL_LIBS}
)

target_compile_features(imgui PUBLIC cxx_std_23)
