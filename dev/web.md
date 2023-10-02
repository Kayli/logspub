# notes about web development ha

## basics

- simple 3-tier application
  - browser (stateful)
  - webserver (stateless)
  - database (stateful)

- check domain public informtaion https://who.is/


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


## rpc/apis

- rest
  - industry most popular choice for apis
  - cons: lacks standardization
    - therefore unified observability and introspection is hindered across heterogeneous stack
    - but check https://oai.github.io/Documentation as it suggests some standard and generators

- graphql
  - queryable apis
  - reduces amount of work required on server side, when you need richer queries support
  - provides introspection over its schema [5]


## single sign-on (sso)

- protocols
  - oauth
  - openid connect (oidc)
    - uses signed jwt document to share information across identity services
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
