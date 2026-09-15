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

## O1ARCH1H1C-FIX1 Qt installer update

- Python is pinned through ctions/setup-python@v5 with version 3.12.
- install-qt-action@v4 now uses explicit host, 	arget, and rch inputs.
- qtsource is set to git+https://github.com/miurahr/aqtinstall.git to avoid the older default aqtinstall 3.3.x Qt 6.11.x layout issue.
- setup-python: false is set so the action uses the pinned Python environment.
- Qt verification/fail-early step added before Vulkan/LLVM/RPCS3 build.

## O1ARCH1H1C-FIX2 manual Qt install update

- Removed jurplel/install-qt-action@v4 completely.
- Added ctions/setup-python@v6 with Python 3.12.
- Added manual pinned aqtinstall install from commit 9e49c82edc6d946db376dec907cca5b4b486eec5.
- Added manual command: python -m aqt install-qt windows desktop 6.11.2 win64_msvc2022_64 -O C:\Qt -m qtmultimedia qtsvg.
- Verified workflow contains zero install-qt-action occurrences and zero old default aqtinstall markers.

## O1ARCH1H1C-FIX3 stream-safe aqt version check

- Replaced direct PowerShell assignment from python -m aqt version with stream-safe capture:
  $installerVersion = (& python -m aqt version 2>&1 | Out-String).Trim()
- Added null/whitespace guard before legacy-version comparison.
- Kept Python 3.12, Qt 6.11.2, pinned aqt commit, Vulkan SDK 1.4.341.1, LLVM strategy, Release build, RPCS3 commit, and instrumentation patch unchanged.
