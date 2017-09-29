
Use .net core as preferred msbuild host

```
    "FSharp.msbuildHost": ".net core",
```

Some nice editor improvements

```
    // whitespace
    "editor.renderWhitespace": "boundary",

    // linelens instead of codelens
    "editor.codeLens": false,
    "FSharp.lineLens.enabled": "replaceCodeLens",
```

Enable ionide diagnostics

```
    "FSharp.logLanguageServiceRequests": "both",
    "FSharp.logLanguageServiceRequestsOutputWindowLevel": "DEBUG",
```

Disable defaults

```
    "editor.minimap.enabled": false,
    "workbench.startupEditor": "none"
```