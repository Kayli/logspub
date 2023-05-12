# notes about java programming language and infrastructure around it

## basics

- java language is part of jdk and they have same versioning
  - in contrast with c# where language and framework versions are different

- jdk
  - latest version is 18 as of oct 2022
  - lts releases 8, 11, 17
  - main distributions
    - oracleJDK 
      - proprietary implementation
    - openJDK [^1] 
      - opensource https://github.com/openjdk/
      - oracle does not provide support for OpenJDK Java builds
      - support is available from many 3rd parties
        - third parties will also port Oracle security fixes to OpenJDK builds

- build systems
  - maven
  - gradle
  - intellij

- as of oct 2022
  - there is no easy to use cli to bootstrap a basic command-line (or whatever) apps 
    - there are some web-framework specific tools like 'spring boot' or something like that
    - had to use ide gui wizards to do basic scaffolding, which is sad
    - looks like ppl copypasting xmls from internets in order to make shit work? or just use ides wizards


## useful links

- see ./dev-ide.md 'idea' section for ide specifics
- https://whichjdk.com/
- https://www.ibm.com/cloud/blog/jvm-vs-jre-vs-jdk
- vscode and java https://code.visualstudio.com/docs/languages/java


## references

[^1]: https://stackoverflow.com/questions/47236543/what-is-the-reason-to-use-openjdk
