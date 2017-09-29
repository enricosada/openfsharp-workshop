This workshop will help library authors and F# developers to fully use the new .NET Sdk in their existing projects. 

I'll provide an example project, if partecipants doesnt want use their project. 

- support multiple target frameworks, cross platform (mono, .NET and .net core)
- add abstraction like .NET Standard 
- new simplified msbuild project and extensibility

Participants can bring their existing library/project/app to the workshop and i will guide them to:
  - use new sdk (in parallel or directly migrating) 
  - check for .net standard portability issues (dependencies/code)
  - add .net standard support for libraries
  - support previous target framework (.NET)
  - ~adapt build orchestration and CI (like travis/appveyor)~
  - make it cross platform friendly to developers, not only final artifact
  
  - ~add unsupported profiles (like PCL) to final nuget package, with minimal maintenance~

And finally add new functionalities like:

- templates, using new .NET Templating
- show useful basic msbuild configurability for developers and maintainers
- new msbuild extensibility for library authors
- add .net core support if make sense (console app)
- extend .net cli tools if make sense in the project
- dockerize it The participants can use their preferred ide/editors and OS

