---
layout: docs
title: Home
published: 2022-12-13
add toc: true
add sidebar: _sidebars\mainSidebar.md
add support: false
---

Welcome to the ARC Commander *Developer* Docs. Feel free to explore topics in the sidebar.
The following part addresses all who want to contribute to the ARC Commander development.

> *Users*, please check out the materials and info about ARC Commander [in our knowledge base](https://nfdi4plants.org/nfdi4plants.knowledgebase/docs/implementation/ArcCommander.html).


### Prerequisites

- .NET SDK >= .net 6 
    
### Build

Check the Build.fsproj to take a look at the build targets. Here are some examples:

#### via dotnet cli

- run `.\build.cmd <YourBuildTargetHere>` to run the buildchain of `<YourBuildTargetHere>`

Examples:

- `.\build.cmd` run the default buildchain (clean artifacts, build projects, copy binaries to /bin)

- `.\build.cmd runTests` (clean artifacts, build projects, copy binaries to /bin, **run unit tests**)
    
- `.\build.cmd publishBinaries<OS>` (clean artifacts, build projects, copy binaries to /bin, **publish project as single-file executable** depending on `<OS>` which can be either `Win`, `Mac`, or `Linux`)

- run `.\build.cmd releaseNotes semver:<numberID>` to update the Release Notes with commits not added yet (Look [here](https://github.com/Freymaurer/Fake.Extensions.Release#releaseupdate) for the correct syntax).

For Linux use `build.sh` with the same syntax.

### Release on github
    
To release the newest versions of the ArcCommander binaries on github, just `push` the newest version to the `main` branch. You must `update the release notes` as described above prior to this, as otherwise an old release may be overwritten by the new one.

Release workflow is based on https://github.com/marketplace/actions/automatic-releases    
    
#### testing the binary

After running the default build target, binaries of the arcCommander tool will lie in ./bin/ArcCommander. To run the binary, either use the `ArcCommander.exe` file on windows or `dotnet ArcCommander.dll` on linux.