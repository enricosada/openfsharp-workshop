


## Sample 1 - console app

In a `sample1` directory

> RUN `mkdir sample1 && cd sample1`

let's open code

> RUN `code .`

Now let's create a console app 

> RUN

```
dotnet new console -lang f#
```

This create:
- a `sample1.fsproj`: the project file
- a `Program.fs`: the source file

> DO open the `Program.fs` in the editor

This is the entrypoint of the of the program, the `main` and the args passed to the console app

When ionide is started, make the `F# PROJECT EXPLORER` visible on bottom-left corner of code.
This contains the projects loaded

