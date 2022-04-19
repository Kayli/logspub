# notes about web development ha

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

- isomorphic javascript frameworks
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


## references

[^1]: https://www.gatsbyjs.com/plugins/#cms
