# SimpleTool
A basic .NET Core Global Tool

A .NET Core Global Tool it's a special kind of NuGet package that contains a .NET Core Console Application. 
You can install and use a Gloabl Tool similar to NPM packages.

Windows installation folder: "%USERPROFILE%\.dotnet\tools" (ENV variable)
Each Tool it's installed per user, not per machine.

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
