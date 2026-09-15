# TASK9 RPCS3 Cloud Build Harness

This folder is a small GitHub Actions project. It does not contain RPCS3 source code and does not contain any PES game files.

## What it builds

The workflow downloads public RPCS3 source, checks out:

`2416d652625eaed5df2ff8d67063fa145021a883`

Then it applies:

`patches/RPCS3_TASK9_LIVE_TRACE_FIXED.patch`

and builds a Release x64 RPCS3 package on GitHub's Windows runner.

## Simple GitHub steps

1. Create a new private GitHub repository.
2. Upload this harness folder to that repository.
3. Open the repository on GitHub.
4. Click **Actions**.
5. Select **TASK9 RPCS3 cloud build**.
6. Click **Run workflow**.
7. Wait for the job to finish.
8. Open the completed workflow run.
9. Download the artifact named:

`RPCS3_TASK9_TRACE_2416d652`

## PowerShell push commands

Run these from:

`D:\New project pes\TASK9_OUTPUT\PHASE_O1ARCH1H1C_GITHUB_ACTIONS_BUILD`

Replace `YOUR_GITHUB_REPO_URL` with your private repository URL.

```powershell
git init
git add .
git commit -m "Add TASK9 RPCS3 cloud build harness"
git branch -M main
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

## Runtime trace switch

After downloading the built artifact, set this environment variable before launching the instrumented `rpcs3.exe`:

```powershell
$env:RPCS3_TASK9_TRACE = "1"
.\rpcs3.exe
```

The build logs only the narrow TASK9 diagnostic events from the instrumentation patch.
