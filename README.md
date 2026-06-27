# cmake-ready-imgui-sdl3

Dear ImGui with SDL3 backend, packaged for CMake FetchContent.

## Vendored version

- Dear ImGui: **v1.92.8** (https://github.com/ocornut/imgui/releases/tag/v1.92.8)
- Source obtained: 2026-06-27
- Branch: master (non-docking)

## Included backends

- `imgui_impl_sdl3` (platform)
- `imgui_impl_sdlrenderer3` (renderer)

## Usage

```cmake
include(FetchContent)

# SDL3 must be available before this is fetched
FetchContent_Declare(SDL3
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG release-3.2.0  # adjust to whatever you're pinning
)
FetchContent_MakeAvailable(SDL3)

FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/LoshkinOleg/cmake-ready-imgui-sdl3.git
    GIT_TAG        5acd6de3ed4efb06d665628b01fba0fe3e63f7bc
    GIT_SHALLOW    FALSE # Has to be FALSE to be able to use a commit SHA 
)
FetchContent_MakeAvailable(imgui)

target_link_libraries(my_app PRIVATE imgui::imgui)

## Updating

To bump to a newer ImGui release:
1. Download the release tarball from https://github.com/ocornut/imgui/releases
2. Replace imgui*.{cpp,h}, imstb_*.h, imconfig.h at the repo root
3. Replace files in backends/ (only the SDL3 ones we use)
4. Verify LICENSE.txt is still current
5. Update this README's version line
6. Tag as `vX.Y.Z-sdl3-cmake-N`
