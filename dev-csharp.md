# notes related to csharp programming language

## new language features [^1][^2]

important features been introduced in recent years

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


## references

[^1]: https://www.youtube.com/c/Elfocrash
[^2]: https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10