# Cloud Build Harness Validation

## Current workflow status

- Workflow path: .github/workflows/build-rpcs3-task9.yml
- Trigger: workflow_dispatch
- Runner: windows-2022
- Artifact: RPCS3_TASK9_TRACE_2416d652

## Source and patch

- RPCS3 commit pinned: 2416d652625eaed5df2ff8d67063fa145021a883
- Recursive submodule initialization: YES
- Patch included: patches/RPCS3_TASK9_LIVE_TRACE_FIXED.patch
- Patch SHA256: $patchSha
- Patch validation included: git apply --check --whitespace=error-all
- Patch whitespace check included: git diff --check

## Qt

- Python setup: ctions/setup-python@v6, Python 3.12
- Qt install method: manual python -m aqt install-qt
- Pinned aqt source: git+https://github.com/miurahr/aqtinstall.git@9e49c82edc6d946db376dec907cca5b4b486eec5
- Qt version: 6.11.2
- Qt arch: win64_msvc2022_64
- Qt modules: qtmultimedia qtsvg
- install-qt-action occurrences: 0
- Qt verification/fail-early: YES

## Vulkan

- Vulkan SDK version: 1.4.341.1
- Download URL: https://sdk.lunarg.com/sdk/download/$sdkVersion/windows/vulkan_sdk.exe
- Copy-only CI install: copy_only=1
- Installer exit-code check: YES
- SDK root validation: YES
- glslangValidator.exe validation: YES
- ulkan.h validation: YES

## LLVM

- Precompiled LLVM download: REMOVED
- Historical llvmlibs_mt.7z download: REMOVED
- Stale precompiled path removed before build: pcs3-src\build\lib_ext\Release-x64
- LLVM build method: MSBuild rpcs3.sln /t:llvm_build
- LLVM configuration: Release|x64
- Same MSBuild/MSVC path used for LLVM and RPCS3: YES
- LLVM output validation: searches generated LLVM*.lib files and reports representative libs.

## RPCS3 build

- Solution: pcs3.sln
- Configuration: Release
- Platform: x64
- RPCS3 build runs after llvm_build: YES
- RPCS3 build exit-code check: YES

## Local structural validation

PASS

Checks passed:

- workflow file exists
- patch path exists
- workflow_dispatch exists
- runner is windows-2022
- exact RPCS3 commit appears in workflow
- recursive submodule update appears in workflow
- git apply --check --whitespace=error-all appears in workflow
- Qt 6.11.2 appears in workflow
- Vulkan SDK 1.4.341.1 appears in workflow
- MSBuild discovery appears in workflow
- llvm_build target appears before RPCS3 build
- precompiled LLVM download strings are absent
- Release x64 build setting appears in workflow
- artifact upload appears in workflow

## Not performed locally

- GitHub Actions workflow was not run locally.
- RPCS3 was not built locally.
- No PES files were modified.
- No DATA.BIN, EDIT.bin, or dt0c files were touched.
