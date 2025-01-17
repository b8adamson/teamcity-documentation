[//]: # (title: JetBrains dotCover)
[//]: # (auxiliary-id: JetBrains dotCover)

TeamCity comes bundled with the console runner of [JetBrains dotCover](http://www.jetbrains.com/dotcover/). __Since TeamCity 2017.1__, in addition to the bundled version, it is possible to install another version of JetBrains dotCover Command Line Tools and/or change the defaults using the __[Administration | Tools](installing-agent-tools.md)__ page.

After choosing the appropriate option in the .Net coverage section of a build step, you will be able to collect code coverage for your .Net project and then view the coverage statistics and detailed coverage report inside the [TeamCity web UI](working-with-build-results.md).

If you have a license for dotCover and have it installed on a developer machine, TeamCity\-collected coverage results can be downloaded and viewed inside Visual Studio with the help of the [TeamCity Visual Studio Add-in](visual-studio-addin.md).

<tip>

.NET Framework 3.5 or newer must be installed on the agent machine. This is necessary for the bundled dotCover to work. Your project can depend on another .NET Framework version.   
dotCover 2018.2 or newer requires .NET Framework 4.6.1 or newer.
</tip>


## dotCover Settings

<table>

<tr>

<td></td><td></td>

</tr>


<tr>

<td>

Path to dotCover Home


</td>

<td>

Leave this field blank to use the default dotCover. The [bundled version](#Bundled+dotCover+Versions) is set as default prior to TeamCity 2017.1; after this version you can mark any of the [additionally installed](installing-agent-tools.md) versions as default.   
Alternatively, specify the path to the dotCover installed on a build agent.


</td></tr><tr>

<td>

Filters


</td>

<td>

Specify a new\-line separated list of filters for code coverage. Use `+|-:assembly=*;type=**;method=***` to include or exclude assemblies from covered assemblies:

<include src="branch-filter.md" include-id="OR-syntax-tip"/>

For example, to run coverage on all `MyDemoApp` assemblies but not on `MyDemoApp.*.Tests`, specify the following assembly filters for coverage:   
`+:MyDemoApp.*`   
`-:MyDemoApp.*.Tests`

See also [this blog post](https://blog.jetbrains.com/dotnet/2010/12/10/coverage-with-dotcover-teamcity-mstest-nunit-or-mspec/).


</td></tr><tr>

<td>

Attribute Filters


</td>

<td>

If you do not want to know the coverage data solution\-wide, you can exclude the code marked with an attribute (for example, with `ObsoleteAttribute`) from the coverage statistics. You only need to specify these attribute filters here in the following format: the filters should be a new\-line separated list; the `-:attributeName` syntax should be used to exclude the code marked with the attributes from code coverage. Use the asterisk (`*`) as a wildcard if needed.   
Supported only for dotCover 2.0 or newer.


</td></tr><tr>

<td>

Additional dotCover.exe arguments


</td>

<td>

Provide a new\-line separated list of additional commandline parameters to pass to dotCover.exe


</td></tr></table>

Note that dotCover coverage engine reports statement coverage instead of line coverage.

## Compile and Test in Different Builds

To build a consistent coverage report, dotCover has to be able to find source files under the build checkout directory which should be easy if you build binaries and collect coverage in the same build, or if you use different builds, but they use a [snapshot dependency](build-dependencies-setup.md#Snapshot+Dependencies) and the same agent as well as the same [VCS settings](configuring-vcs-settings.md).

If you need to build binaries in one build and collect code coverage in another one using different [checkout settings](vcs-checkout-rules.md), some additional properties are required. It is assumed that:
* Build configuration __A__ compiles code with debugging information and creates an artifact with assemblies and `.pdb` files
* Build configuration __B__ runs tests with dotCover enabled and has a [snapshot dependency](build-dependencies-setup.md#Snapshot+Dependencies) on A.

To display the source code in the [Code Coverage tab](working-with-build-results.md#Code+Coverage+Results) of build results of B, you need to point B to the same [VCS root](configuring-vcs-roots.md) as A to get your source code in an appropriate location (the [checkout root](build-checkout-directory.md)) and add an [artifact dependency](build-dependencies-setup.md#Artifact+Dependencies) on __build from the same chain__ of A (for dotCover to get the paths to the sources from the `.pdb` files).

You also need to tell TeamCity where to find the source code. To do this, perform the following:
1. Add the `teamcity.dotCover.sourceBase` configuration parameter with the value `%teamcity.build.checkoutDir%` to the compiling build configuration A.
2. Add the configuration parameter `dotNetCoverage.dotCover.source.mapping` to your test configuration B with the value `%dep.btA.teamcity.dotCover.sourceBase%=>%teamcity.build.checkoutDir%`, where `btA` is the actual [ID](identifier.md) of your configuration A.

### Bundled dotCover Versions

This section provides information on the versions of dotCover bundled with TeamCity 10\+ versions. For information on the earlier TeamCity releases, see the [previous documentation version](https://confluence.jetbrains.com/display/TCD9/JetBrains+dotCover#JetBrainsdotCover-BundleddotCoverVersions).

<table><tr>

<td>

TeamCity Version


</td>

<td>

dotCover Version


</td></tr><tr>

<td>

2018.1

</td>

<td>

2018.1.2

</td></tr><tr>

<td>

2018.2

</td>

<td>

2018.1.4

</td></tr><tr>

<td>

2019.1

</td>

<td>

2019.1.1

</td></tr>



</table>

 

You can view the installed versions of dotCover on the __Server Administration | Tools__ page. The bundled version is set as default, you can install other versions and change the default settings.

 __  __

__See also:__



__Administrator's Guide__: [Manually Configuring Reporting Coverage](manually-configuring-reporting-coverage.md) 

__Troubleshooting__: [dotCover issues](reporting-issues.md)

 

 

 

 

 

 
