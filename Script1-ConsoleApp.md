


## Sample 1 - console app

In a `sample1` directory

> RUN `mkdir sample1 && cd sample1`

### dotnet new

Now let's create a console app 

> RUN

```
dotnet new console -lang f#
```

let's open code to inspect it

> RUN `code .`

A normal console app is:
- a `sample1.fsproj`: the project file.
- a `Program.fs`: the source file

> DO open the `Program.fs` in the editor

This is the entrypoint of the of the program, the `main` and the args passed to the console app

When ionide is started, make the `F# PROJECT EXPLORER` visible on bottom-left corner of code.
This contains the projects loaded

Now, let's build it.
It can be done in the the terminal

**TIP** code has an embedded terminal. Open it with `View -> Integrated Terminal`

### dotnet build

> RUN `dotnet build`

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

> RUN `dotnet bin/Debug/netcoreapp2.0/sample1.dll`

Now let's pass some arguments.
First change the program to print the arguments.

> DO add to the main

```
printfn "%A" argv
```

### dotnet run

Now another time, compile and execute

> RUN

```
dotnet build
dotnet bin/Debug/netcoreapp2.0/sample1.dll a b --other a
```

A faster way to do it, is use `dotnet run` command, who does the same thing

> RUN `dotnet run -- a b`

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
  - PRO doesnt require .net core runtime installed on target machine

First let's try FDD

> RUN `dotnet publish`





