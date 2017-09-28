---
permalink: /msbuild/
---

# MSBuild features


New features of the Sdk

- Create a custom nuget package (like with `nuspec`)


<a name="custom-pack"></a>
## create nuget packages custom (no compilation)

Useful for templates, custom packages, etc.
This can be used to replace the `.nuspec` files

Any msbuild project using `Microsoft.NET.Sdk` has a `Pack` target

Is possibile to create a file with `.*proj` extension (`.proj` is ok) and `dotnet pack` it

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard1.0</TargetFramework>

    <IncludeBuildOutput>false</IncludeBuildOutput>
    <DisableImplicitFrameworkReferences>true</DisableImplicitFrameworkReferences>
    <PackProjectInputFile>$(MSBuildProjectFullPath)</PackProjectInputFile>
    <NoBuild>true</NoBuild>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="prova.txt">
      <PackagePath>build/prova.txt</PackagePath>
      <Pack>true</Pack>
    </Content>
  </ItemGroup>

</Project>
```

To create the nuget

> RUN `dotnet pack`

The first properties are needed to skip compilation, ignore implicit references

**NOTE** I added just a `Content` because `dotnet pack` fails if the package is totally empty 

All the usual `Pack` properties (like `PackageId`, `Authors`, etc) can be used.
Also `PackageReference` if needed.

