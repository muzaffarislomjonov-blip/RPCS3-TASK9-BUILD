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

The workflow builds RPCS3's LLVM dependency from source using the exact source/submodule state checked out by this RPCS3 revision.

It intentionally does not download the historical precompiled LLVM archive, because that binary package produced MSVC STL unresolved externals on the GitHub runner.

Before building LLVM, the workflow removes any stale precompiled path:

`rpcs3-src\build\lib_ext\Release-x64`

Then it runs:

```powershell
& $env:MSBUILD_EXE rpcs3.sln `
  3rdparty\llvm\llvm_build.vcxproj `
  /m `
  /p:Configuration=Release `
  /p:Platform=x64 `
  /p:PreferredToolArchitecture=x64 `
  "/p:SolutionDir=<rpcs3-src>\"
```

The workflow builds the `llvm_build.vcxproj` project directly. It does not invoke the old solution-level LLVM target form on `rpcs3.sln`.

This makes LLVM and RPCS3 use the same Visual Studio/MSVC toolchain in the same workflow while avoiding target propagation to unrelated projects.

## Safety

The harness must not include:

- PES game files
- PS3 firmware
- save data
- `DATA.BIN`
- `EDIT.bin`
- `dt0c`
- copyrighted game content
