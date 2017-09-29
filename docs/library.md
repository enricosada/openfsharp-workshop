---
permalink: /library/
---

# library

In a `sample2` directory, run

```
mkdir sample2 && cd sample2
```

## dotnet new

Now let's create a library app, run

```
dotnet new lib -n l1 -lang f#
```

the `-n` pass the name of the project, and create a subdirectory.

and open 

```
code .
```

Because the project is in a subdirectory, the `dotnet build` fails because doesnt know
what project to build. Is enough to pass the directory or the path of project file.

```
dotnet build l1
```

Same in code, in `tasks.json`, set `"command": "dotnet build l1",`

## reference from a console app

as before, create a simple console app `c1`

```
dotnet new console -n c1 -lang f#
```

And now reference the `l1` from `c1`

```
dotnet add c1 reference l1/l1.fsproj
```

Is now possibile to use the methods from l1 in c1
Add to main

```fsharp
    l1.Say.hello "Openfsharp!"
```

to run it:

- or `dotnet run -p c1` from terminal
- or update the `tasks.json` and `launch.json` to correct c1 paths, for code

this is neeeded because `dotnet build` doesnt build all project in the subdirectories, but
all project referenced from the initial one.

## test with xunit

To add an unit test project, based on [xUnit](https://xunit.github.io/) Library

```
dotnet new xunit -n l1.Tests -lang f#
```

And add the project reference to `l1`

```
dotnet add l1.Tests reference l1/l1.fsproj
```

Now let's change the l1 to refactor and extract an `helloMessage` function

```fsharp
    let helloMessage name =
        sprintf "Hello %s" name

    let hello name =
        printfn "%s" (helloMessage name)
```

and test it in `Tests.fs`

```fsharp
[<Fact>]
let ``hello`` () =
    Assert.Equal("Hello openfsharp", (l1.Say.helloMessage "openfsharp conf"))
```

the test can be run with `dotnet test l1.Tests`

In vscode, configure the test task

- `> Tasks: Configure Task Runner`
- same as build task, but with:
  - group kind `test` instead of `build`
  - command: `dotnet test l1.Tests`

Now tests can be executed with

- `> Tasks: Run Test Task`

## test with expecto

The `dotnet new` allow to import additinal templates.
for example, let use expecto

First let's import the template

```
dotnet new -i Expecto.Template::*
```

now the expecto template is installed (see `dotnet new --list`)

```
Templates                         Short Name       Language          Tags
-------------------------------------------------------------------------
Expecto .net core Template        expecto          F#                Test
```

to create a new project (`-o` is needed to specify output path)

```
dotnet new expecto -n l1.Test2 -o l1.Tests2 -lang f#
```

**NOTE** The expecto template use .net core 1, let's change it to .net core 2
- remove `FSharp.NET.Sdk`, `FSharp.Core` references 
- change tfm to `<TargetFramework>netcoreapp2.0</TargetFramework>`
- change `Microsoft.DotNet.Watcher.Tools` version to `2.0.0`

more info in [netcorecli-fsc wiki page 1.0 -> 2.0](https://github.com/dotnet/netcorecli-fsc/wiki/How-to-migrate-1.0-projects-to-2.0)


And add the project reference to `l1`

```
dotnet add l1.Tests2 reference l1/l1.fsproj
```

and add a new test case

```fsharp
    testCase "helloMessage" <| fun _ ->
      Expect.equal (l1.Say.helloMessage "openfsharp") "Hello openfsharp conf" "These should equal"
```

and run it with `dotnet run -p l1.Tests2`.

Because is a normal console app, it's possibile to debug it.

**NOTE** Ionide has also a support for expecto builtin, try the `> Expecto: `

## pack

To create the nuget package from library, is possibile to use the `dotnet pack` command

```
dotnet pack l1 -c Release /p:Version=1.2.3
```

this will create a package

```
Successfully created package 'E:\wssf\sample2\l1\bin\Release\l1.1.2.3.nupkg'.
```

To specify other package metadata (like `Version`), is possibile to:

- pass it as command line, like `/p:Version=1.2.3`
- pass is as environment variable (so `Version`)
- or specify it in an msbuild property inside the like `<Version>1.2.3</Version>`

Others `Authors`, `Summary`, `Description`, `PackageTags`, etc

## push

to push a package to a nuget feed, you can use `dotnet nuget push`

For example, to push to myget feed

RUN

```
dotnet nuget push l1/bin/Release/l1.1.2.3.nupkg -s https://www.myget.org/F/openfsharp-workshop/api/v2/package -k e89848f5-a549-4238-8016-24cbed33dfcc
```

to restore from a dev feed:

```
dotnet add package l1 --version 1.2.3 --source https://www.myget.org/F/openfsharp-workshop/api/v3/index.json
```
