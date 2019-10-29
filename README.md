# SimpleTool
A basic .NET Core Global Tool

A .NET Core Global Tool it's a special kind of NuGet package that contains a .NET Core Console Application. 
You can install and use a Global Tool similar to NPM packages.

On Windows, each Global Tool will be installed into: "%USERPROFILE%\.dotnet\tools" (also located into user *Path environment variable*)
Each Tool it's installed for a user, not for all users of the machine.

To create a Global Tool follow the steps:

1. Create a .NET Core Console app
```
 dotnet new console -o simpletool
```
2. Setup Global Tool
* Add the following code to the .csproj file.
```xml
<PropertyGroup>
  <PackAsTool>true</PackAsTool>
  <ToolCommandName>simpletool</ToolCommandName>
  <PackageOutputPath>./nuget</PackageOutputPath>
</PropertyGroup>
```
* PackAsTool

[Required] Indicates that the application will be packaged for install as a Global Tool.

* ToolCommandName

[Optional] The name of the tool. If not specified, tool name will be the same as project name (csproj name).

* PackageOutputPath

[Optional] The folder where the NuGet Package will be saved. Default folder it's the folder of the .csproj file.

3. Generate the NuGet Package
```
dotnet pack
```
* [Optional] Publish the NuGet Package to any NuGet feed.
4. Install the Global Tool
```
dotnet tool install --global simpletool
```
* If the package is located anywhere else other than [Official NuGet](https://www.nuget.org.) make sure to include a NuGet.config file at the root of your solution.

The NuGet.config file should contain your private/local feed.

Example:
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear />
    <add key="Local" value="./SimpleTool/nuget" />
  </packageSources>
</configuration>
```
5. If everything went ok you can use the tool similar to any CLI tool
```
simpletool
> Hello
```
[More info](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools)
