# notes about web development ha

## basics

- simple 3-tier application
  - browser (stateful)
  - webserver (stateless)
  - database (stateful)

- check domain public informtaion https://who.is/


## popular frameworks

- react (ui)
- vue (ui)
- angular (ui)
- django (ui, api)
- flask (api)
- spring (ui, api)
- aspnet core (ui, api)
- laravel (ui, api)
- ember (ui)
- express (ui, api)
- gatsby (ui)
  - webpack + graphql + react
  - integration with cms plugins like strapi, graphcms and many others [^1]
  - deferred static generation
  - server-side rendering 

- isomorphic approach
  - allows to do server-side render in order to
    - be seo friendly
    - load site faster very first time
  - useful techniques: server side includes [^3]
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
  - provides introspection over its schema [^5]


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


## atomic design [^2]

- atoms: button, label, image
- molecules: label input, form
- organisms
- templates: where molecules and organisms are coming together to form a page template
- pages: instance of a template


## streaming

- websocket frameworks
  - socket.io (crossplatform)
  - signalr (microsoft)


## references

[^1]: https://www.gatsbyjs.com/plugins/#cms
[^2]: https://bradfrost.com/blog/post/atomic-web-design/
[^3]: https://en.wikipedia.org/wiki/Server_Side_Includes
