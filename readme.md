# Cake.Coverlet

[![Build status](https://ci.appveyor.com/api/projects/status/pr3lyh3baynax8gx/branch/master?svg=true)](https://ci.appveyor.com/project/Romanx/cake-coverlet/branch/master)
[![NuGet version](https://img.shields.io/nuget/v/Cake.Coverlet.svg)](https://www.nuget.org/packages/Cake.Coverlet/)

## Usage
In order to use the addin please make sure you've included Coverlet in the project you wish to cover and add the following to your cake build file
```csharp
#addin nuget:?package=Cake.Coverlet
```

Then use one of the following snippets

```csharp
Task("Test")
    .IsDependentOn("Build")
    .Does<MyBuildData>((data) =>
{
    var testSettings = new DotNetCoreTestSettings {
    };
    
    var coveletSettings = new CoverletSettings {
        CollectCoverage = true,
        CoverletOutputFormat = CoverletOutputFormat.opencover,
        CoverletOutputDirectory = Directory(".\coverage-results\"),
        CoverletOutputName = $"results-{DateTime.UtcNow:dd-MM-yyyy-HH-mm-ss-FFF}"
    };

    DotNetCoreTest("./test/Stubble.Core.Tests/Stubble.Core.Tests.csproj", testSetting, coveletSettings);
}
```