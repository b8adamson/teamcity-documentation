[//]: # (title: .NET CLI (dotnet))
[//]: # (auxiliary-id: .NET CLI (dotnet))
TeamCity comes with built\-in support of .NET CLI toolchain providing .NET CLI (dotnet) build steps, CLI detection on the build agents, and auto\-discovery of build steps in your repository.

This page provides details on configuring the .NET CLI (dotnet) runner. Also see the related [blog post](https://blog.jetbrains.com/teamcity/2016/11/teamcity-dotnet-core/).

* [.NET Core SDK](https://dotnet.microsoft.com/download) has to be installed on your build agent machines.
* The .NET CLI tools path has to be added to the `PATH` environment variable. You can also configure the `DOTNET_HOME` environment variable for your TeamCity build agent user, for example, `DOTNET_HOME=C:\Program Files\dotnet\`

<table><tr>

<td>

Option

</td>

<td>

Description

</td></tr><tr>

<td>

Command


</td>

<td>

Select a `dotnet` command from the drop\-down. Depending on the selected command, some of the options below will vary. The currently supported commands are:

* [`build`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-build)
* [`clean`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-clean)
* [`pack`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-pack)
* [`publish`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-publish)
* [`restore`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-restore)    
(requires .NET CLI 2.1.400\+ for [authentication in private feeds](net-cli-dotnet.md))
* [`run`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-run)
* [`test`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-test)
* [`vstest`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-vstest)
* [`msbuild`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)
* [`nuget delete`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-delete)    
 (requires .NET CLI 2.1.500\+ for [authentication in private feeds](net-cli-dotnet.md#Authentication+in+private+NuGet+Feeds))
* [`nuget push`](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-push)    
(requires .NET CLI 2.1.500\+ for [authentication in private feeds](net-cli-dotnet.md#Authentication+in+private+NuGet+Feeds))


</td></tr><tr>

<td>

Projects


</td>

<td>

Specify paths to projects and solutions. Wildcards are supported. Parameter references are supported. If you have a finished build, you can use the file/directory chooser here.


</td></tr><tr>

<td>

Working directory


</td>

<td>

Optional, set if differs from the checkout directory. Parameter references are supported. If you have a finished build, you can use the file/directory chooser here.


</td></tr><tr>

<td>

Framework


</td>

<td>

Specify the target framework, for example, netcoreapp or netstandard. Parameter references are supported.


</td></tr><tr>

<td>

Configuration


</td>

<td>

Specify the target configuration, for example, Release or Debug. Parameter references are supported.


</td></tr><tr>

<td>

Runtime


</td>

<td>

Specify the target runtime. Parameter references are supported.


</td></tr><tr>

<td>

Output directory


</td>

<td>

The directory where to place outputs. Parameter references are supported. If you have a finished build, you can use the file/directory selector here.


</td></tr><tr>

<td>

Version suffix


</td>

<td>

Defines the value of the `$(VersionSuffix)` property in the project. Parameter references are supported.


</td></tr><tr>

<td>

Command line parameters


</td>

<td>

Enter [additional command line parameters](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-build?tabs=netcore2x) for `dotnet`.


</td></tr><tr>

<td>

Logging verbosity

</td>

<td>

Select from the &lt;Default&gt;, Minimal, Normal, Detailed or Diagnostic.


</td></tr></table>

### Docker Settings

__Since TeamCity 2018.1__, the .NET CLI build step can be run in a [specified Docker container](docker-wrapper.md).

### Code Coverage

[JetBrains dotCover](jetbrains-dotcover.md) is supported as a coverage tool for the `msbuild`, `test`, and `vstest` commands.

### Authentication in private NuGet Feeds

TeamCity allows you to authenticate using private NuGet feeds. Read more in [NuGet](nuget.md#Authentication+in+private+NuGet+Feeds).

### Parameters Reported by Agent

When starting, the build agent reports the following parameters:

<table><tr>

<td>

Parameter

</td>

<td>

Description

</td></tr><tr>

<td>

`DotNetCLI`

</td>

<td>

The .NET CLI version

</td></tr><tr>

<td>

`DotNetCLI_Path`

</td>

<td>

The path to .NET CLI executable

</td></tr><tr>

<td>

`DotNetCoreSDKx.x_Path`

</td>

<td>

The .NET Core SDK version

</td></tr></table>
