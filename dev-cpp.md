# notes about c++ language and related tools


## version 20  [^1]

- so now you should write all your module code in .mpp file
  - and you can simply import mymodule.mpp from your main.cpp
  - pragma once junk is no longer necessary
- during compilation mymodule.mpp translates to mymodule.bmi
  - bmi - binary module interface
  - it is essentially a cleaned-up and standardised precompiled header 
    - which is easier to reuse and automatically analyze
- you can import header files using import keyword and it will automatically generate .bmi file
- order of import statements doesn't matter anymore
- module structure 
  - global module fragment
    - starts with "module;" statement
    - can contain preprocessor directives only (includes, ifdefs and such)
    - includes are still sensitive to order
  - module preamble
    - starts with "export module mymodulename;"
    - contains import declarations only, order doesn't matter
  - module body
    - the rest of stuff
- aggregate module pattern
  - export module hello;
  - export import hello.format;


## build/package managers

- cmake
  - foss cross-platform family of tools designed to build, test and package software
  - considered to be a most popular one

- bazel
  - foss build and test tool that scalably supports multi-language and multi-platform projects
  - 18k stars

- conan
  - decentralized, foss (mit) C/C++ package manager
  - 6k stars

- build2 toolchain https://build2.org
  - 404 stars


## reference

[^1]: https://youtu.be/szHV6RdQdg8?t=1088
