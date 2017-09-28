---
permalink: /template/
---

Based on the .NET Templating engine [https://github.com/dotnet/templating](https://github.com/dotnet/templating).

This engine is used in the `dotnet new` command ([docs](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new?tabs=netcore2x)) and in Visual Studio (`File -> New -> ..`)

Features:

- additional templates can be installed from a directory or a nuget package (remote by id or local)
- support options, bundling files, post install actions, variabile substitution, etc
- discovery of template packages by package type
- template can contains files, a project, multiple projects, anything.
- some types (like project) have special features (target framework, etc)

Some Docs:

- [dotnet new docs](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new?tabs=netcore2x)
- [Custom templates docs](https://docs.microsoft.com/en-us/dotnet/core/tools/custom-templates)

Some samples and how to:

- [.net template samples](https://github.com/dotnet/dotnet-template-samples)
- [list of additional avaiable packages](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)



The base is the `.template.config/template.json` file, who contains the info about the template.


