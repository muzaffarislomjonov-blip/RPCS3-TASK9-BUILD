# Build Requirements

These requirements come from the `BUILDING.md` file in RPCS3 commit:

`2416d652625eaed5df2ff8d67063fa145021a883`

## GitHub runner

- `windows-2022`

## Toolchain

- Visual Studio 2022 / MSBuild
- Python 3.6 or newer
- Qt `6.11.2`
- Qt compiler kit `msvc2022_64`
- Qt modules: `qtmultimedia`, `qtsvg`
- Vulkan SDK `1.4.341.1`

## Build mode

- RPCS3 solution: `rpcs3.sln`
- Configuration: `Release`
- Platform: `x64`

## LLVM dependency strategy

The workflow uses the precompiled LLVM archive referenced by this commit's `BUILDING.md`:

`https://github.com/RPCS3/llvm-mirror/releases/download/custom-build-win-22.1.8/llvmlibs_mt.7z`

It extracts the archive to:

`rpcs3-src\build\lib_ext\Release-x64`

This avoids building LLVM from source during the GitHub Actions run.

## Safety

The harness must not include:

- PES game files
- PS3 firmware
- save data
- `DATA.BIN`
- `EDIT.bin`
- `dt0c`
- copyrighted game content
