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

## Qt, Vulkan, LLVM

- Python setup: ctions/setup-python@v6, Python 3.12
- Qt: manual install, version 6.11.2, arch win64_msvc2022_64, modules qtmultimedia qtsvg
- Vulkan SDK: 1.4.341.1, official ulkan_sdk.exe URL, copy-only CI install
- LLVM: direct MSBuild of 3rdparty\llvm\llvm_build.vcxproj, no precompiled LLVM archive

## RPCS3 build and test exclusion

- Original pcs3.sln is copied to temporary pcs3_task9_ci.sln before final application build.
- Original pcs3.sln is not edited by the workflow.
- Test project GUID excluded from temp solution Build.0 mappings: D1CBF84E-07F8-4ACB-9CD2-BD205FDEEE1E
- Test project Release|x64.ActiveCfg is verified preserved.
- Main RPCS3 project GUID: 70CD65B0-91D6-4FAE-9A7B-4AF55D0D1B12
- Main Release|x64.ActiveCfg is verified with -SimpleMatch and braces included.
- Main Release|x64.Build.0 is verified with -SimpleMatch and braces included.
- Old missing-brace regex check is removed.
- GoogleTest installation: NOT USED
- Final application build uses pcs3_task9_ci.sln.
- pcs3.exe verification added after build: FullName, Length, LastWriteTime.

## Local structural validation

PASS

Checks passed:

- old $mainGuid\.Release\|x64\.Build\.0 regex is absent
- -SimpleMatch is used for solution GUID verification
- test Build.0 mappings are removed while ActiveCfg is preserved
- main Release ActiveCfg and Build.0 are both verified
- LLVM local source build remains unchanged
- final MSBuild uses the CI solution
- exact RPCS3 commit and instrumentation patch remain unchanged

## Not performed locally

- GitHub Actions workflow was not run locally.
- RPCS3 was not built locally.
- No PES files were modified.
- No DATA.BIN, EDIT.bin, or dt0c files were touched.
