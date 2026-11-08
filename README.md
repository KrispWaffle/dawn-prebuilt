# dawn-prebuilt

Prebuilt [Dawn](https://dawn.googlesource.com/dawn) shared libraries for
[intellect](https://github.com/KrispWaffle/intellect)'s WebGPU backend. Each
release holds Dawn's C API (`webgpu.h`) as one library, built from the Google
Dawn release with the same tag:

| Archive | Contents | Needs |
| --- | --- | --- |
| `dawn-<tag>-linux-x64.tar.gz` | `libwebgpu_dawn.so` (Vulkan) | glibc 2.28+, a Vulkan driver |
| `dawn-<tag>-macos-arm64.tar.gz` | `libwebgpu_dawn.dylib` (Metal) | macOS 13+ on Apple silicon |
| `dawn-<tag>-windows-x64.tar.gz` | `webgpu_dawn.dll`, `dxcompiler.dll` (D3D12) | Windows 10+, the Visual C++ runtime |

`SHA256SUMS` lists each archive's hash. intellect's `scripts/fetch_dawn.py`
pins those hashes, so it rejects an archive that changes after release.

To add a release, run the **Build Dawn** workflow with a Dawn release tag
such as `v20261016.190333`. It builds with the cache file Dawn's own release
builds use (`.github/workflows/dawn-ci.cmake`), plus
`DAWN_BUILD_MONOLITHIC_LIBRARY=SHARED` and without samples, tests, GLFW, X11,
Wayland or OpenGL.

Dawn is BSD-3-Clause (`LICENSE-dawn.txt` in each archive); the Windows
archive's DXC is under the University of Illinois/NCSA license
(`LICENSE-dxc.txt`).
