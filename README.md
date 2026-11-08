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

GitHub lists each archive's SHA-256 on the release page. intellect's
`scripts/fetch_dawn.py` pins those hashes, so it rejects an archive that
changes after release.

To add a release, run the **Build Dawn** workflow with a Dawn release tag
such as `v20261016.190333`, and optionally a JSON list of platforms to build.
It builds with the cache file Dawn's own release builds use
(`.github/workflows/dawn-ci.cmake`), plus `DAWN_BUILD_MONOLITHIC_LIBRARY=SHARED`
and without samples, tests, GLFW, X11, Wayland or OpenGL, then adds the
archives to the release with that tag. An archive built on another machine
with the same steps can be added with `gh release upload <tag> <archive>`;
the release notes say which archives were built that way.

Dawn is BSD-3-Clause (`LICENSE-dawn.txt` in each archive); the Windows
archive's DXC is under the University of Illinois/NCSA license
(`LICENSE-dxc.txt`).
