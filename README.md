# imgui-sdl3-cmake

Dear ImGui with SDL3 backend, packaged for CMake FetchContent.

## Vendored version

- Dear ImGui: **v1.91.8** (https://github.com/ocornut/imgui/releases/tag/v1.92.8)
- Source obtained: 2026-06-27
- Branch: master (non-docking)

## Included backends

- `imgui_impl_sdl3` (platform)
- `imgui_impl_sdlrenderer3` (renderer)

## Usage

[FetchContent snippet]

## Updating

To bump to a newer ImGui release:
1. Download the release tarball from https://github.com/ocornut/imgui/releases
2. Replace imgui*.{cpp,h}, imstb_*.h, imconfig.h at the repo root
3. Replace files in backends/ (only the SDL3 ones we use)
4. Verify LICENSE.txt is still current
5. Update this README's version line
6. Tag as `vX.Y.Z-sdl3-cmake-N`