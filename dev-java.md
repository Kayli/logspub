# notes about java programming language and infrastructure around it

## basics

- java language is part of jdk and they have same versioning
  - in contrast with c# where language and framework versions are different

- java implemented in c++

- jdk
  - latest version is 18 as of oct 2022
  - lts releases 8, 11, 17
  - main distributions
    - oracleJDK 
      - proprietary implementation
    - openJDK [^3] 
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

- enterprise application server (not what you may think)
  - is integrated set of development tools and application servers that you use to deploy Web applications that support high-volume traffic, dynamic content, and intensive online transaction processing

- top jre languages: java, kotlin, scala, groovy
  - gosu is not even in top 14 [^1]

- webservers
  - spring boot embedded
  - lightweight
    - jetty
    - undertow 
  - old generation
    - ibm websphere
    - apache tomcat

- war file (web application resource or web application archive)
  - java web application package format used for traditional deployment
  - used to distribute a collection of JAR-files, JavaServer Pages, Java Servlets, Java classes, XML files, tag libraries, static web pages (HTML and related files)
  - in modern stacks substituted with containers?

- jcp: java community process
  - mechanism for developing standard technical specifications for Java technology

- jms: java message service
  - messaging standard
  - allows application components based on the java ee to create, send, receive, and read messages

- jpa: java persistence api
  - is not a product but a specification
  - you need a provider to provide an implementation
  - hibernate is one example of JPA implementation
  - provides standard set of attributes to decorate your pojos with and some other stuff

- liberty
  - is a lightweight java runtime
  - supposed to be ideal for building microservices, modern monolithic applications, and anything in between
    - according to ibm's marketing blurb
  - openliberty is an opensource part of websphere liberty
  - detailed comparison of different gists of liberty
    https://www.ibm.com/docs/en/was-liberty/base?topic=management-liberty-features

- JavaBean
  - it is a regular java class, except it follows certain conventions
    - allows access to properties using public getter and setter methods
    - has public no-argument constructor
    - implements Serializable

- pom
  - Project Object Model is the fundamental unit of work in Maven
  - it is an XML file that contains information about the project and configuration details used by Maven to build the project

- H2
  - is a relational database management system written in java
  - it can be embedded in java applications or run in client-server mode


## notable language features timeline

- 2004: java 5 tiger
  - generics
  - metadata or annotations (attributes in csharp)
  - enumerations
  - varargs
  - static imports
  - rmi (aka remoting in dotnet, deprecated in java 9)

- 2006: java 6 mustang
  - java goes opensource
  - swing updates (gui widget toolkit)
  - dramatic performance improvements

- 2011: java 7 dolphin
  - support for dynamic languages
  - catching multiple exception types and rethrowing exceptions with improved type checking
  - jigsaw: java module system

- 2014: java 8 (lts till 2030)
  - lambdas, streams
  - introduction of jeps: jdk enhancement proposals

- 2017: java 9
  - modularization of the jdk
  - jshell repl
  - high dpi support for awt/swing

- 2018
  - java 10: var keyword
  - java 11 (lts): flight recorder: low-overhead data collection framework (low-level, for debugging?)

- 2019
  - java 12: switch expressions
  - java 13: multiline string literals

- 2020
  - java 14
    - pattern matching for instanceof
    - records
    - helpful NullPointerExceptions: describing precisely which variable was null
  - java 15
    - new garbage collectors

- 2021
  - java 16
    - dropped mercurial and moved open-7jdk sources to github
    - vectorization support via vectorapi
    - jpackage: ability to pack a self-contained java application
  - java 17
    - jdk port to macos/aarch64 in a response to apple's transition from x64 architecture
    - sealed classes and interfaces

- 2022
  - java 18
    - utf by default
    - javadoc code snippets: facilitate the validation of source code fragments, by providing API access to those fragments
    - finalization deprecated

