---
permalink: /consoleapp/
---

# Sample 1 - console app

In a `sample1` directory, run

```
mkdir sample1 && cd sample1
```

### dotnet new

Now let's create a console app 

RUN

```
dotnet new console -lang f#
```

let's open code to inspect it, run

```
code .
```

A normal console app is:
- a `sample1.fsproj`: the project file.
- a `Program.fs`: the source file

Open the `Program.fs` in the editor

This is the entrypoint of the of the program, the `main` and the args passed to the console app

When ionide is started, make the `F# PROJECT EXPLORER` visible on bottom-left corner of code.
This contains the projects loaded

Now, let's build it.
It can be done in the the terminal

**TIP** code has an embedded terminal. Open it with `View -> Integrated Terminal`

### dotnet build

run

```
dotnet build
```

This compile the project and show the output:

```
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  sample1 -> E:\wssf\sample1\bin\Debug\netcoreapp2.0\sample1.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

So the output is `bin/Debug/netcoreapp2.0/sample1.dll`

To run it:

```
dotnet bin/Debug/netcoreapp2.0/sample1.dll
```

Now let's pass some arguments.
First change the program to print the arguments.

DO add to the main

```
printfn "%A" argv
```

### dotnet run

Now another time, compile and execute. Run:

```
dotnet build
dotnet bin/Debug/netcoreapp2.0/sample1.dll a b --other a
```

A faster way to do it, is use `dotnet run` command, who does the same thing

```
dotnet run -- a b
```

### dotnet publish

What if i want to use my app in another machine?

Two possibilities of deployment:

- `framework dependent` (FDD)
  - CONS require .net core runtime installed in target machine
  - CONS executed as `dotnet app.dll`
  - PRO same binaries for all os
  - PRO small size of binaries
- `self contained` (SCD)
  - CONS bigger size of binaries
  - CONS distinct binaries for all os
  - PRO is a normal native app (`app.exe` or `app`)
  - PRO doesnt require .net core runtime installed on target machine,- CONS require .net core deps (like libunwind, OpenSSL) installed

### First let's try FDD

Run 

```
dotnet publish
```

This create the `bin/Debug/netcoreapp2.0/publish/` directory
who can be copied in another machine, and run with

```
dotnet sample1.dll
```

### Now a SCD, in another directory

Run 

```
dotnet publish --self-contained --runtime win-x64 --output out
```

and that directory `out` contains `sample1.exe`

Doing the same for osx

```
dotnet publish --self-contained --runtime osx-x64 --output outosx
```

Or linux, run

```
dotnet publish --self-contained -r linux-x64 -o outlinux -c Release
```

NOTE on linux .net core apps has some requirements, like the `libunwind8` package installed (can be installed with `apt-get install libunwind8`)


**NOTE** is possibile to bundle these deps as local copies, ref https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md


**NOTE** the runtime can be specified also in the fsproj

```xml
    <RuntimeIdentifiers>win10-x64;osx-x64</RuntimeIdentifiers>
```

### VSCode settings

Let's configure VS Code to build/debug this project
VSCode use tasks to run things.

- VSCODE `> Tasks: Configure Task Runner`
- choose `.NET Core`

To run it:

- VSCODE `> Tasks: Run Build Task`
- choose `build`

We can also set this task as the default one.

- VSCODE `> Tasks: Configure Default Build Task`
- choose `build`

So now the default run build use that

If there is an error, are shown in `PROBLEMS` tab
You can move between errors with

- VSCODE `> Go to Next Error or Warning`

Now, to debug

- Right click on the project in `F# PROJECT EXPLORER`
- `Configure as Start up project for Debugging`

and to debug

- or `> Debug: continue`
- or `F5`

### External package

For example we need to parse the command line arguments
We want to use [Argu](http://fsprojects.github.io/Argu/) library

to manage the packages in the project, we can use the `dotnet add` and `dotnet remove` commands

```
dotnet add package Argu
```

this add a packagereference to the project

```xml
    <PackageReference Include="Argu" Version="3.7.0" />
```

and restore the project (download the package).

We can now use argu to manage command line args
First declaring the arguments

```fsharp
open Argu

type CLIArguments =
    | Port of tcp_port:int
with
    interface IArgParserTemplate with
        member s.Usage =
            match s with
            | Port _ -> "specify a primary port."
```

and doing the parsing in the `main`

```fsharp
    let parser = ArgumentParser.Create<CLIArguments>(programName = "sample1")

    try
        let args = parser.Parse argv

        match args.GetAllResults() with
        | [Port p] -> printfn "set port %i" p
        | _ -> ()

        0 // return an integer exit code
    with
    | :? ArguParseException as ex ->
        printfn "%s" ex.Message
        1
    | ex ->
        printfn "Internal Error:"
        printfn "%s" ex.Message
        2
```

to check is working:

```
dotnet run -- --help
dotnet run -- --port 81
```

**NOTE** by default configuration, the `--help` raise an exception in Argu.
Try with debugging, you can see the `ex.ErrorCode` is `HelpText`
