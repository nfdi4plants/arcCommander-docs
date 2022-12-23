---
layout: docs
title: "ARC Commander Development"
date: 2022-12-21
add toc: true
add support: false
add sidebar: _sidebars/mainSidebar.md
---

### Prerequisites

- .NET SDK >= 3.1.00 (should roll forward to .net 6 if you are using that)
- To test the generated cli tool you will need the .NET 3.1 runtime.
    
### Build

Check the [build.fsx file](https://github.com/nfdi4plants/arcCommander/blob/developer/build.fsx) to take a look at the build targets. Here are some examples:

#### via dotnet cli

- run `dotnet tool restore` once to restore local tools needed in the buildchain

- run `dotnet fake build -t <YourBuildTargetHere>` to run the buildchain of `<YourBuildTargetHere>`

    Examples:

    - `dotnet fake build` run the default buildchain (clean artifacts, build projects, copy binaries to /bin)

    - `dotnet fake build -t runTests` (clean artifacts, build projects, copy binaries to /bin, **run unit tests**)
    
    - `dotnet fake build -t publishBinaries<OS>` (clean artifacts, build projects, copy binaries to /bin, **publish project as single-file executable** depending on `<OS>` which can be either `Win`, `Mac`, or `Linux`)

#### using the shell scripts

```shell
# Windows

# Build only
./build.cmd

# Full release buildchain: build, test, pack, build the docs, push a git tag, publish the nuget package, release the docs
./build.cmd -t release

# The same for prerelease versions:
./build.cmd -t prerelease
    
# Publish buildchain: build, publish for the respective OS
./publishBinariesWin.cmd
./publishBinariesMac.cmd
./publishBinariesLnx.cmd


# Linux/mac

# Build only
build.sh

# Full release buildchain: build, test, pack, build the docs, push a git tag, publsih the nuget package, release the docs
build.sh -t release

# The same for prerelease versions:
build.sh -t prerelease

```

### Update Release Notes
    
Every developer with writing rights shall update the Release Notes after every PR merge:
    
#### via dotnet cli
    
- run `dotnet tool restore` once to restore local tools needed in the buildchain (if not done already)

- run `dotnet fake build -t releaseNotes` to update the Release Notes with commits not added yet **to the CURRENT version release**
    
- run `dotnet fake build -t releaseNotes semver:<numberID>` to update the Release Notes with commits not added yet **to a NEW version release**; the new version depends on the `<numberID` used: `major` for an increase of the major number (e.g. 0.0.0 -> 1.0.0), `minor` for an increase of the minor number (e.g. 0.0.0 -> 0.1.0), `patch` for an increase of the patch number (e.g. 0.0.0 -> 0.0.1)

### Release on github
    
To release the newest versions of the ArcCommander binaries on github, just `push` the newest version to the `main` branch. You must `update the release notes` as described above prior to this, as otherwise an old release may be overwritten by the new one.

Release workflow is based on https://github.com/marketplace/actions/automatic-releases    
    
#### testing the binary

After running the default build target, binaries of the arcCommander tool will lie in ./bin/ArcCommander. To run the binary, either use the `ArcCommander.exe` file on windows or `dotnet ArcCommander.dll` on linux.