- 2023
  - java 20: scoped values (incubating)
  - java 21
    - unnamed classes
    - record patterns to deconstruct record values
    - virtual threads: lightweight threads that dramatically reduce the effort of writing, maintaining, and observing high-throughput concurrent applications
      - see Thread.Builder api


## reflection

- java.lang.reflect package


## dependency injection

- cdi: contexts and dependency injection
  - is a standard dependency injection framework included in Java EE 6 and higher
  - requires presence of beans.xml file to start working even if there is no custom configuration

- weld: reference implementation in Java SE
  - http://weld.cdi-spec.org/


## useful links

- see ./dev-ide.md 'idea' section for ide specifics
- which version of jdk should i use: https://whichjdk.com/
- https://www.ibm.com/cloud/blog/jvm-vs-jre-vs-jdk
- vscode and java https://code.visualstudio.com/docs/languages/java
- streams guide https://stackify.com/streams-guide-java-8/


## historical perspective [^2]

- JBoss Wildfly and Wesphere Liberty are the old enterprise application servers of a previous era (Tomcat may also fit in that, I worked similarly using Tomcat to deploy java web apps back in 2010). You would deploy all your Java applications (there could be many) on the application server, and that would take care of monitoring, logging, providing secrets and other services like JMS and JNDI, re-deploying applications etc... the stuff you might have been doing more recently using k8s/OpenShift/AWS if you're into microservices and not an older enterprise Java shop.
... The whole thing was designed to run on a big server (or a few) that your company maintained and everybody thought deploying to the cloud was a crazy idea that would never catch on

- Quarkus belongs to the "new school" of frameworks that was designed for "microservices" (though they can be as big as your old monoliths, of course) and to run "on the cloud". Other tools in this area are Micronaut, Vert.x and Spring Boot. They are not meant to run multiple Java applications, they're usually a lot smaller in scope than application servers: they just provide you with tools to write servers easily. Vert.x and Micronaut can be used as simple libraries, though they tend to provide a dependency injection (DI) framework, ways to declare HTTP endpoints

- if you're starting a project today, go with either Quarkus or Micronaut and you can't get it wrong: they are modern, lightweight and easy to use... they use modern specifications and are pretty well thought out. Spring Boot may be in the same category but I think Spring is a little bit too bloated with its long history dating back to when application servers were king, though it's still probably the most popular framework by far going by what I've seen in most rankings - so if your concern is on getting people who already have experience on your tech stack, it may still be the preferred option.


## gradle

- may take several seconds to run a trivial command
  - to speedup execution, enable daemon mode [^4]


## desktop apps development [^5]

- awt
  - is an abstract window toolkit that provides various component classes like Label, Button, TextField, etc., to show window components on the screen
  - it is heavy-weight in use because it is generated by the system’s host operating system
  - contains a large number of classes and methods, which are used for creating and managing GUI
  - it will not work the same on every system, although it tries
  - uses native GUI widgets, your OS knows about them and handles putting them in front of each other, etc
  - package: Java.awt

- swing
  - lightweight
  - 100% portable and is the same across platforms
  - swing widgets are meaningless pixels within a window from your OS's point of view
    - does not use os native widgets
    - used to be slower because of that, but not anymore?
  - follows mvc pattern?


## useful info

- solr: is an open-source enterprise-search platform, written in java
- java streams vs linq comparison
  - https://www.iodigital.com/en/history/foreach/java-and-net-comparing-streams-linq

- dce vm: dynamic code evolution virtual machine
  - uses dynamic code evolution java virtual machine to propagate changes to running app in dev mode

- jdk main-line development: https://github.com/openjdk/jdk


## references

[^1]: https://www.spec-india.com/blog/jvm-languages
[^2]: https://www.reddit.com/r/java/comments/wifvo5/choose_the_right_java_runtime_for_the_job_2020/
[^3]: https://stackoverflow.com/questions/47236543/what-is-the-reason-to-use-openjdk
[^4]: https://docs.gradle.org/current/userguide/gradle_daemon.html
[^5]: https://stackoverflow.com/questions/408820/what-is-the-difference-between-swing-and-awt
