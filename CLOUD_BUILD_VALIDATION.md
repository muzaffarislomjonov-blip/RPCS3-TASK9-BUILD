# Cloud Build Harness Validation

## Local validation performed

- Fixed instrumentation patch is present at patches/RPCS3_TASK9_LIVE_TRACE_FIXED.patch.
- Patch SHA256:

$patchSha

- Workflow path exists:

.github/workflows/build-rpcs3-task9.yml

- Workflow trigger is workflow_dispatch.
- Runner is windows-2022.
- RPCS3 commit is pinned to:

2416d652625eaed5df2ff8d67063fa145021a883

- Recursive submodule initialization is included.
- Patch validation commands are included:

`powershell
git apply --check --whitespace=error-all $patch
git diff --check
`

- Qt is configured as 6.11.2 / win64_msvc2022_64.
- Vulkan SDK is configured as 1.4.341.1.
- Visual Studio / MSBuild discovery is included.
- Release x64 build is configured for pcs3.sln.
- Precompiled LLVM library extraction path is configured:

pcs3-src\build\lib_ext\Release-x64

- Artifact upload is configured as:

RPCS3_TASK9_TRACE_2416d652

## YAML validation

Local structural validation: PASS

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
- Release build setting appears in workflow
- artifact upload appears in workflow

Note: no external YAML parser is installed locally in this Windows environment. The workflow was not executed in GitHub Actions in this phase.

## Not performed in this phase

- The GitHub Actions build was not run locally.
- RPCS3 was not built locally.
- No PES files were modified.
- No DATA.BIN, EDIT.bin, or dt0c files were touched.
