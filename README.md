# Purpose

MsBuild helper for Wix auto-harvesting (using heat.exe) during build.

See role in the build process:
![WixAutoHarvest in the build process](https://github.com/IvanBoyko/WixAutoHarvest/blob/master/images/WixCommon-as-part-of-the-build.png)

# Usage

1) In your Wix project (.wixproj) Install a NuGet package - depending on the type of a project being packaged to MSI use:
- for console apps: https://www.nuget.org/packages/WixAutoHarvest.ConsoleApp
- for web apps: https://www.nuget.org/packages/WixAutoHarvest.WebApp

2) In your Wix project Add a reference to the project to be packaged to MSI

3) In **Product.wxs** add ComponentGroup **include_cg** to a Feature, see example:
```
<Feature ...>
	...
	<ComponentGroupRef Id="include_cg" />
</Feature>
```

3) [optonal] if you require any alterations to harvested file generated by heat.exe - create .xslt file and pass it in **TransformFile** property in your .wixproj

4) [optonal] if Platform of the target packaged project is not "Any CPU", add **ReferencedProjectPlatform** property to .wixproj with correct value, see example for "x86" platform:
```
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <ReferencedProjectPlatform>x86</ReferencedProjectPlatform>
    ...
```
    
# Development

## Preparation
1. Clone this repo
2. Get NuGet API key from your account on nuget.org
3. Store API key locally: ```nuget setApiKey %API_KEY% -Source https://www.nuget.org/api/v2/package```

## Dev cycle
1. Make changes
2. Package locally by: ```nuget pack```
3. Install locally to a Wix project and test that it builds
4. Once happy, package and publish by running: ```nuget-pack-and-push.bat```
