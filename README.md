# Github Action for publishing dotnet projects
Automatically deploy dotnet projects using [msbuild](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild?view=vs-2022) as part of your Github Actions workflow.

## Usage
Running on `pull_request` type `closed`
```yaml
name: "[CD]Deploy"

on:
  pull_request:
    branches: [ "Release" ]
    types: [ "closed" ]

jobs:
    Release:
        runs-on: windows-latest
        steps:
            -   uses: actions/checkout@v2
            -   name: Release
                uses: tegrasystems/dotnet-publish@v1
                with:
                    project-path: PATH_TO_PROJECT
                    publishprofile: PATH_TO_PUBLISHPROFILE
                    password: PASSWORD
                    configuration: CONFIGURATION
```

## Parameters
### Inputs

| Name | Description | Type |
| --- | ----------- | ----- |
| project-path | Path to `.csproj` to deploy | string |
| publishprofile | Path to `.pubxml` of the project to deploy | string |
| password | Password needed for `publishprofile`  | string |
| configuration | (optional) Name of configuration  | string |
| additional-arguments | (optional) Additional switches to use in msbuild command, see [msbuild documentation](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-command-line-reference?view=vs-2022#switches) for more information | string |

### Outputs
Currently there is no outputs

## Limitations
At this moment it is not possible to run this Github Action without using a publishprofile, for more information about making publishprofile see [Microsoft documentation](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/visual-studio-publish-profiles?view=aspnetcore-6.0)

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/xt0rted/dotnet-format/blob/main/LICENSE)