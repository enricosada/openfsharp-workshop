
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