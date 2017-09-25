---
permalink: /requirements/
---

# Requirements

- [.NET Core Sdk 2.0](#dotnetsdk)
- [Mono](#mono) (on unix/mac)
- [Docker and images](#docker)
- [Visual Studio Code](#vscode)
  - C# extension
  - Ionide-fsharp extension

<a name="dotnetsdk"></a>
## .NET Core Sdk 2.0

Install the Sdk (not the Runtime):

[https://www.microsoft.com/net/download/core#/sdk](https://www.microsoft.com/net/download/core#/sdk)

In the page there are also the `Step-by-step instructions`

Prerequisites:

- [linux](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore2x)
- [osx](https://docs.microsoft.com/en-us/dotnet/core/macos-prerequisites)
- [windows](https://docs.microsoft.com/en-us/dotnet/core/windows-prerequisites?tabs=netcore2x)

Check if is installed correctly with `dotnet --info` should print:

```
.NET Command Line Tools (2.0.0)

Product Information:
 Version:            2.0.0

<additional info about os>
```

<a name="mono"></a>
## Mono on unix/mac

For unix/mac, Windows doesnt need it

[http://www.mono-project.com/download/](http://www.mono-project.com/download/)

Recommended 5.2 , required >= 4.8

the package is the `mono-complete`, who contains the `mono-devel`

Check if is installed correctly with `mono --version` should print:

```
Mono JIT compiler version 5.2.0.224 (tarball Mon Sep 18 17:33:20 UTC 2017)
```

<a name="docker"></a>
## Docker images

Docker 17.06 or higher is recommended because the workshop use the [multi stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/), but can be adapted if a previous versions.

Docker images to download:

```bash
docker pull microsoft/dotnet:2.0-sdk
docker pull microsoft/dotnet:2.0-runtime
docker pull microsoft/dotnet:2.0-runtime-deps
```

Check is installed correctly:

```bash
docker run --rm microsoft/dotnet:2.0-sdk dotnet --info
```

should print:

```
.NET Command Line Tools (2.0.0)

Product Information:
 Version:            2.0.0
 Commit SHA-1 hash:  cdcd1928c9

Runtime Environment:
 OS Name:     debian
 OS Version:  9
 OS Platform: Linux
 RID:         linux-x64
 Base Path:   /usr/share/dotnet/sdk/2.0.0/

Microsoft .NET Core Shared Framework Host

  Version  : 2.0.0
  Build    : e8b8861ac7faf042c87a5c2f9f2d04c98b69f28d
```

and

```bash
docker run --rm microsoft/dotnet:2.0-runtime dotnet --info
```

should print:

```
Microsoft .NET Core Shared Framework Host

  Version  : 2.0.0
  Build    : e8b8861ac7faf042c87a5c2f9f2d04c98b69f28d
```

<a name="vscode"></a>
## Visual Studio Code

Install:

[https://code.visualstudio.com/download](https://code.visualstudio.com/download)

Extensions to install ([docs](https://code.visualstudio.com/docs/editor/extension-gallery)):

- [C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
- [Ionide-fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)
