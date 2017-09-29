---
permalink: /compatibility/
---

# Check for compatibility

- Some help if your library use unsupported api:
  - apiport
  - .NET standard [docs](https://github.com/dotnet/standard/blob/master/docs/versions.md)


<a name="apiport"></a>
## Api Port

https://github.com/Microsoft/dotnet-apiport (download in Releases)

- `ApiPort.exe analyze --file bin\net40\Argu.dll -r HTML`

=> report `files/apiport/ApiPortAnalysis.html`

This can show some help, when needed.
Ignore the FSharp.Core related api

