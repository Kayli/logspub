# notes related to csharp programming language

## basics

- latest versions as of jan 13, 2023
  - csharp 11 released in November 2022
  - dotnet 7.0 released in January 2023
  - visual studio 2022 ide

- important legacy versions
  - .net framework 4.8.1 released in August, 2022
    - preinstalled on windows 11
  - no longer officially supported
    - .net framework 3.5, 4, 4.5, 4.6, 4.7
    - .net core 2.1, 3.1, 5
  - visual studio: 2013, 2015, 2017, 2019

- 2014, Microsoft introduced .net core as a cross-platform, open-source successor to .net framework
  - .net core through version 3.1, next version was named .net 5

- roslyn compiler services
  - provide extensibility model for compiler
  - allows custom extensions for c# language

- dotnet tool
  - special NuGet package that contains a console application
  - can be global (access from anywhere) or local (specific folder or any of its subfolders)


## auth

- common standards
  - openid connect
  - oauth

- implementations
  - microsoft 
    - identity platform
      - collection of azure services that enables developers to build secure and scalable identity solutions 
      - built on top of Azure AD 
      - provides additional capabilities such as 
        - token-based authentication and API access control
        - supports third-party identity providers like twitter, google, amazon, etc.
    - azure active directory (free below 50k monthly active users)
      - supports multifactor
    - msal - client authentication libraries, support different programming platforms
  - openiddict
  - identityserver6 (ex identityserver4, now supported by duende)
  - ikeycloak, sponsored by redhat
  - auth0


## .net (ex core)

- cross-platform, opensource

- why latest versions of .net are faster
  - improvements related to new processor extensions and alike are not backported to .net framework
  - related mostly to computation-heavy tasks, io-bound operations will be likely the same

- comes as a collection of nuget packages
  - can be trimmed down even further using optimization flag: PublishTrimmed

- no support for remoting, app domains or code access security
  - instead it is recommended to simply run untrusted code in a separate process
  - in the future
    - you will have WebAssembly and wasi
    - those new apis are experimental as of mid 2022


## .net 7, csharp 11

- default language version: csharp 11
- app trimming improvements based on actual usage
- simplified tar file management
- high precision support for datetime: nanoseconds added
- simplified linq sorting with Order() for primitive types and ones implementing IComparable
- multiline sting interpolation
- blazor lists (scroll) virtualization added, to speed up rendering
- static abstract interface members
  - allow each implementing member of an interface to implement their version of a static member
- INumber<T> can be used as generic constraint to enable arithmetic on T
- 'required' keyword for properties
- grpc
  - performance improvements
  - restful api transcoding + openapi support
    - means that you can mirror your grpc endpoints to http2/rest automatically

## .net 6

- default language version: csharp 10
- startup.cs was eliminated from web projects
- DateOnly/TimeOnly capture date and time correspondingly
- multiplatform app ui (maui) replaces xamarin for cross-platform mobile development
- blazor desktop for writing html-based desktop apps


## .net 5

- default language version: csharp 9
- top level statements: only one file in your application may use top-level statements


## .net core 3

- default language version: csharp 8
- interface default method implementations
  - so now csharp interfaces are whats called 'traits' in other languages
- interface static constructors and members


## new language features [1][2]

- csharp 10 and earlier

  - inplace out variables for out parameters
    > int.TryParse(str, out var value)

  - expression-bodied members
    - getters and setters: lambda-like bodies instead of curly braces
    - methods: short methods can have lambda-like bodies
    - constructors: works only for ctors with 1 argument

  - discards: underscore '_' symbol means variable that we okay to discard (pacifies compilers, linters)
    - useful when working with 
      - awatable methods
      - argument validation combined with throw expressions
        > _ = name ?? throw new ArgumentNullException();

  - null conditional operator (elvis operator)
    > if (order?.Recipient?.EmailAddress != null) ...

  - null coalescent assignments
    > options ??= MyOptions.Default

  - verified reference types: reference types are implicitly non-nullable
    - with <Nullable>enable</Nullable> <WarningsAsErrors>nullable</WarningsAsErrors> in your csproj file
    - now you have to explicitly state that some type is nullable

  - named tuples: useful for return types
    - deconstruction
      > var (isSuccess, response) = doSomething();

  - is/as simplification
    > if (item is string str) { /* do something with the str */ }
    - you can also do typechecks inside case statements
      > case ILoggable loggable when loggable.LogLevel == LogLevel.Warn: ...

  - non-overridable equality operator
    > if (x is null) ...

  - synonyms for '&', '|' operators: 'and', 'or'

  - switch expression-bodied method: simpler map-like syntax for pattern matching

  - records: simplify declaration of immutable dtos by generating ctor, equality operator, properties
    > public record Order (int Id, string ArticleName, decimal Total);
    - cloning a record with mutated field
      > var order2 = order1 with { ArticleName = "something else"};

  - global usings: you now can have a file with 'global using' statements which will apply project-wide

  - reduced nesting of a namespace if its the only namespace statement

  - index from end operator ^
    - var lastItem = array[1]; 

  - init-only setters: optional parameters that can be set via initializer during object construction
    > var note = new Note(required1, required2) { Optional1 = 5, Optional2 = "s" }

  - local (nested) functions: you can declare one function inside another one

  - switch/case statements can do type matching


## new framework features

