---
permalink: /vscode/
---

## First time install

You probably need the debugger.

```
> Debug: Download .NET Core debugger
```

**NOTE** That require the `C#` extension to be installed, see Requirements


## Issues with intellisense

For issue (red squiggles, references not works, etc), you can try

to restart

```
> Reload Window
```

To clear cache of project info

```
> F#: Clear cache
```

and to change the workspace/sln

```
> F#: Change Workspace or Solution
```

## Settings

can be changed for repo, workspace or user with

```
> Change User Settings
```

Use .net core as preferred msbuild host

```json
    "FSharp.msbuildHost": ".net core",
```

Some nice editor improvements

```json
    // whitespace
    "editor.renderWhitespace": "boundary",

    // linelens instead of codelens
    "editor.codeLens": false,
    "FSharp.lineLens.enabled": "replaceCodeLens",
```

Enable ionide diagnostics

```json
    "FSharp.logLanguageServiceRequests": "both",
    "FSharp.logLanguageServiceRequestsOutputWindowLevel": "DEBUG",
```

Disable defaults

```json
    "editor.minimap.enabled": false,
    "workbench.startupEditor": "none"
```
