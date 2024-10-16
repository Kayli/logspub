# notes about web development ha

## basics

- simple 3-tier application
  - browser (stateful)
  - webserver (stateless)
  - database (stateful)

- check domain public informtaion https://who.is/
- email addresses are not case sensitive


## popular frameworks

- react (ui)
- angular (ui)
- vue (ui)
- python
  - django (ui, api)
  - flask (api)
  - fastapi
  - tornado
- spring (ui, api)
- aspnet core (ui, api)
- laravel (ui, api)
- ember (ui)
- nodejs
  - express (ui, api)
- gatsby (ui)
  - webpack + graphql + react
  - integration with cms plugins like strapi, graphcms and many others [1]
  - deferred static generation
  - server-side rendering 

- isomorphic approach
  - allows to do server-side render in order to
    - be seo friendly
    - load site faster very first time
  - useful techniques: server side includes [3]
  - frameworks
    - asp.net blazor
    - meteor
    - python
      - anpylar
      - nagare

- progressive web apps
  - asp.net blazor
  - tbd: there are more frameworks here


## headless cms

- foss
  - strapi (gatsby plugin)
  - ghost
  - cockpit
  - apostrophe
  - directus
  - graphcms
- hz
  - contentful
  - wordpress
  - drupal
  - sanity
  - datocms
  - contentstack
  - kentico
  - netlify 
    - hosts content in a git repository
  - agilitycms
  - flotiq
  - prismic
  - buttercms


## api architecture styles

- soap: xml-based
- restful: focused on resources and utilize http verbs more fully
- graphql
  - flexibility for querying specific data client needs
  - reduces amount of dev work required on server side, when you need richer queries support
  - but steep learning curve, more processing server-side
- grpc
  - default serialization is protocol buffers (binary)
  - widely used for communication between microservices inside distributed system
  - limited browser support
- websocket: async bi-directional low-latency data exchange
- webhook: async event-driven communication
  - similar to pubsub, but may not involve the concept of channels or topics
  - focus on delivering specific event notifications to specific endpoints


## http auth

- uses header to authorize http requests, comes in the following format:
    Authorization: <scheme> <parameters>

- authorization schemas
  - Basic
    - parameters are base64 encoded username and password separated with colon (:) 
  - Bearer
    - can be
      - opaque token string (easier to revoke)
      - or jwt string
    - server will check for a valid JWT in the Authorization header, and if it's present, the user will be allowed to access protected resources. If the JWT contains the necessary data, the need to query the database for certain operations may be reduced, though this may not always be the case


## single sign-on (sso)

- protocols
  - oauth
    - authorization framework
    - may or may not use jwt to store data on a client
    
  - openid connect (oidc)
    - rely on signed jwt document to share information across identity services
    - is a thin layer that sits on top of OAuth 2.0 that adds login and profile information about the person who is logged in

  - security assertion markup language (saml)
  - lightweight directory access protocol (ldap)
  - active directory federation services (adfs)
  - kerberos
  - radius


## web assembly

- web standard to distribute/use compiled binary code in a web browser
- wasi (web assembly system interface)
  - standard system libraries available on every platform where modern browser runs
  - sandbox feature
    - allows to run code in sandboxed vm on server-side (similar to app domains in dotnet framework)


## blazor

- emcc (emscripten compiler)
  - a tool to compile c code to browser compatible format
  - compiles to webassembly by default


## atomic design [2]

- atoms: button, label, image
- molecules: label input, form
- organisms
- templates: where molecules and organisms are coming together to form a page template
- pages: instance of a template


## streaming?

- websocket 
  - frameworks
    - socket.io (crossplatform)
    - signalr (microsoft)

- xmpp


## single-page applications

- most popular frameworks: react, angular, vue
- key aspects to be aware of
  - state management
  - components and their lifecycle
  - dependency injection
  - routing
  - bundling/minimization
  - server-side rendering


## iis useful commands

- get iis logs from powershell
  - https://stackoverflow.com/questions/26784883/get-iis-log-location-via-powershell


## references

[1]: https://www.gatsbyjs.com/plugins/#cms
[2]: https://bradfrost.com/blog/post/atomic-web-design/
[3]: https://en.wikipedia.org/wiki/Server_Side_Includes