- async timer class: PeriodicTimer
- separate classes for time and date: TimeOnly, DateOnly
- linq
  - split collection into chunks of size n: items.Chunk(n)
  - MinBy and MaxBy as a shorter version of OrderBy + First

- trimmed self-contained applications
  - the output publishing folder contains all components of the app, including the .NET libraries 
    and target runtime. The app is isolated from other .NET apps and doesn't use a locally installed 
    shared runtime. The user of your app isn't required to download and install .NET
  - example
    > dotnet publish -r win-x64 -p:PublishTrimmed=true


## dotnet cli

- list supported new app templates
  > dotnet new list

- create new solution
  > dotnet new sln

- create new project
  > dotnet new <template_name> -o <folder_name>

- add project to solution
  > dotnet sln add <project_name>

- pass arguments to an application
  > dotnet run -- <arg1> ... <argN>

- watch project for changes and re-run
  > dotnet watch [--project <my_project.csproj>] run

- list local project templates
  > dotnet new --list

- add nuget package
  > dotnet add package <package_name>

## async/await

- one way to return result from asynchronous method
  > var data = new { myprop = "something" };
  > return Task.FromResult(data);

- unintuitive behavior of aggregate exception
  - with the following code awaiting for both tasks to complete
    > await Task.WhenAll(firstTask, secondTask);
  - for await continuations it always gets unwrapped as its first inner exception, by design
    - meaning that if there is more than one exception, dotnet unwraps AggregateException and only first one will be thrown


## System.CommandLine

- standard library for building cli applications
- supports posix and windows style of parameters, autocomplete, typo correction suggestion
- features overview https://www.youtube.com/watch?v=MOweq3EttPU


## interop

- using dotnet framework assemblies from dotnet core
  - no, unless 
    - your assembly is multiplatform
    - targets netstandard or netcoreapp
    - using 'compatibility shim', with which there is no guarantee that code will work
  - your multiplatform code will likely end up with a bunch of #ifdefs
  - warning: adding a .net standard 2.0 library to a v4.6.1 framework applications bloats the runtime by an extra 97 DLLs

- with python
  - pythonnet https://github.com/pythonnet/pythonnet
    - supports import of .net assemblies from python and python modules from dotnet
    - you can use pandas and all sorts of other cool libraries
  - ironpython: microsoft abandoned it (and its sister project IronRuby) in late 2010


## dependency injection

- application builder simplifies registration of typical components like controllers
- .NET provides a built-in service container, IServiceProvider [4]
  - services are typically registered at the app's start-up and appended to an IServiceCollection
  - once all services are added, you use BuildServiceProvider to create the service container


## webapi

- support for openapi (new name for swagger since 2016)
  - schema can be defined as .json or .yaml, but there is no difference in functionality

- supports api versioning
  - by adding versioning nuget package: integrates into startup plumbing easily


## asp.net

- for asp.net applications the default stack size is only 256k, comparing to 1mb for desktop app
  - can be changed in the PE header

- asp.net mvc
  - Hsts is a security feature to force SSL


## web servers

- iis/iis express
  - log, request tracking, reverse proxy, server farm
  - rich functions for tracing/logging allow better debugging experience

- kestrel
  - lightweight server
  - can run under user account (no need for admin elevation)
  - uses a new request pipeline with ASP.NET Core (instead of old iis HTTP modules & handlers)
  - typical scenario: reverse proxy behind iis


## scripting support

- csx files can be made executable 
  - dotnet script tool is installed
    > dotnet tool install -g dotnet-script
  - for unix: when script contains following shebang: #!/usr/bin/env dotnet-script

- https://ttu.github.io/dotnet-script/


## useful tools

- dotnet fiddle online compiler with .net 6 support: https://dotnetfiddle.net
- specflow: library for writing bdd gherkin style tests
  - supports .net 6 (but not .net 7 yet, as of june 2023)


## support models

- short term support (sts): 18 month
- long term support (lts): 3 years


## compatability

- assemblies targeting .net standard 2.0 will run on
  - .net core 2.0+
  - .net framework 4.6.1+
  - mono 5.4+
- .net 5+ can reference .net framework assemblies with limitations
  - however exception will be thrown if method is not supported
  - nontrivial dependencies will fail to resolve


## installation on debian

- add the following lines to your .profile file
  > export PATH=$PATH:/home/illiak/.dotnet
  > export DOTNET_ROOT=/home/illiak/.dotnet


## console application

- handling configuration file with self-contained executable
  ```csharp
    var builder = new ConfigurationBuilder()
      .SetBasePath(Path.GetDirectoryName(System.Diagnostics.Process.GetCurrentProcess().MainModule.FileName))
      .AddJsonFile("appsettings.json", optional: false, reloadOnChange: false);
    this.config = builder.Build();
  ```


## web application

- install react and angular app scaffolding templates
  > dotnet new install Microsoft.DotNet.Web.Spa.ProjectTemplates


## notable language features timeline

- 2010: C# 4.0 (.NET 4.5)
  - introduced a new type called dynamic


## interesting links

- map result of raw sql query to dto
  - https://stackoverflow.com/questions/67971055/how-do-i-map-result-rows-of-complex-sql-query-into-custom-dto-with-entity-framew


## references

[1]: https://www.youtube.com/c/Elfocrash
[2]: https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10
[3]: https://docs.microsoft.com/en-us/dotnet/core/deploying/trimming/trim-self-contained
[4]: https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection