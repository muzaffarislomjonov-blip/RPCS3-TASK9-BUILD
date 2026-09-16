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

## Qt and Vulkan

- Python setup: ctions/setup-python@v6, Python 3.12
- Qt install: manual python -m aqt install-qt, Qt 6.11.2, arch win64_msvc2022_64
- Qt modules: qtmultimedia qtsvg
- Vulkan SDK: 1.4.341.1, official ulkan_sdk.exe URL, copy-only CI install

## LLVM

- Precompiled LLVM download: REMOVED
- Historical llvmlibs_mt.7z download: REMOVED
- LLVM build method: direct MSBuild of 3rdparty\llvm\llvm_build.vcxproj
- Old solution-level LLVM target invocation on pcs3.sln: ABSENT
- SolutionDir explicitly supplied to the project build: YES
- LLVM configuration: Release|x64
- LLVM output validation: checks uild\lib\Release-x64\llvm_build and generated LLVM*.lib files.

## RPCS3 build

- Original pcs3.sln is copied to temporary pcs3_task9_ci.sln before final application build.
- Original pcs3.sln is not edited by the workflow.
- Test project GUID excluded from temp solution Build.0 mappings: D1CBF84E-07F8-4ACB-9CD2-BD205FDEEE1E
- Main RPCS3 project GUID Build.0 mapping verified present: 70CD65B0-91D6-4FAE-9A7B-4AF55D0D1B12
- GoogleTest installation: NOT USED
- Final application build uses pcs3_task9_ci.sln.
- pcs3.exe verification added after build: FullName, Length, LastWriteTime.

## Local structural validation

PASS

Checks passed:

- workflow file exists
- patch path exists
- workflow_dispatch exists
- exact RPCS3 commit appears in workflow
- Qt 6.11.2 and Vulkan SDK 1.4.341.1 remain configured
- LLVM local source build remains configured
- no GoogleTest install command appears
- temporary CI solution creation appears
- test project Build.0 removal appears
- main RPCS3 Build.0 preservation check appears
- final build uses CI solution
- rpcs3.exe verification appears
- artifact upload appears

## Not performed locally

- GitHub Actions workflow was not run locally.
- RPCS3 was not built locally.
- No PES files were modified.
- No DATA.BIN, EDIT.bin, or dt0c files were touched.
