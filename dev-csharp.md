# notes related to csharp programming language

## basics

- as of may 17, 2022
  - c# latest version is 10 
  - dotnet latest version is 6.0 (recommended), 7.0 (in preview)
  - ide latest version: visual studio 2022


## installation on debian

- add the following lines to your .profile file
  > export PATH=$PATH:/home/illiak/.dotnet
  > export DOTNET_ROOT=/home/illiak/.dotnet


## new language features [^1][^2]

- csharp 11
  - static abstract interface members
  - INumber<T> can be used as generic constraint to enable arithmetic on T

- csharp 10 and earlier

  - top level statements
    - only one file in your application may use top-level statements

  - enter repl by running 'csi' tool

  - interface default method implementations
    - so now csharp interfaces are whats called 'traits' in other languages

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
    - var lastItem = array[^1]; 

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


## interop

- with python
  - pythonnet https://github.com/pythonnet/pythonnet
    - supports import of .net assemblies from python and python modules from dotnet
    - you can use pandas and all sorts of other cool libraries
  - ironpython: microsoft abandoned it (and its sister project IronRuby) in late 2010


## asp.net

- for asp.net applications the default stack size is only 256k, comparing to 1mb for desktop app
  - can be changed in the PE header


## useful tools

- dotnet fiddle online compiler with .net 6 support: https://dotnetfiddle.net


## references

[^1]: https://www.youtube.com/c/Elfocrash
[^2]: https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10
[^3]: https://docs.microsoft.com/en-us/dotnet/core/deploying/trimming/trim-self-contained
